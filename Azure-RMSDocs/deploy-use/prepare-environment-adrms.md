---
title: Preparación del entorno para Azure RMS y AD RMS
description: Use esta guía si tiene Azure Rights Management con AD RMS implementado.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/29/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 11ffa730-c5dc-4b6b-9c1e-c58eff8aafc2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 142f8b0683cbf18fb72cec303587481f3e9e3018
ms.sourcegitcommit: 6bdc1e5c328ad3b63aeb6f60ba9905551261a7a1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2018
ms.locfileid: "37137821"
---
# <a name="preparing-the-environment-for-azure-rights-management-when-you-also-have-active-directory-rights-management-services-ad-rms"></a>Preparación del entorno para Azure Rights Management con Active Directory Rights Management Services (AD RMS)

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!IMPORTANT]
> Orientaciones para el uso de Active Directory Rights Management Services (AD RMS)

Si el servicio Azure Rights Management está activado y también usa AD RMS, esta combinación no es compatible. Sin seguir pasos adicionales, algunos equipos podrían empezar a usar el servicio de Azure Rights Management automáticamente, así como conectarse a su clúster de AD RMS. Esta combinación no es compatible y ofrece resultados que no son de confianza, así que es importante que adopte medidas adicionales. 

**Para comprobar si ha implementado AD RMS:**

1. Aunque es opcional, la mayoría de las implementaciones de AD RMS publican el punto de conexión de servicio en Active Directory para que los equipos del dominio puedan detectar el clúster de AD RMS. 
    
    Utilice el Editor ADSI para ver si tiene un punto de conexión de servicio publicado en Active Directory: `CN=Configuration [server name], CN=Services, CN=RightsManagementServices, CN=SCP`

