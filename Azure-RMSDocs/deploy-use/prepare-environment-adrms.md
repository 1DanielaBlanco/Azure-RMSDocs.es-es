---
title: "Preparación del entorno para Azure RMS y AD RMS"
description: "Use esta guía si tiene Azure Rights Management con AD RMS implementado."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 11ffa730-c5dc-4b6b-9c1e-c58eff8aafc2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 577f91958c4b54c4fb023d973475c917b28f72b3
ms.sourcegitcommit: 7bec3dfe3ce61793a33d53691046c5b2bdba3fb9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/27/2017
---
# <a name="preparing-the-environment-for-azure-rights-management-when-you-also-have-active-directory-rights-management-services-ad-rms"></a>Preparación del entorno para Azure Rights Management con Active Directory Rights Management Services (AD RMS)

>*Se aplica a: Azure Information Protection, Office 365*

Instrucciones importantes si ya usa Active Directory Rights Management Services (AD RMS) y se aplica el siguiente contexto:

## <a name="you-see-an-option-to-activate-azure-rms-when-you-configure-azure-information-protection"></a>Al configurar Azure Information Protection, verá una opción para activar Azure RMS.

La hoja **Azure Information Protection: configuración de RMS (versión preliminar)** tiene una opción para activar el servicio Azure Rights Management (Azure RMS). 

Si también usa Active Directory Rights Management Services (AD RMS), no seleccione la opción **Activar**. Esto se debe a que, si también tiene AD RS, no es posible activar Azure Rights Management. Esta combinación no es compatible, ya que ofrece resultados que no son de confianza, de modo que es importante que no active Azure Rights Management en este momento. 

Cuando esté listo para mover los equipos de AD RMS al servicio Azure Rights Management, inicie el proceso de migración. Uno de los pasos de la migración es activar el servicio, pero tiene que hacerlo después de haber exportado la información de AD RMS al servicio Azure Rights Management. Este proceso garantiza que los documentos y los correos electrónicos protegidos con AD RMS se sigan pudiendo abrir.

Si el servicio Azure Rights Management no está activado, podrá seguir usando Azure Information Protection para las etiquetas que solo se apliquen a la clasificación. Se creará una directiva predeterminada especial que no incluirá la protección de datos. Estas opciones de configuración seguirán sin estar disponibles hasta que se active el servicio Azure Rights Management.

### <a name="step-1-configure-your-azure-information-protection-policy-for-classification-and-labeling---without-protection"></a>Paso 1: Configuración de la directiva de Azure Information Protection para la clasificación y el etiquetado (sin protección)

Desde la hoja **Azure Information Protection** inicial, seleccione **Directiva global** para ver y configurar la directiva predeterminada, que no incluirá opciones para la protección de datos. Para más información, consulte [Configuración de la directiva de Azure Information Protection](configure-policy.md).

### <a name="step-2-start-planning-for-migration"></a>Paso 2: Inicio del planeamiento de la migración

Siga la guía [Migración desde AD RMS a Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

### <a name="step-3-start-to-configure-labels-for-protection"></a>Paso 3: Inicio de la configuración de las etiquetas para la protección

Después de haber activado el servicio Azure Rights Management como parte del proceso de migración, podrá configurar etiquetas para la protección de datos. Sin embargo, si migra usuarios en lotes, asegúrese de que las etiquetas que apliquen la protección solo tengan como [ámbito](configure-policy-scope.md) los usuarios que se hayan migrado.


[!INCLUDE[Commenting house rules](../includes/houserules.md)]


