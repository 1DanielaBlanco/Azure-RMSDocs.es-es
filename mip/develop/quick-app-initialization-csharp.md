---
title: 'Inicio rápido: inicialización de Microsoft Information Protection (MIP) SDK C# clientes'
description: Una guía de inicio rápido que muestra cómo escribir la lógica de inicialización para un Microsoft Information Protection (MIP) SDK C# las aplicaciones cliente.
author: tommoser
ms.service: information-protection
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.date: 01/04/2019
ms.author: tommos
ms.openlocfilehash: 17c7bb1bd887b4009f450cb5bbf75900587de4f1
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56252103"
---
# <a name="quickstart-client-application-initialization-c"></a>Inicio rápido: Inicialización de la aplicación cliente (C#)

Este inicio rápido le mostrará cómo implementar el patrón de inicialización del cliente, utilizado por el contenedor de .NET SDK de MIP en tiempo de ejecución.

> [!NOTE]
> Los pasos descritos en este tutorial rápido son necesarios para cualquier aplicación cliente que utiliza el contenedor de .NET de MIP archivo o directiva de API. La API de protección no está aún disponible. Aunque en esta guía de inicio rápido se muestra cómo usar las API de archivo, este mismo patrón puede aplicarse en los clientes que usen las API de protección y directiva. Las guías de inicio rápido futuras se realizarán en serie, ya que cada una se basa en la anterior, siendo esta la primera.

## <a name="prerequisites"></a>Requisitos previos

Si aún no lo ha hecho, asegúrese de:

- Completar los pasos que se indican en [Instalación y configuración del SDK de Microsoft Information Protection (MIP)](setup-configure-mip.md). La guía de inicio rápido “Inicialización de la aplicación cliente” se basa en la instalación y configuración del SDK adecuada realizada anteriormente.
- Opcionalmente:
  - Vea [Objetos de perfil y motor](concept-profile-engine-cpp.md). Los objetos de perfil y motor son conceptos universales que necesitan los clientes que usan las API de protección, directiva o archivos de MIP. 
  - Vea [Conceptos de autenticación](concept-authentication-cpp.md) para obtener información sobre cómo la aplicación cliente y el SDK implementan el consentimiento y la autenticación.

## <a name="create-a-visual-studio-solution-and-project"></a>Crear un proyecto y una solución de Visual Studio

Primero, crearemos y configuraremos el proyecto y la solución de Visual Studio iniciales en los que se basan el resto de las guías de inicio rápido.

