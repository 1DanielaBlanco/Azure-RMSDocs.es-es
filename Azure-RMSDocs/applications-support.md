---
title: Compatibilidad de las aplicaciones con Azure Rights Management en AIP
description: Conozca cómo la mayoría de las aplicaciones de usuario final (como las aplicaciones de Office, Word, Excel, PowerPoint y Outlook) y los servicios (como Exchange y SharePoint) más usados pueden utilizar el servicio Azure Rights Management de Azure Information Protection para ayudar a proteger los documentos y correos electrónicos de su organización.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: f529b761ef757612b621e948a49805448f9414ba
ms.sourcegitcommit: 949bf02d5d12bef8e26d89ad5d6a0d5cc7826135
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39474672"
---
# <a name="how-applications-support-the-azure-rights-management-service"></a>Cómo admiten las aplicaciones el servicio Azure Rights Management

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Use la información siguiente para conocer cómo las aplicaciones y servicios de usuario final más usados pueden usar el servicio Azure Rights Management de Azure Information Protection para ayudar a proteger los documentos y los correos electrónicos de su organización. Entre estas aplicaciones se incluyen Word, Excel, PowerPoint y Outlook. Entre los servicios se incluyen Exchange y SharePoint.

> [!NOTE]
> Para comprobar las aplicaciones y versiones que son compatibles con el servicio Azure Rights Management, vea [Aplicaciones compatibles con la protección de datos de Azure Rights Management](./requirements-applications.md).

En algunos casos, el servicio Azure Rights Management aplica la protección automáticamente, según las directivas que configuren los administradores. Por ejemplo, este es el caso de las bibliotecas de SharePoint y las reglas de transporte de Exchange. En otros casos, los usuarios finales deben aplicar la protección por sí mismos desde sus aplicaciones. Por ejemplo, los usuarios pueden seleccionar una etiqueta de clasificación configurada para aplicar la protección, o bien pueden seleccionar una plantilla u opciones específicas. Los usuarios aplican protección cuando quieren proteger un archivo para compartirlo y, al mismo tiempo, restringir su acceso o uso a determinados usuarios o a usuarios ajenos a la organización.

Las plantillas facilitan a los usuarios (y a los administradores que configuran las directivas) la aplicación del nivel de protección adecuado y restringen el acceso a personas de dentro de la organización. Aunque en el servicio Azure Rights Management se incluyen dos plantillas predeterminadas, es probable que quiera crear plantillas personalizadas para reducir las ocasiones en las que los usuarios y los administradores deben especificar opciones individuales. Para obtener más información sobre las plantillas, vea [Configuración y administración de plantillas para Azure Information Protection](./deploy-use/configure-policy-templates.md).

En los casos en que los usuarios deban aplicar ellos mismos la protección, asegúrese de proporcionarles las instrucciones y las directrices sobre cómo y cuándo deben hacerlo. Las instrucciones deben ser específicas de la aplicación y las versiones que se usan y del uso que se hace de ellas. Proporcione también a los usuarios información sobre cuándo y cómo aplicar la protección adecuada para el negocio. Para más información, vea [Ayuda a los usuarios para proteger archivos mediante Azure Rights Management](./deploy-use/help-users.md).

Para obtener información sobre cómo configurar estas aplicaciones para el servicio Azure Rights Management de Azure Information Protection, vea [Configurar aplicaciones para Azure Rights Management](./deploy-use/configure-applications.md).

Los servicios de búsqueda se pueden integrar con Rights Management de maneras diferentes. Por ejemplo: 

- Exchange Online y Exchange Server usan la indexación del servicio para que los mensajes de correo electrónico protegidos de un usuario se muestren automáticamente en los resultados de búsqueda. 

- SharePoint Online y SharePoint Server aplican la protección de Rights Management a los archivos únicamente durante la descarga. Como consecuencia de esta implementación, los resultados de la indexación y de la búsqueda en SharePoint no se ven afectados por esta solución de protección de documentos. Aun así, si tiene un documento que quiere guardar en SharePoint y no se debe devolver en los resultados de la búsqueda, protéjalo antes de cargarlo en SharePoint.

- La búsqueda de escritorio de Windows usa un índice compartido entre distintos usuarios del dispositivo, por lo que para proteger los datos de los documentos protegidos, no indexa los archivos protegidos. Esto significa que, aunque los resultados de la búsqueda no incluyen los archivos que ha protegido, puede estar seguro de que los archivos que contienen datos confidenciales no se mostrarán en los resultados de la búsqueda de otros usuarios que inicien sesión en su equipo o se conecten a este. 

## <a name="next-steps"></a>Pasos siguientes

Obtenga más información sobre la compatibilidad de las aplicaciones y los servicios siguientes con el servicio Azure Rights Management:

-   [Aplicación RMS sharing para Windows y plataformas móviles](sharing-app-support.md)

-   [Aplicaciones y servicios de Office](office-apps-services-support.md)

-   [Servidores de archivos que ejecutan Windows Server y usan Infraestructura de clasificación de archivos (FCI)](file-server-support.md)

-   [Otras aplicaciones compatibles con las API de RMS](api-support.md)

