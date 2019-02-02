---
title: 'Inicio rápido: Set y get una etiqueta de confidencialidad en un archivo mediante el C# SDK de MIP'
description: Guía de inicio rápido que muestra cómo usar el contenedor de .NET Microsoft SDK de protección de información para establecer y obtener una etiqueta de confidencialidad en un archivo.
services: information-protection
author: BryanLa
ms.service: information-protection
ms.topic: quickstart
ms.date: 01/09/2019
ms.author: bryanla
ms.openlocfilehash: 726f0cf5b3c087d21323b46c9b7748b545932428
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651969"
---
# <a name="quickstart-set-and-get-a-sensitivity-label-c"></a>Inicio rápido: Establecer y obtener una etiqueta de confidencialidad (C#)

En esta guía de inicio rápido se muestra cómo usar más de las API de archivo de MIP. Al utilizar una de las etiquetas de confidencialidad que aparece en la guía de inicio rápido anterior, utilice un controlador de archivo para establecer y obtener la etiqueta en un archivo. La clase del controlador de archivos expone varias operaciones de configuración/obtención de etiquetas, o de protección, para los tipos de archivo admitidos.

## <a name="prerequisites"></a>Requisitos previos

Si aún no lo ha hecho, asegúrese de completar los siguientes requisitos previos antes de continuar:

- Completa [inicio rápido: Lista de las etiquetas de confidencialidad (C#)](quick-file-list-labels-csharp.md) first, que crea un inicio de la solución de Visual Studio, para obtener una lista de las etiquetas de confidencialidad de la organización. Esta guía de inicio rápido "Establecer y obtener una etiqueta de confidencialidad" se basa en la anterior.
- Opcionalmente: Revisión [controladores de archivos en el SDK de MIP](concept-handler-file-cpp.md) conceptos.

## <a name="add-logic-to-set-and-get-a-sensitivity-label"></a>Agregar lógica para establecer y obtener una etiqueta de confidencialidad

Agregue lógica para establecer y obtener una etiqueta de confidencialidad en un archivo mediante el objeto del motor de archivo. 

1. Uso de **el Explorador de soluciones**, abra el archivo .cs en el proyecto que contiene la implementación de Main()' método. El valor predeterminado es el mismo nombre que el proyecto que lo contiene, el cual ha especificado al crear el proyecto. 

2. Hacia el final del cuerpo de `Main()`, debajo de `Console.ReadKey()` y encima de `}` (donde se quedó en la guía de inicio rápido anterior), inserte el código siguiente:

   ```csharp
     //Set paths and label ID
     string inputFilePath = "<input-file-path>";
     string labelId = "<label-id>";
     string outputFilePath = "<output-file-path>";

     //Create a file handler for that file
     //Note: the 2nd inputFilePath is used to provide a human-readable content identifier for admin auditing. 
     var handler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(inputFilePath, inputFilePath, ContentState.Rest, true)).Result;

     //Set Labeling Options
     LabelingOptions labelingOptions = new LabelingOptions()
     {
          ActionSource = ActionSource.Manual,
          AssignmentMethod = AssignmentMethod.Standard
     };

     // Set a label on input file
     handler.SetLabel(labelId, labelingOptions);

     // Commit changes, save as outputFilePath
     var result = Task.Run(async () => await handler.CommitAsync(outputFilePath)).Result;

     // Create a new handler to read the labeled file metadata
     var handlerModified = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(outputFilePath, outputFilePath, ContentState.Rest, true)).Result;

     // Get the label from output file
     var contentLabel = handlerModified.Label;
     Console.WriteLine(string.Format("Getting the label committed to file: {0}", outputFilePath));
     Console.WriteLine(string.Format("File Label: {0} \r\nIsProtected: {1}", contentLabel.Label, contentLabel.IsProtectionAppliedFromLabel.ToString()));
     Console.WriteLine("Press a key to continue.");
     Console.ReadKey();
   ```

3. Reemplace los valores de marcador de posición en el código fuente que acaba de pegar con los valores siguientes:

   | Marcador | Valor |
   |:----------- |:----- |
   | \<input-file-path\> | La ruta de acceso completa a un archivo de entrada de prueba, por ejemplo: `c:\\Test\\Test.docx`. |
   | \<label-id\> | Un identificador de etiqueta de confidencialidad, que se copia desde la salida de la consola en la guía de inicio rápido anterior, por ejemplo: `f42a3342-8706-4288-bd31-ebb85995028z`. |
   | \<output-file-path\> | La ruta de acceso completa al archivo de salida, que será una copia con la etiqueta del archivo de entrada, por ejemplo: `c:\\Test\\Test_labeled.docx`. |

## <a name="build-and-test-the-application"></a>Compilar y probar la aplicación

Compile y pruebe la aplicación cliente. 

1. Use CTRL-MAYÚS-B (**compilar solución**) para compilar la aplicación cliente. Si no aparece ningún error de compilación, presione F5 (**Iniciar depuración**) para ejecutar la aplicación.

2. Si el proyecto se compila y se ejecuta correctamente, la aplicación *puede* solicitará la autenticación mediante AAL cada vez las llamadas SDK su `AcquireToken()` método. Si ya existen credenciales almacenadas en caché, no se le pida que inicie sesión y ver la lista de etiquetas, seguido de la información en la etiqueta aplicada y modificar el archivo.

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

   Applying Label ID 074e457c-5848-4542-9a6f-34a182080e7z to c:\Test\Test.docx
   Committing changes
   
   Label committed to file: c:\Test\Test_labeled.docx
   Press any key to continue . . .
  
   Getting the label committed to file: c:\Test\Test_labeled.docx
   Name: Confidential
   Id: 074e457c-5848-4542-9a6f-34a182080e7z
   Press any key to continue . . .
   ```

Para comprobar la aplicación de la etiqueta, abra el archivo de salida e inspeccione visualmente la configuración de protección de información del documento.

> [!NOTE]
> Si está etiquetando un documento de Office, pero no ha iniciado sesión con una cuenta del inquilino de Azure Active Directory (AD) en la que se ha obtenido el token de acceso (y se configuran las etiquetas de confidencialidad), puede que se le pida que inicie sesión para poder abrir el documento etiquetado. 
