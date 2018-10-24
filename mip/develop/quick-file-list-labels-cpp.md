---
title: 'Inicio rápido: mostrar etiquetas de confidencialidad en un inquilino de Microsoft Information Protection (MIP) que usa el SDK de MIP en C++'
description: Una guía de inicio rápido donde se muestra cómo usar el SDK de Microsoft Information Protection en C++ para mostrar una lista de las etiquetas de confidencialidad en el inquilino.
author: BryanLa
ms.service: information-protection
ms.topic: quickstart
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: fc8d4b43bae9a7b74edef10947ef5aa22e5d1267
ms.sourcegitcommit: d677088db8588fb2cc4a5d7dd296e76d0d9a2e9c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/03/2018
ms.locfileid: "48251784"
---
# <a name="quickstart-list-sensitivity-labels-c"></a>Inicio rápido: mostrar etiquetas de confidencialidad (C++)

En esta guía de inicio rápido, se muestra cómo usar la API de archivo de MIP para crear una lista de las etiquetas de confidencialidad configuradas para su organización.

## <a name="prerequisites"></a>Requisitos previos

Si aún no lo ha hecho, asegúrese de completar los siguientes requisitos previos antes de continuar:

- Complete primero la [Guía de inicio rápido: inicialización de la aplicación cliente (C++)](quick-app-initialization-cpp.md), que compila una solución de Visual Studio inicial. La guía de inicio rápido “Mostrar etiquetas de confidencialidad” se basa en la guía de inicio rápido anterior para crear correctamente la solución inicial.
- Opcional: revisar los conceptos de las [etiquetas de clasificación](concept-classification-labels.md).

## <a name="add-logic-to-list-the-sensitivity-labels"></a>Agregar una lógica para mostrar una lista de las etiquetas de confidencialidad

Agregue una lógica para mostrar una lista de las etiquetas de confidencialidad de la organización con el objeto del motor de archivo. 

1. Abra la solución de Visual Studio que ha creado en el artículo anterior “Inicio rápido: inicialización de la aplicación cliente (C++)”.

2. Mediante el **Explorador de soluciones**, abra el archivo .cpp en el proyecto que contiene la implementación del método `main()`. El valor predeterminado es el mismo nombre que el proyecto que lo contiene, el cual ha especificado al crear el proyecto. 

3. Agregue la siguiente directiva de `using` después de `using mip::FileEngine;`, cerca de la parte superior del archivo:

   ```cpp
   using std::endl;
   ```

4. Cerca del final del cuerpo de `main()`, debajo de la llave de cierre `}` del bloque `catch` y encima de `return 0;` (donde haya terminado en la guía de inicio rápido anterior), inserte el código siguiente:

   ```cpp
   // List sensitivity labels
   cout << "\nSensitivity labels for your organization:\n";
   auto labels = engine->ListSensitivityLabels();
   for (const auto& label : labels)
   {
      cout << label->GetName() << " : " << label->GetId() << endl;

      for (const auto& child : label->GetChildren())
      {
        cout << "->  " << child->GetName() << " : " << child->GetId() << endl;
      }
   }
   system("pause");
   ``` 

## <a name="create-a-powershell-script-to-generate-access-tokens"></a>Crear un script de PowerShell para generar tokens de acceso

Use el siguiente script de PowerShell para generar tokens de acceso, según lo que solicite el SDK. El script usa el cmdlet `Get-ADALToken` del módulo ADAL.PS que ha instalado anteriormente en “Instalación y configuración del SDK de MIP”. 

1. Cree un archivo de script de PowerShell (extensión .ps1) y, después, copie y pegue el script siguiente en el archivo:

   - Actualice las variables `$appId` y `$redirectUri` para hacer coincidir los valores especificados en el registro de la aplicación de Azure AD. 
   - `$authority` y `$resourceUrl` se actualizan más tarde en la sección siguiente.

   ```powershell
   $authority = '<authority-url>'                   # Enforced by MIP SDK
   $resourceUrl = '<resource-url>'                  # Enforced by MIP SDK; matches a resource/API URL requested in the app registration
   $appId = '0edbblll-8773-44de-b87c-b8c6276d41eb'  # App ID of the Azure AD app registration
   $redirectUri = 'bltest://authorize'              # Must match the redirect URI of the Azure AD app registration
   $response = Get-ADALToken -Resource $resourceUrl -ClientId $appId -RedirectUri $redirectUri -Authority $authority -PromptBehavior:RefreshSession 
   $response.AccessToken | clip                     # Copy the access token text to the clipboard
   ```

