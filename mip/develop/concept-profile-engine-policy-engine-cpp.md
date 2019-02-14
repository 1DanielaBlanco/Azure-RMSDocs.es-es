---
title: 'Conceptos: el objeto del motor de la API de directiva'
description: Este artículo le ayudará a comprender los conceptos básicos sobre el objeto del motor de directivas, que se crea durante la inicialización de la aplicación.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 9aac5fb0e010c8c73776c3e62ba9e98bdeff77d2
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56252782"
---
# <a name="microsoft-information-protection-sdk---policy-api-engine-concepts"></a>SDK de Microsoft Information Protection: conceptos del motor de la API de directiva

`mip::PolicyEngine` implementa todas las operaciones que puede realizar la API de directiva, excepto cargar el perfil. 

## <a name="implementation-add-a-policy-engine"></a>Implementación: Agregar un motor de directiva

### <a name="implementation-create-policy-engine-settings"></a>Implementación: Crear la configuración del motor de directiva

De forma similar a un perfil, el motor también necesita un objeto de configuración, `mip::PolicyEngine::Settings`. Este objeto almacena el identificador único del motor, los datos de cliente personalizables que pueden usarse para depurar o para telemetría y, opcionalmente, la configuración regional.

Aquí, creamos un objeto `PolicyEngine::Settings` llamado *engineSettings*.

```cpp
PolicyEngine::Settings engineSettings("UniqueID", "");
```

Le recomendamos que el primer parámetro (**id**) sea algo que permita al motor conectarse fácilmente al usuario asociado (preferiblemente, el nombre principal de usuario).

### <a name="implementation-add-the-policy-engine"></a>Implementación: Agregar el motor de directiva

Para agregar el motor, volveremos al patrón de promesa o futuro usado para cargar el perfil. En lugar de crear la promesa para `mip::Profile`, usaremos `mip::PolicyEngine`.

```cpp

  //auto profile will be std::shared_ptr<mip::Profile>
  auto profile = profileFuture.get();

  //Create the PolicyEngine::Settings object
  PolicyEngine::Settings engineSettings("UniqueID", "");

  //Create a promise for std::shared_ptr<mip::PolicyEngine>
  auto enginePromise = std::make_shared<std::promise<std::shared_ptr<mip::PolicyEngine>>>();

  //Instantiate the future from the promise
  auto engineFuture = enginePromise->get_future();

  //Add the engine using AddEngineAsync, passing in the engine settings and the promise
  profile->AddEngineAsync(engineSettings, enginePromise);

  //get the future value and store in std::shared_ptr<mip::PolicyEngine>
  auto engine = engineFuture.get();
```

El resultado final del código anterior es que hemos agregado correctamente al perfil un motor para el usuario autenticado.

## <a name="implementation-list-sensitivity-labels"></a>Implementación: Mostrar etiquetas de confidencialidad

Después de agregar el motor, ahora se puede mostrar una lista de todas las etiquetas de confidencialidad disponibles para el usuario autenticado mediante una llamada a `engine->ListSensitivityLabels()`.

`ListSensitivityLabels()` capturará la lista de etiquetas y atributos de esas etiquetas para un usuario específico del servicio. El resultado se almacena en un vector de `std::shared_ptr<mip::Label>`.

### <a name="implementation-listsensitivitylabels"></a>Implementación: ListSensitivityLabels()

```cpp
std::vector<shared_ptr<mip::Label>> labels = engine->ListSensitivityLabels();
```

### <a name="implementation-print-the-labels"></a>Implementación: Imprimir las etiquetas

```cpp
//Iterate through all labels in the vector
for (const auto& label : labels) {
  //print the label name
  cout << label->GetName() << endl;
  //Iterate through all child labels
  for (const auto& child : label->GetChildren()) {
    //Print the label with some formatting
    cout << "->  " << child->GetName() << endl;
  }
}
```

Imprimir los nombres es una forma sencilla de mostrar que hemos extraído correctamente la directiva del servicio y hemos podido obtener las etiquetas. Para aplicar la etiqueta, se necesita el identificador de la etiqueta. Al modificar el fragmento anterior para devolver el identificador de etiqueta, se obtiene este resultado:

```cpp
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

