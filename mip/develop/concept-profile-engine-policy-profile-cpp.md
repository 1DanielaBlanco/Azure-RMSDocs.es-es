---
title: 'Conceptos: el objeto del perfil de la API de directiva'
description: Este artículo le ayudará a comprender los conceptos básicos sobre el objeto de perfil de directiva que se crea durante la inicialización de aplicaciones.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: b229148c3028f4478f83cbbc928e19666c2f44b5
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445434"
---
# <a name="microsoft-information-protection-sdk---policy-api-profile-concepts"></a>SDK de Microsoft Information Protection: conceptos del perfil de la API de directiva

Es necesario cargar `mip::Profile` antes de realizar cualquier operación de la API de directiva.

En los dos ejemplos siguientes, se muestra cómo crear el objeto profileSettings con almacenamiento local para el almacenamiento de estados, así como solo en memoria. En ambos ejemplos, se da por hecho que el objeto `authDelegateImpl` ya se ha creado.

## <a name="load-a-profile"></a>Cargar un perfil

Tenga en cuenta que se definen `ProfileObserver` y `AuthDelegateImpl`, que usaremos para crear una instancia de `mip::PolicyProfile`. Para crear el objeto `mip::PolicyProfile`, se necesita [`mip::PolicyProfile::Settings`](reference/class_mip_PolicyProfile_settings.md).

### <a name="profilesettings-parameters"></a>Parámetros de Profile::Settings

- `std::string path`: ruta del archivo donde se almacenan los datos de registro, telemetría y otros estados persistentes.
- `bool useInMemoryStorage`: define si todos los estados se tienen que almacenar o no en memoria (en lugar de almacenarlos en el disco).
- `std::shared_ptr<mip::AuthDelegate> authDelegate`: un puntero compartido de la clase `mip::AuthDelegate`. 
- `std::shared_ptr<mip::PolicyProfile::Observer> observer`: un puntero compartido de la implementación de `PolicyProfile::Observer`.
- `mip::ApplicationInfo applicationInfo`: objeto. Se usa para definir información relacionada con la aplicación que usa el SDK.

En los dos ejemplos siguientes, se muestra cómo crear el objeto profileSettings con almacenamiento local para el almacenamiento de estados, así como solo en memoria. En ambos ejemplos, se da por hecho que el objeto `authDelegateImpl` ya se ha creado.

#### <a name="store-state-in-memory-only"></a>Almacenar el estado solo en memoria

```cpp
Profile::Settings profileSettings("",
    true,
    authDelegateImpl,
    std::make_shared<ProfileObserver>(),
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" });
```

#### <a name="readwrite-profile-settings-from-storage-path-on-disk"></a>Configuración del perfil de lectura y escritura de la ruta de almacenamiento en el disco

```cpp
Profile::Settings profileSettings("./mip_app_data",
    false,
    authDelegateImpl,
    std::make_shared<ProfileObserver>(),
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" });
```

Después, use el patrón de promesa o futuro para cargar el elemento `Profile`.

```cpp
auto profilePromise = std::make_shared<std::promise<std::shared_ptr<Profile>>>();
auto profileFuture = profilePromise->get_future();
Profile::LoadAsync(profileSettings, profilePromise);
```

Si se carga un perfil correctamente (`ProfileObserver::OnLoadSuccess`), se notificará de nuestra implementación de `mip::Profile::Observer::OnLoadSuccess`. El objeto resultante (en este caso, `mip::Profile`), así como el contexto, se pasan como parámetros a la función del observador.

El *contexto* es un puntero al objeto `std::promise` que hemos creado para controlar la operación asincrónica. La función simplemente establece el valor de la promesa en el objeto de perfil que se pasó para el primer parámetro. Cuando la función principal usa `Future.get()`, el resultado se puede almacenar en un nuevo objeto en el subproceso que realiza la llamada.

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

    Profile::Settings profileSettings("", false, authDelegateImpl, std::make_shared<ProfileObserver>(), mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" });

    auto profilePromise = std::make_shared<promise<shared_ptr<Profile>>>();
    auto profileFuture = profilePromise->get_future();
    Profile::LoadAsync(profileSettings, profilePromise);
    auto profile = profileFuture.get();
}
```

Como resultado final, cargaremos correctamente el perfil y lo almacenaremos en el objeto llamado `profile`.

## <a name="next-steps"></a>Pasos siguientes

Después de agregar el perfil, el paso siguiente es agregar un motor al perfil.

[Conceptos del motor de directivas](concept-profile-engine-policy-engine-cpp.md)