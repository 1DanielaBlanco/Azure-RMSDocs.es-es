---
title: 'Conceptos: el objeto del perfil de la API de archivo'
description: Este artículo le ayudará a comprender los conceptos básicos sobre el objeto del perfil de archivo que se crea durante la inicialización de aplicaciones.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 33ec266068d15e827267b7d518344aebd0f8f072
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445910"
---
# <a name="microsoft-information-protection-sdk---file-api-profile-concepts"></a>SDK de Microsoft Information Protection: conceptos del perfil de la API de archivo

El perfil es la clase raíz de todas las operaciones en el SDK de MIP. Antes de usar cualquiera de las funciones de la API de archivo, es necesario crear un elemento `FileProfile` y todas las operaciones futuras se realizarán con el perfil o con otros objetos *agregados* al perfil.

Hay algunos requisitos previos de código que es necesario cumplir antes de intentar crear una instancia de un perfil:

- `AuthDelegateImpl` se implementa para extender `mip::AuthDelegate`.
- `ConsentDelegateImpl` se implementa para extender `mip::ConsentDelegate`.
- La aplicación se ha [registrado en Azure Active Directory](/azure/active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad.md) y el identificador de cliente se ha codificado de forma rígida en los archivos de configuración o la aplicación. 
- Se ha implementado correctamente una clase que hereda `mip::FileProfile::Observer`.

## <a name="load-a-profile"></a>Cargar un perfil

Después de definir `ProfileObserver`, `ConsentDelegateImpl` y `AuthDelegateImpl`, ya se puede crear una instancia de `mip::FileProfile`. Para crear el objeto `mip::FileProfile`, es necesario que [`mip::FileProfile::Settings`](reference/class_mip_fileprofile_settings.md) almacene toda la información de configuración sobre `FileProfile`.

### <a name="fileprofilesettings-parameters"></a>Parámetros de FileProfile::Settings

El constructor `FileProfile::Settings` admite cinco parámetros, que se indican abajo:

- `std::string path`: ruta del archivo donde se almacenan los datos de registro, telemetría y otros estados persistentes.
- `bool useInMemoryStorage`: define si todos los estados se tienen que almacenar o no en memoria (en lugar de almacenarlos en el disco).
- `std::shared_ptr<mip::AuthDelegate> authDelegate`: un puntero compartido de la clase `mip::AuthDelegate`. 
- `std::shared_ptr<mip::ConsentDelegate>`: 
- `std::shared_ptr<mip::FileProfile::Observer> observer`: un puntero compartido de la implementación de `FileProfile::Observer`.
- `mip::ApplicationInfo applicationInfo`: objeto. Se usa para definir información relacionada con la aplicación que usa el SDK.

En los ejemplos siguientes, se muestra cómo crear el objeto `profileSettings` con almacenamiento local para el almacenamiento de estados, así como solo en memoria. En ambos ejemplos, se da por hecho que el objeto `authDelegateImpl` ya se ha creado.

#### <a name="store-state-in-memory-only"></a>Almacenar el estado solo en memoria

```cpp
FileProfile::Settings profileSettings(
    "",                                          //path to store settings
    true,                                        //useInMemoryStorage
    authDelegateImpl,                            //auth delegate object
    std::make_shared<ConsentDelegateImpl>(),     //new consent delegate
    std::make_shared<FileProfileObserverImpl>(), //new protection profile observer
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" }); //ApplicationInfo object
```

#### <a name="readwrite-profile-settings-from-storage-path-on-disk"></a>Configuración del perfil de lectura y escritura de la ruta de almacenamiento en el disco

En el fragmento de código siguiente, se indica al objeto `FileProfile` que almacene todos los datos de estados de la aplicación en `./mip_app_data`.

```cpp
FileProfile::Settings profileSettings(
    "./mip_app_data",                            //path to store settings
    false,                                       //useInMemoryStorage
    authDelegateImpl,                            //auth delegate object
    std::make_shared<ConsentDelegateImpl>(),     //new consent delegate
    std::make_shared<FileProfileObserverImpl>(), //new protection profile observer
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" }); //ApplicationInfo object
```

#### <a name="load-the-profile"></a>Cargar el perfil

Usando algunos de los detalles de los métodos anteriores, ahora use el patrón de promesa o futuro para cargar el elemento `FileProfile`.

```cpp
auto profilePromise = std::make_shared<std::promise<std::shared_ptr<FileProfile>>>();
auto profileFuture = profilePromise->get_future();
FileProfile::LoadAsync(profileSettings, profilePromise);
```

Si carga un perfil y la operación se completa correctamente (`ProfileObserver::OnLoadSuccess`), se realizará una llamada a la implementación de `mip::FileProfile::Observer::OnLoadSuccess`. El puntero de excepción u objeto resultante, así como el contexto, se pasan como parámetros a la función. El contexto es un puntero al objeto `std::promise` que hemos creado para controlar la operación asincrónica. La función simplemente establece el valor de la promesa en el objeto FileProfile que se ha pasado para el primer parámetro. Cuando la función principal usa `Future.get()`, el resultado se puede almacenar en un nuevo objeto.

```cpp
//get the future value and store in profile. 
auto profile = profileFuture.get();
```

### <a name="putting-it-together"></a>Resumen

Después de implementar por completo los observadores y el delegado de autenticación, ya podemos cargar por completo un perfil. En el fragmento de código siguiente, se da por hecho que ya se han incluido todos los encabezados necesarios.

```cpp
int main()
{
    const string userName = "MyTestUser@consoto.com";
    const string password = "P@ssw0rd!";
    const string clientId = "MyClientId";
    auto authDelegateImpl = make_shared<sample::auth::AuthDelegateImpl>(userName, password, clientId);

    FileProfile::Settings profileSettings("",
            false,
            authDelegateImpl,
            std::make_shared<ConsentDelegateImpl>(),
            std::make_shared<ProfileObserver>(),
            mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" });

    auto profilePromise = std::make_shared<promise<shared_ptr<FileProfile>>>();
    auto profileFuture = profilePromise->get_future();
    FileProfile::LoadAsync(profileSettings, profilePromise);
    auto profile = profileFuture.get();
}
```

Como resultado final, cargaremos correctamente el perfil y lo almacenaremos en el objeto llamado `profile`.

## <a name="next-steps"></a>Pasos siguientes

Después de agregar el perfil, el paso siguiente es agregar un motor al perfil. 

- [Conceptos del motor de archivo](concept-profile-engine-file-engine-cpp.md)