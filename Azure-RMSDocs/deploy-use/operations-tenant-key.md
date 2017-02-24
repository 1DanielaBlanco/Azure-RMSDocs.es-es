---
title: Operaciones para la clave de inquilino de Azure Information Protection
description: Identifique los diferentes niveles de control y responsabilidad que tiene para su clave de inquilino de Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 0895050d1bc0528f9ab230bdeac9e2a3ee787b31


---

# <a name="operations-for-your-azure-information-protection-tenant-key"></a>Operaciones para la clave de inquilino de Azure Information Protection

>*Se aplica a: Azure Information Protection, Office 365*

Según la topología de claves de inquilino (administrada por Microsoft o administrada por el cliente), puede usar diferentes niveles de control y responsabilidad para su clave de inquilino de Azure Information Protection después de su implementación.

La administración de su propia clave de inquilino en el Almacén de claves de Azure se conoce como BYOK, o "aportar su propia clave". Para más información sobre este escenario y acerca de cómo elegir entre las dos topologías clave, vea [Planeamiento e implementación de la clave de inquilino de Azure Rights Management](../plan-design/plan-implement-tenant-key.md).

En la tabla siguiente se identifican las operaciones que puede realizar según la topología que haya elegido para su clave de inquilino de Azure Information Protection.

|Operación del ciclo de vida|Administrada por Microsoft (predeterminada)|Administrada por el cliente (BYOK)|
|-----------------------|-------------------------------|---------------------------|
|Revocar su clave de inquilino|No automática|Sí|
|Vuelva a introducir su clave de inquilino|Sí|Sí|
|Realizar una copia de seguridad y recuperar la clave de inquilino|No|Sí|
|Exportar su clave de inquilino|Sí|No|
|Responder a una infracción|Sí|Sí|

Después de identificar la topología que ha implementado, seleccione una de las secciones siguientes para obtener más información sobre estas operaciones de su clave de inquilino de Azure Information Protection:


- [Clave de inquilino administrada por Microsoft](operations-microsoft-managed-tenant-key.md)
- [Clave de inquilino administrada por el cliente](operations-customer-managed-tenant-key.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



<!--HONumber=Feb17_HO4-->


