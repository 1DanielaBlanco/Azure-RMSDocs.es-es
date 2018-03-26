---
title: Implementación del conector de Rights Management - AIP
description: Instrucciones para implementar el conector de RMS, que ofrece protección de datos para las implementaciones locales existentes que usan Exchange Server, SharePoint Server o Windows Server y la Infraestructura de clasificación de archivos (FCI).
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/07/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 90e7e33f-9ecc-497b-89c5-09205ffc5066
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 87746ad526f191907ad2670604c357e5e926b84e
ms.sourcegitcommit: 758e0cfeb6c05f4c6f5310dc36fbf0c02c256eed
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/17/2018
---
# <a name="deploying-the-azure-rights-management-connector"></a>Implementación del conector de Azure Rights Management

>*Se aplica a: Azure Information Protection, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2*

Utilice esta información para obtener información sobre el conector de Azure Rights Management y, a continuación, cómo implementarlo correctamente para su organización. Este conector ofrece protección de datos para las implementaciones locales existentes que usan Microsoft **Exchange Server**, **SharePoint Server** o servidores de archivo que ejecutan Windows Server y la **Infraestructura de clasificación de archivos** (FCI).


## <a name="overview-of-the-microsoft-rights-management-connector"></a>Visión general del conector Rights Management de Microsoft
El conector Rights Management (RMS) de Microsoft le permite habilitar rápidamente servidores locales existentes para usar su funcionalidad de Information Rights Management (IRM) con el servicio Rights Management de Microsoft basado en la nube (Azure RMS). Con esta funcionalidad, los TI y los usuarios pueden proteger fácilmente documentos e imágenes tanto dentro como fuera de la organización, sin tener que instalar más infraestructuras o establecer relaciones de confianza con otras organizaciones. 

El conector de RMS es un servicio de tamaño reducido que se instala en servidores locales que ejecutan Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 o Windows Server 2008 R2. Además de ejecutar el conector en equipos físicos, también puede ejecutarlo en máquinas virtuales, incluidas las máquinas virtuales de IaaS de Azure. Después de instalar y configurar el conector, actúa como una interfaz de comunicaciones (una retransmisión) entre servidores locales y el servicio en la nube, tal como se muestra en la imagen siguiente. Las flechas indican la dirección en la que se inician las conexiones de red.

![Introducción a la arquitectura de conector RMS](../media/RMS_connector.png)


### <a name="on-premises-servers-supported"></a>Servidores locales admitidos

El conector de RMS admite los siguientes servidores locales: Exchange Server, SharePoint Server y servidores de archivos que ejecutan Windows Server y usan la infraestructura de clasificación de archivos para clasificar y aplicar directivas en documentos de Office de una carpeta. 

> [!NOTE]
> Si desea proteger varios tipos de archivos (no solo documentos de Office) mediante la infraestructura de clasificación de archivos, no use el conector RMS, sino los [cmdlets AzureInformationProtection](/powershell/azureinformationprotection/vlatest/aip).

Para obtener más información acerca de las versiones de estos servidores locales que admite el conector RMS, consulte [Servidores locales que son compatibles con Azure RMS](..\get-started\requirements-servers.md).


### <a name="support-for-hybrid-scenarios"></a>Compatibilidad con los escenarios híbridos

Puede usar el conector RMS incluso si algunos de los usuarios se conectan a servicios en línea, en un escenario híbrido. Por ejemplo, los buzones de algunos usuarios usan Exchange Online y los buzones de otros usuarios usan Exchange Server. Después de instalar el conector RMS, todos los usuarios pueden proteger y consumir mensajes de correo electrónico y archivos adjuntos con Azure RMS, y la protección de la información funciona sin problemas entre las dos configuraciones de implementación.

### <a name="support-for-customer-managed-keys-byok"></a>Compatibilidad con las claves administradas por los clientes (BYOK)

Si administra su propia clave de inquilino para Azure RMS, con el escenario Bring your own key (BYOK, Traiga su propia clave), el conector RMS y los servidores locales que la usan no tienen acceso al módulo de seguridad de hardware (HSM) que contiene la clave de inquilino. Esto se debe a que todas las operaciones criptográficas que utilizan la clave de inquilino se ejecutan en Azure RMS y no a nivel local.

Para obtener más información sobre la administración de la clave de inquilino, consulte [Planeamiento e implementación de la clave de inquilino de Azure Information Protection](../plan-design\plan-implement-tenant-key.md).

## <a name="prerequisites-for-the-rms-connector"></a>Requisitos previos para el conector RMS
Antes de instalar el conector RMS, asegúrese de que se cumplen los requisitos siguientes.

