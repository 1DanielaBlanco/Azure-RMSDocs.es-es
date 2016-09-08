---
title: Requisitos de Azure RMS&#58; Directorio de Azure AD | Azure RMS
description: "Debe disponer de un directorio de Azure AD para poder usar Azure Rights Management (Azure RMS). Use la cuenta de la organización para este directorio para poder iniciar sesión en el Portal de Azure clásico, en donde, por ejemplo, podrá configurar y administrar las plantillas de Rights Management."
author: cabailey
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: get-started-article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ed25aa83-e272-437b-b445-3f01e985860c
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: 8083c2f7e4cfdbf65748007ae21a48a49a56599f


---

# Requisitos de Azure RMS: Directorio de Azure AD

>*Se aplica a: Azure Rights Management, Office 365*


Debe disponer de un directorio de Azure AD para poder usar Azure Rights Management (Azure RMS). Use la cuenta de la organización para este directorio para poder iniciar sesión en el Portal de Azure clásico, en donde, por ejemplo, podrá configurar y administrar las plantillas de Rights Management.

Si no dispone aún de suscripción de Azure para su organización, puede obtener una si se registra para una prueba gratuita: vaya a la página [Introducción a Azure](https://account.windowsazure.com/organization) y siga las instrucciones.

Para más información, consulte los recursos siguientes en la documentación de Azure Active Directory:

-   [¿Qué es un directorio de Azure AD?](/active-directory/active-directory-whatis)

-   [Asociación de las suscripciones a Azure con Azure Active Directory](/active-directory/active-directory-how-subscriptions-associated-directory)

Si desea integrar el directorio de Azure AD con los bosques de AD locales, consulte [Integración de las identidades locales con Azure Active Directory](/active-directory/active-directory-aadconnect).

> [!NOTE]
> Si tiene dispositivos móviles o equipos que realizan la autenticación localmente utilizando AD FS o un proveedor de autenticación equivalente:
> 
> -   Debe usar AD FS en la versión mínima de servidor de **Windows Server 2012 R2** o un proveedor de autenticación alternativo que admita el protocolo OAuth 2.0.

## Multi-Factor Authentication (MFA) y Azure RMS
Para usar Multi-Factor Authentication (MFA) con Azure RMS hace falta como mínimo uno de los siguientes:

-   Office 2013 (versión mínima):

    -   Si tiene Office 2013, también debe instalar la [actualización del 9 de junio de 2015 para Office 2013 (KB3054853)](https://support.microsoft.com/kb/3054853). Para más información sobre esta actualización y sobre la manera en que la autenticación moderna proporciona el inicio de sesión basado en la Biblioteca de autenticación de Active Directory (ADAL) para Office 2013, consulte [Anuncio de la versión preliminar pública de la autenticación moderna de Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/) en el blog de Office.

-   Aplicación para uso compartido de Rights Management para Windows:

    -   Debe tener instalada la versión mínima de 1.0.1908.0, lo que puede confirmar mediante el Panel de control, Programas y características. Para más información sobre la aplicación de uso compartido, consulte [Aplicación de uso compartido Rights Management para Windows](../rms-client/sharing-app-windows.md).

-   Aplicación para uso compartido de Rights Management para dispositivos móviles y equipos Mac:

    -   Asegúrese de que tiene la última versión instalada. La compatibilidad con MFA se incluyó en la versión de septiembre de 2015 de la aplicación para uso compartido de RMS.

A continuación, configure la solución MFA:

-   Para inquilinos administrados por Microsoft (dispone de Azure Active Directory u Office 365):

    -   Configure Azure MFA para aplicar MFA en los usuarios. Para obtener instrucciones, consulte [Introducción a Azure Multi-Factor Authentication en la nube](/multi-factor-authentication/multi-factor-authentication-get-started-cloud) en la documentación de Multi-factor Authentication.

        Para más información sobre Azure MFA, consulte [¿Qué es Azure Multi-Factor Authentication?](/multi-factor-authentication/multi-factor-authentication)

-   Para inquilinos federados (los servidores de federación funcionan localmente):

    -   Configure los servidores de federación para Azure Active Directory u Office 365. Por ejemplo, si usa AD FS, consulte [Configurar métodos de autenticación adicionales para AD FS](https://technet.microsoft.com/library/dn758113.aspx) en TechNet.

        Para más información sobre este escenario, consulte [Programa Works with Office 365 – Identity ahora simplificado](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/) en el blog de Office.

## Pasos siguientes
Para buscar otros requisitos, consulte [Requisitos de Azure Rights Management](requirements-azure-rms.md).




<!--HONumber=Aug16_HO4-->


