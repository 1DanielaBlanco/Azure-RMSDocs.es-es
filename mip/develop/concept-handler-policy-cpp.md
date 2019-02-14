---
title: 'Conceptos: controladores de directivas en el SDK de MIP.'
description: Este artículo le ayudará a comprender cómo se crean y usan los controladores de la API de directiva para llamar a operaciones.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 11/16/2018
ms.author: tommos
ms.openlocfilehash: cc35475086de76b869428c62cfc35e73fc3060db
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56258783"
---
# <a name="microsoft-information-protection-sdk---policy-handler-concepts"></a>SDK de Microsoft Information Protection: conceptos del controlador de directivas

En la API de la directiva, `mip::PolicyHandler` expone las operaciones que se usan para calcular las acciones de directiva y enviar eventos de auditoría.

## <a name="policy-handler-functions"></a>Funciones del controlador de directivas

`mip::PolicyHandler` expone métodos para leer, escribir y quitar información de protección y etiquetas. Vea la lista completa en la [Referencia de la API](reference/class_mip_PolicyHandler.md).

En este artículo, se explicarán los métodos siguientes:

- `ComputeActions`
- `NotifyCommittedActions`

## <a name="requirements"></a>Requisitos

Para crear un elemento `PolicyHandler` se necesita:

- Una función `PolicyProfile`
- Una función `PolicyEngine` agregada a `PolicyProfile`
- Una clase que hereda `mip::PolicyHandler::Observer`

## <a name="create-a-policy-handler"></a>Crear un controlador de directivas

El primer paso necesario para obtener acciones de directiva consiste en crear un objeto `PolicyHandler`. Esta clase implementa la funcionalidad necesaria para obtener la lista de acciones que debe realizar una etiqueta específica. También implementa la función para desencadenar un evento de auditoría.

Crear el objeto `PolicyHandler` es tan fácil como llamar a la función `CreatePolicyHandlerAsync` de `PolicyEngine` con el patrón de promesa o futuro.

`CreatePolicyHandlerAsync` acepta un único parámetro: **isAuditDiscoveryEnabled**. Establezca este valor en **true** si la aplicación debe mostrar los eventos de latido en el registro de auditoría.

> [!NOTE]
> La clase `mip::PolicyHandler::Observer` tiene que implementarse en una clase derivada, ya que `CreatePolicyHandler` necesita el objeto `Observer`. 

```cpp
auto createPolicyHandlerPromise = std::make_shared<std::promise<std::shared_ptr<mip::PolicyHandler>>>();
auto createPolicyHandlerFuture = createPolicyHandlerPromise->get_future();
PolicyEngine->CreatePolicyHandlerAsync(true);
auto handler = createPolicyHandlerFuture.get();
```

Después de crear correctamente el objeto `PolicyHandler`, se pueden calcular las acciones y se pueden enviar los eventos de auditoría.

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha aprendido sobre la creación de un controlador de la directiva:

- Obtenga información sobre cómo [crear una clase de estado de ejecución](concept-handler-policy-executionstate-cpp.md), que se usa para determinar las acciones del proceso.
- Descargue el [ejemplos de directivas de API desde GitHub y pruebe la API de directiva](https://azure.microsoft.com/resources/samples/?sort=0&term=mipsdk+policyapi)
