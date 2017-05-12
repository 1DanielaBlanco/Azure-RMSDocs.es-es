---
title: "Mapa de ruta de implementación de Azure Information Protection"
description: "Siga estos pasos para preparar, implementar y administrar Azure Information Protection en su organización."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/01/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: dcee393a46830b293bde84bc019655ff95d098ad
ms.sourcegitcommit: b471c20eda011a7b75ee801c34081fb4773b64dc
ms.translationtype: HT
ms.contentlocale: es-ES
---
# <a name="azure-information-protection-deployment-roadmap"></a>Mapa de ruta de implementación de Azure Information Protection

>*Se aplica a: Azure Information Protection, Office 365*

Siga este procedimiento para preparar, implementar y administrar Azure Information Protection en su organización.

Si lo que quiere es probar rápidamente Azure Information Protection en lugar de implementarlo en un entorno de producción, vea [Tutorial de inicio rápido para Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md).

> [!IMPORTANT]
> Antes de seguir este procedimiento, asegúrese de revisar los [Requisitos de Azure Information Protection](../get-started/requirements-azure-rms.md).

Elija el mapa de ruta de implementación que sea adecuado para su organización y que coincida con [las funciones y las características de las suscripciones](https://www.microsoft.com/cloud-platform/azure-information-protection-features) que necesite:

- [Usar funciones de clasificación, etiquetado y protección](#deployment-roadmap-for-classification-labeling-and-protection)

- [Usar solo la protección de datos](#deployment-roadmap-for-data-protection-only)


## <a name="deployment-roadmap-for-classification-labeling-and-protection"></a>Mapa de ruta de implementación para clasificación, etiquetado y protección

> [!NOTE]
> ¿Ya usa el servicio Azure Rights Management para la protección de datos? Puede omitir muchos de estos pasos y centrarse en los pasos 3 y 5.1.

### <a name="step-1-confirm-your-subscription-and-assign-user-licenses"></a>Paso 1: Confirmar la suscripción y asignar licencias de usuario
Revise la [información de la suscripción](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) y la [lista de características](https://www.microsoft.com/cloud-platform/azure-information-protection-features) en el sitio de Azure Information Protection para confirmar que la organización tiene una suscripción en la que se incluyen las funciones y las características que necesita. Después, asigne una licencia de esta suscripción a todos los usuarios de la organización que vayan a clasificar, etiquetar y proteger documentos y correos electrónicos.

Nota: No asigne manualmente licencias de usuario desde la suscripción gratuita de RMS para individuos y no utilice esta licencia para administrar el servicio de Azure Rights Management para su organización. Estas licencias se muestran como **Rights Management Adhoc** en el centro de administración de Office 365 y como **RIGHTSMANAGEMENT_ADHOC** al ejecutar el cmdlet de Azure AD PowerShell, [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx). Para obtener más información acerca de cómo se otorga automáticamente la suscripción RMS para individuos y se asigna a los usuarios, consulte [RMS para individuos y Azure Information Protection](../understand-explore/rms-for-individuals.md).


### <a name="step-2-prepare-your-tenant-to-use-azure-information-protection"></a>Paso 2: Preparar el inquilino para usar Azure Information Protection
Antes de empezar a usar Azure Information Protection, siga este procedimiento de preparación:

- Asegúrese de que tiene cuentas de usuario y grupos en Office 365 o Azure Active Directory que Azure Information Protection usará para autenticar y autorizar a los usuarios de la organización. Si es necesario, cree estas cuentas y grupos, o sincronícelos desde el directorio local. Para más información, consulte [Preparación de usuarios y grupos para Azure Information Protection](prepare.md).

### <a name="step-3-configure-and-deploy-classification-and-labeling"></a>Paso 3: Configurar e implementar la clasificación y el etiquetado

Si aún no tiene una estrategia de clasificación, revise la [directiva predeterminada de Azure Information Protection](../deploy-use/configure-policy-default.md) y úsela como base para determinar las etiquetas de clasificación que se asignarán a los datos de la organización. Puede personalizarlas para adaptarlas a sus requisitos empresariales. 

Vuelva a configurar las etiquetas predeterminadas de Azure Information Protection para realizar los cambios que necesite a fin de adaptarlas a sus decisiones de clasificación. Configure la directiva para el etiquetado manual por parte de los usuarios y escriba directrices para explicar a los usuarios qué etiquetas es necesario aplicar y cuándo. Para más información sobre cómo configurar la directiva de Azure Information Protection, vea [Configuración de la directiva de Azure Information Protection](../deploy-use/configure-policy.md).

Después, implemente el cliente de Azure Information Protection para los usuarios y, como ayuda, ofrezca a los usuarios aprendizaje e instrucciones específicas para saber cuándo tienen que seleccionar las etiquetas. Para más información sobre la instalación y compatibilidad del cliente, vea [Guía para administradores del cliente de Azure Information Protection](../rms-client/client-admin-guide.md).

Después de un período de tiempo, cuando los usuarios estén acostumbrados a etiquetar sus documentos y correos electrónicos, introduzca otras configuraciones más avanzadas. Estos podrían ser algunos ejemplos:

- Aplicar una etiqueta predeterminada

- Pedir a los usuarios una justificación si han elegido una etiqueta con un nivel de clasificación inferior

- Obligar a que todos los documentos y correos electrónicos tengan una etiqueta

- Encabezados, pies de página o marcas de agua personalizados

- Condiciones complementarias para las recomendaciones y el etiquetado automático

En este momento, no seleccione la opción para proteger documentos y correos electrónicos.

### <a name="step-4-prepare-for-rights-management-data-protection"></a>Paso 4: Preparación para la protección de datos de Rights Management

Cuando los usuarios estén acostumbrados a etiquetar documentos y correos electrónicos, podrá empezar a introducir la protección de datos para la información más confidencial. En esta fase es necesario realizar la preparación siguiente para el servicio Azure Rights Management:

1. Decide si quieres que Microsoft administre tu clave de inquilino (la predeterminada) o generarla y administrarla tú mismo (conocido como Aportar tu propia clave, o BYOK). Tenga en cuenta que actualmente, no se puede usar BYOK si se usa Exchange Online. Para más información, vea [Planeamiento e implementación de su clave de inquilino de Azure Information Protection](plan-implement-tenant-key.md).

2. Instalación del módulo de Windows PowerShell para [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] en al menos un equipo que tenga acceso a Internet. Este paso puedes hacerlo ahora o más tarde. Para más información, vea [Instalación de Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md).

3. Si actualmente está utilizando servicios locales de Rights Management, realice una migración para mover las claves, las plantillas y las direcciones URL a la nube. Para más información, vea [Migración desde AD RMS a Information Protection](migrate-from-ad-rms-to-azure-rms.md).

4. Active el servicio Azure Rights Management para empezar a proteger documentos y correos electrónicos. Si se requiere una implementación en fases, configure los controles de incorporación de usuarios para restringir el uso a usuarios específicos. Para más información, consulte [Activación de Azure Rights Management](../deploy-use/activate-service.md).

De forma opcional, considera configurar lo siguiente:

-   Plantillas personalizadas si las plantillas de directiva de derechos predeterminadas no son suficientes para tu organización. Este paso puedes hacerlo ahora o más tarde. Para más información, vea [Configuración de plantillas personalizadas para el servicio Azure Rights Management](../deploy-use/configure-custom-templates.md).

-   Registro de uso para que puedas controlar cómo se usa Rights Management en tu organización. Este paso puedes hacerlo ahora o más tarde. Para obtener más información, consulte [Registro y análisis del uso del servicio Azure Rights Management](../deploy-use/log-analyze-usage.md).

### <a name="step-5-configure-your-azure-information-protection-policy-applications-and-services-for-rights-management-data-protection"></a>Paso 5: Configurar la directiva de Azure Information Protection, las aplicaciones y los servicios para la protección de datos de Rights Management

1. Actualizar la directiva de Azure Information Protection para aplicar la protección de datos
    
    Modifique la directiva de Azure Information Protection para que una o más etiquetas apliquen la protección de Rights Management. Para obtener más información, consulte [Configuración de una etiqueta para aplicar protección de Rights Management](../deploy-use/configure-policy-protection.md).
    
    Tenga en cuenta que los usuarios pueden aplicar etiquetas en Outlook que a su vez aplicarán la protección de Rights Management incluso si Exchange no está configurado para Information Rights Management (IRM). Sin embargo, hasta que no se configure Exchange para IRM, su organización no disfrutará de toda la funcionalidad derivada del uso de la protección de Azure Rights Management con Exchange. Esta configuración adicional se incluye en el paso 3 para Exchange Online y el paso 6 para Exchange local. 

2. Configurar las aplicaciones y los servicios de Office para IRM
    
    Configure las aplicaciones de Office y los servicios para las características de Information Rights Management (IRM) en SharePoint Online o en Exchange Online. Para más información, consulte [Configuración de plantillas personalizadas para Azure Rights Management](../deploy-use/configure-applications.md).

3. Configurar la característica de superusuario para la recuperación de datos
    
    Si tiene servicios de TI existentes que necesita para inspeccionar los archivos que se protegerán con Azure Rights Management (como soluciones de prevención de pérdida de datos [DLP], puertas de enlace de cifrado de contenido [CEG] y productos antimalware), configure las cuentas de servicio como superusuarios para Azure Rights Management. Para obtener más información, consulte [Configuring super users for Azure Rights Management and discovery services or data recovery](../deploy-use/configure-super-users.md) (Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos).

4. Clasificar y proteger los archivos de forma masiva, según proceda
    
    Los cmdlets de PowerShell que permiten clasificar y proteger archivos, así como quitar la clasificación y la protección, se instalan automáticamente con el cliente de Azure Information Protection. Para más información, vea [Uso de PowerShell con el cliente de Azure Information Protection](..\rms-client\client-admin-guide-powershell.md) en la guía del administrador.

6. Implementar el conector para servidores locales
    
    Si tiene servicios locales que quiere usar con el servicio Azure Rights Management, instale y configure el conector de Rights Management. Para más información, consulte [Implementación del conector de Azure Rights Management](../deploy-use/deploy-rms-connector.md).

### <a name="step-4-use-and-monitor-your-data-protection-solutions"></a>Paso 4: Usar y supervisar las soluciones de protección de datos
Ahora ya está listo para proteger los datos y registrar cómo la empresa usa las etiquetas que se han configurado y la protección de datos de Rights Management. Para obtener información adicional sobre la compatibilidad de esta fase de implementación, vea lo siguiente:

- [Ayuda a los usuarios para proteger archivos mediante el servicio Azure Rights Management](../deploy-use/help-users.md)

-  [Registro y análisis del uso del servicio Azure Rights Management](../deploy-use/log-analyze-usage.md)

- [Archivos de cliente y registro de uso](../rms-client/client-admin-guide-files-and-logging.md)

Si le interesa proteger automáticamente los archivos mediante la infraestructura de clasificación de archivos en un servidor de archivos basado en Windows, consulte [Protección de RMS con la infraestructura de clasificación de archivos (FCI) de Windows Server](../rms-client/configure-fci.md).

### <a name="step-5-administer-the-rights-management-service-for-your-tenant-account-as-needed"></a>Paso 5: Administrar el servicio Rights Management para la cuenta de inquilino según sea necesario
Cuando empiece a usar el servicio Azure Rights Management, es posible que le resulte útil usar Windows PowerShell para procesar con scripts o automatizar cambios administrativos. Para más información, vea [Administración del servicio Azure Rights Management mediante Windows PowerShell](../deploy-use/administer-powershell.md).


## <a name="deployment-roadmap-for-data-protection-only"></a>Mapa de ruta de implementación para solo la protección de datos

### <a name="step-1-confirm-that-you-have-a-subscription-that-includes-azure-rights-management"></a>Paso 1: Confirme que tiene una suscripción que incluye Azure Rights Management.
Revise la [información de la suscripción](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) y la [lista de características](https://www.microsoft.com/cloud-platform/azure-information-protection-features) en el sitio de Azure Information Protection para confirmar que la organización tiene una suscripción en la que se incluyen las funciones y las características que necesita. Después, asigne una licencia de esta suscripción a todos los usuarios de la organización que vayan a proteger documentos y correos electrónicos con el servicio Azure Rights Management.

Nota: No asigne manualmente licencias de usuario desde la suscripción gratuita de RMS para individuos y no utilice esta licencia para administrar el servicio de Azure Rights Management para su organización. Estas licencias se muestran como **Rights Management Adhoc** en el centro de administración de Office 365 y como **RIGHTSMANAGEMENT_ADHOC** al ejecutar el cmdlet de Azure AD PowerShell, [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx). Para obtener más información acerca de cómo se otorga automáticamente la suscripción RMS para individuos y se asigna a los usuarios, consulte [RMS para individuos y Azure Information Protection](../understand-explore/rms-for-individuals.md).


### <a name="step-2-prepare-your-tenant-to-use-the-azure-rights-management-service"></a>Paso 2: Preparar la cuenta de inquilino para usar el servicio Azure Rights Management
Antes de empezar a usar [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], tenga en cuenta los siguientes pasos previos:

1.  Asegúrese de que el inquilino de Office 365 tenga las cuentas de usuario y los grupos que usará Azure Information Protection para autenticar y autorizar a los usuarios de su organización. Si es necesario, cree estas cuentas y grupos, o sincronícelos desde el directorio local. Para más información, consulte [Preparación de usuarios y grupos para Azure Information Protection](prepare.md).

2. Decide si quieres que Microsoft administre tu clave de inquilino (la predeterminada) o generarla y administrarla tú mismo (conocido como Aportar tu propia clave, o BYOK). Tenga en cuenta que actualmente, no se puede usar BYOK si se usa Exchange Online. Para más información, vea [Planeamiento e implementación de su clave de inquilino de Azure Information Protection](plan-implement-tenant-key.md).

3. Instalación del módulo de Windows PowerShell para [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] en al menos un equipo que tenga acceso a Internet. Este paso puedes hacerlo ahora o más tarde. Para más información, consulte [Instalación de Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md).

4. Si actualmente está utilizando servicios locales de Rights Management, realice una migración para mover las claves, las plantillas y las direcciones URL a la nube. Para obtener más información, vea [Migración desde AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

5. Activa Rights Management para que puedas empezar a usar el servicio. Si se requiere una implementación en fases, configure los controles de incorporación de usuarios para restringir el uso a usuarios específicos. Para más información, consulte [Activación de Azure Rights Management](../deploy-use/activate-service.md).

De forma opcional, considera configurar lo siguiente:

-   Plantillas personalizadas si las plantillas de directiva de derechos predeterminadas no son suficientes para tu organización. Este paso puedes hacerlo ahora o más tarde. Para más información, vea [Configuración de plantillas personalizadas para el servicio Azure Rights Management](../deploy-use/configure-custom-templates.md).

-   Registro de uso para que puedas controlar cómo se usa Rights Management en tu organización. Este paso puedes hacerlo ahora o más tarde. Para obtener más información, consulte [Registro y análisis del uso del servicio Azure Rights Management](../deploy-use/log-analyze-usage.md).

### <a name="step-3-install-the-client-and-configure-applications-and-services-for-rights-management"></a>Paso 3: Instalar el cliente y configurar aplicaciones y servicios para Rights Management

1. Implementar el cliente de Azure Information Protection
    
    Instale Azure Information Protection para usuarios, para admitir Office 2010, para proteger correos electrónicos y archivos que no sean documentos de Office y realizar un seguimiento de los documentos protegidos. Ofrezca a los usuarios aprendizaje para este cliente. Para más información, vea [Cliente de Azure Information Protection para Windows](../rms-client/aip-client.md).

2. Configurar las aplicaciones y los servicios de Office para IRM
    
    Configure las aplicaciones de Office y los servicios para las características de Information Rights Management (IRM) en SharePoint Online o en Exchange Online. Para más información, consulte [Configuración de plantillas personalizadas para Azure Rights Management](../deploy-use/configure-applications.md).

3. Configurar la característica de superusuario para la recuperación de datos
    
    Si tiene servicios de TI existentes que necesita para inspeccionar los archivos que se protegerán con Azure Rights Management (como soluciones de prevención de pérdida de datos [DLP], puertas de enlace de cifrado de contenido [CEG] y productos antimalware), configure las cuentas de servicio como superusuarios para Azure Rights Management. Para obtener más información, consulte [Configuring super users for Azure Rights Management and discovery services or data recovery](../deploy-use/configure-super-users.md) (Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos).

4. Proteger archivos de forma masiva, según proceda 
    
    Los cmdlets de PowerShell que permiten proteger o desproteger varios tipos de archivos de forma masiva se instalan automáticamente con el cliente de Azure Information Protection. Para más información, vea [Uso de PowerShell con el cliente de Azure Information Protection](..\rms-client\client-admin-guide-powershell.md) en la guía del administrador.

5. Implementar el conector para servidores locales
    
    Si tiene servicios locales que quiere usar con el servicio Azure Rights Management, instale y configure el conector de Rights Management. Para más información, consulte [Implementación del conector de Azure Rights Management](../deploy-use/deploy-rms-connector.md).


### <a name="step-4-use-and-monitor-your-data-protection-solutions"></a>Paso 4: Usar y supervisar las soluciones de protección de datos
Ahora está preparado para proteger los datos y registrar la forma en que su compañía usa Rights Management. Para obtener más información sobre cómo contribuir en esta fase de implementación, vea [Ayuda a los usuarios para proteger archivos mediante Azure Rights Management](../deploy-use/help-users.md) y [Registro y análisis del uso del servicio Azure Rights Management](../deploy-use/log-analyze-usage.md).

Si le interesa proteger automáticamente los archivos mediante la infraestructura de clasificación de archivos en un servidor de archivos basado en Windows, consulte [Protección de RMS con la infraestructura de clasificación de archivos (FCI) de Windows Server](../rms-client/configure-fci.md).

### <a name="step-5-administer-the-rights-management-service-for-your-tenant-account-as-needed"></a>Paso 5: Administrar el servicio Rights Management para la cuenta de inquilino según sea necesario
Cuando empiece a usar el servicio Azure Rights Management, es posible que le resulte útil usar Windows PowerShell para procesar con scripts o automatizar cambios administrativos. Para más información, vea [Administración del servicio Azure Rights Management mediante Windows PowerShell](../deploy-use/administer-powershell.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