2. Guarde el archivo de script para poder ejecutarlo más tarde, cuando lo solicite la aplicación cliente.

## <a name="build-and-test-the-application"></a>Compilar y probar la aplicación

Compile y pruebe la aplicación cliente. 

1. Presione F6 (**Compilar solución**) para compilar la aplicación cliente. Si no aparece ningún error de compilación, presione F5 (**Iniciar depuración**) para ejecutar la aplicación.

2. Si el proyecto se compila y se ejecuta correctamente, la aplicación pedirá un token de acceso cada vez que el SDK llame al método `AcquireOAuth2Token()`. Puede reutilizar un token generado anteriormente si se le pide varias veces y los valores solicitados son los mismos:

   ```console
   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/common/oauth2/authorize
   Set $resourceUrl to: https://syncservice.o365syncservice.com/
   Be sure to sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token:
   ```

3. Para proporcionar una respuesta a la petición anterior, vuelva al script de PowerShell y:

   - Actualice las variables `$authority` y `$resourceUrl`. Tienen que coincidir con los valores especificados en la salida de la consola del paso 2. El SDK de MIP proporciona estos valores en el parámetro `challenge` de `AcquireOAuth2Token()`:
     - `$authority` tiene que ser `https://login.windows.net/common/oauth2/authorize`
     - `$resourceUrl` tiene que ser `https://syncservice.o365syncservice.com/` o `https://aadrm.com`
   - Ejecute el script de PowerShell. El cmdlet `Get-ADALToken` desencadena una petición de autenticación de Azure AD similar al ejemplo siguiente. Especifique la misma cuenta proporcionada en la salida de la consola del paso 2. Después de iniciar sesión correctamente, el token de acceso se copiará en el Portapapeles.

     [![Inicio de sesión para la obtención del token por Visual Studio](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox)

   - Puede que también necesite conceder permiso para que la aplicación acceda a las API de MIP mientras se ejecuta con la cuenta de inicio de sesión. Esto ocurre cuando no se concede de forma previa el registro de la aplicación de Azure AD (como se indica en “Instalación y configuración del SDK de MIP”), o bien si ha iniciado sesión con una cuenta desde otro inquilino (un inquilino donde no se ha registrado la aplicación). Solo tiene que hacer clic en **Aceptar** para registrar el consentimiento.

     [![Consentimiento de Visual Studio](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

4. Después de especificar los tokens de acceso, en la salida de la consola se mostrarán las etiquetas de confidencialidad, de forma similar al ejemplo siguiente:

   ```console
   Non-Business : 87ba5c36-17cf-14793-bbc2-bd5b3a9f95cz
   Public : 83867195-f2b8-2ac2-b0b6-6bb73cb33afz
   General : f42a3342-8706-4288-bd31-ebb85995028z
   Confidential : 074e457c-5848-4542-9a6f-34a182080e7z
   Highly Confidential : f55c2dea-db0f-47cd-8520-a52e1590fb6z

   Press any key to continue . . .
   ```

   > [!NOTE]
   > Copie y guarde el identificador de una o más de las etiquetas de confidencialidad (por ejemplo, `f42a3342-8706-4288-bd31-ebb85995028z`), ya que las usará en la próxima guía de inicio rápido.

## <a name="troubleshooting"></a>Solucionar problemas

### <a name="problems-during-execution-of-powershell-script"></a>Problemas durante la ejecución del script de PowerShell 

| Resumen | Mensaje de error | Solución |
|---------|---------------|----------|
| URI de redireccionamiento incorrecto en el registro de la aplicación o el script de PowerShell (AADSTS50011) |*AADSTS50011: la URL de respuesta especificada en la solicitud no coincide con las URL de respuesta configuradas para la aplicación: “ac6348d6-0d2f-4786-af33-07ad46e69bfc”.* | Para comprobar el URI de redireccionamiento usado, siga uno de estos procedimientos:<br><br><li>Actualice el URI de redireccionamiento en la configuración de la aplicación de Azure AD para que coincida con el script de PowerShell. Vea [Instalación y configuración del SDK de MIP](setup-configure-mip.md#register-a-client-application-with-azure-active-directory) para asegurarse de que ha configurado correctamente la propiedad del URI de redireccionamiento.<br><li>Actualice la variable `redirectUri` en el script de PowerShell para que coincida con el registro de la aplicación. |
| Cuenta de inicio de sesión incorrecta (AADSTS50020) | *AADSTS50020: la cuenta de usuario “user@domain.com” del proveedor de identidades “https://sts.windows.net/72f988bl-86f1-41af-91ab-2d7cd011db47/” no existe en el inquilino “nombre de la organización” y no se puede acceder a la aplicación “0edbblll-8773-44de-b87c-b8c6276d41eb” en ese inquilino.* | Siga uno de estos procedimientos:<br><br><li>Vuelva a ejecutar el script de PowerShell, pero asegúrese de usar una cuenta del mismo inquilino donde se ha registrado la aplicación de Azure AD.<br><li>Si la cuenta de inicio de sesión era correcta, es posible que la sesión del host de PowerShell ya se haya autenticado con otra cuenta. En ese caso, salga del host del script y, después, vuelva a abrirlo e intente volver a ejecutarlo.<br><li>Si usa esta guía de inicio rápido con una aplicación web (en lugar de una aplicación nativa) y necesita iniciar sesión con una cuenta desde otro inquilino, asegúrese de que el registro de la aplicación de Azure AD esté habilitado para el uso multiinquilino. Para verificarlo, use la característica “Editar manifiesto” en el registro de la aplicación y asegúrese de que especifique `"availableToOtherTenants": true,`. |
| Permisos incorrectos en el registro de la aplicación (AADSTS65005) | *AADSTS65005: recurso no válido. El cliente ha solicitado el acceso a un recurso, que no se muestra en los permisos solicitados del registro de la aplicación del cliente. Identificador de la aplicación cliente: 0edbblll-8773-44de-b87c-b8c6276d41eb. Valor de recurso de la solicitud: https://syncservice.o365syncservice.com/. Identificador de la aplicación del recurso: 870c4f2e-85b6-4d43-bdda-6ed9a579b725. Lista de recursos válidos del registro de la aplicación: 00000002-0000-0000-c000-000000000000.* | Actualice las solicitudes de permisos en la configuración de la aplicación de Azure AD. Vea [Instalación y configuración del SDK de MIP](setup-configure-mip.md#register-a-client-application-with-azure-active-directory) para asegurarse de que ha configurado correctamente las solicitudes de permisos en el registro de la aplicación. |

### <a name="problems-during-execution-of-c-application"></a>Problemas durante la ejecución de la aplicación en C++

| Resumen | Mensaje de error | Solución |
|---------|---------------|----------|
| Token de acceso incorrecto | *Se ha producido una excepción… ¿Es incorrecto el token de acceso o ha expirado?<br><br>Llamada API incorrecta: profile_add_engine_async Error: [clase mip::PolicySyncException] No se pudo obtener la directiva, la solicitud ha producido errores con el código de estado HTTP: 401, x-ms-diagnostics: [2000001;reason="el token de OAuth enviado con la solicitud no se puede analizar.";error_category="invalid_token"], correlationId:[35bc0023-3727-4eff-8062-000006d5d672]<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe (proceso 29924) se ha cerrado con el código 0.<br><br>Presione cualquier tecla para cerrar esta ventana…* | Si el proyecto se compila correctamente, pero se muestra un resultado similar al que aparece a la izquierda, es probable que tenga un token no válido o expirado en el método `AcquireOAuth2Token()`. Vuelva al paso [Actualizar la lógica de obtención de tokens](#update-the-token-acquisition-logic-with-a-valid-access-token) y genere de nuevo el token de acceso, vuelva a actualizar `AcquireOAuth2Token()` y, por último, repita la compilación y las pruebas. También puede examinar y verificar el token y sus notificaciones con la aplicación web de una página [jwt.ms](https://jwt.ms/). |
| Las etiquetas de confidencialidad no se han configurado | n/a | Si el proyecto se compila correctamente, pero no se muestra ningún resultado en la ventana de la consola, asegúrese de que las etiquetas de confidencialidad de la organización se hayan configurado correctamente. Para obtener más información, vea [Instalación y configuración del SDK de MIP](setup-configure-mip.md) en “Definir la configuración de protección y taxonomía de etiquetas”.  |

## <a name="next-steps"></a>Pasos siguientes

Ahora que ya conoce cómo mostrar una lista de las etiquetas de confidencialidad de la organización, pruebe la siguiente guía de inicio rápido:

> [!div class="nextstepaction"]
> [Establecer y obtener una etiqueta de confidencialidad](quick-file-set-get-label-cpp.md)
