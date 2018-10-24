---
title: 'Conceptos: el objeto del perfil de la API de protección'
description: Este artículo le ayudará a comprender los conceptos básicos sobre el objeto de perfil de protección que se crea durante la inicialización de aplicaciones.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: ae6699212d45a6c8a2fa95f648e7f5a2be3de93e
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445315"
---
# <a name="microsoft-information-protection-sdk---protection-api-profile-concepts"></a>SDK de Microsoft Information Protection: conceptos del perfil de la API de protección

En los dos ejemplos siguientes, se muestra cómo crear el objeto profileSettings con almacenamiento local para el almacenamiento de estados, así como solo en memoria. En ambos ejemplos, se da por hecho que el objeto `authDelegateImpl` ya se ha creado.

## <a name="load-a-profile"></a>Cargar un perfil

Tenga en cuenta que se definen `ProtectionProfileObserverImpl` y `AuthDelegateImpl`, que usaremos para crear una instancia de `mip::ProtectionProfile`. Para crear el objeto `mip::ProtectionProfile`, se necesita [`mip::ProtectionProfile::Settings`](reference/class_mip_ProtectionProfile_settings.md).

### <a name="protectionprofilesettings-parameters"></a>Parámetros de ProtectionProfile::Settings

- `std::string path`: ruta del archivo donde se almacenan los datos de registro, telemetría y otros estados persistentes.
- `bool useInMemoryStorage`: define si todos los estados se tienen que almacenar o no en memoria (en lugar de almacenarlos en el disco).
- `std::shared_ptr<mip::AuthDelegate> authDelegate`: un puntero compartido de la clase `mip::AuthDelegate`.
- `std::shared_ptr<mip::ProtectionProfile::Observer> observer`: un puntero compartido de la implementación de `ProtectionProfile::Observer`.
- `mip::ApplicationInfo applicationInfo`: objeto. Se usa para definir información relacionada con la aplicación que usa el SDK.

En los dos ejemplos siguientes, se muestra cómo crear el objeto profileSettings con almacenamiento local para el almacenamiento de estados, así como solo en memoria. En ambos ejemplos, se da por hecho que el objeto `authDelegateImpl` ya se ha creado.

#### <a name="store-state-in-memory-only"></a>Almacenar el estado solo en memoria

```cpp
ProtectionProfile::Settings profileSettings(
    "",                                     //path to store settings
    true,                                   //useInMemoryStorage
    authDelegateImpl,                       //auth delegate object
    std::make_shared<ConsentDelegateImpl>(),//new consent delegate
    std::make_shared<ProtectionProfileObserverImpl>(), //new protection profile observer
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" }); //ApplicationInfo object
```

#### <a name="readwrite-profile-settings-from-storage-path-on-disk"></a>Configuración del perfil de lectura y escritura de la ruta de almacenamiento en el disco

```cpp
ProtectionProfile::Settings profileSettings(
    "./mip_app_data",                       //path to store settings
    false,                                  //useInMemoryStorage
    authDelegateImpl,                       //auth delegate object
    std::make_shared<ConsentDelegateImpl>(),//new consent delegate
    std::make_shared<ProtectionProfileObserverImpl>(), //new protection profile
    mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" }); //ApplicationInfo object
```

Después, use el patrón de promesa o futuro para cargar el elemento `ProtectionProfile`.

```cpp
auto profilePromise = std::make_shared<std::promise<std::shared_ptr<ProtectionProfile>>>();
auto profileFuture = profilePromise->get_future();
ProtectionProfile::LoadAsync(profileSettings, profilePromise);
```

Si carga un perfil y la operación se completa correctamente (`ProtectionProfileObserverImpl::OnLoadSuccess`), se realizará una llamada a la implementación de `mip::ProtectionProfile::Observer::OnLoadSuccess`. El puntero de excepción u objeto resultante, así como el contexto, se pasan como parámetros a la función. El contexto es un puntero al objeto `std::promise` que hemos creado para controlar la operación asincrónica. La función simplemente establece el valor de la promesa en el objeto ProtectionProfile (contexto). Cuando la función principal usa `Future.get()`, el resultado se puede almacenar en un nuevo objeto.

```cpp
//get the future value and store in profile.
auto profile = profileFuture.get();
```

### <a name="putting-it-together"></a>Resumen

Después de implementar por completo los observadores y el delegado de autenticación, ya podemos cargar por completo un perfil. En el fragmento de código siguiente, se da por hecho que ya se han incluido todos los encabezados necesarios.

```cpp
int main()
{
    const string userName = "MyTestUser@contoso.com";
    const string password = "P@ssw0rd!";
    const string clientId = "MyClientId";
    auto authDelegateImpl = make_shared<sample::auth::AuthDelegateImpl>(userName, password, clientId);

    ProtectionProfile::Settings profileSettings("",
        false,
        authDelegateImpl,
        std::make_shared<ConsentDelegateImpl>(),
        std::make_shared<ProfileObserver>(),
        mip::ApplicationInfo{ "MyClientId", "MyAppFriendlyName" });

    auto profilePromise = std::make_shared<promise<shared_ptr<ProtectionProfile>>>();
    auto profileFuture = profilePromise->get_future();
    ProtectionProfile::LoadAsync(profileSettings, profilePromise);
    auto profile = profileFuture.get();
}
```

Como resultado final, cargaremos correctamente el perfil y lo almacenaremos en el objeto llamado `profile`.

## <a name="next-steps"></a>Pasos siguientes

Después de agregar el perfil, el paso siguiente es agregar un motor al perfil.

[Conceptos del motor de protección](concept-profile-engine-protection-engine-cpp.md)