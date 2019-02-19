---
title: 'Conceptos: controladores de archivos en el SDK de MIP.'
description: Este artículo le ayudará a comprender cómo se crean y usan los controladores de la API de archivo para llamar a operaciones.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: b021f5a05ad484b32af3a189c10522564da6d86d
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56254856"
---
# <a name="microsoft-information-protection-sdk---file-handler-concepts"></a>SDK de Microsoft Information Protection: conceptos del controlador de archivos

En la API de archivo del SDK de MIP, el objeto `mip::FileHandler` expone las distintas operaciones que pueden usarse para las etiquetas de lectura y escritura o protección en todo un conjunto de tipos de archivo en los que se integra la compatibilidad. 

## <a name="supported-file-types"></a>Tipos de archivo admitidos

- Formatos de archivo de Office basados en OCP (Office 2010 y versiones posteriores)
- Formatos de archivo de Office heredados (Office 2007)
- PDF
- Compatibilidad con archivos PFILE genéricos
- Archivos compatibles con Adobe XMP

## <a name="file-handler-functions"></a>Funciones del controlador de archivos

`mip::FileHandler` expone métodos para leer, escribir y quitar información de protección y etiquetas. Vea la lista completa en la [Referencia de la API](reference/class_mip_filehandler.md).

En este artículo, se explicarán los métodos siguientes:

- `GetLabelAsync()`
- `SetLabel()`
- `DeleteLabel()`
- `CommitAsync()`

## <a name="requirements"></a>Requisitos

Para crear un elemento `FileHandler` con el fin trabajar con un archivo específico, se necesita lo siguiente:

- Una función `FileProfile`
- Una función `FileEngine` agregada a `FileProfile`
- Una clase que hereda `mip::FileHandler::Observer`

## <a name="create-a-file-handler"></a>Crear un controlador de archivos

El primer paso necesario para administrar cualquier archivo en la API de archivo es crear un objeto `FileHandler`. Esta clase implementa todas las funciones necesarias para obtener, establecer, actualizar, eliminar y confirmar cambios de etiquetas en los archivos.

Crear el objeto `FileHandler` es tan fácil como llamar a la función `CreateFileHandlerAsync` de `FileEngine` con el patrón de promesa o futuro.

`CreateFileHandlerAsync` acepta tres parámetros: La ruta de acceso al archivo que se debe leer o modificar, el `mip::FileHandler::Observer` para notificaciones de eventos asincrónicos y el compromiso para el `FileHandler`.

**Nota:** La clase `mip::FileHandler::Observer` tiene que implementarse en una clase derivada, ya que `CreateFileHandler` necesita el objeto `Observer`. 

```cpp
auto createFileHandlerPromise = std::make_shared<std::promise<std::shared_ptr<mip::FileHandler>>>();
auto createFileHandlerFuture = createFileHandlerPromise->get_future();
fileEngine->CreateFileHandlerAsync(filePath, std::make_shared<FileHandlerObserver>(), createFileHandlerPromise);
auto handler = createFileHandlerFuture.get();
```

Después de crear correctamente el objeto `FileHandler`, se pueden realizar operaciones de archivo (get/set/delete/commit).

## <a name="read-a-label"></a>Leer una etiqueta

### <a name="metadata-requirements"></a>Requisitos de metadatos

Hay algunos requisitos para leer correctamente metadatos desde un archivo y traducirlos en contenido que pueda usarse en las aplicaciones.

- La etiqueta leída tiene que existir aún en el servicio de Office 365. Si se ha eliminado por completo, el SDK no podrá obtener información sobre esa etiqueta y mostrará un error.
- Los metadatos del archivo tienen que estar intactos. En los metadatos, se incluye lo siguiente:
  - Atributo1
  - Atributo2

### <a name="getlabelasync"></a>GetLabelAsync()

Después de crear el controlador para apuntar a un archivo específico, devolvemos el patrón de promesa o futuro para leer la etiqueta de forma asincrónica. La promesa es para un objeto `mip::ContentLabel` que contiene toda la información sobre la etiqueta aplicada.

Después de crear las instancias de los objetos `promise` y `future`, leemos la etiqueta (para hacerlo, realice una llamada a `handler->GetLabelAsync()` y especifique el elemento `promise` como el único parámetro). Por último, la etiqueta se puede almacenar en un objeto `mip::ContentLabel` que se obtendrá desde el elemento `future`.