1. Abra Visual Studio 2017, seleccione el menú **Archivo**, **Nuevo**, **Proyecto**. En el cuadro de diálogo **Nuevo proyecto**:
   - En el panel izquierdo, bajo **instalado**, **Visual C#** , seleccione **Windows Desktop**.
   - En el panel central, seleccione **aplicación de consola (.NET Framework)**
   - En el panel inferior, actualice el **Nombre** y la **Ubicación** del proyecto, así como el **Nombre de la solución** que lo contiene.
   - Cuando haya terminado, haga clic en el botón **Aceptar** de la parte inferior derecha. 

     [![Crear la solución de Visual Studio](media/quick-app-initialization-csharp/create-vs-solution.png)](media/quick-app-initialization-csharp/create-vs-solution.png#lightbox)

2. Agregue al proyecto el paquete NuGet para la API de archivo del SDK de MIP:
   - En el **Explorador de soluciones**, haga clic con el botón derecho en el nodo de proyecto (justo debajo del nodo de la solución superior) y seleccione **Administrar paquetes NuGet…**:
   - Cuando se abra la pestaña **Administrador de paquetes NuGet** en el área de pestañas del grupo del editor:
     - Seleccione **Examinar**.
     - Escriba “Microsoft.InformationProtection” en el cuadro de búsqueda.
     - Seleccione el paquete “Microsoft.InformationProtection.File”.
     - Haga clic en “Instalar” y, cuando se muestre el cuadro de diálogo de confirmación **Vista previa de los cambios**, haga clic en “Aceptar”.

3. Repita los pasos anteriores para agregar el paquete de la API de archivo del SDK de MIP, pero en su lugar, agregue "Microsoft.IdentityModel.Clients.ActiveDirectory" a la aplicación.

## <a name="implement-an-authentication-delegate"></a>Implementar un delegado de autenticación

El SDK de MIP implementa la autenticación con la extensibilidad de la clase, que proporciona un mecanismo para compartir la autenticación con la aplicación cliente. El cliente tiene que obtener un token de acceso de OAuth2 adecuado y proporcionarlo al SDK de MIP en tiempo de ejecución.

Ahora cree una implementación para un delegado de autenticación, extendiendo el SDK `Microsoft.InformationProtection.IAuthDelegate` interfaz y reemplazar e implementar el `IAuthDelegate.AcquireToken()` función virtual. El delegado de autenticación se crea y se utiliza más adelante el `FileProfile` y `FileEngine` objetos.

1. Haga clic en el nombre del proyecto en Visual Studio, seleccione **agregar** , a continuación, **clase**.
2. Escriba "AuthDelegateImplementation" en el **nombre** campo. Haga clic en **Agregar**.
3. Agregar instrucciones using para Active Directory Authentication Library (ADAL) y la biblioteca de MIP:

     ```csharp
     using Microsoft.InformationProtection;
     using Microsoft.IdentityModel.Clients.ActiveDirectory;
     ```

4. Establecer `AuthDelegateImplementation` heredar `Microsoft.InformationProtection.IAuthDelegate` e implementar una variable privada de `Microsoft.InformationProtection.ApplicationInfo` y un constructor que acepta el mismo tipo.

     ```csharp
     public class AuthDelegateImplementation : IAuthDelegate
     {
        private ApplicationInfo _appInfo;
        private string redirectUri = "mip-sdk-app://authorize";
        public AuthDelegateImplementation(ApplicationInfo appInfo)
        {
            _appInfo = appInfo;
        }
     }
     ```

La `ApplicationInfo` objeto contiene dos propiedades. El `_appInfo.ApplicationId` se usará en el `AuthDelegateImplementation` clase para proporcionar el identificador de cliente a la biblioteca de autenticación.

5. Agregar el `public string AcquireToken()` clase. Esta clase debe aceptar `Microsoft.InformationProtection.Identity`y dos cadenas: autoridad y recursos. Estas variables de cadena se pasará en la biblioteca de autenticación mediante la API y no deberían ser manipuladas. Edición puede producir un error de autenticación.

     ```csharp
     public string AcquireToken(Identity identity, string authority, string resource)
     {
          AuthenticationContext authContext = new AuthenticationContext(authority);
          var result = authContext.AcquireTokenAsync(resource, _appInfo.ApplicationId, new Uri(redirectUri), new PlatformParameters(PromptBehavior.Auto, null), UserIdentifier.AnyUser).Result;
          return result.AccessToken;
     }
     ```

## <a name="implement-a-consent-delegate"></a>Implementar un delegado de consentimiento

Ahora cree una implementación para un delegado de consentimiento, extendiendo el SDK `Microsoft.InformationProtection.IConsentDelegate` interfaz y la implementación de invalidación/`GetUserConsent()`. Se creará una instancia del delegado de consentimiento y se usará más tarde con los objetos del motor de archivo y de perfil de archivo. El delegado de consentimiento es proporcionada con la dirección del servicio el usuario debe dar su consentimiento para usar en el `url` parámetro. El delegado generalmente debe proporcionar algún flujo que permite al usuario Aceptar o rechazar para dar su consentimiento para acceder al servicio. Para esta guía de inicio rápido codificar `Consent.Accept`.

1. Con la misma característica “Agregar clase” de Visual Studio que hemos usado anteriormente, agregue otra clase al proyecto. En este momento, escriba "ConsentDelegateImplementation" en el **nombre de la clase** campo. 

2. Actualizar ahora **ConsentDelegateImpl.cs** para implementar la nueva clase de delegado de consentimiento. Agregar el uso de la instrucción para `Microsoft.InformationProtection` y establezca la clase para heredar `IConsentDelegate`.

     ```csharp
     class ConsentDelegateImplementation : IConsentDelegate
     {
          public Consent GetUserConsent(string url)
          {
               return Consent.Accept;
          }
     }
     ```

3. Si lo desea, intenta compilar la solución para asegurarse de que se compila sin errores.

## <a name="initialize-the-mip-sdk-managed-wrapper"></a>Inicializar el contenedor administrado del SDK de MIP

1. Desde **el Explorador de soluciones**, abra el archivo .cs en el proyecto que contiene la implementación de la `Main()` método. El valor predeterminado es el mismo nombre que el proyecto que lo contiene, el cual ha especificado al crear el proyecto.

2. Quite la implementación generada de `main()`. 

3. El contenedor administrado incluye una clase estática, `Microsoft.InformationProtection.MIP` utiliza para la inicialización, los perfiles de carga y, liberando los recursos. Para inicializar el contenedor para las operaciones de API de archivo, llame a MIP. Initialize, pasando `MipComponent.File` para cargar las bibliotecas necesarias para las operaciones de archivo. 

4. En `Main()` en *Program.cs* agregue lo siguiente, reemplazando **\<identificador de la aplicación\>** con el identificador del registro de aplicación de AD Azure creado anteriormente.

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.InformationProtection;
using Microsoft.InformationProtection.File;

namespace mip_sdk_dotnet_quickstart
{
    class Program
    {
        private const string clientId = "<application-id>";
        private const string appName = "<friendly-name>";

        static void Main(string[] args)
        {
            //Initialize Wrapper for File API operations 
            MIP.Initialize(MipComponent.File);
        }
    }
}
```

## <a name="construct-a-file-profile-and-engine"></a>Crear un perfil del archivo y motor

Como se mencionó, los objetos de perfil y del motor son necesarios para clientes del SDK de MIP APIs de uso. Complete la parte de la codificación de este inicio rápido, mediante la adición de código para cargar los archivos DLL nativas, a continuación, crear instancias de los objetos de perfil y del motor.

   ```csharp
using System;
using System.Threading.Tasks;
using Microsoft.InformationProtection;
using Microsoft.InformationProtection.File;

namespace mip_sdk_dotnet_quickstart
{
     class Program
     {
          private const string clientId = "<application-id>";
          private const string appName = "<friendly-name>";

          static void Main(string[] args)
          {
               //Initialize Wrapper for File API operations
               MIP.Initialize(MipComponent.File);

               //Create ApplicationInfo, setting the clientID from Azure AD App Registration as the ApplicationId
               ApplicationInfo appInfo = new ApplicationInfo()
               {
                    ApplicationId = clientId,
                    ApplicationName = appName,
                    ApplicationVersion = "1.0.0"
               };

               //Instatiate the AuthDelegateImpl object, passing in AppInfo. 
               AuthDelegateImplementation authDelegate = new AuthDelegateImplementation(appInfo);

               //Initialize and instantiate the File Profile
               //Create the FileProfileSettings object
               var profileSettings = new FileProfileSettings("mip_data", false, authDelegate, new ConsentDelegateImplementation(), appInfo, LogLevel.Trace);

               //Load the Profile async and wait for the result
               var fileProfile = Task.Run(async () => await MIP.LoadFileProfileAsync(profileSettings)).Result;

               //Create a FileEngineSettings object, then use that to add an engine to the profile
               var engineSettings = new FileEngineSettings("user1@tenant.com", "", "en-US");
               engineSettings.Identity = new Identity("user1@tenant.com");
               var fileEngine = Task.Run(async () => await fileProfile.AddEngineAsync(engineSettings)).Result;
          }
     }
}
``` 

3. Reemplace los valores de marcador de posición en el código fuente que pegó en, mediante los siguientes valores:

   | Marcador | Valor | Ejemplo |
   |:----------- |:----- |:--------|
   | \<application-id\> | El identificador de aplicación de Azure AD asignado a la aplicación registrada en “Instalación y configuración del SDK de MIP” (dos instancias).  | 0edbblll-8773-44de-b87c-b8c6276d41eb |
   | \<friendly-name\> | Nombre descriptivo definido por el usuario para la aplicación. | AppInitialization |


4. Ahora, realice una compilación final de la aplicación y solucione los posibles errores. El código debe compilarse correctamente.

## <a name="next-steps"></a>Pasos siguientes

Después de completar el código de inicialización, estará preparado para la próxima guía de inicio rápido, donde empezará a probar las API de archivo de MIP.

> [!div class="nextstepaction"]
> [Mostrar etiquetas de confidencialidad](quick-file-list-labels-csharp.md)
