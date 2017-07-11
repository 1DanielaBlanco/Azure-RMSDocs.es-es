---
title: Requirements for Azure Information Protection (Requisitos de Azure Information Protection)
description: "Identifique los requisitos previos para implementar Azure Information Protection en su organización."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/09/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 66874f6e60c2cd5efb2dedaae470170811a84a67
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2017
---
<a id="requirements-for-azure-information-protection" class="xliff"></a>

# Requirements for Azure Information Protection (Requisitos de Azure Information Protection)

>*Se aplica a: Azure Information Protection, Office 365*

Antes de implementar Azure Information Protection para su organización, asegúrese de que tiene los siguientes requisitos previos. 

|Requisito|Más información|
|---------------|--------------------|
|Una suscripción a Azure Information Protection|Para clasificación, etiquetado y protección, debe tener un [plan de Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing). Si solo desea protección, debe tener un [plan de Office 365 que incluya Rights Management](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).<br /><br /> Revise la [información sobre la suscripción](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) y la [lista de características](https://www.microsoft.com/cloud-platform/azure-information-protection-features) en el sitio de Azure Information Protection para asegurarse de que la suscripción de la organización incluye las características de Azure Information Protection que quiere usar.<br /><br />Nota: Si tiene alguna pregunta sobre las suscripciones o licencias, no las publique en esta página. En lugar de eso, póngase en contacto con el administrador de cuentas de Microsoft o con [Soporte técnico de Microsoft](information-support.md#to-contact-microsoft-support). |
|Azure Active Directory|Su organización debe tener un directorio de Azure Active Directory (Azure AD) para admitir la autenticación y autorización de usuario para Azure Information Protection. Además, si desea usar sus cuentas de usuario desde su directorio local (AD DS), también deberá configurar la integración de directorios.<br /><br />Multi-Factor Authentication (MFA) es compatible con Azure Information Protection si tiene el software cliente necesario y la infraestructura de MFA configurada correctamente.<br /><br />Para obtener más información sobre los requisitos de autenticación, consulte [Requisitos de Azure Active Directory para Azure Information Protection](requirements-azure-ad.md). <br /><br />Para más información acerca de los requisitos de usuario y cuentas de grupo para la autorización, consulte [Preparación de usuarios y grupos para Azure Information Protection](../plan-design/prepare.md).|
|Dispositivos cliente|Los usuarios deben tener dispositivos cliente (equipo o dispositivo móvil) que ejecuten un sistema operativo compatible con Azure Information Protection.<br /><br />Los siguientes dispositivos admiten el cliente de Azure Information Protection, que permite a los usuarios clasificar y etiquetar los correos electrónicos y documentos de Office:<br /><br />- Windows 10 (x86 y x64)<br /><br />- Windows 8.1 (x86 y x64)<br /><br />- Windows 8 (x86 y x64)<br /><br />- Windows 7 Service Pack 1 (x86 y x64)<br /><br />- Windows Server 2016 <br /><br /> - Windows Server 2012 R2 y Windows Server 2012<br /><br />Cuando este cliente protege los datos mediante el servicio Azure Rights Management, pueden consumirlos los mismos dispositivos (Windows, Mac, iOS y Android), que admiten el servicio Azure Rights Management. <br /><br />Para obtener información sobre los dispositivos que admiten el servicio Azure Rights Management, vea [Requisitos de Azure RMS: Dispositivos cliente que son compatibles con Azure RMS](../get-started/requirements-client-devices.md).|
|Aplicaciones|El cliente de Azure Information Protection puede etiquetar y proteger archivos y correos electrónicos mediante las aplicaciones de Office **Word**, **Excel**, **PowerPoint** y **Outlook** de cualquiera de las siguientes ediciones de Office:<br /><br /> - Office 365 ProPlus con aplicaciones de 2016 o 2013 (hacer clic y ejecutar o instalación basada en Windows Installer)<br /><br />- Office Professional Plus 2016<br /><br />- Office Professional Plus 2013 con Service Pack 1<br /><br />- Office Professional Plus 2010 <br /><br />Las demás ediciones de Office no pueden proteger los documentos y correos electrónicos mediante un servicio de Rights Management. En el caso de estas ediciones, Azure Information Protection solo se admite para la clasificación y las etiquetas que aplican protección no aparecen en la barra de Azure Information Protection. <br /><br />Para obtener información sobre las ediciones de Office que son compatibles con el servicio de protección de datos, vea [Aplicaciones compatibles con la protección de datos de Azure Rights Management](requirements-applications.md).|
|Infraestructura compatible con la conectividad a Internet y dependiente de los servicios en la nube|Si tiene un firewall o dispositivos de red de intervención similares que deban configurarse para permitir conexiones específicas, vea la información de **Azure Rights Management (RMS)** en la sección [Portal de Office 365 e infraestructura compartida](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US#bkmk_portal-identity) del siguiente artículo de Office: [URL de Office 365 e intervalos de direcciones IP](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).<br /><br />Siga las instrucciones de este artículo de Office para suscribirse a una fuente RSS y mantenerse así al día de los cambios que se hagan en esta información.<br /><br />Además de la información del artículo de Office específica de Azure Information Protection:<br /><br />- Permita tráfico HTTPS en TCP 443 a **api.informationprotection.azure.com**.<br /><br />- No termine la conexión TLS de cliente a servicio (por ejemplo, para realizar una inspección de los paquetes). Al hacerlo, se interrumpe la asignación de certificados que los clientes de RMS utilizan con las entidades de certificación administradas por Microsoft para ayudar a proteger su comunicación con Azure RMS.<br /><br />- Si usa un proxy web que precisa de autenticación, debe configurarlo para usar autenticación integrada de Windows con las credenciales de inicio de sesión de Active Directory del usuario.|

Si quiere usar el servicio Azure Rights Management de Azure Information Protection con servidores locales, los siguientes productos son compatibles:

-   Exchange Server

-   Servidor de SharePoint

-   Servidores de archivos de Windows Server que son compatibles con la Infraestructura de la clasificación de archivos

Para más información sobre los requisitos adicionales para este escenario, vea [Requisitos de Azure RMS: Servidores locales que son compatibles con Azure RMS](requirements-servers.md).

> [!IMPORTANT]
> El siguiente escenario de implementación no se admite a no ser que esté usando la protección de AD RMS con Azure Information Protection (la configuración “conserve su propia clave” o HYOK):
> 
> -   Ejecución de AD RMS y Azure RMS en paralelo en la misma organización, salvo durante la migración, tal como se describe en [Migración desde AD RMS a Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).
> 
> Existe una ruta de acceso de migración que se admite [desde AD RMS a Azure Information Protection](http://technet.microsoft.com/library/Dn858447.aspx) y desde [Azure Information Protection a AD RMS](/powershell/module/aadrm/Set-AadrmMigrationUrl). Si implementa Azure Information Protection y después decide que ya no quiere usar este servicio en la nube, vea [Retirada y desactivación de Azure Information Protection](../deploy-use/decommission-deactivate.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