|Requisito|Más información|
|---------------|--------------------|
|El servicio Rights Management (RMS) está activado|[Activar Rights Management de Azure](activate-service.md)|
|Sincronización de directorios entre los bosques de Active Directory locales y Azure Active Directory|Tras activar RMS, se debe configurar Azure Active Directory para trabajar con los usuarios y grupos de tu base de datos de Active Directory.<br /><br />**Importante**: debe realizar este paso de sincronización de directorios para que el conector de RMS funcione, incluso en una red de prueba. Aunque puede usar Office 365 y Azure Active Directory mediante cuentas que crea manualmente en Azure Active Directory, este conector requiere que las cuentas de Azure Active Directory se sincronicen con Servicios de dominio de Active Directory; la sincronización de contraseñas manual no es suficiente.<br /><br />Para obtener más información, vea los recursos siguientes:<br /><br />[Integración de las identidades locales con Azure Active Directory](/active-directory/active-directory-aadconnect)<br /><br />[Comparación de las herramientas de integración de directorios de identidad híbrida](/active-directory/active-directory-hybrid-identity-design-considerations-tools-comparison)|
|Opcional pero recomendable:<br /><br />Habilitar la federación entre los Active Directory y Azure Active Directory locales|Puede habilitar la federación de identidades entre sus directorios locales y Azure Active Directory. Esta configuración habilita una experiencia de usuario más sencilla mediante un único inicio de sesión en el servicio RMS. Sin un inicio de sesión único, a los usuarios se les piden sus credenciales para que puedan usar el contenido protegido por derechos.<br /><br />Para obtener información para configurar la federación mediante Active Directory Federation Services (AD FS) entre los Servicios de dominio Active Directory y Azure Active Directory, vea la [Lista de comprobación: Usar AD FS para implementar y administrar inicios de sesión únicos](http://technet.microsoft.com/library/jj205462.aspx) en la biblioteca de Windows Server.|
|Dos equipos miembro como mínimo en los que instalar el conector RMS:<br /><br />- Un equipo virtual o físico de 64 bits ejecuta uno de los siguientes sistemas operativos: Windows Server 2016, Windows Server 2012 R2,  Windows Server 2012 o Windows Server 2008 R2.<br /><br />- Como mínimo 1 GB de RAM.<br /><br />- Un mínimo de 64 GB de espacio en disco.<br /><br />- Como mínimo una interfaz de red.<br /><br />- Acceso a Internet a través de un firewall (o proxy web) que no precise autenticación.<br /><br />- Debe encontrarse en un bosque o dominio que confíe en otros bosques de la organización que contengan instalaciones de servidores de Exchange o SharePoint que quiera usar con el conector RMS.|Para la tolerancia a errores y alta disponibilidad, debe instalar el conector RMS como mínimo en dos equipos.<br /><br />**Sugerencia**: Si utiliza Outlook Web Access o dispositivos móviles que emplean Exchange ActiveSync IRM y es fundamental mantener el acceso a correos electrónicos y archivos adjuntos protegidos por Azure RMS, se recomienda implementar un grupo de servidores de conector de carga equilibrada para garantizar una alta disponibilidad.<br /><br />No necesita servidores dedicados para ejecutar el conector pero debe instalarlo en un ordenador independiente respecto a los servidores que usarán el conector.<br /><br />**Importante**: No instale el conector en un equipo que ejecute Exchange Server, SharePoint Server o un servidor de archivos que esté configurado para la infraestructura de clasificación de archivos si quiere usar la funcionalidad desde estos servicios con Azure RMS. Además, no instale este conector en un controlador de dominio.<br /><br />Si tiene cargas de trabajo de servidor que desea usar con el conector RMS pero sus servidores están en dominios que no son de confianza para el dominio desde el que va a ejecutar el conector, puede instalar servidores de conector RMS adicionales en estos dominios que no son de confianza o en otros dominios de su bosque. <br /><br />No hay ningún límite en el número de servidores de conector que se pueden ejecutar para la organización y todos los servidores de conector instalados en una organización comparten la misma configuración. Sin embargo, para configurar el conector para autorizar servidores, debe ser capaz de examinar las cuentas de servidor o servicio que desea autorizar, lo que significa que debe ejecutar la herramienta de administración de RMS en un bosque desde el que puede examinar esas cuentas.|


## <a name="steps-to-deploy-the-rms-connector"></a>Pasos para implementar el conector RMS

El conector no comprueba automáticamente todos los [requisitos previos](deploy-rms-connector.md#prerequisites-for-the-rms-connector) que necesita para llevar a cabo una implementación correcta, por lo que debe asegurarse de que los cumpla antes de empezar. La implementación requiere que instale el conector, lo configure y, a continuación, configure los servidores que quiera que usen el conector. 

-   **Paso 1:** [Instalación del conector de RMS](install-configure-rms-connector.md#installing-the-rms-connector)

-   **Paso 2:** [Especificación de credenciales](install-configure-rms-connector.md#entering-credentials)

-   **Paso 3:** [Autorización de los servidores para usar el conector de RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)

-   **Paso 4:** [Configuración del equilibrio de carga y alta disponibilidad](install-configure-rms-connector.md#configuring-load-balancing-and-high-availability)

-   Opcional: [Configuración del conector de RMS para usar HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https)

-   Opcional: [Configuración del conector de RMS para un servidor proxy web](install-configure-rms-connector.md#configuring-the-rms-connector-for-a-web-proxy-server)

-   Opcional: [Instalación de la herramienta de administración del conector de RMS en equipos administrativos](install-configure-rms-connector.md#installing-the-rms-connector-administration-tool-on-administrative-computers)

-   **Paso 5:** [Configuración de servidores para usar el conector de RMS](configure-servers-rms-connector.md)

    -   [Configuración de un servidor Exchange para usar el conector](configure-servers-rms-connector.md#configuring-an-exchange-server-to-use-the-connector)

    -   [Configuración de un servidor SharePoint para usar el conector](configure-servers-rms-connector.md#configuring-a-sharepoint-server-to-use-the-connector)

    -   [Configuración de un servidor de archivos para que la Infraestructura de clasificación de archivos use el conector](configure-servers-rms-connector.md#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)


## <a name="next-steps"></a>Pasos siguientes

Vaya al paso 1: [Instalación y configuración del conector de Azure Rights Management](install-configure-rms-connector.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]