---
title: Requisitos de Azure Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/17/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 50ebcd71336baeb68687e2d0c1ff1f0608925761
ms.openlocfilehash: 72a75712da9efa201865440affa80461dcd7df53


---

# Requisitos de Azure Rights Management

*Se aplica a: Azure Rights Management, Office 365*


Para implementar Microsoft Azure Rights Management (Azure RMS) en su organización, asegúrese de que cumple con los siguientes requisitos previos. Podrá entonces usar el [Plan para la implementación de Azure Rights Management](../plan-design/deployment-roadmap.md) a fin de implementar Rights Management para su organización.

|Requisito|Más información|
|---------------|--------------------|
|Una suscripción en la nube para RMS|Su organización debe tener una suscripción en la nube que admita RMS.<br /><br />Para obtener información sobre la obtención de licencias, consulte la sección [Suscripciones en la nube que son compatibles con Azure RMS](requirements-subscriptions.md).|
|Directorio de Azure AD|Su organización debe tener un directorio de Azure AD que admita la autenticación de usuario para RMS. Además, si desea usar sus cuentas de usuario desde su directorio local (AD DS), también deberá configurar la integración de directorios.<br /><br />Multi-Factor Authentication (MFA) es compatible con Azure RMS si tiene el software cliente necesario y la infraestructura de MFA configurada correctamente.<br /><br />Para más información, consulte [Azure Active Directory](requirements-azure-ad.md).|
|Dispositivos cliente|Los usuarios deben tener dispositivos cliente (equipo o dispositivo móvil) que ejecuten un sistema operativo compatible con RMS.<br /><br />Para más información, consulte [Dispositivos cliente que son compatibles con Azure RMS](requirements-client-devices.md).|
|Aplicaciones|Los usuarios deben ejecutar aplicaciones que sean compatibles con RMS.<br /><br />Para más información, consulte [Aplicaciones que son compatibles con Azure RMS](requirements-applications.md).|
|Infraestructura compatible con la conectividad a Internet y dependiente de los servicios en la nube|Si tiene un firewall o dispositivos de red que intervengan que se deben configurar para permitir conexiones específicas, consulte [Direcciones URL e intervalos de direcciones IP de Office 365](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).<br /><br />La lista de direcciones URL y direcciones IP en las secciones **Portal de Office 365 e infraestructura compartida** y **Autenticación e identidad de Office 365** es aplicable al Portal de Office 365, a los recursos de Azure Active Directory y a Azure Rights Management. Siga las instrucciones de este artículo para suscribirse a una fuente RSS y mantenerse así al día de los cambios que se realicen en esta información.<br /><br />Además de la información del artículo de Office específica de Azure RMS:<br /><br />- No termine la conexión TLS de cliente a servicio (por ejemplo, para realizar una inspección de los paquetes). Al hacerlo, se interrumpe la asignación de certificados que los clientes de RMS utilizan con las entidades de certificación administradas por Microsoft para ayudar a proteger su comunicación con Azure RMS.<br /><br />- Si usa un proxy web que precisa de autenticación, debe configurarlo para usar autenticación integrada de Windows con las credenciales de inicio de sesión de Active Directory del usuario.|

Si desea usar Azure RMS con servidores locales, se admiten los siguientes productos:

-   Exchange Server

-   Servidor de SharePoint

-   Servidores de archivos de Windows Server que son compatibles con la Infraestructura de la clasificación de archivos

Para más información sobre los requisitos adicionales de Azure RMS para este escenario, consulte [Servidores locales compatibles con Azure RMS](requirements-servers.md).

> [!IMPORTANT]
> El siguiente escenario de implementación no es compatible:
> 
> -   Ejecución de AD RMS y Azure RMS en paralelo en la misma organización, salvo durante la migración, tal como se describe en [Migración desde AD RMS a Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md).
> 
> Hay una ruta de acceso de migración compatible [desde AD RMS a Azure RMS](http://technet.microsoft.com/library/Dn858447.aspx) y desde [Azure RMS a AD RMS](http://msdn.microsoft.com/library/azure/dn629429.aspx). Si implementa Azure RMS y después decide que ya no desea usar este servicio en la nube, consulte [Retirada y desactivación de Azure Rights Management](../deploy-use/decommission-deactivate.md).






<!--HONumber=Jul16_HO2-->


