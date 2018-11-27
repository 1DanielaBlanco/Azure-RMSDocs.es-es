---
title: 'Conceptos: implementar ExecutionState en el SDK de Microsoft Information Protection'
description: Este artículo le ayudará a entender cómo se utiliza el elemento ExecutionState en el SDK de Microsoft Information Protection para calcular acciones y proporcionar detalles para el registro de auditoría.
services: information-protection
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/01/2018
ms.author: tommos
ms.openlocfilehash: 71cc6f08e130fe4a97604924643d13fd341a5625
ms.sourcegitcommit: ef70dab87478084fca853f389dab2408b95d1df1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/26/2018
ms.locfileid: "52304170"
---
# <a name="implement-executionstate"></a>Implementar ExecutionState

La operación de pasar información al SDK de MIP para calcular una acción que se debe llevar a cabo, según el estado actual y el estado deseado, se implementa con la clase `mip::ExecutionState`. Al igual que las demás clases del SDK, `ExecutionState` es una clase abstracta que debe implementar el desarrollador.

> Para ver un ejemplo completo de una implementación de `ExecutionState`, observe el siguiente origen de ejemplo:
>
> * [execution_state_impl.h](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic/blob/master/mipsdk-policyapi-cpp-sample-basic/execution_state_impl.h)
> * [execution_state_impl.cpp](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic/blob/master/mipsdk-policyapi-cpp-sample-basic/execution_state_impl.cpp)

## <a name="mipexecutionstate-members"></a>mip::ExecutionState Members

`ExecutionState` expone los siguientes miembros virtuales. Cada uno de ellos proporciona algún contexto al motor de directivas para devolver información sobre las acciones que debería llevar a cabo la aplicación. Además, esta información se puede emplear para proporcionar información de auditoría a la característica Azure Information Protection Reporting.


| Miembro                                                                           | Devuelve                                                                                                              |
|----------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| `std::string GetNewLabelId()`                                                      | Devuelve el identificador de etiqueta que se va a aplicar al objeto.                                                                    |
| `mip::ContentState GetContentState()`                                              | Devuelve el elemento mip::ContentState del objeto.                                                                         |
| `std::pair<bool, std::string> IsDowngradeJustified()`                              | Devuelve un elemento a std::pair que expresa si la degradación está justificada o no, así como la justificación correspondiente.                                 |
| `std::string GetContentIdentifier()`                                               | Devuelve el identificador de contenido. Debe ser un identificador legible que indique la ubicación del objeto.   |
| `mip::ActionSource GetNewLabelActionSource()`                                      | Devuelve el elemento mip::ActionSource de la etiqueta.                                                                          |
| `mip::AssignmentMethod GetNewLabelAssignmentMethod()`                              | Devuelve el elemento mip::AssignmentMethod de la etiqueta.                                                                        |
| `std::vector<std::pair<std::string, std::string>> GetNewLabelExtendedProperties()` | Devuelve un elemento std::vector de std::pairs de cadenas, que contiene los metadatos personalizados que se aplicarán al documento. |
| `std::vector<std::pair<std::string, std::string>> GetContentMetadata()`            | Devuelve un elemento std::vector de std::pairs de la cadena que contiene los metadatos del contenido actual.                               |
| `std::shared_ptr<mip::ProtectionDescriptor> GetProtectionDescriptor()`           | Devuelve un puntero a un elemento mip::ProtectionDescriptor.                                                                     |
| `mip::ContentFormat GetContentFormat()`                                            | Devuelve el elemento mip::ContentFormat.                                                                                           |
| `mip::ActionType GetSupportedActions()`                                           | Devuelve el elemento mip::ActionTypes de la etiqueta.                                                                              |

Todos ellos deben invalidarse en una implementación de una clase derivada de `mip::ExecutionState`. En la aplicación de ejemplo que se indica arriba, este proceso se efectúa implementando una estructura llamada `ExecutionStateOptions` y pasándola al constructor de la clase derivada.

En el [ejemplo](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic/blob/master/mipsdk-policyapi-cpp-sample-basic/execution_state_impl.h), se define una estructura llamada `ExecutionStateOptions` del siguiente modo:

```cpp
struct ExecutionStateOptions {
    std::unordered_map<std::string, std::string> metadata;
    std::string newLabelId;
    std::string contentIdentifier;
    mip::ActionSource actionSource = mip::ActionSource::MANUAL;
    mip::ContentState contentState = mip::ContentState::REST;
    mip::AssignmentMethod assignmentMethod = mip::AssignmentMethod::STANDARD;
    bool isDowngradeJustified = false;
    std::string downgradeJustification;
    std::string templateId;
    mip::ContentFormat contentFormat = mip::ContentFormat::DEFAULT;
};
```

Cada propiedad la establece la aplicación. Luego, se pasa `ExecutionStateOptions` al constructor de la clase derivada de `mip::ExecutionState`. Esta información se emplea para determinar las acciones que se deben llevar a cabo. Los datos proporcionados en `mip::ExecutionState` también se mostrarán en Azure Information Protection Analytics.

### <a name="next-steps"></a>Pasos siguientes

- Obtenga información sobre cómo determinar [acciones para una etiqueta nueva o existente de proceso](concept-handler-policy-computeactions-cpp.md), según el estado actual y el deseado.
- Descargue el [ejemplos de directivas de API desde GitHub y pruebe la API de directiva](https://azure.microsoft.com/resources/samples/?sort=0&term=mipsdk+policyapi)
