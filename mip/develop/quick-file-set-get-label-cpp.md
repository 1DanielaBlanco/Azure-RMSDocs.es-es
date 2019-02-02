---
title: 'Inicio rápido: establecer y obtener una etiqueta de confidencialidad en un archivo mediante el SDK de MIP de C++'
description: Guía de inicio rápido que muestra cómo usar el SDK de C++ de Microsoft Information Protection para establecer y obtener una etiqueta de confidencialidad en un archivo.
services: information-protection
author: BryanLa
ms.service: information-protection
ms.topic: quickstart
ms.date: 01/18/2019
ms.author: bryanla
ms.openlocfilehash: 4898aefc996c26df5f4831c95be63c9fa1a45dc4
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651214"
---
# <a name="quickstart-set-and-get-a-sensitivity-label-c"></a>Inicio rápido: Establecer y obtener una etiqueta de confidencialidad (C++)

En esta guía de inicio rápido se muestra cómo usar más de las API de archivo de MIP. Al utilizar una de las etiquetas de confidencialidad que aparece en la guía de inicio rápido anterior, utilice un controlador de archivo para establecer y obtener la etiqueta en un archivo. La clase del controlador de archivos expone varias operaciones de configuración/obtención de etiquetas, o de protección, para los tipos de archivo admitidos.

## <a name="prerequisites"></a>Requisitos previos

Si aún no lo ha hecho, asegúrese de completar los siguientes requisitos previos antes de continuar:

- Completa [inicio rápido: Lista de las etiquetas de confidencialidad (C++)](quick-file-list-labels-cpp.md) first, que crea un inicio de la solución de Visual Studio, para obtener una lista de las etiquetas de confidencialidad de la organización. Esta guía de inicio rápido "Establecer y obtener una etiqueta de confidencialidad" se basa en la anterior.
- Opcionalmente: Revisión [controladores de archivos en el SDK de MIP](concept-handler-file-cpp.md) conceptos.

## <a name="implement-an-observer-class-to-monitor-the-file-handler-object"></a>Implemente una clase de observador para supervisar el objeto de controlador de archivos

De forma similar al observador que ha implementado (para el motor y perfil del archivo) en la guía de inicio rápido de inicialización de la aplicación, implemente ahora una clase de observador para un objeto del controlador de archivos.

Crear una implementación básica para un observador de controlador de archivo mediante la ampliación del SDK `mip::FileHandler::Observer` clase. Se crea una instancia del observador, que se usa más adelante para supervisar las operaciones del controlador de archivos.

1. Abra la solución de Visual Studio ha trabajado en el anterior "Guía de inicio rápido: Lista de las etiquetas de confidencialidad (C++) "artículo.

2. Agregue una nueva clase al proyecto, que genera automáticamente los archivos de encabezado/.h e implementación/.cpp:

   - En el **el Explorador de soluciones**, haga clic en el nodo del proyecto nuevo, seleccione **agregar**, a continuación, seleccione **clase**.
   - En el cuadro de diálogo **Agregar clase**:
     - En el campo **Nombre de clase**, escriba "filehandler_observer". Tenga en cuenta que tanto el campo **Archivo .h** como el campo **Archivo .cpp** se rellenan automáticamente, según el nombre especificado.
     - Cuando haya terminado, haga clic en el botón **Aceptar**.

