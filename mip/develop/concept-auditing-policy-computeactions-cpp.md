---
title: 'Conceptos: utilizar el SDK de Microsoft Information Protection para generar eventos de auditoría'
description: Este artículo le ayudará a comprender cómo se utiliza el SDK de Microsoft Information Protection para efectuar cálculos.
services: information-protection
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/01/2018
ms.author: tommos
ms.openlocfilehash: 2bb757746e6a730442ff487492af8676cf7bdcd1
ms.sourcegitcommit: 05fdaf43f74013eecb5886b95b09dd5e00670753
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2018
ms.locfileid: "51297845"
---
# <a name="compute-an-action"></a>Calcular una acción

Tal y como se ha indicado antes, las funciones principales de la API de directiva son las siguientes:
- Enumerar las etiquetas disponibles
- Devolver el conjunto específico de acciones que se deben llevar a cabo según el estado actual y el estado deseado

El último paso del proceso consiste en proporcionar a la función `ComputeActions()` un identificador de etiqueta y, opcionalmente, metadatos sobre la etiqueta existente.

En GitHub encontrará código de ejemplo para este artículo.

* [mipsdk-policyapi-cpp-sample-basic](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic)

## <a name="compute-an-action-for-a-new-label"></a>Calcular una acción para una etiqueta nueva

El cálculo del elemento `mip::Actions` de una etiqueta nueva se puede hacer utilizando el elemento `ExecutionStateImpl` definido en [ExecutionState](concept-auditing-policy-executionstate-cpp.md).

```cpp
// Replace with valid label ID.
string newLabelId = "d7b93a40-4df3-47e4-b2fd-7862fc6b095c"; 
sample::policy::ExecutionStateOptions options;

// Set desired newLabelId in ExecutionStateOptions.
options.newLabelId = newLabelId;

// Initialize ExecutionStateImpl with options, create handler, call ComputeActions.
std::unique_ptr<ExecutionStateImpl> state(new ExecutionStateImpl(options));
auto handler = mEngine->CreatePolicyHandler(false); // Don't generate audit event.
auto actions = handler->ComputeActions(*state);
```

Si solo se escribe el elemento `mip::MetadataActions` devuelto como parte de `actions`, se mostrará lo siguiente:

```cpp
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Enabled : true
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SetDate : 2018-10-23T20:39:06-0800
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Method : Standard
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Name : Contoso FTEs (C)
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SiteId : 94f6984e-8d31-4794-bdeb-3ac89ad2b660
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ActionId : 2266fbe8-a0d9-44e8-bad8-00008f2a0915
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ContentBits : 3
```

El elemento `PolicyHandler` calcula las acciones y devuelve un `std::vector` de `mip::Action`. Es elección del desarrollador de aplicaciones aplicar estos metadatos al archivo o datos.

> [!NOTE]
> En el ejemplo anterior solo se muestra la salida de `mip::MetadataAction`. Para ver un ejemplo de visualización de tipos de acción adicionales, revise las agrupaciones de ejemplo con la [descarga de la API de directiva](https://aka.ms/mipsdkbins).

## <a name="compute-actions-with-an-existing-label"></a>Calcular acciones con una etiqueta existente

Al usar la API de directiva, es elección de la aplicación leer los metadatos del contenido. Estos metadatos se proporcionan a la API como parte del elemento `mip::ExecutionState`. `ComputeActions()` puede controlar operaciones más complejas que al aplicar una etiqueta nueva a un documento sin etiquetar. En el ejemplo siguiente se muestra cómo degradar una etiqueta de un nivel más sensible a un nivel menos sensible, donde ya existe una etiqueta. Este proceso se simula leyéndose en una cadena de metadatos separados por comas y proporcionándose en la API con `mip::ExecutionState`.

> [!NOTE]
> En el ejemplo se utiliza una función de utilidad denominada `SplitString()`. [Aquí](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic/blob/master/mipsdk-policyapi-cpp-sample-basic/utils.cpp) encontrará un ejemplo

```cpp
// Replace with valid label ID.
string newLabelId = "d7b93a40-4df3-47e4-b2fd-7862fc6b095c";

// Comma and Pipe Delimited Metadata.
string metadata = "MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Enabled|true,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SetDate|2018-10-23T21:53:31-0800,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Method|Standard,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Name|Contoso FTEs (C),MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SiteId|94f6984e-8d31-4794-bdeb-3ac89ad2b660,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ActionId|b56491d9-155f-40ff-866f-0000acd85c31,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ContentBits|7";

// Create ExecutionStateOptions and set newLabelId.
sample::policy::ExecutionStateOptions options;
options.newLabelId = newLabelId;

// Split metadata string by commas, store in vector.
vector<string> metadataPairs = sample::utils::SplitString(metadata, ','); 

// Iterate through each string, splitting by the pipe.
// Add each key/value pair to ExecutionStateOptions metadata.
for (const string& metadataPair : metadataPairs) {
    vector<string> keyValue = sample::utils::SplitString(metadataPair, '|');
    options.metadata[keyValue[0]] = keyValue[1];
}

// Initialize ExecutionStateImpl with options, create handler, call ComputeActions
std::unique_ptr<ExecutionStateImpl> state(new ExecutionStateImpl(options));
auto handler = mEngine->CreatePolicyHandler(false); // Don't generate audit event.
auto actions = handler->ComputeActions(*state);
```

El ejemplo anterior puede dar lugar a varias acciones. Estas acciones dependen de las etiquetas que se proporcionan como entrada, así como de la configuración de la etiqueta. Como mínimo, el resultado será una `mip::MetadataAction` que contiene los datos que se van a quitar con `GetMetadataToRemove()` y los datos que se van a agregar con `GetMetadataToAdd()`.

```
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_Enabled : true
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_SetDate : 2018-10-23T23:59:41-0800
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_Method : Standard
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_Name : General
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_SiteId : 94f6984e-8d31-4794-bdeb-3ac89ad2b660
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_ActionId : 447a996b-28ea-482c-b0b5-000075bd4bb3
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_ContentBits : 7
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Name
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Enabled
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SiteId
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SetDate
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Method
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ContentBits
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ActionId
```

## <a name="next-steps"></a>Pasos siguientes

* A continuación, descargue los [ejemplos de la API de directiva en GitHub y pruebe la API de directiva](https://azure.microsoft.com/resources/samples/?sort=0&term=mipsdk+policyapi)
* Obtenga información sobre cómo [pasar eventos de auditoría a la canalización de auditoría de Azure Information Protection](concept-auditing-policy-cpp.md)