---
title: Operaciones para la clave de inquilino de Azure Information Protection
description: Identifique los diferentes niveles de control y responsabilidad que tiene para su clave de inquilino de Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/22/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: a12d0a885b4ed4762124511929bb9f139e8c02db
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39369782"
---
# <a name="operations-for-your-azure-information-protection-tenant-key"></a>Operaciones para la clave de inquilino de Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

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

