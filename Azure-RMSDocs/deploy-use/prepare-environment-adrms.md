---
title: Preparación del entorno para Azure RMS y AD RMS
description: Use esta guía si tiene Azure Rights Management con AD RMS implementado.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/21/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 11ffa730-c5dc-4b6b-9c1e-c58eff8aafc2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: a233ddab67832e2de59b1fc0727296a8f3017db7
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="preparing-the-environment-for-azure-rights-management-when-you-also-have-active-directory-rights-management-services-ad-rms"></a>Preparación del entorno para Azure Rights Management con Active Directory Rights Management Services (AD RMS)

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Instrucciones importantes si ya usa Active Directory Rights Management Services (AD RMS) y se aplica cualquiera de los siguientes escenarios:

- [La suscripción que incluye Azure Rights Management se compró en febrero de 2018 o después](#your-subscription-was-purchased-during-or-after-february-2018).

- [Al configurar la directiva de Azure Information Protection en Azure Portal, verá una opción para activar la protección](#you-see-an-option-to activate-azure-rights-management-when-you-configure-azure-information-protection).

## <a name="your-subscription-was-purchased-during-or-after-february-2018"></a>La suscripción se compró en febrero de 2018 o después

Hacia finales de febrero de 2018, las nuevas suscripciones que incluyan Azure Information Protection activarán el servicio Azure Rights Management de forma predeterminada. Si este servicio se activa automáticamente para usted y también usa Active Directory Rights Management Services (AD RMS), esta combinación no es compatible. Sin seguir pasos adicionales, algunos equipos podrían empezar a usar el servicio de Azure Rights Management automáticamente, así como conectarse a su clúster de AD RMS. Este escenario no es compatible y tiene unos resultados que no son de confianza, de modo que es importante que desactive el servicio de Azure Rights Management cuanto antes. 

Cuando esté listo para mover los equipos de AD RMS al servicio Azure Rights Management, puede iniciar el proceso de migración. Uno de los pasos de la migración consiste en volver a activar el servicio, pero tiene que seguir este paso después de haber exportado la información de AD RMS al servicio de Azure Rights Management. Este orden garantiza que los documentos y los correos electrónicos protegidos con AD RMS se puedan seguir abriendo.

El primer paso consiste en desactivar el servicio de Azure Rights Management.

### <a name="step-1-deactivate-azure-rights-management"></a>Paso 1: Desactivar Azure Rights Management
Use uno de los procedimientos siguientes para desactivar [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

> [!TIP]
> También puede usar el cmdlet [Disable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629422.aspx) de Windows PowerShell para desactivar [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].

#### <a name="to-deactivate-rights-management-from-the-office-365-admin-center"></a>Para desactivar Rights Management desde el centro de administración de Office 365

1. Vaya a la [página de Rights Management](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) para los administradores de Office 365.
    
    Si se le solicita que inicie sesión, use una cuenta de administrador global de Office 365.

2. En la página **Rights Management** , haga clic en **Desactivar**.

3.  Cuando vea el mensaje **¿Desea desactivar Rights Management?**, haga clic en **Desactivar**.

Ahora debería ver **Rights Management no está activado** y la opción para activarlo.

#### <a name="to-deactivate-rights-management-from-the-azure-portal"></a>Para desactivar Rights Management desde el Portal de Azure

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e [inicie sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal). Después, vaya a la hoja **Azure Information Protection**.
    
    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.
    
    Si no ha tenido acceso antes a la hoja de Azure Information Protection, vea los [pasos adicionales](configure-policy.md#to-access-the-azure-information-protection-blade-for-the-first-time) para agregar esta hoja al portal.

2. En la hoja inicial de **Azure Information Protection**, seleccione **Protección de la activación**. 

3.  En la hoja **Azure Information Protection - Protección de la activación**, seleccione **Desactivar**. Seleccione **Sí** para confirmar su elección.

En la barra de información se muestra **Deactivation finished successfully** (La desactivación ha finalizado correctamente) y **Activar** reemplaza a **Desactivar**. 

### <a name="step-2-start-planning-for-migration"></a>Paso 2: Inicio del planeamiento de la migración

Consulte la guía [Migración desde AD RMS a Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

## <a name="you-see-an-option-to-activate-protection-when-you-configure-azure-information-protection"></a>Al configurar Azure Information Protection, verá una opción para activar la protección.

La hoja **Azure Information Protection: Activación de la protección** tiene una opción para activar el servicio Azure Rights Management (Azure RMS).  

Si también usa Active Directory Rights Management Services (AD RMS), no seleccione la opción **Activar**. Esto se debe a que, si también tiene AD RS, no es posible activar Azure Rights Management. Esta combinación no es compatible, ya que ofrece resultados que no son de confianza, de modo que es importante que no active Azure Rights Management en este momento.  

Cuando esté listo para mover los equipos de AD RMS al servicio Azure Rights Management, inicie el proceso de migración. Uno de los pasos de la migración es activar el servicio, pero tiene que hacerlo después de haber exportado la información de AD RMS al servicio Azure Rights Management. Este proceso garantiza que los documentos y los correos electrónicos protegidos con AD RMS se sigan pudiendo abrir. 

Si el servicio Azure Rights Management no está activado, podrá seguir usando Azure Information Protection para las etiquetas que solo se apliquen a la clasificación. Se creará una directiva predeterminada especial que no incluirá la protección de datos. Estas opciones de configuración seguirán sin estar disponibles hasta que se active el servicio Azure Rights Management.

### <a name="step-1-configure-your-azure-information-protection-policy-for-classification-and-labeling---without-protection"></a>Paso 1: Configuración de la directiva de Azure Information Protection para la clasificación y el etiquetado (sin protección)

Desde la hoja **Azure Information Protection** inicial, seleccione **Directiva global** para ver y configurar la directiva predeterminada, que no incluirá opciones para la protección de datos. Para más información, consulte [Configuración de la directiva de Azure Information Protection](configure-policy.md).

### <a name="step-2-start-planning-for-migration"></a>Paso 2: Inicio del planeamiento de la migración

Consulte la guía [Migración desde AD RMS a Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

### <a name="step-3-start-to-configure-labels-for-protection"></a>Paso 3: Inicio de la configuración de las etiquetas para la protección

Después de haber activado el servicio Azure Rights Management como parte del proceso de migración, podrá configurar etiquetas para la protección de datos. Pero si migra usuarios en lotes, asegúrese de que las etiquetas que apliquen la protección tengan como ámbito únicamente los usuarios migrados.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