3. Después de generar los archivos .h y .cpp para la clase, ambos archivos se abren en pestañas del Grupo de editores. Ahora, actualice cada archivo para implementar la nueva clase de observador:

   - Actualice "filehandler_observer.h" al seleccionar o eliminar la clase `filehandler_observer` generada. **No** quite las directivas de preprocesador generadas en el paso anterior (#pragma, #include). Después, copie y pegue el siguiente código fuente en el archivo, después de las directivas de preprocesador existentes:

     ```cpp
     #include <memory>
     #include "mip/file/file_engine.h"
     #include "mip/file/file_handler.h"

     class FileHandlerObserver final : public mip::FileHandler::Observer {
     public:
        FileHandlerObserver() { }
        // Observer implementation
        void OnCreateFileHandlerSuccess(const std::shared_ptr<mip::FileHandler>& fileHandler, const std::shared_ptr<void>& context) override;
        void OnCreateFileHandlerFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
        void OnCommitSuccess(bool committed, const std::shared_ptr<void>& context) override;
        void OnCommitFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;       
     };
     ```

   - Actualice "filehandler_observer.cpp" al seleccionar o eliminar la implementación de clase `filehandler_observer` generada. **No** quite las directivas de preprocesador generadas en el paso anterior (#pragma, #include). Después, copie y pegue el siguiente código fuente en el archivo, después de las directivas de preprocesador existentes:

     ```cpp
     void FileHandlerObserver::OnCreateFileHandlerSuccess(const std::shared_ptr<mip::FileHandler>& fileHandler, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileHandler>>>(context);
        promise->set_value(fileHandler);
     }

     void FileHandlerObserver::OnCreateFileHandlerFailure(const std::exception_ptr & error, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileHandler>>>(context);
        promise->set_exception(error);
     }

     void FileHandlerObserver::OnCommitSuccess(bool committed, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<bool>>(context);
        promise->set_value(committed);
     }

     void FileHandlerObserver::OnCommitFailure(const std::exception_ptr & error, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<bool>>(context);
        promise->set_exception(error);
     }
     ```

4. También puede presionar F6 (**Compilar solución**) para ejecutar una compilación o vínculo de prueba de la solución y asegurarse de que se compila correctamente antes de continuar.

## <a name="add-logic-to-set-and-get-a-sensitivity-label"></a>Agregar lógica para establecer y obtener una etiqueta de confidencialidad

Agregue lógica para establecer y obtener una etiqueta de confidencialidad en un archivo mediante el objeto del motor de archivo. 

1. Mediante el **Explorador de soluciones**, abra el archivo .cpp en el proyecto que contiene la implementación del método `main()`. El valor predeterminado es el mismo nombre que el proyecto que lo contiene, el cual ha especificado al crear el proyecto. 

2. Agregue las siguientes directivas `#include` y `using`, debajo de las directivas existentes correspondientes, en la parte superior del archivo:

   ```cpp
   #include "filehandler_observer.h" 
   #include "mip/file/file_handler.h" 

   using mip::FileHandler;
   ```
3. Hacia el final del cuerpo de `main()`, debajo de `system("pause");` y encima de `return 0;` (donde se quedó en la guía de inicio rápido anterior), inserte el código siguiente:

   ```cpp
   // Set up async FileHandler for input file operations
   string filePathIn = "<input-file-path>";
   string contentIdentifier = "<content-identifier>";
   std::shared_ptr<FileHandler> handler;
   try
   {
        auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
        auto handlerFuture = handlerPromise->get_future();
        engine->CreateFileHandlerAsync(
             filePathIn, 
             contentIdentifier,
             mip::ContentState::REST, 
             true, 
             std::make_shared<FileHandlerObserver>(), 
             handlerPromise);
        handler = handlerFuture.get();
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid input file path?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
   }

   // Set a label on input file
   try
   {
        string labelId = "<label-id>";
        cout << "\nApplying Label ID " << labelId << " to " << filePathIn << endl;
        mip::LabelingOptions labelingOptions(mip::AssignmentMethod::PRIVILEGED, mip::ActionSource::MANUAL);
        handler->SetLabel(labelId, labelingOptions);
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid label ID?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
   }

   // Commit changes, save as a different/output file
   string filePathOut = "<output-file-path>";
   try
   {
        cout << "Committing changes" << endl;
        auto commitPromise = std::make_shared<std::promise<bool>>();
        auto commitFuture = commitPromise->get_future();
        handler->CommitAsync(filePathOut, commitPromise);
        if (commitFuture.get()) {
            cout << "\nLabel committed to file: " << filePathOut << endl;
        }
        else {
            cout << "Failed to label: " + filePathOut << endl;
            return 1;
        }
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid commit file path?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
   }
   system("pause");

   // Set up async FileHandler for output file operations
   contentIdentifier = "<content-identifier>";
   try
   {
        auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
        auto handlerFuture = handlerPromise->get_future();
        engine->CreateFileHandlerAsync(
             filePathOut, 
             contentIdentifier,
             mip::ContentState::REST,
             true,
             std::make_shared<FileHandlerObserver>(),
             handlerPromise);

        handler = handlerFuture.get();
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid output file path?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
   }

   // Get the label from output file
   try
   {
        cout << "\nGetting the label committed to file: " << filePathOut << endl;
        auto label = handler->GetLabel();
        cout << "Name: " + label->GetLabel()->GetName() << endl;
        cout << "Id: " + label->GetLabel()->GetId() << endl;
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid label ID?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
   }
   system("pause");
   ```

4. Reemplace los valores de marcador de posición en el código fuente que acaba de pegar en como sigue, con las constantes de cadena:

   | Marcador | Valor |
   |:----------- |:----- |
   | \<input-file-path\> | La ruta de acceso completa a un archivo de entrada de prueba, por ejemplo: `"c:\\Test\\Test.docx"`. |
   | \<content-identifier\> | Un identificador legible para el contenido. Por ejemplo: <ul><li>para un archivo, considere la posibilidad de ruta\nombre_archivo: `"c:\Test\Test.docx"`</li><li>para un correo electrónico, considere la posibilidad de asunto: del remitente: `"RE: Audit design:user1@contoso.com"`</li></ul> |
   | \<label-id\> | Un identificador de etiqueta de confidencialidad, que se copia desde la salida de la consola en la guía de inicio rápido anterior, por ejemplo: `"f42a3342-8706-4288-bd31-ebb85995028z"`. |
   | \<output-file-path\> | La ruta de acceso completa al archivo de salida, que será una copia con la etiqueta del archivo de entrada, por ejemplo: `"c:\\Test\\Test_labeled.docx"`. |

## <a name="build-and-test-the-application"></a>Compilar y probar la aplicación

Compile y pruebe la aplicación cliente. 

1. Presione F6 (**Compilar solución**) para compilar la aplicación cliente. Si no aparece ningún error de compilación, presione F5 (**Iniciar depuración**) para ejecutar la aplicación.

2. Si el proyecto se compila y se ejecuta correctamente, la aplicación solicita un token de acceso, cada vez que las llamadas SDK su `AcquireOAuth2Token()` método. Como hizo anteriormente en la "Lista de las etiquetas de confidencialidad" Inicio rápido, ejecute el script de PowerShell para adquirir el token cada vez, utilizando los valores proporcionados para $authority y $resourceUrl. 

   ```console
   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/common/oauth2/authorize
   Set $resourceUrl to: https://syncservice.o365syncservice.com/
   Sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token: <paste-access-token-here>
   Press any key to continue . . .

   Sensitivity labels for your organization:
   Non-Business : 87ba5c36-17cf-14793-bbc2-bd5b3a9f95cz
   Public : 83867195-f2b8-2ac2-b0b6-6bb73cb33afz
   General : f42a3342-8706-4288-bd31-ebb85995028z
   Confidential : 074e457c-5848-4542-9a6f-34a182080e7z
   Highly Confidential : f55c2dea-db0f-47cd-8520-a52e1590fb6z
   Press any key to continue . . .

   Applying Label ID 074e457c-5848-4542-9a6f-34a182080e7z to c:\Test\Test.docx
   Committing changes

   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/common/oauth2/authorize
   Set $resourceUrl to: https://aadrm.com
   Sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token: <paste-access-token-here>
   Press any key to continue . . .

   Label committed to file: c:\Test\Test_labeled.docx
   Press any key to continue . . .

   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/94f69844-8d34-4794-bde4-3ac89ad2b664/oauth2/authorize
   Set $resourceUrl to: https://aadrm.com
   Sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token: <paste-access-token-here>
   Press any key to continue . . .

   Getting the label committed to file: c:\Test\Test_labeled.docx
   Name: Confidential
   Id: 074e457c-5848-4542-9a6f-34a182080e7z
   Press any key to continue . . .
   ```

Para comprobar la aplicación de la etiqueta, abra el archivo de salida e inspeccione visualmente la configuración de protección de información del documento.

> [!NOTE]
> Si está etiquetando un documento de Office, pero no ha iniciado sesión con una cuenta del inquilino de Azure Active Directory (AD) en la que se ha obtenido el token de acceso (y se configuran las etiquetas de confidencialidad), puede que se le pida que inicie sesión para poder abrir el documento etiquetado. 



