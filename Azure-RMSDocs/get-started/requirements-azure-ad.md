---
title: Requisitos de Azure Active Directory | Azure Information Protection
description: Identifique los requisitos de Azure AD para usar Azure Information Protection de forma que los usuarios se puedan autenticar correctamente.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ed25aa83-e272-437b-b445-3f01e985860c
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d704751bcc7a968c204d0bab0dc55776411d9593
ms.openlocfilehash: ecb85e8fd2f09579536782f00a1babddb9466c54


---

# <a name="azure-active-directory-requirements-for-azure-information-protection"></a>Requisitos de Azure Active Directory para Azure Information Protection

>*Se aplica a: Azure Information Protection, Office 365*

Para poder usar Azure Information Protection se necesita un directorio de Azure AD. Use la cuenta de la organización para este directorio para poder iniciar sesión en el Portal de Azure clásico, en donde, por ejemplo, podrá configurar y administrar las plantillas de Rights Management.

Si no dispone aún de suscripción de Azure para su organización, puede obtener una si se registra para una evaluación gratuita: Vaya a la página de [Introducción a Azure](https://account.windowsazure.com/organization) y siga las instrucciones.

Para más información, consulte los recursos siguientes en la documentación de Azure Active Directory:

-   [¿Qué es el directorio de Azure AD?](/active-directory/active-directory-whatis)

-   [Asociación de las suscripciones a Azure con Azure Active Directory](/active-directory/active-directory-how-subscriptions-associated-directory)

Si desea integrar el directorio de Azure AD con los bosques de AD locales, consulte [Integración de las identidades locales con Azure Active Directory](/active-directory/active-directory-aadconnect).

### <a name="scenarios-that-have-specific-requirements"></a>Escenarios que tienen requisitos específicos 

Equipos que ejecutan Office 2010: 

- Si las cuentas de usuario están federadas (por ejemplo, usa AD FS), deben usar la autenticación integrada de Windows. En este escenario la autenticación basada en formularios no podrá autenticar a los usuarios en Azure Information Protection.

Dispositivos móviles o equipos Mac que se autentican localmente mediante AD FS o un proveedor de autenticación equivalente:

- Debe usar AD FS en la versión mínima de servidor de **Windows Server 2012 R2** o un proveedor de autenticación alternativo que admita el protocolo OAuth 2.0.

## <a name="multi-factor-authentication-mfa-and-azure-information-protection"></a>Multi-Factor Authentication (MFA) y Azure Information Protection
Para usar Multi-Factor Authentication (MFA) con Azure Information Protection se necesita como mínimo uno de los dos requisitos siguientes:

-   Office 2013 (versión mínima):

    -   Si tiene Office 2013, también debe instalar la [actualización del 9 de junio de 2015 para Office 2013 (KB3054853)](https://support.microsoft.com/kb/3054853). Para más información sobre esta actualización y sobre la manera en que la autenticación moderna proporciona el inicio de sesión basado en la Biblioteca de autenticación de Active Directory (ADAL) para Office 2013, consulte [Anuncio de la versión preliminar pública de la autenticación moderna de Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/) en el blog de Office.

- Cliente de Azure Information Protection:

    - El [cliente de Azure Information Protection](../rms-client/aip-client.md) para Windows y para iOS y Android siempre ha admitido MFA; no se requiere ninguna versión mínima. 

-   Aplicación para uso compartido de Rights Management para Windows:

    -   Debe tener instalada la versión mínima de 1.0.1908.0, lo que puede confirmar mediante el Panel de control, Programas y características. Tenga en cuenta que la aplicación Rights Management sharing ahora se reemplaza por el cliente de Azure Information Protection. Para más información sobre la aplicación de uso compartido, consulte [Aplicación de uso compartido Rights Management para Windows](../rms-client/sharing-app-windows.md).

-   Aplicación para uso compartido de Rights Management para dispositivos móviles y equipos Mac:

    -   Asegúrese de que tiene la última versión instalada. La compatibilidad con MFA se incluyó en la versión de septiembre de 2015 de la aplicación para uso compartido de RMS.

A continuación, configure la solución MFA:

-   Para inquilinos administrados por Microsoft (dispone de Azure Active Directory u Office 365):

    -   Configure Azure MFA para aplicar MFA en los usuarios. Para obtener instrucciones, consulte [Introducción a Azure Multi-Factor Authentication en la nube](/multi-factor-authentication/multi-factor-authentication-get-started-cloud) en la documentación de Multi-factor Authentication.

        Para más información sobre Azure MFA, consulte [¿Qué es Azure Multi-Factor Authentication?](/multi-factor-authentication/multi-factor-authentication)

-   Para inquilinos federados (los servidores de federación funcionan localmente):

    -   Configure los servidores de federación para Azure Active Directory u Office 365. Por ejemplo, si usa AD FS, consulte [Configurar métodos de autenticación adicionales para AD FS](https://technet.microsoft.com/library/dn758113.aspx) en TechNet.

        Para más información sobre este escenario, consulte [Programa Works with Office 365 – Identity ahora simplificado](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/) en el blog de Office.

## <a name="next-steps"></a>Pasos siguientes
Para comprobar otros requisitos, vea [Requisitos para Azure Information Protection](requirements-azure-rms.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



<!--HONumber=Feb17_HO2-->


