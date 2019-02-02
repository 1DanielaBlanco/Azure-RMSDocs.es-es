---
title: 'Inicio rápido: Mostrar etiquetas de confidencialidad en un inquilino de Microsoft Information Protection (MIP) mediante el SDK de MIP C# contenedor'
description: Una guía de inicio rápido que muestra cómo usar el SDK de Microsoft Information Protection C# contenedor para mostrar las etiquetas de confidencialidad de su inquilino.
author: BryanLa
ms.service: information-protection
ms.topic: quickstart
ms.date: 01/04/2019
ms.author: bryanla
ms.openlocfilehash: 52432a1d6be683d6ed40d95e653ef42353b58400
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651901"
---
# <a name="quickstart-list-sensitivity-labels-c"></a>Inicio rápido: Lista de las etiquetas de confidencialidad (C#)

En este tutorial rápido se muestra cómo usar la API de archivo del SDK de MIP para mostrar las etiquetas de confidencialidad configuradas para su organización.

## <a name="prerequisites"></a>Requisitos previos

Si aún no lo ha hecho, asegúrese de completar los siguientes requisitos previos antes de continuar:

- Completa [inicio rápido: Inicialización de la aplicación cliente (C#)](quick-app-initialization-csharp.md) first, que crea un inicio de solución de Visual Studio. La guía de inicio rápido “Mostrar etiquetas de confidencialidad” se basa en la guía de inicio rápido anterior para crear correctamente la solución inicial.
- Opcionalmente: Revisión [etiquetas de clasificación](concept-classification-labels.md) conceptos.

## <a name="add-logic-to-list-the-sensitivity-labels"></a>Agregar una lógica para mostrar una lista de las etiquetas de confidencialidad

Agregue una lógica para mostrar una lista de las etiquetas de confidencialidad de la organización con el objeto del motor de archivo. 

1. Abra la solución de Visual Studio que creó en el anterior "Guía de inicio rápido: Inicialización de la aplicación cliente (C#) "artículo.

2. Uso de **el Explorador de soluciones**, abra el archivo .cs en el proyecto que contiene la implementación de la `Main()` método. El valor predeterminado es el mismo nombre que el proyecto que lo contiene, el cual ha especificado al crear el proyecto. 

3. Hacia el final de la `Main()` cuerpo, debajo de la llave de cierre `}` de la `Main()` función (donde lo dejó en el tutorial anterior), inserte el código siguiente:

  ```csharp
  // List sensitivity labels from fileEngine and display name and id  
  foreach(var label in fileEngine.SensitivityLabels)
  {
      Console.WriteLine(string.Format("{0} : {1}", label.Name, label.Id));

      if (label.Children.Count != 0)
      {
          foreach (var child in label.Children)
          {
              Console.WriteLine(string.Format("{0}{1} : {2}", "\t",child.Name, child.Id));
          }
      }
  }
  ``` 

## <a name="build-and-test-the-application"></a>Compilar y probar la aplicación

Compile y pruebe la aplicación cliente. 

1. Use CTRL-MAYÚS-B (**compilar solución**) para compilar la aplicación cliente. Si no aparece ningún error de compilación, presione F5 (**Iniciar depuración**) para ejecutar la aplicación.

2. Si el proyecto se compila y se ejecuta correctamente, la aplicación *puede* solicitará la autenticación mediante AAL cada vez las llamadas SDK su `AcquireToken()` método. Si ya existen credenciales almacenadas en caché, no se pedirá que inicie sesión y ver la lista de etiquetas. 

     [![Inicio de sesión para la obtención del token por Visual Studio](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox)

   - Puede que también necesite conceder permiso para que la aplicación acceda a las API de MIP mientras se ejecuta con la cuenta de inicio de sesión. Esto ocurre cuando no se concede de forma previa el registro de la aplicación de Azure AD (como se indica en “Instalación y configuración del SDK de MIP”), o bien si ha iniciado sesión con una cuenta desde otro inquilino (un inquilino donde no se ha registrado la aplicación). Solo tiene que hacer clic en **Aceptar** para registrar el consentimiento.

     [![Consentimiento de Visual Studio](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

3. Después de la autenticación, la salida de la consola debería mostrar las etiquetas de confidencialidad, similares al ejemplo siguiente:

  ```console
  Personal : 73c47c6a-eb00-4a6a-8e19-efaada66dee6
  Public : 73254501-3d5b-4426-979a-657881dfcb1e
  General : da480625-e536-430a-9a9e-028d16a29c59
  Confidential : 569af77e-61ea-4deb-b7e6-79dc73653959
        Recipients Only (C) : d98c4267-727b-430e-a2d9-4181ca5265b0
        All Employees (C) : 2096f6a2-d2f7-48be-b329-b73aaa526e5d
        Anyone (not protected) (C) : 63a945ec-1131-420d-80da-2fedd15d3bc0
  Highly Confidential : 905845d6-b548-439c-9ce5-73b2e06be157
        Recipients Only : 05ee72d9-1a75-441f-94e2-dca5cacfe012
        All Employees : 922b06ef-044b-44a3-a8aa-df12509d1bfe
        Anyone (not protected) : c83fc820-961d-40d4-ba12-c63f72a970a3
  Press a key to continue.
  ```

   > [!NOTE]
   > Copie y guarde el identificador de una o más de las etiquetas de confidencialidad (por ejemplo, `f42a3342-8706-4288-bd31-ebb85995028z`), ya que las usará en la próxima guía de inicio rápido.

## <a name="troubleshooting"></a>Solución de problemas

### <a name="problems-during-execution-of-c-application"></a>Problemas durante la ejecución de C# aplicación

| Resumen | Mensaje de error | Solución |
|---------|---------------|----------|
| Token de acceso incorrecto | *¿Se produjo una excepción... es el token de acceso incorrecto o que haya expirado? <br> <br>Llamada API de error: no se pudo profile_add_engine_async con: [clase mip::PolicySyncException] Error de directiva de adquisición, error de solicitud con el código de estado http: 401, x-ms-diagnostics: [2000001; motivo = "enviada con la solicitud de token de OAuth no se puede analizar."; error_category = "invalid_token"], correlationId: [35bc0023-3727-4eff-8062-000006d5d672]'<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe (proceso 29924) se cerró con el código 0.<br> <br>Presione cualquier tecla para cerrar esta ventana...* | Si el proyecto se compila correctamente, pero se muestra un resultado similar al que aparece a la izquierda, es probable que tenga un token no válido o expirado en el método `AcquireOAuth2Token()`. Vuelva al paso [Actualizar la lógica de obtención de tokens](#update-the-token-acquisition-logic-with-a-valid-access-token) y genere de nuevo el token de acceso, vuelva a actualizar `AcquireOAuth2Token()` y, por último, repita la compilación y las pruebas. También puede examinar y verificar el token y sus notificaciones con la aplicación web de una página [jwt.ms](https://jwt.ms/). |
| Las etiquetas de confidencialidad no se han configurado | n/a | Si el proyecto se compila correctamente, pero no se muestra ningún resultado en la ventana de la consola, asegúrese de que las etiquetas de confidencialidad de la organización se hayan configurado correctamente. Para obtener más información, vea [Instalación y configuración del SDK de MIP](setup-configure-mip.md) en “Definir la configuración de protección y taxonomía de etiquetas”.  |

## <a name="next-steps"></a>Pasos siguientes

Ahora que ya conoce cómo mostrar una lista de las etiquetas de confidencialidad de la organización, pruebe la siguiente guía de inicio rápido:

> [!div class="nextstepaction"]
> [Establecer y obtener una etiqueta de confidencialidad](quick-file-set-get-label-csharp.md)
