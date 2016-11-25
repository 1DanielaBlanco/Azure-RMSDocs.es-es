---
title: Configurando aplicaciones para el servicio Azure Rights Management| Azure Information Protection
description: "Instrucciones para administradores para configurar aplicaciones y servicios para admitir el servicio de protección de Azure Rights Management para Azure Information Protection. Por ejemplo, aplicaciones de Office, como Word 2013 y Word 2010, y servicios, como Exchange Online (reglas de transporte, prevención de pérdida de datos, no reenviar y cifrado de mensajes) y SharePoint Online (bibliotecas protegidas)."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/05/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ea09cbc5-b98b-444e-8b60-5bc3cb199c36
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: c4b510dac964d0703b7eba8266a244f40b83f403


---

# <a name="configuring-applications-for-azure-rights-management"></a>Configuración de aplicaciones para Azure Rights Management

>*Se aplica a: Azure Information Protection, Office 365*

> [!NOTE]
> Esta información está destinada a los asesores y administradores de TI que han implementado Azure Information Protection. Si busca ayuda e información sobre cómo usar la funcionalidad de Rights Management con una aplicación específica o cómo abrir un archivo protegido por derechos, use la ayuda y las instrucciones que se incluyen con la aplicación.
>
> Por ejemplo, para las aplicaciones de Office, haga clic en el icono de Ayuda y escriba términos de búsqueda como **Rights Management** o **IRM**. Para la aplicación RMS sharing para Windows, consulte la [guía de usuario de la aplicación Rights Management sharing](../rms-client/sharing-app-user-guide.md).

Después de haber implementado Azure Information Protection para su organización, use la siguiente información para configurar aplicaciones y servicios compatibles con el servicio Azure Rights Management de Azure Information Protection. Aquí se incluyen aplicaciones de Office, como Word 2013 y Word 2010, y servicios, como Exchange Online (reglas de transporte, prevención de pérdida de datos, no reenviar y cifrado de mensajes) y SharePoint Online (bibliotecas protegidas). Para obtener más información sobre la compatibilidad de estas aplicaciones y servicios con Rights Management, vea [Cómo son compatibles las aplicaciones con Azure Rights Management](../understand-explore/applications-support.md).

> [!IMPORTANT]
> Para más información sobre versiones compatibles y otros requisitos, consulte [Requirements for Azure Rights Management](../get-started/requirements-azure-rms.md) (Requisitos para Azure Rights Management).

-   [Office 365: Configuración para clientes y servicios en línea](configure-office365.md)

    -   [Exchange Online: Configuración de IRM](configure-office365.md#exchange-online-irm-configuration)

    -   [SharePoint Online y OneDrive para la Empresa: Configuración de IRM](configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)

- [Aplicaciones de Office: configuración para clientes](configure-office-apps.md)

    -   [Office 2016 y Office 2013](configure-office-apps.md#office-2016-and-office-2013)

    -   [Office 2010](configure-office-apps.md#office-2010)

-   [Aplicación Rights Management sharing: Instalación y configuración para clientes](configure-sharing-app.md)

    -   [La aplicación RMS sharing para Windows: Instalación y configuración](configure-sharing-app.md#the-rms-sharing-application-for-windows-installation-and-configuration)

    -   [La aplicación RMS sharing para plataformas móviles: instalación y administración](configure-sharing-app.md#the-rms-sharing-application-for-mobile-platforms-installation-and-management)


Para configurar servidores locales como Exchange Server y SharePoint Server, consulte [Deploying the Azure Rights Management connector](deploy-rms-connector.md) (Implementación del conector de Azure Rights Management).

> [!TIP]
> Para obtener ejemplos de alto nivel y capturas de pantalla de aplicaciones configuradas para usar el servicio Azure Rights Management, vea [Azure RMS en acción: Qué ven los administradores y los usuarios](../understand-explore/what-admins-users-see.md).


Además de estas aplicaciones y servicios, hay otras aplicaciones que admiten las API de Rights Management. Esta categoría incluye aplicaciones de línea de negocio que se han diseñado internamente mediante el SDK de Rights Management y aplicaciones de proveedores de software que se han diseñado mediante el SDK de Rights Management. Para estas aplicaciones, sigue las instrucciones suministradas junto a la aplicación.

## <a name="next-steps"></a>Pasos siguientes
Después de configurar las aplicaciones para que sean compatibles con el servicio Azure Rights Management, use el [mapa de ruta de implementación de Azure Information Protection](../plan-design/deployment-roadmap.md) para comprobar si hay otros pasos de configuración que puedan ser necesarios antes de implementar Azure Information Protection en usuarios y administradores. Si no, es posible que encuentre útil la siguiente información operativa:

- [Comprobar el servicio Azure Rights Management](verify.md)

- [Ayuda a los usuarios para proteger archivos mediante el servicio Azure Rights Management](help-users.md)

- [Registro y análisis del servicio Azure Rights Management](log-analyze-usage.md)

- [Operaciones para la clave de inquilino de Azure Information Protection](operations-tenant-key.md)





<!--HONumber=Nov16_HO2-->