2. Si no usa un punto de conexión de servicio, los equipos de Windows que se conectan a un clúster de AD RMS deben configurarse para la detección de servicios de cliente o el redireccionamiento de la administración de licencias mediante el Registro de Windows: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation` o `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSIPC\ServiceLocation`
    
    Para obtener más información acerca de estas configuraciones del Registro, consulte [Habilitación de la detección de servicios del cliente con el Registro de Windows](../rms-client/client-deployment-notes.md#enabling-client-side-service-discovery-by-using-the-windows-registry) y [Redirección del tráfico del servidor de licencias](../rms-client/client-deployment-notes.md#redirecting-licensing-server-traffic).   

Si se implementa AD RMS para su organización, considere si puede migrar a Azure Information Protection. Azure Information Protection plantea muchas ventajas respecto a AD RMS. Por ejemplo, una mejor compatibilidad con dispositivos móviles e integración con servicios de Office 365, así como con Exchange Server y SharePoint Server. Para obtener más información, consulte [Comparación de Azure Information Protection y AD RMS](../understand-explore/compare-on-premise.md).

Al migrar a Azure Information Protection, no perderá el acceso al contenido protegido anteriormente y no tiene que desproteger o volver a proteger su contenido. Los documentos y los correos electrónicos protegidos con AD RMS se puedan seguir abriendo incluso después de desaprovisionar AD RMS.

Si decide migrar a Azure Information Protection o decide aceptar las limitaciones del uso de la implementación de AD RMS actual, primero debe asegurarse de que el servicio Azure Rights Management está desactivado. Para obtener instrucciones, siga los pasos para el escenario que se aplica a su situación:

- [La suscripción que incluye Azure Rights Management se compró en febrero de 2018 o después](#your-subscription-was-purchased-during-or-after-february-2018).

- [La suscripción se compró antes de febrero de 2018 o en ese mes y tiene Exchange Online](#your-subscription-was-purchased-before-or-during-february-2018-and-you-have-exchange-online)

- [Al configurar la directiva de Azure Information Protection en Azure Portal, verá una opción para activar la protección](#you-see-an-option-to-activate-protection-when-you-configure-azure-information-protection).


## <a name="your-subscription-was-purchased-during-or-after-february-2018"></a>La suscripción se compró en febrero de 2018 o después

Hacia finales de febrero de 2018, las nuevas suscripciones que incluyan Azure Information Protection activarán el servicio Azure Rights Management de forma predeterminada. Si este servicio se activa automáticamente y también usa Active Directory Rights Management Services (AD RMS), esta combinación no es compatible, así que es importante que desactive el servicio Active Directory Rights Management Services lo antes posible. 

### <a name="step-1-deactivate-azure-rights-management"></a>Paso 1: Desactivar Azure Rights Management
Use uno de los procedimientos siguientes para desactivar [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

> [!TIP]
> También puede usar el cmdlet [Disable-Aadrm](/powershell/module/aadrm/disable-aadrm) de Windows PowerShell para desactivar el servicio Azure Rights Management.

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

2. Seleccione **Activación de la protección** en las opciones del menú. 

3.  En la hoja **Azure Information Protection - Protección de la activación**, seleccione **Desactivar**. Seleccione **Sí** para confirmar su elección.

En la barra de información se muestra **Deactivation finished successfully** (La desactivación ha finalizado correctamente) y **Activar** reemplaza a **Desactivar**. 

### <a name="step-2-start-planning-for-migration"></a>Paso 2: Inicio del planeamiento de la migración

Consulte la guía [Migración desde AD RMS a Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).


## <a name="your-subscription-was-purchased-before-or-during-february-2018-and-you-have-exchange-online"></a>La suscripción se compró antes de febrero de 2018 o en ese mes y tiene Exchange Online

Microsoft está empezando a activar el servicio Azure Rights Management para las suscripciones que incluyen Azure Rights Management o Azure Information Protection, y los inquilinos usan Exchange Online. Para estos inquilinos, la activación automática empezará a aplicarse a partir del 1 de agosto de 2018.

Si el servicio se activa automáticamente y también usa AD RMS, esta combinación no es compatible, por lo que es importante que el inquilino no participe en la actualización automática del servicio. 

### <a name="step-1-opt-out-from-the-automatic-service-update"></a>Paso 1: No participar en la actualización automática del servicio

Use el siguiente comando [Set-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/set-irmconfiguration) de PowerShell para Exchange Online:`Set-IRMConfiguration -AutomaticServiceUpdateEnabled $false`

[Más información](https://support.office.com/article/protection-features-in-azure-information-protection-rolling-out-to-existing-office-365-tenants-7ad6f58e-65d7-4c82-8e65-0b773666634d) 

### <a name="step-2-start-planning-for-migration"></a>Paso 2: Inicio del planeamiento de la migración

Consulte la guía [Migración desde AD RMS a Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).


## <a name="you-see-an-option-to-activate-protection-when-you-configure-azure-information-protection"></a>Al configurar Azure Information Protection, verá una opción para activar la protección.

La hoja **Azure Information Protection: activación de la protección** tiene una opción para activar el servicio Azure Rights Management.  

Si también usa AD RMS, no seleccione la opción **Activar**. Si el servicio Azure Rights Management no está activado, podrá seguir usando Azure Information Protection para las etiquetas que solo se apliquen a la clasificación. Se creará una directiva predeterminada especial que no incluirá la protección de datos. Estas opciones de configuración seguirán sin estar disponibles hasta que se active el servicio Azure Rights Management.

### <a name="step-1-configure-your-azure-information-protection-policy-for-classification-and-labeling---without-protection"></a>Paso 1: Configuración de la directiva de Azure Information Protection para la clasificación y el etiquetado (sin protección)

En la hoja **Azure Information Protection: etiquetas**, vea y configure las etiquetas que no incluyen opciones para la protección de datos. Para obtener más información sobre cómo configurar las etiquetas y los parámetros de directivas, consulte [Configuración de la directiva de Azure Information Protection](configure-policy.md).

### <a name="step-2-start-planning-for-migration"></a>Paso 2: Inicio del planeamiento de la migración

Consulte la guía [Migración desde AD RMS a Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

### <a name="step-3-configure-labels-for-protection"></a>Paso 3: Configuración de etiquetas para la protección

Después de haber activado el servicio Azure Rights Management como parte del proceso de migración, podrá configurar etiquetas para la protección de datos. Pero si migra usuarios en lotes, asegúrese de que las etiquetas que apliquen la protección tengan como ámbito únicamente los usuarios migrados.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

