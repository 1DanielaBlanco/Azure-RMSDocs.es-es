---
title: 'Conceptos: el objeto de motor de la API de archivo'
description: Este artículo le ayudará a comprender los conceptos básicos sobre el objeto de motor de archivo, que se crea durante la inicialización de la aplicación.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 09b4db10523539f093a54c54d1fc6b7de8f7ddb0
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259293"
---
# <a name="microsoft-information-protection-sdk---file-api-engine-concepts"></a>SDK de Microsoft Information Protection: conceptos del motor de la API de archivo

El elemento `mip::FileEngine` en la API de archivo del SDK de MIP proporciona una interfaz para todas las operaciones que se realizan en nombre de una identidad especificada. Se agregará un motor para cada usuario que inicie sesión en la aplicación; además, todas las operaciones que el motor realiza se llevarán a cabo en el contexto de esa identidad.

El `FileEngine` tiene dos responsabilidades principales: Lista de etiquetas para un usuario autenticado y creación de controladores de archivo para realizar operaciones de archivos en nombre del usuario. 

- [`mip::FileEngine`](reference/class_mip_fileengine.md)
- `ListSensitivityLabels()`: Obtiene la lista de etiquetas para el motor cargado.
- `CreateFileHandler()`: Crea un `mip::FileHandler` para un archivo o flujo concreto.

## <a name="add-a-file-engine"></a>Agregar un motor de archivo

Como se explica en el tema sobre [Objetos de perfil y motor](concept-profile-engine-cpp.md), un motor puede tener dos estados: `CREATED` o `LOADED`. Si no está en uno de estos dos estados, no existe. Para crear y cargar un estado, solo es necesario realizar una única llamada a `FileProfile::LoadAsync`. Si el motor ya existe en el estado almacenado en caché, será `LOADED`. Si no existe, será `CREATED` y `LOADED`. `CREATED` implica que la aplicación tiene toda la información del servicio necesaria para cargar el motor. `LOADED` implica que todas las estructuras de datos necesarias para aprovechar el motor se han creado en la memoria.

### <a name="create-file-engine-settings"></a>Crear la configuración del motor de archivo

De forma similar a un perfil, el motor también necesita un objeto de configuración, `mip::FileEngine::Settings`. Este objeto almacena el identificador único del motor, los datos de cliente personalizables que pueden usarse para depurar o para telemetría y, opcionalmente, la configuración regional.

Aquí, creamos un objeto `FileEngine::Settings` llamado *engineSettings*. 

```cpp
FileEngine::Settings engineSettings("UniqueID", "");
```

Como práctica recomendada, el primer parámetro, `id`, debe ser algo que permita que el motor se conecte fácilmente al usuario asociado. Algo como una dirección de correo electrónico, un UPN o un GUID del objeto de AAD garantizará que el identificador es único y se puede cargar desde el estado local sin llamar al servicio.

### <a name="add-the-file-engine"></a>Agregar el motor de archivo

Para agregar el motor, retrocedemos al patrón de promesa o futuro usado para cargar el perfil. En lugar de crear la promesa para `mip::FileProfile`, se crea mediante `mip::FileEngine`.

```cpp
  //auto profile will be std::shared_ptr<mip::FileProfile>
  auto profile = profileFuture.get();

  //Create the FileEngine::Settings object
  FileEngine::Settings engineSettings("UniqueID", "");

  //Create a promise for std::shared_ptr<mip::FileEngine>
  auto enginePromise = std::make_shared<std::promise<std::shared_ptr<mip::FileEngine>>>();

  //Instantiate the future from the promise
  auto engineFuture = enginePromise->get_future();

  //Add the engine using AddEngineAsync, passing in the engine settings and the promise
  profile->AddEngineAsync(engineSettings, enginePromise);

  //get the future value and store in std::shared_ptr<mip::FileEngine>
  auto engine = engineFuture.get();
```

El resultado final del código anterior es que el motor para el usuario autenticado se agregará al perfil.

## <a name="list-sensitivity-labels"></a>Mostrar etiquetas de confidencialidad

Después de agregar el motor, ahora se puede mostrar una lista de todas las etiquetas de confidencialidad disponibles para el usuario autenticado mediante una llamada a `engine->ListSensitivityLabels()`.

`ListSensitivityLabels()` capturará la lista de etiquetas y atributos de esas etiquetas para un usuario específico del servicio. El resultado se almacena en un vector de `std::shared_ptr<mip::Label>`.

Obtenga más información [aquí]() acerca de `mip::Label`.

### <a name="listsensitivitylabels"></a>ListSensitivityLabels()

```cpp
std::vector<shared_ptr<mip::Label>> labels = engine->ListSensitivityLabels();
```

O bien, de forma simplificada:

```cpp
auto labels = engine->ListSensitivityLabels();
```

### <a name="print-the-labels-and-ids"></a>Imprimir las etiquetas y los identificadores

Imprimir los nombres es una forma sencilla de mostrar que hemos extraído correctamente la directiva del servicio y hemos podido obtener las etiquetas. Para aplicar la etiqueta, se necesita el identificador de la etiqueta. El código siguiente se repite en todas las etiquetas, mostrando `name` y `id` para cada etiqueta primaria y secundaria.

```cpp
//Iterate through all labels in the vector
for (const auto& label : labels) {
  //Print label name and GUID
  cout << label->GetName() << " : " << label->GetId() << endl;

  //Print child label name and GUID
  for (const auto& child : label->GetChildren()) {
    cout << "->  " << child->GetName() <<  " : " << child->GetId() << endl;
  }
}
```

La recopilación de `mip::Label` que devuelve `GetSensitivityLabels()` puede usarse para mostrar todas las etiquetas disponibles para el usuario y, después, cuando se selecciona, usar el identificador para aplicar etiquetas a un archivo.

## <a name="next-steps"></a>Pasos siguientes

Ahora que se ha cargado el perfil, se ha agregado el motor y tenemos etiquetas, podemos agregar un controlador para empezar a leer, escribir o eliminar etiquetas de los archivos. Consulte [Controladores de archivo en el SDK de MIP](concept-handler-file-cpp.md).

