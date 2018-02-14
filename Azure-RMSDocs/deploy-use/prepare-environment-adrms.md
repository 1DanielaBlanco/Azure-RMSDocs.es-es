---
title: "Preparación del entorno para Azure Rights Management Services y Active Directory Rights Management Services"
description: Instrucciones, si dispone de Azure Rights Management con Active Directory Rights Management Services implementado.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 11ffa730-c5dc-4b6b-9c1e-c58eff8aafc2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 6d7a1d2ed61e1d12d6ca50db50c5b516e6e4f54e
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/29/2018
---
# <a name="preparing-the-environment-for-azure-rights-management-when-you-also-have-active-directory-rights-management-services-ad-rms"></a>Preparación del entorno para Azure Rights Management si también tiene Active Directory Rights Management Services (AD RMS)

>*Válido para: Azure Information Protection, Office 365*

Instrucciones importantes si ya usa Active Directory Rights Management Services (AD RMS) y se aplica el siguiente contexto:

## <a name="you-see-an-option-to-activate-protection-when-you-configure-azure-information-protection"></a>Verá una opción para activar la protección al configurar Azure Information Protection

La hoja **Azure Information Protection: Activación de la protección** tiene una opción para activar el servicio Azure Rights Management (Azure RMS). 

Si también usa Active Directory Rights Management Services (AD RMS), no seleccione la opción **Activar**. Activar Azure Rights Management junto con AD RMS no es una combinación compatible. Este escenario no se admite y sus resultados son poco confiables, por lo que es importante que no active Azure Rights Management en este momento. 

Cuando esté preparado para pasar los equipos de AD RMS al servicio Azure Rights Management, podrá iniciar un proceso de migración. Uno de los pasos de la migración es activar el servicio, pero hágalo después de haber exportado la información de configuración de AD RMS al servicio Azure Rights Management. Este proceso garantiza que se sigan pudiendo abrir los documentos y mensajes de correo electrónico que se protegieran con AD RMS.

Cuando el servicio Azure Rights Management no está activado, podrá seguir usando Azure Information Protection para las etiquetas que se aplican solo a la clasificación. Se crea una directiva predeterminada especial que no incluye la protección de datos y esas opciones de configuración siguen sin estar disponibles hasta que el servicio Azure Rights Management se activa.

### <a name="step-1-configure-your-azure-information-protection-policy-for-classification-and-labeling---without-protection"></a>Paso 1: Configuración de la directiva de Azure Information Protection para la clasificación y etiquetado (sin protección)

Desde la hoja **Azure Information Protection** inicial, seleccione **Directiva global** para ver y configurar la directiva predeterminada que no incluya opciones para la protección de datos. Para más información, consulte [Configuración de la directiva de Azure Information Protection](configure-policy.md).

### <a name="step-2-start-planning-for-migration"></a>Paso 2: Inicio del planeamiento de la migración

Siga la guía [Migración desde AD RMS a Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

### <a name="step-3-start-to-configure-labels-for-protection"></a>Paso 3: Inicio de la configuración de las etiquetas para la protección

Después de haber activado el servicio Azure Rights Management como parte del proceso de migración, podrá configurar etiquetas para la protección de datos. Sin embargo, si migra los usuarios en lotes, asegúrese de que el [ámbito](configure-policy-scope.md) de las etiquetas que apliquen la protección se limite solo a los usuarios migrados.


[!INCLUDE[Commenting house rules](../includes/houserules.md)]


