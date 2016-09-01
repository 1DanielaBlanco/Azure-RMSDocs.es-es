---
title: "Operaciones para la clave de inquilino de Administración de permisos de Azure | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 08/17/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 437afd88efebd9719a3db98f8ab0ae07403053f7
ms.openlocfilehash: 19cae6be4de2eec65414596976062736af4b63b2


---

# Operaciones para la clave de inquilino de Administración de permisos de Azure

*Se aplica a: Azure Rights Management, Office 365*

En función de la topología de la clave de inquilino (administrada por Microsoft o por el cliente), tiene diferentes niveles de control y responsabilidad para su clave de inquilino de Microsoft Azure Rights Management (Azure RMS) una vez implementada.

La administración de su propia clave de inquilino en el Almacén de claves de Azure se conoce como BYOK, o "aportar su propia clave". Para más información sobre este escenario y acerca de cómo elegir entre las dos topologías clave, vea [Planeamiento e implementación de la clave de inquilino de Azure Rights Management](../plan-design/plan-implement-tenant-key.md).

La tabla siguiente identifica qué operaciones puede realizar en función de la topología que eligió para su clave de inquilino de Azure RMS.

|Operación del ciclo de vida|Administrada por Microsoft (predeterminada)|Administrada por el cliente (BYOK)|
|-----------------------|-------------------------------|---------------------------|
|Revocar su clave de inquilino|No automática|Sí|
|Vuelva a introducir su clave de inquilino|Sí|Sí|
|Realizar una copia de seguridad y recuperar la clave de inquilino|No|Sí|
|Exportar su clave de inquilino|Sí|No|
|Responder a una infracción|Sí|Sí|

Una vez que identifique qué topología implementó, seleccione una de las siguientes secciones para más información sobre estas operaciones de su clave de inquilino de Azure RMS:


- [Clave de inquilino administrada por Microsoft](operations-microsoft-managed-tenant-key.md)
- [Clave de inquilino administrada por el cliente](operations-customer-managed-tenant-key.md)







<!--HONumber=Aug16_HO3-->


