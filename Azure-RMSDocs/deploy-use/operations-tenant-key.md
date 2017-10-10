---
title: Operaciones para la clave de inquilino de Azure Information Protection
description: Identifique los diferentes niveles de control y responsabilidad que tiene para su clave de inquilino de Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/22/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: afe33bcee3516589bd87642b0f15206b90a4bb41
ms.sourcegitcommit: faaab68064f365c977dfd1890f7c8b05a144a95c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2017
---
# <a name="operations-for-your-azure-information-protection-tenant-key"></a>Operaciones para la clave de inquilino de Azure Information Protection

>*Se aplica a: Azure Information Protection, Office 365*

Según la topología de claves de inquilino para Azure Information Protection, tiene distintos niveles de control y responsabilidad para la clave de inquilino de Azure Information Protection. Las dos topologías de claves son **administrada por Microsoft** y **administrada por el cliente**.

La administración de su propia clave de inquilino en el Almacén de claves de Azure se conoce como BYOK, o "aportar su propia clave". Para más información sobre este escenario y cómo elegir entre las dos topologías clave, vea [Planeamiento e implementación de su clave de inquilino de Azure Information Protection](../plan-design/plan-implement-tenant-key.md).

En la tabla siguiente se identifican las operaciones que puede realizar según la topología que haya elegido para su clave de inquilino de Azure Information Protection.

|Operación del ciclo de vida|Administrada por Microsoft (predeterminada)|Administrada por el cliente (BYOK)|
|-----------------------|-------------------------------|---------------------------|
|Revocar su clave de inquilino|No automática|Sí|
|Regenerar su clave de inquilino|Sí|Sí|
|Realizar una copia de seguridad y recuperar la clave de inquilino|No|Sí|
|Exportar su clave de inquilino|Sí|No|
|Responder a una infracción|Sí|Sí|

Después de identificar la topología que ha implementado, seleccione uno de los vínculos siguientes para saber más sobre estas operaciones de su clave de inquilino de Azure Information Protection:

- [Clave de inquilino administrada por Microsoft](operations-microsoft-managed-tenant-key.md)
- [Clave de inquilino administrada por el cliente](operations-customer-managed-tenant-key.md)

Sin embargo, si desea crear una clave de inquilino de Azure Information Protection a través de la importación de un dominio de publicación de confianza (TPD) desde Active Directory Rights Management Services, esta operación de importación forma parte de la [migración de AD RMS a Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
