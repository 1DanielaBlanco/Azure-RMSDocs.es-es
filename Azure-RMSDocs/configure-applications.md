---
title: Configuración de aplicaciones para Azure Rights Management - AIP
description: Instrucciones para administradores para configurar aplicaciones y servicios para admitir el servicio de protección de Azure Rights Management para Azure Information Protection. Por ejemplo, aplicaciones de Office, como Word 2013 y Word 2010, y servicios, como Exchange Online (reglas de transporte, prevención de pérdida de datos, no reenviar y cifrado de mensajes) y SharePoint Online (bibliotecas protegidas).
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/31/2018
ms.topic: article
ms.service: information-protection
ms.assetid: ea09cbc5-b98b-444e-8b60-5bc3cb199c36
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: bb8f790458f57ccf0fdafa93de0383de82a7c631
ms.sourcegitcommit: 99b33cee47bc4588174d44e90ade16edba12ee44
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/31/2018
ms.locfileid: "43380584"
---
# <a name="configuring-applications-for-azure-rights-management"></a>Configuración de aplicaciones para Azure Rights Management

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!NOTE]
> Esta información está destinada a los asesores y administradores de TI que han implementado Azure Information Protection. Si busca ayuda e información sobre cómo usar la funcionalidad de Rights Management con una aplicación específica o cómo abrir un archivo protegido por derechos, use la ayuda y las instrucciones que se incluyen con la aplicación.
>
> Por ejemplo, para las aplicaciones de Office, haga clic en el icono de Ayuda y escriba términos de búsqueda como **Rights Management** o **IRM**. Para el cliente de Azure Information Protection para Windows, vea la [Guía del usuario de Azure Information Protection](./rms-client/client-user-guide.md).

Después de haber implementado Azure Information Protection para su organización, use la siguiente información para configurar aplicaciones, el cliente de Azure Information Protection y los servicios. Por ejemplo, aplicaciones de Office como Word 2016, Word 2013 y Word 2010. Los servicios como Exchange Online (reglas de transporte, prevención de pérdida de datos, no reenviar y cifrado de mensajes) y SharePoint Online (bibliotecas protegidas). Para obtener información sobre cómo estas aplicaciones y estos servicios admiten el servicio de protección de datos de Azure Information Protection, vea [Cómo admiten las aplicaciones el servicio Azure Rights Management](applications-support.md).

> [!IMPORTANT]
> Para más información sobre versiones compatibles y otros requisitos, consulte [Requirements for Azure Rights Management](requirements.md) (Requisitos para Azure Rights Management).

-   [Office 365: Configuración para clientes y servicios en línea](configure-office365.md)

    -   [Exchange Online: Configuración de IRM](configure-office365.md#exchange-online-irm-configuration)

    -   [SharePoint Online y OneDrive para la Empresa: Configuración de IRM](configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)

- [Aplicaciones de Office: configuración para clientes](configure-office-apps.md)

    -   [Office 2016 y Office 2013](configure-office-apps.md#office-2016-and-office-2013)

    -   [Office 2010](configure-office-apps.md#office-2010)

-   [Cliente de Azure Information Protection: instalación y configuración de clientes](configure-sharing-app.md)

-   [Aplicación Rights Management sharing: Instalación y configuración para clientes](configure-sharing-app.md)


Para configurar servidores locales como Exchange Server y SharePoint Server, consulte [Deploying the Azure Rights Management connector](deploy-rms-connector.md) (Implementación del conector de Azure Rights Management).

Además de estas aplicaciones y servicios, hay otras aplicaciones que admiten las API de Rights Management. Esta categoría incluye aplicaciones de línea de negocio que se han diseñado internamente mediante el SDK de Rights Management y aplicaciones de proveedores de software que se han diseñado mediante el SDK de Rights Management. Para estas aplicaciones, sigue las instrucciones suministradas junto a la aplicación.

## <a name="next-steps"></a>Pasos siguientes
Después de configurar las aplicaciones para que sean compatibles con el servicio Azure Rights Management, use el [mapa de ruta de implementación de Azure Information Protection](deployment-roadmap.md) para comprobar si hay otros pasos de configuración que puedan ser necesarios antes de implementar Azure Information Protection en usuarios y administradores. Si no, es posible que encuentre útil la siguiente información operativa:

- [Comprobar el servicio Azure Rights Management](verify.md)

- [Ayuda a los usuarios para proteger archivos mediante el servicio Azure Rights Management](help-users.md)

- [Registro y análisis del servicio Azure Rights Management](log-analyze-usage.md)

- [Operaciones para la clave de inquilino de Azure Information Protection](operations-tenant-key.md)


