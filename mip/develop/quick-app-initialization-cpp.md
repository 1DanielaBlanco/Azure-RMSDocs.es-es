---
title: 'Guía de inicio rápido: inicialización para clientes del SDK de Microsoft Information Protection (MIP) con C++'
description: Guía de inicio rápido donde se muestra cómo escribir la lógica de inicialización para aplicaciones cliente del SDK de Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: quickstart
ms.date: 01/18/2019
ms.author: bryanla
ms.openlocfilehash: 2fb19aa5071fa13f9801de9e9ed1106717f5adf9
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651435"
---
# <a name="quickstart-client-application-initialization-c"></a>Inicio rápido: Inicialización de la aplicación cliente (C++)

En este tutorial rápido se muestra cómo implementar el patrón de inicialización del cliente, usando el SDK de C++ de MIP en tiempo de ejecución. 

> [!NOTE]
> Los pasos que se describen en esta guía de inicio rápido son obligatorios para cualquier aplicación cliente que use las API de protección, directiva o archivos de MIP. Aunque en esta guía de inicio rápido se muestra cómo usar las API de archivo, este mismo patrón puede aplicarse en los clientes que usen las API de protección y directiva. Complete los tutoriales restantes en serie, como cada uno de ellos se basa en la anterior, por este otro que se va la primera.

## <a name="prerequisites"></a>Requisitos previos

Si aún no lo ha hecho, asegúrese de:

- Completar los pasos que se indican en [Instalación y configuración del SDK de Microsoft Information Protection (MIP)](setup-configure-mip.md). La guía de inicio rápido “Inicialización de la aplicación cliente” se basa en la instalación y configuración del SDK adecuada realizada anteriormente.
- Opcionalmente:
  - Vea [Objetos de perfil y motor](concept-profile-engine-cpp.md). Los objetos de perfil y motor son conceptos universales que necesitan los clientes que usan las API de protección, directiva o archivos de MIP. 
  - Revisión [conceptos de autenticación](concept-authentication-cpp.md) para obtener información sobre cómo se implementan la autenticación y autorización mediante el SDK y la aplicación cliente.
  - Vea [Conceptos del observador](concept-async-observers.md) para obtener más información sobre los observadores y cómo se han implementado. El SDK de MIP se utiliza el patrón de observador para implementar notificaciones de eventos asincrónicos.

## <a name="create-a-visual-studio-solution-and-project"></a>Crear un proyecto y una solución de Visual Studio

En primer lugar, cree y configure la solución de Visual Studio y el proyecto, en el que crear otros inicios rápidos inicial. 

