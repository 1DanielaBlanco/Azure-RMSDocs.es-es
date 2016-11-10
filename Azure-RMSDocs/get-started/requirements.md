---
title: Requisitos de Azure Information Protection | Azure RMS
description: "Identifique los requisitos previos para implementar Azure Information Protection en su organización."
author: cabailey
manager: mbaldwin
ms.date: 10/19/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8b456ae32446a2c429f33b76563eef53ea92a902
ms.openlocfilehash: bbcc5f71eda6b100ad16f33793752b92ddfa4304


---

# <a name="requirements-for-azure-information-protection"></a>Requirements for Azure Information Protection (Requisitos de Azure Information Protection)

>*Se aplica a: Azure Information Protection, Office 365*

Antes de implementar Azure Information Protection para su organización, asegúrese de que tiene los siguientes requisitos previos. 

|Requisito|Más información|
|---------------|--------------------|
|Una suscripción a Azure Information Protection|Revise la [información sobre la suscripción](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing) y la [lista de características](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features) en el sitio de Azure Information Protection para asegurarse de que la suscripción de la organización incluye las características de Azure Information Protection que quiere usar.|
|Azure Active Directory|Su organización debe tener un directorio de Azure Active Directory (Azure AD) para admitir la autenticación de usuario para Azure Information Protection. Además, si desea usar sus cuentas de usuario desde su directorio local (AD DS), también deberá configurar la integración de directorios.<br /><br />Si las cuentas están federadas (por ejemplo, usa AD FS), deben usar la autenticación integrada de Windows. No se admite la autenticación basada en formularios en Azure Information Protection.<br /><br />Multi-Factor Authentication (MFA) es compatible con Azure Information Protection si tiene el software cliente necesario y la infraestructura de MFA configurada correctamente.<br /><br />Para obtener más información, vea [Requisitos de Azure Active Directory para Azure Information Protection](requirements-azure-ad.md).|
|Dispositivos cliente|Los usuarios deben tener dispositivos cliente (equipo o dispositivo móvil) que ejecuten un sistema operativo compatible con Azure Information Protection.<br /><br />Los siguientes dispositivos admiten el cliente de Azure Information Protection, que permite a los usuarios clasificar y etiquetar los correos electrónicos y documentos de Office:<br /><br />- Windows 10 (x86 y x64)<br /><br />- Windows 8.1 (x86 y x64)<br /><br />- Windows 8 (x86 y x64)<br /><br />- Windows 7 Service Pack 1 (x86 y x64)<br /><br />Cuando este cliente protege los datos mediante el servicio Azure Rights Management, puede consumirse por los mismos dispositivos (Windows, Mac, iOS, Android), que admiten el servicio Azure Rights Management. <br /><br />Para obtener información sobre los dispositivos que admiten el servicio Azure Rights Management, vea [Requisitos de Azure RMS: Dispositivos cliente que son compatibles con Azure RMS](../get-started/requirements-client-devices.md).|
|Aplicaciones|El cliente de Azure Information Protection admite el etiquetado y la protección de archivos y correos electrónicos creados con las siguientes aplicaciones de Office: **Word**, **Excel**, **PowerPoint** y **Outlook** desde los siguientes paquetes de Office:<br /><br />- Office Professional Plus 2016<br /><br />- Office Professional Plus 2013 con Service Pack 1<br /><br />- Office Professional Plus 2010<br /><br />Para obtener información sobre las aplicaciones que son compatibles con el servicio Azure Rights Management, vea [Aplicaciones compatibles con la protección de datos de Azure Rights Management](requirements-applications.md).|
|Infraestructura compatible con la conectividad a Internet y dependiente de los servicios en la nube|Si tiene un firewall o dispositivos de red de intervención similares que deban configurarse para permitir conexiones específicas, vea la información de **Azure Rights Management (RMS)** en la sección [Portal de Office 365 e infraestructura compartida](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#BKMK_Portal-identity) del siguiente artículo de Office: [URL de Office 365 e intervalos de direcciones IP](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).<br /><br />Siga las instrucciones de este artículo de Office para suscribirse a una fuente RSS y mantenerse así al día de los cambios que se hagan en esta información.<br /><br />Además de la información del artículo de Office específica de Azure Information Protection:<br /><br />- Permita tráfico HTTPS en TCP 443 a **api.informationprotection.azure.com**.<br /><br />- No termine la conexión TLS de cliente a servicio (por ejemplo, para realizar una inspección de los paquetes). Al hacerlo, se interrumpe la asignación de certificados que los clientes de RMS utilizan con las entidades de certificación administradas por Microsoft para ayudar a proteger su comunicación con Azure RMS.<br /><br />- Si usa un proxy web que precisa de autenticación, debe configurarlo para usar autenticación integrada de Windows con las credenciales de inicio de sesión de Active Directory del usuario.|

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
> Existe una ruta de acceso de migración que se admite [desde AD RMS a Azure Information Protection](http://technet.microsoft.com/library/Dn858447.aspx) y desde [Azure Information Protection a AD RMS](http://msdn.microsoft.com/library/azure/dn629429.aspx). Si implementa Azure Information Protection y después decide que ya no quiere usar este servicio en la nube, vea [Retirada y desactivación de Azure Information Protection](../deploy-use/decommission-deactivate.md).






<!--HONumber=Nov16_HO1-->


