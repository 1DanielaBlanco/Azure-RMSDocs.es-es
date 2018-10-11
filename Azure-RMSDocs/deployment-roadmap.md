---
title: Mapa de ruta de implementación de Azure Information Protection
description: Siga estos pasos para preparar, implementar y administrar Azure Information Protection en su organización.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/05/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 20fcfa3790dc9ad1612a508f4fe28f72997fc475
ms.sourcegitcommit: bf58c5d94eb44a043f53711fbdcf19ce503f8aab
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47211282"
---
# <a name="azure-information-protection-deployment-roadmap"></a>Mapa de ruta de implementación de Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Utilice los pasos siguientes como recomendaciones para ayudarlo a preparar, implementar y administrar Azure Information Protection en su organización.

Si lo que quiere es probar rápidamente Azure Information Protection en lugar de implementarlo en un entorno de producción, vea [Tutorial de inicio rápido para Azure Information Protection](./infoprotect-quick-start-tutorial.md).

> [!IMPORTANT]
> Antes de seguir este procedimiento, asegúrese de revisar los [Requisitos de Azure Information Protection](./requirements.md).

Elija el mapa de ruta de implementación que sea adecuado para su organización y que coincida con [las funciones y las características de las suscripciones](https://azure.microsoft.com/pricing/details/information-protection/) que necesite:

- [Usar funciones de clasificación, etiquetado y protección](#deployment-roadmap-for-classification-labeling-and-protection)

- [Usar solo la protección de datos](#deployment-roadmap-for-data-protection-only)


## <a name="deployment-roadmap-for-classification-labeling-and-protection"></a>Mapa de ruta de implementación para clasificación, etiquetado y protección

> [!NOTE]
> ¿Ya está usando la funcionalidad de protección de Azure Information Protection? Puede omitir muchos de estos pasos y centrarse en los pasos 3 y 5.1.

### <a name="step-1-confirm-your-subscription-and-assign-user-licenses"></a>Paso 1: Confirmar la suscripción y asignar licencias de usuario
Revise la información de la suscripción y la lista de características en la página [Precios de Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) para confirmar que la organización tenga una suscripción en la que se incluyan las funciones y las características que necesite. Después, asigne una licencia de esta suscripción a todos los usuarios de la organización que vayan a clasificar, etiquetar y proteger documentos y correos electrónicos.

Nota: No asigne manualmente licencias de usuario desde la suscripción gratuita de RMS para individuos y no utilice esta licencia para administrar el servicio de Azure Rights Management para su organización. Estas licencias se muestran como **Rights Management Adhoc** en el centro de administración de Office 365 y como **RIGHTSMANAGEMENT_ADHOC** al ejecutar el cmdlet de Azure AD PowerShell, [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx). Para obtener más información acerca de cómo se otorga automáticamente la suscripción RMS para individuos y se asigna a los usuarios, consulte [RMS para individuos y Azure Information Protection](./rms-for-individuals.md).


### <a name="step-2-prepare-your-tenant-to-use-azure-information-protection"></a>Paso 2: Preparar el inquilino para usar Azure Information Protection
Antes de empezar a usar Azure Information Protection, siga este procedimiento de preparación:

- Asegúrese de que tiene cuentas de usuario y grupos en Office 365 o Azure Active Directory que Azure Information Protection usará para autenticar y autorizar a los usuarios de la organización. Si es necesario, cree estas cuentas y grupos, o sincronícelos desde el directorio local. Para más información, consulte [Preparación de usuarios y grupos para Azure Information Protection](prepare.md).

### <a name="step-3-configure-and-deploy-classification-and-labeling"></a>Paso 3: Configurar e implementar la clasificación y el etiquetado

Si aún no tiene una estrategia de clasificación, revise la [directiva predeterminada de Azure Information Protection](./configure-policy-default.md) y úsela como base para determinar las etiquetas de clasificación que se asignarán a los datos de la organización. Puede personalizarlas para adaptarlas a sus requisitos empresariales. 

Vuelva a configurar las etiquetas predeterminadas de Azure Information Protection para realizar los cambios que necesite a fin de adaptarlas a sus decisiones de clasificación. Configure la directiva para el etiquetado manual por parte de los usuarios y escriba directrices para explicar a los usuarios qué etiquetas es necesario aplicar y cuándo. Si la directiva predeterminada se ha creado con etiquetas que aplican la protección automáticamente, elimine la configuración de protección o deshabilite la etiqueta en cuestión. Para más información sobre cómo configurar la directiva de Azure Information Protection, vea [Configuración de la directiva de Azure Information Protection](./configure-policy.md).

Después, implemente el cliente de Azure Information Protection para los usuarios y, como ayuda, ofrezca a los usuarios aprendizaje e instrucciones específicas para saber cuándo tienen que seleccionar las etiquetas. Para más información sobre la instalación y compatibilidad del cliente, vea [Guía para administradores del cliente de Azure Information Protection](./rms-client/client-admin-guide.md).

Después de un período de tiempo, cuando los usuarios estén acostumbrados a etiquetar sus documentos y correos electrónicos, introduzca otras configuraciones más avanzadas. Estos podrían ser algunos ejemplos:

- Aplicar una etiqueta predeterminada

- Pedir a los usuarios una justificación si han elegido una etiqueta con un nivel de clasificación inferior

- Obligar a que todos los documentos y correos electrónicos tengan una etiqueta

- Encabezados, pies de página o marcas de agua personalizados

- Condiciones complementarias para las recomendaciones y el etiquetado automático

En este momento, no seleccione la opción para proteger documentos y correos electrónicos.

### <a name="step-4-prepare-for-data-protection"></a>Paso 4: Preparación de la protección de datos

Cuando los usuarios estén acostumbrados a etiquetar documentos y correos electrónicos, podrá empezar a introducir la protección de datos para la información más confidencial. Esta fase requiere los siguientes pasos previos:

1. Decide si quieres que Microsoft administre tu clave de inquilino (la predeterminada) o generarla y administrarla tú mismo (conocido como Aportar tu propia clave, o BYOK). Para más información, vea [Planeamiento e implementación de su clave de inquilino de Azure Information Protection](plan-implement-tenant-key.md).

2. Instale el módulo de PowerShell para AADRM en al menos un equipo que tenga acceso a Internet. Este paso puedes hacerlo ahora o más tarde. Para más información, vea [Instalación del módulo de PowerShell para AADRM](./install-powershell.md).

3. Si actualmente está usando AD RMS, realice una migración para mover las claves, las plantillas y las direcciones URL a la nube. Para más información, vea [Migración desde AD RMS a Information Protection](migrate-from-ad-rms-to-azure-rms.md).

4. Asegúrese de que el servicio de protección esté activado para poder comenzar a proteger documentos y correos electrónicos. Si se requiere una implementación en fases, configure los controles de incorporación de usuarios para restringir el uso a usuarios específicos. Para más información, consulte [Activación de Azure Rights Management](./activate-service.md).

De forma opcional, considera configurar lo siguiente:

-   Plantillas personalizadas para la configuración de protección si las predeterminadas no son suficientes para la organización. Este paso puedes hacerlo ahora o más tarde. Para obtener más información, vea [Configuración y administración de plantillas para Azure Information Protection](./configure-policy-templates.md).

-   Registro de uso para poder supervisar el uso del servicio de protección por parte de su organización. Este paso puedes hacerlo ahora o más tarde. Para obtener más información, consulte [Registro y análisis del uso del servicio Azure Rights Management](./log-analyze-usage.md).

### <a name="step-5-configure-your-azure-information-protection-policy-applications-and-services-for-data-protection"></a>Paso 5: Configurar la directiva de Azure Information Protection, las aplicaciones y los servicios para la protección de datos

1. Actualizar la directiva de Azure Information Protection para aplicar la protección de datos
    
    Modifique la directiva de Azure Information Protection para que al menos una etiqueta aplique la protección. Para obtener más información, consulte [Configuración de una etiqueta para aplicar protección de Rights Management](./configure-policy-protection.md).
    
    Tenga en cuenta que los usuarios pueden aplicar etiquetas en Outlook que a su vez aplicarán la protección de Rights Management incluso si Exchange no está configurado para Information Rights Management (IRM). Sin embargo, hasta que no se configure Exchange para IRM o el [cifrado de mensajes de Office 365 con nuevas capacidades](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e), su organización no disfrutará de toda la funcionalidad derivada del uso de la protección de Azure Rights Management con Exchange. Esta configuración adicional se incluye en la lista siguiente (2 para Exchange Online y 5 para Exchange local). 

2. Configuración de aplicaciones y servicios de Office
    
    Configure las aplicaciones de Office y los servicios para las características de Information Rights Management (IRM) en SharePoint Online o en Exchange Online. Para más información, consulte [Configuración de plantillas personalizadas para Azure Rights Management](./configure-applications.md).

3. Configurar la característica de superusuario para la recuperación de datos
    
    Si tiene servicios de TI existentes que necesita para inspeccionar los archivos que se protegerán con Azure Information Protection (como soluciones de prevención de pérdida de datos [DLP], puertas de enlace de cifrado de contenido [CEG] y productos antimalware), configure las cuentas de servicio como superusuarios para Azure Rights Management. Para obtener más información, consulte [Configuring super users for Azure Rights Management and discovery services or data recovery](./configure-super-users.md) (Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos).

4. Clasificar y proteger los archivos de forma masiva, según proceda
    
    Los cmdlets de PowerShell que permiten clasificar y proteger archivos, así como quitar la clasificación y la protección, se instalan automáticamente con el cliente de Azure Information Protection. Para más información, vea [Uso de PowerShell con el cliente de Azure Information Protection](./rms-client/client-admin-guide-powershell.md) en la guía del administrador.

6. Implementar el conector para servidores locales
    
    Si tiene servicios locales que quiera usar con el servicio de protección, instale y configure el conector de Rights Management. Para más información, consulte [Implementación del conector de Azure Rights Management](./deploy-rms-connector.md).

### <a name="step-6-use-and-monitor-your-data-protection-solutions"></a>Paso 6: Usar y supervisar las soluciones de protección de datos
Ahora ya está a punto para proteger los datos y registrar el uso de las etiquetas que se han configurado y la protección de datos por parte de su empresa. Para obtener información adicional sobre la compatibilidad de esta fase de implementación, vea lo siguiente:

- [Reporting for Azure Information Protection](reports-aip.md) (Informes para Azure Information Protection)

- [Ayuda a los usuarios para proteger archivos mediante el servicio Azure Rights Management](./help-users.md)

- [Registro y análisis del uso del servicio Azure Rights Management](./log-analyze-usage.md)

- [Archivos de cliente y registro de uso](./rms-client/client-admin-guide-files-and-logging.md)

Si le interesa proteger automáticamente los archivos mediante la infraestructura de clasificación de archivos en un servidor de archivos basado en Windows, consulte [Protección de RMS con la infraestructura de clasificación de archivos (FCI) de Windows Server](./rms-client/configure-fci.md).

### <a name="step-7-administer-the-protection-service-for-your-tenant-account-as-needed"></a>Paso 7: Administrar el servicio de protección para la cuenta de inquilino según sea necesario
Cuando empiece a usar el servicio de protección, puede que PowerShell le resulte útil para generar scripts o automatizar cambios administrativos. Para más información, vea [Administración del servicio Azure Rights Management mediante Windows PowerShell](./administer-powershell.md).


## <a name="deployment-roadmap-for-data-protection-only"></a>Mapa de ruta de implementación para solo la protección de datos

### <a name="step-1-confirm-that-you-have-a-subscription-that-includes-the-protection-service-from-azure-information-protection"></a>Paso 1: Confirmar que tenga una suscripción que incluya el servicio de protección de Azure Information Protection
Revise la información de la suscripción y la lista de características en la página [Precios de Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) para confirmar que la organización tenga una suscripción en la que se incluyan las funciones y las características que necesite. Después, asigne una licencia de esta suscripción a todos los usuarios de la organización que vayan a proteger documentos y correos electrónicos.

Nota: No asigne manualmente licencias de usuario desde la suscripción gratuita de RMS para individuos y no utilice esta licencia para administrar el servicio de Azure Rights Management para su organización. Estas licencias se muestran como **Rights Management Adhoc** en el centro de administración de Office 365 y como **RIGHTSMANAGEMENT_ADHOC** al ejecutar el cmdlet de Azure AD PowerShell, [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx). Para obtener más información acerca de cómo se otorga automáticamente la suscripción RMS para individuos y se asigna a los usuarios, consulte [RMS para individuos y Azure Information Protection](./rms-for-individuals.md).


### <a name="step-2-prepare-your-tenant-to-use-azure-information-protection"></a>Paso 2: Preparar el inquilino para usar Azure Information Protection
Antes de empezar a usar el servicio de protección de Azure Information Protection, siga estos pasos previos:

1.  Asegúrese de que el inquilino de Office 365 tenga las cuentas de usuario y los grupos que usará Azure Information Protection para autenticar y autorizar a los usuarios de su organización. Si es necesario, cree estas cuentas y grupos, o sincronícelos desde el directorio local. Para más información, consulte [Preparación de usuarios y grupos para Azure Information Protection](prepare.md).

2. Decide si quieres que Microsoft administre tu clave de inquilino (la predeterminada) o generarla y administrarla tú mismo (conocido como Aportar tu propia clave, o BYOK). Para más información, vea [Planeamiento e implementación de su clave de inquilino de Azure Information Protection](plan-implement-tenant-key.md).

3. Instale el módulo de PowerShell para AADRM en al menos un equipo que tenga acceso a Internet. Este paso puedes hacerlo ahora o más tarde. Para más información, vea [Instalación del módulo de PowerShell para AADRM](./install-powershell.md).

4. Si actualmente está usando AD RMS, realice una migración para mover las claves, las plantillas y las direcciones URL a la nube. Para obtener más información, vea [Migración desde AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

5. Asegúrese de que el servicio de protección esté activado para poder comenzar a proteger documentos y correos electrónicos. Si se requiere una implementación en fases, configure los controles de incorporación de usuarios para restringir el uso a usuarios específicos. Para más información, consulte [Activación de Azure Rights Management](./activate-service.md).

De forma opcional, considera configurar lo siguiente:

-   Plantillas personalizadas para la configuración de protección si las predeterminadas no son suficientes para la organización. Este paso puedes hacerlo ahora o más tarde. Para obtener más información, vea [Configuración y administración de plantillas para Azure Information Protection](./configure-policy-templates.md).

- Registro de uso para poder supervisar el uso del servicio de protección por parte de su organización. Este paso puedes hacerlo ahora o más tarde. Para obtener más información, consulte [Registro y análisis del uso del servicio Azure Rights Management](./log-analyze-usage.md).

### <a name="step-3-install-the-client-and-configure-applications-and-services-for-rights-management"></a>Paso 3: Instalar el cliente y configurar aplicaciones y servicios para Rights Management

1. Implementar el cliente de Azure Information Protection
    
    Instale Azure Information Protection para usuarios, para admitir Office 2010, para proteger correos electrónicos y archivos que no sean documentos de Office y realizar un seguimiento de los documentos protegidos. Ofrezca a los usuarios aprendizaje para este cliente. Para más información, vea [Cliente de Azure Information Protection para Windows](./rms-client/aip-client.md).

2. Configuración de aplicaciones y servicios de Office
    
    Configure las aplicaciones de Office y los servicios para las características de Information Rights Management (IRM) en SharePoint Online o en Exchange Online. Para más información, consulte [Configuración de plantillas personalizadas para Azure Rights Management](./configure-applications.md).

3. Configurar la característica de superusuario para la recuperación de datos
    
    Si tiene servicios de TI existentes que necesita para inspeccionar los archivos que se protegerán con Azure Information Protection (como soluciones de prevención de pérdida de datos [DLP], puertas de enlace de cifrado de contenido [CEG] y productos antimalware), configure las cuentas de servicio como superusuarios para Azure Rights Management. Para obtener más información, consulte [Configuring super users for Azure Rights Management and discovery services or data recovery](./configure-super-users.md) (Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos).

4. Proteger archivos de forma masiva, según proceda 
    
    Los cmdlets de PowerShell que permiten proteger o desproteger varios tipos de archivos de forma masiva se instalan automáticamente con el cliente de Azure Information Protection. Para más información, vea [Uso de PowerShell con el cliente de Azure Information Protection](./rms-client/client-admin-guide-powershell.md) en la guía del administrador.

5. Implementar el conector para servidores locales
    
    Si tiene servicios locales que quiera usar con el servicio de protección, instale y configure el conector de Rights Management. Para más información, consulte [Implementación del conector de Azure Rights Management](./deploy-rms-connector.md).


### <a name="step-4-use-and-monitor-your-data-protection-solutions"></a>Paso 4: Usar y supervisar las soluciones de protección de datos
Ahora está a punto para proteger los datos y registrar la forma en la que su empresa usa el servicio de protección. Para obtener más información sobre cómo contribuir en esta fase de implementación, vea [Ayuda a los usuarios para proteger archivos mediante Azure Rights Management](./help-users.md) y [Registro y análisis del uso del servicio Azure Rights Management](./log-analyze-usage.md).

Si le interesa proteger automáticamente los archivos mediante la infraestructura de clasificación de archivos en un servidor de archivos basado en Windows, consulte [Protección de RMS con la infraestructura de clasificación de archivos (FCI) de Windows Server](./rms-client/configure-fci.md).

### <a name="step-5-administer-the-protection-service-for-your-tenant-account-as-needed"></a>Paso 5: Administrar el servicio de protección para la cuenta de inquilino según sea necesario
Cuando empiece a usar el servicio de protección, puede que PowerShell le resulte útil para generar scripts o automatizar cambios administrativos. Para más información, vea [Administración del servicio Azure Rights Management mediante Windows PowerShell](./administer-powershell.md).

