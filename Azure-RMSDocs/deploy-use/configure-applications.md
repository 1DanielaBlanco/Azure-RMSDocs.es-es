---
# required metadata

title: Configuración de aplicaciones para Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ea09cbc5-b98b-444e-8b60-5bc3cb199c36

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configuración de aplicaciones para Azure Rights Management
> [!NOTE]
> Esta información está destinada a los asesores y administradores de TI que han implementado Azure Rights Management. Si busca ayuda e información sobre cómo usar Rights Management con una aplicación específica o cómo abrir un archivo protegido por derechos, use la ayuda y las instrucciones que se incluyen con la aplicación.
>
> Por ejemplo, para las aplicaciones de Office, haga clic en el icono de Ayuda y escriba términos de búsqueda como **Rights Management** o **IRM**. Para la aplicación RMS sharing para Windows, consulte la [guía de usuario de la aplicación Rights Management sharing](../rms-client/sharing-app-user-guide.md).

Después de haber implementado Azure Rights Management (Azure RMS) en su organización, use la siguiente información para configurar aplicaciones y servicios compatibles con Azure RMS. Aquí se incluyen aplicaciones de Office, como Word 2013 y Word 2010, y servicios, como Exchange Online (reglas de transporte, prevención de pérdida de datos, no reenviar y cifrado de mensajes) y SharePoint Online (bibliotecas protegidas). Para más información sobre la compatibilidad de estas aplicaciones y servicios con Azure Rights Management, consulte [How applications support Azure Rights Management](../understand-explore/applications-support.md) (Compatibilidad de las aplicaciones con Azure Rights Management).

> [!IMPORTANT]
> Para más información sobre versiones compatibles y otros requisitos, consulte [Requirements for Azure Rights Management](../get-started/requirements-azure-rms.md) (Requisitos para Azure Rights Management).

-   [Office 365: Configuración para clientes y servicios en línea](configure-office365.md)

    -   [Exchange Online: Configuración de IRM](configure-office365.md#exchange-online-irm-configuration)

    -   [SharePoint Online y OneDrive para la Empresa: Configuración de IRM](configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)

- [Aplicaciones de Office: configuración para clientes](configure-office-apps.md)

    -   [Office 2016 y Office 2013](configure-office-apps.md#office-2016-and-office-2013)

    -   [Office 2010](configure-office-apps.md#office-2010)

-   [Aplicación de uso compartido Rights Management Instalación y configuración para clientes](configure-sharing-app.md)

    -   [La aplicación de uso compartido de RMS para Windows: Instalación y configuración](configure-sharing-app.md#the-rms-sharing-application-for-windows-installation-and-configuration)

    -   [La aplicación RMS sharing para plataformas móviles: instalación y administración](configure-sharing-app.md#the-rms-sharing-application-for-mobile-platforms-installation-and-management)


Para configurar servidores locales como Exchange Server y SharePoint Server, consulte [Deploying the Azure Rights Management connector](deploy-rms-connector.md) (Implementación del conector de Azure Rights Management).

> [!TIP]
> Para obtener ejemplos de alto nivel y capturas de pantalla de aplicaciones configuradas para usar Azure RMS, consulte [Azure RMS in action: What administrators and users see](../understand-explore/what-admins-users-see.md) (Azure RMS en acción: Qué ven los administradores y los usuarios).


Además de estas aplicaciones y servicios, hay otras aplicaciones que admiten las API de RMS. Esta categoría incluye aplicaciones de línea de negocio que se han diseñado internamente mediante el SDK de RMS y aplicaciones de proveedores de software que se han diseñado mediante el SDK de RMS. Para estas aplicaciones, sigue las instrucciones suministradas junto a la aplicación.

## Pasos siguientes
Después de configurar las aplicaciones para que sean compatibles con Azure Rights Management, consulte [Azure Rights Management deployment roadmap](../plan-design/deployment-roadmap.md) (Mapa de ruta de implementación de Azure Rights Management) para comprobar si hay otros pasos de configuración que puedan ser necesarios antes de implementar [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] en usuarios y administradores. Si no, es posible que encuentre útil la siguiente información operativa:

- [Comprobación de Azure Rights Management](verify.md)

- [Ayuda a los usuarios para proteger archivos mediante Azure Rights Management](help-users.md)

- [Registro y análisis del uso de Azure Rights Management](log-analyze-usage.md)

- [Operaciones para la clave de inquilino de Administración de permisos de Azure](operations-tenant-key.md)




<!--HONumber=Apr16_HO3-->