1. Abra Visual Studio 2017, seleccione el menú **Archivo**, **Nuevo**, **Proyecto**. En el cuadro de diálogo **Nuevo proyecto**:
   - En el panel izquierdo, en **Instalados**, **Otros lenguajes**, seleccione **Visual C++**.
   - En el panel central, seleccione **Aplicación de consola Windows**.
   - En el panel inferior, actualice el **Nombre** y la **Ubicación** del proyecto, así como el **Nombre de la solución** que lo contiene.
   - Cuando haya terminado, haga clic en el botón **Aceptar** de la parte inferior derecha.

     [![Crear la solución de Visual Studio](media/quick-app-initialization-cpp/create-vs-solution.png)](media/quick-app-initialization-cpp/create-vs-solution.png#lightbox)

2. Agregue al proyecto el paquete NuGet para la API de archivo del SDK de MIP:
   - En el **el Explorador de soluciones**, haga clic en el nodo de proyecto (directamente bajo el nodo superior o solución) y seleccione **administrar paquetes NuGet...** :
   - Cuando se abra la pestaña **Administrador de paquetes NuGet** en el área de pestañas del grupo del editor:
     - Seleccione **Examinar**.
     - Escriba “Microsoft.InformationProtection” en el cuadro de búsqueda.
     - Seleccione el paquete “Microsoft.InformationProtection.File”.
     - Haga clic en “Instalar” y, cuando se muestre el cuadro de diálogo de confirmación **Vista previa de los cambios**, haga clic en “Aceptar”.
   
     [![Agregar un paquete NuGet a Visual Studio](media/quick-app-initialization-cpp/add-nuget-package.png)](media/quick-app-initialization-cpp/add-nuget-package.png#lightbox)
 
## <a name="implement-an-observer-class-to-monitor-the-file-profile-and-engine-objects"></a>Implementar una clase de observador para supervisar los objetos de perfil y motor de archivo

Ahora, para crear una implementación básica para una clase de observador del perfil de archivo, extienda la clase `mip::FileProfile::Observer` del SDK. Se creará una instancia del observador y se usará más tarde para supervisar la carga del objeto del perfil de archivo y se agregará el objeto del motor al perfil.

1. Agregue una nueva clase al proyecto, que genera automáticamente los archivos de encabezado/.h e implementación/.cpp:

   - En el **el Explorador de soluciones**, haga clic en el nodo del proyecto nuevo, seleccione **agregar**, a continuación, seleccione **clase**.
   - En el cuadro de diálogo **Agregar clase**:
     - En el campo **Nombre de clase**, escriba “profile_observer”. Tenga en cuenta que tanto el campo **archivo .h** como el campo **archivo .cpp** se rellenan automáticamente, según el nombre especificado.
     - Cuando haya terminado, haga clic en el botón **Aceptar**.

     [![Agregar una clase a Visual Studio](media/quick-app-initialization-cpp/add-class.png)](media/quick-app-initialization-cpp/add-class.png#lightbox)

2. Después de generar los archivos .h y .cpp para la clase, ambos archivos se abren en pestañas del Grupo de editores. Ahora, actualice cada archivo para implementar la nueva clase de observador:

   - Actualice “profile_observer.h”; para hacerlo, seleccione o elimine la clase `profile_observer` generada. **No** quite las directivas de preprocesador generadas en el paso anterior (#pragma, #include). Después, copie y pegue el siguiente código fuente en el archivo, después de las directivas de preprocesador existentes:

     ```cpp
     #include <memory>
     #include "mip/file/file_profile.h"

     class ProfileObserver final : public mip::FileProfile::Observer {
     public:
          ProfileObserver() { }
          void OnLoadSuccess(const std::shared_ptr<mip::FileProfile>& profile, const std::shared_ptr<void>& context) override;
          void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
          void OnAddEngineSuccess(const std::shared_ptr<mip::FileEngine>& engine, const std::shared_ptr<void>& context) override;
          void OnAddEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
     };
     ```

   - Actualice “profile_observer.cpp”; para hacerlo, seleccione o elimine la implementación de clase `profile_observer` generada. **No** quite las directivas de preprocesador generadas en el paso anterior (#pragma, #include). Después, copie y pegue el siguiente código fuente en el archivo, después de las directivas de preprocesador existentes:

     ```cpp
     #include <future>

     using std::promise;
     using std::shared_ptr;
     using std::static_pointer_cast;
     using mip::FileEngine;
     using mip::FileProfile;

     void ProfileObserver::OnLoadSuccess(const shared_ptr<FileProfile>& profile, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<FileProfile>>>(context);
          promise->set_value(profile);
     }

     void ProfileObserver::OnLoadFailure(const std::exception_ptr& error, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<FileProfile>>>(context);
          promise->set_exception(error);
     }

     void ProfileObserver::OnAddEngineSuccess(const shared_ptr<FileEngine>& engine, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<FileEngine>>>(context);
          promise->set_value(engine);
     }

     void ProfileObserver::OnAddEngineFailure(const std::exception_ptr& error, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<FileEngine>>>(context);
          promise->set_exception(error);
     }
     ```

3. También puede presionar F6 (**Compilar solución**) para ejecutar una compilación o vínculo de prueba de la solución y asegurarse de que se compila correctamente antes de continuar.

## <a name="implement-an-authentication-delegate"></a>Implementar un delegado de autenticación

El SDK de MIP implementa la autenticación con la extensibilidad de la clase, que proporciona un mecanismo para compartir la autenticación con la aplicación cliente. El cliente tiene que obtener un token de acceso de OAuth2 adecuado y proporcionarlo al SDK de MIP en tiempo de ejecución. 

Ahora, cree una implementación para un delegado de autenticación; para hacerlo, extienda la clase `mip::AuthDelegate` del SDK y reemplace o implemente la función virtual pura `mip::AuthDelegate::AcquireOAuth2Token()`. Se creará una instancia del delegado de autenticación y se usará más tarde con los objetos del motor de archivo y de perfil de archivo.

1. Con la misma característica “Agregar clase” de Visual Studio que usamos en el paso 1 de la sección anterior, agregue otra clase al proyecto. Esta vez, escriba “auth_delegate” en el campo **Nombre de clase**. 

2. Ahora, actualice cada archivo para implementar la nueva clase del delegado de autenticación:

   - Actualice “auth_delegate.h”; para hacerlo, reemplace todo el código de clase `auth_delegate` generado con el código fuente siguiente. **No** quite las directivas de preprocesador generadas en el paso anterior (#pragma, #include):

     ```cpp
     #include <string>
     #include "mip/common_types.h"

     class AuthDelegateImpl final : public mip::AuthDelegate {
     public:
          AuthDelegateImpl() = delete;        // Prevents default constructor
          
          AuthDelegateImpl(
            const std::string& appId)         // AppID for registered AAD app
            : mAppId(appId) {};

          bool AcquireOAuth2Token(            // Called by MIP SDK to get a token
            const mip::Identity& identity,    // Identity of the account to be authenticated, if known
            const OAuth2Challenge& challenge, // Authority (AAD tenant issuing token), and resource (API being accessed; "aud" claim).
            OAuth2Token& token) override;     // Token handed back to MIP SDK
     private:
          std::string mAppId;
          std::string mToken;
          std::string mAuthority;
          std::string mResource;
     };
     ```

   - Actualice “auth_delegate.cpp”; para hacerlo, reemplace toda la implementación de la clase `auth_delegate` generada por el código fuente siguiente. **No** quite las directivas de preprocesador generadas en el paso anterior (#pragma, #include). 

     > [!IMPORTANT]
     > El siguiente código de obtención de tokens no es adecuado para su uso en producción. En un entorno de producción, esto tiene que reemplazarse por código que obtenga de forma dinámica un token con:
     > - El identificador de la aplicación y el URI de respuesta o redireccionamiento especificado en el registro de la aplicación de Azure AD (el URI de respuesta o redireccionamiento **tiene** que coincidir con el registro de la aplicación).
     > - La URL del recurso y la autoridad pasada por el SDK en el argumento `challenge` (la URL de recurso **tiene** que coincidir con los permisos o las API del registro de la aplicación).
     > - Credenciales de usuario o aplicación válidas, donde la cuenta coincida con el argumento `identity` pasado por el SDK. Los clientes de OAuth2 “nativos” tienen que pedir credenciales de usuario y usar el flujo del “código de autorización”. Los “clientes confidenciales” de OAuth2 pueden usar sus propias credenciales seguras con el flujo de “credenciales de cliente” (por ejemplo, un servicio), o bien pedir las credenciales de usuario con el flujo de “código de autorización” (por ejemplo, una aplicación web). 
     >
     > La obtención de tokens de OAuth2 es un protocolo complejo y suele completarse mediante el uso de una biblioteca. TokenAcquireOAuth2Token() **solo** lo llama el SDK de MIP, según sea necesario.

     ```cpp
     #include <iostream>
     using std::cout;
     using std::cin;
     using std::string;

     bool AuthDelegateImpl::AcquireOAuth2Token(const mip::Identity& identity, const OAuth2Challenge& challenge, OAuth2Token& token) 
     {
          // Acquire a token manually, reuse previous token if same authority/resource. In production, replace with token acquisition code.
          string authority = challenge.GetAuthority();
          string resource = challenge.GetResource();
          if (mToken == "" || (authority != mAuthority || resource != mResource))
          {
              cout << "\nRun the PowerShell script to generate an access token using the following values, then copy/paste it below:\n";
              cout << "Set $authority to: " + authority + "\n";
              cout << "Set $resourceUrl to: " + resource + "\n";
              cout << "Sign in with user account: " + identity.GetEmail() + "\n";
              cout << "Enter access token: ";
              cin >> mToken;
              mAuthority = authority;
              mResource = resource;
              system("pause");
          }

          // Pass access token back to MIP SDK
          token.SetAccessToken(mToken);

          // True = successful token acquisition; False = failure
          return true;
     }
     ``` 
3. También puede presionar F6 (**Compilar solución**) para ejecutar una compilación o vínculo de prueba de la solución y asegurarse de que se compila correctamente antes de continuar.

## <a name="implement-a-consent-delegate"></a>Implementar un delegado de consentimiento

Ahora, cree una implementación para un delegado de consentimiento; para hacerlo, extienda la clase `mip::ConsentDelegate` del SDK y reemplace o implemente la función virtual pura `mip::AuthDelegate::GetUserConsent()`. Se creará una instancia del delegado de consentimiento y se usará más tarde con los objetos del motor de archivo y de perfil de archivo.

1. Con la misma característica “Agregar clase” de Visual Studio que hemos usado anteriormente, agregue otra clase al proyecto. Esta vez, escriba “consent_delegate” en el campo **Nombre de clase**. 

2. Ahora, actualice cada archivo para implementar la nueva clase de delegado de consentimiento:

   - Actualice “consent_delegate.h”; para hacerlo, reemplace todo el código de clase `consent_delegate` generado con el código fuente siguiente. **No** quite las directivas de preprocesador generadas en el paso anterior (#pragma, #include):

     ```cpp
     #include "mip/common_types.h"
     #include <string>

     class ConsentDelegateImpl final : public mip::ConsentDelegate {
     public:
          ConsentDelegateImpl() = default;
          virtual mip::Consent GetUserConsent(const std::string& url) override;
     };
     ```

   - Actualice “consent_delegate.cpp”; para hacerlo, reemplace toda la implementación de la clase `consent_delegate` generada por el código fuente siguiente. **No** quite las directivas de preprocesador generadas en el paso anterior (#pragma, #include). 

     ```cpp
     #include <iostream>
     using mip::Consent;
     using std::string;

     Consent ConsentDelegateImpl::GetUserConsent(const string& url) 
     {
          // Accept the consent to connect to the url
          std::cout << "SDK will connect to: " << url << std::endl;
          return Consent::AcceptAlways;
     }
     ``` 
3. También puede presionar F6 (**Compilar solución**) para ejecutar una compilación o vínculo de prueba de la solución y asegurarse de que se compila correctamente antes de continuar.

## <a name="construct-a-file-profile-and-engine"></a>Crear un motor y un perfil de archivo

Como se mencionó, los objetos de perfil y del motor son necesarios para clientes del SDK de MIP APIs de uso. Complete el fragmento de código siguiente de esta guía de inicio rápido; para hacerlo, agregue código para crear la instancia de los objetos de perfil y motor: 

1. Mediante el **Explorador de soluciones**, abra el archivo .cpp en el proyecto que contiene la implementación del método `main()`. El valor predeterminado es el mismo nombre que el proyecto que lo contiene, el cual ha especificado al crear el proyecto.

2. Quite la implementación generada de `main()`. **No** quite las directivas de preprocesador generadas por Visual Studio durante la creación del proyecto (#pragma, #include). Anexe el código siguiente después de cualquier directiva de preprocesador:

   ```cpp
   #include "auth_delegate.h"
   #include "consent_delegate.h"
   #include "profile_observer.h"

   using std::promise;
   using std::future;
   using std::make_shared;
   using std::shared_ptr;
   using std::string;
   using std::cout;
   using mip::ApplicationInfo; 
   using mip::FileProfile;
   using mip::FileEngine;

   int main()
   {
     // Construct/initialize objects required by the application's profile object
     ApplicationInfo appInfo{"<application-id>",                    // ApplicationInfo object (App ID, name, version)
                 "<application-name>",
                 "<application-version>"};
     auto profileObserver = make_shared<ProfileObserver>();         // Observer object                  
     auto authDelegateImpl = make_shared<AuthDelegateImpl>(         // Authentication delegate object (App ID)
                 "<application-id>");
     auto consentDelegateImpl = make_shared<ConsentDelegateImpl>(); // Consent delegate object
 
     // Construct/initialize profile object
     FileProfile::Settings profileSettings("",    // Path for logging/telemetry/state
       true,                                      // true = use in-memory state storage (vs disk)
       authDelegateImpl,                            
       consentDelegateImpl,                     
       profileObserver,                         
       appInfo);                                    

     // Set up promise/future connection for async profile operations; load profile asynchronously
     auto profilePromise = make_shared<promise<shared_ptr<FileProfile>>>();
     auto profileFuture = profilePromise->get_future();
    try
    { 
        mip::FileProfile::LoadAsync(profileSettings, profilePromise);
    }
    catch (const std::exception& e)
    {
        cout << "An exception occurred... are the Settings and ApplicationInfo objects populated correctly?\n\n"
            << e.what() << "'\n";
        system("pause");
        return 1;

    }
    auto profile = profileFuture.get();

     // Construct/initialize engine object
     FileEngine::Settings engineSettings(
       mip::Identity("<engine-account>"),         // Engine identity (account used for authentication)
       "<engine-state>",                          // User-defined engine state      
       "en-US");                                  // Locale (default = en-US)

     // Set up promise/future connection for async engine operations; add engine to profile asynchronously
     auto enginePromise = make_shared<promise<shared_ptr<FileEngine>>>();
     auto engineFuture = enginePromise->get_future();
     profile->AddEngineAsync(engineSettings, enginePromise);
     std::shared_ptr<FileEngine> engine; 
     try
     {
       engine = engineFuture.get();             
     }
     catch (const std::exception& e)
     {
       cout << "An exception occurred... is the access token incorrect/expired?\n\n"
        << e.what() << "'\n";
       system("pause");
       return 1;
     }

   return 0;
   }
   ``` 

3. Reemplace todos los valores de marcador de posición en el código fuente que acaba de pegar, mediante las constantes de cadena:

   | Marcador | Valor | Ejemplo |
   |:----------- |:----- |:--------|
   | \<application-id\> | El Id. de aplicación de AD Azure (GUID) asignado a la aplicación registrada en [paso #2 de la "instalación del SDK de MIP y configuración"](/information-protection/develop/setup-configure-mip#register-a-client-application-with-azure-active-directory) artículo. Reemplace 2 instancias. | `"0edbblll-8773-44de-b87c-b8c6276d41eb"` |
   | \<application-name\> | Nombre descriptivo definido por el usuario para la aplicación. Debe contener caracteres ASCII válidos (sin incluir ';') y lo ideal es que coincide con el nombre de la aplicación que utilizó en el registro de Azure AD. | `"AppInitialization"` |
   | \<application-version\> | Información de versión definido por el usuario para la aplicación. Debe contener caracteres ASCII válidos (sin incluir ';'). | `"1.1.0.0"` |
   | \<engine-account\> | Cuenta usada para la identidad del motor. Al autenticarse con una cuenta de usuario durante la obtención de tokens, tiene que coincidir con este valor. | `"user1@tenant.onmicrosoft.com"` |
   | \<engine-state\> | Estado definido por el usuario que se asociará al motor. | `"My App State"` |


4. Ahora, realice una compilación final de la aplicación y solucione los posibles errores. El código tiene que compilarse sin errores, pero no se ejecutará correctamente hasta que complete la próxima guía de inicio rápido. Si ejecuta la aplicación, verá un resultado similar al siguiente. No podrá proporcionar un token de acceso hasta que complete la próxima guía de inicio rápido.

   ```console
   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/common/oauth2/authorize
   Set $resourceUrl to: https://syncservice.o365syncservice.com/
   Sign in with user account:
   Enter access token:
   ```

## <a name="next-steps"></a>Pasos siguientes

Después de completar el código de inicialización, estará preparado para la próxima guía de inicio rápido, donde empezará a probar las API de archivo de MIP.

> [!div class="nextstepaction"]
> [Mostrar etiquetas de confidencialidad](quick-file-list-labels-cpp.md)