```cpp
auto loadPromise = std::make_shared<std::promise<std::shared_ptr<mip::ContentLabel>>>();
auto loadFuture = loadPromise->get_future();
handler->GetLabelAsync(loadPromise);
auto label = loadFuture.get();
```

Los datos de etiquetas se pueden leer desde el objeto `label` y se pueden pasar a cualquier otro componente o función en la aplicación.

***

## <a name="set-a-label"></a>Establecer una etiqueta

El proceso para establecer una etiqueta consta de dos partes. Primero, después de crear un controlador que apunte al archivo en cuestión, se puede establecer la etiqueta si se realiza una llamada a `FileHandler->SetLabel()` con un par de parámetros.

```cpp
handler->SetLabel(label->GetId(), mip::LabelingOptions{ mip::AssignmentMethod::PRIVILEGED, "" });
```

El primer parámetro es simplemente el identificador de etiqueta de `ListLabelsAsync()`. Este valor se puede almacenar en una variable dedicada o mediante la lectura de `mip::Label->GetId()`.

En el ejemplo anterior, se da por hecho que hemos guardado el objeto `mip::Label` deseado en un objeto llamado `label`.

### <a name="labeling-options"></a>Opciones de etiquetado

El segundo parámetro necesario para establecer la etiqueta es un objeto `mip::LabelingOptions` que creamos insertado al llamar a la función `SetLabel()`. También se puede crear con antelación.

`LabelingOptions` especifica información adicional sobre la etiqueta, como el objeto `AssignmentMethod` y la justificación para una acción.

- `mip::AssignmentMethod` es simplemente un enumerador que tiene tres valores: `STANDARD`, `PRIVILEGED` o `AUTO`. Para obtener más información, revise la referencia de `mip::AssignmentMethod`.
- La justificación solo es necesaria si la directiva del servicio la exige *y* al reducir la confidencialidad *existente* de un archivo.

```cpp
auto labelingOptions = mip::LabelingOptions();
labelingOptions.SetMethod(mip::AssignmentMethod::STANDARD);
labelingOptions.SetJustificationMessage("Because I made an educated decision based upon the contents of this file.");
```

Ahora, en lugar de crear las opciones de etiquetado insertadas, se pueden pasar a la función `SetLabel()`.

```cpp
handler->SetLabel(label->GetId(), labelingOptions);
```

Después de establecer la etiqueta en el archivo al que hace referencia el controlador, es necesario completar un paso más para confirmar el cambio y escribir un archivo en el disco o crear un flujo de salida.

### <a name="commit-changes"></a>Confirmar cambios

El último paso al confirmar cualquier cambio en un archivo en el SDK de MIP es **confirmar** el cambio. Para hacerlo, se usa la función `FileHandler->CommitAsync()`. 

Para implementar la función de confirmación, devolvemos la promesa o futuro y creamos una promesa para `bool`. La función `CommitAsync()` devolverá “true” si la operación se ha completado correctamente o “false” si se producen errores por cualquier motivo. 

Después de crear el `promise` y `future`, `CommitAsync()` se llama y dos parámetros proporcionados: La ruta de acceso del archivo de salida (`std::string`) y la promesa. Por último, el resultado se obtiene mediante el valor del objeto `future`.

```cpp
auto commitPromise = std::make_shared<std::promise<bool>>();
auto commitFuture = commitPromise->get_future();
handler->CommitAsync(outputFile, commitPromise);
auto wasCommitted = commitFuture.get();
```

**Importante:** El `FileHandler` no actualice ni sobrescribir archivos existentes. El desarrollador tiene que implementar el **reemplazo** del archivo etiquetado. 

Si se escribe una etiqueta para el **ArchivoA.docx**, se creará una copia del archivo (**ArchivoB.docx**) con la etiqueta aplicada. Es necesario escribir código para quitar o cambiar el nombre del **ArchivoA.docx** y para cambiar el nombre del **ArchivoB.docx**.

***

## <a name="delete-a-label"></a>Eliminar una etiqueta

```cpp
auto handler = mEngine->CreateFileHandler(filePath, std::make_shared<FileHandlerObserverImpl>());
handler->DeleteLabel(mip::AssignmentMethod::PRIVILEGED, "Label unnecessary.");
auto commitPromise = std::make_shared<std::promise<bool>>();
auto commitFuture = commitPromise->get_future();
handler->CommitAsync(outputFile, commitPromise);
```
