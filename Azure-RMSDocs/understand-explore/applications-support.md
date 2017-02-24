---
title: Compatibilidad de aplicaciones con el servicio Azure Rights Management | Azure Information Protection
description: "Conozca cómo la mayoría de las aplicaciones de usuario final (como las aplicaciones de Office, Word, Excel, PowerPoint y Outlook) y los servicios (como Exchange y SharePoint) más usados pueden utilizar el servicio Azure Rights Management de Azure Information Protection para ayudar a proteger los documentos y correos electrónicos de su organización."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ffed64826982756072456be18cced0226b6bb6cc
ms.openlocfilehash: 53a77c0e312f44fe2210ed19ead6dedeb36a5a78


---

# <a name="how-applications-support-the-azure-rights-management-service"></a>Cómo admiten las aplicaciones el servicio Azure Rights Management

>*Se aplica a: Azure Information Protection, Office 365*

Use la información siguiente para conocer cómo la mayoría de las aplicaciones de usuario final (como las aplicaciones de Office, Word, Excel, PowerPoint y Outlook) y los servicios (como Exchange y SharePoint) más usados pueden utilizar el servicio Azure Rights Management de Azure Information Protection para ayudar a proteger los documentos y correos electrónicos de su organización. 
> [!NOTE]
> Para comprobar las aplicaciones y versiones que son compatibles con el servicio Azure Rights Management, vea [Aplicaciones compatibles con la protección de datos de Azure Rights Management](../get-started/requirements-applications.md).

En algunos casos, el servicio Azure Rights Management aplica la protección automáticamente, según las directivas que configuren los administradores. Por ejemplo, este es el caso de las bibliotecas de SharePoint y las reglas de transporte de Exchange. En otros casos, los usuarios finales deben aplicar protección propia de la información desde sus aplicaciones, por ejemplo, mediante la selección de una etiqueta de clasificación configurada para aplicar una plantilla, la selección de una plantilla directamente o la selección de opciones específicas. Los usuarios aplican protección cuando quieren proteger un archivo para uso compartido y restringir su acceso o uso a determinados usuarios o a usuarios ajenos a la organización.

Las plantillas facilitan a los usuarios (y a los administradores que configuran las directivas) la aplicación del nivel de protección adecuado y restringen el acceso a personas de dentro de la organización. Aunque en el servicio Azure Rights Management se incluyen dos plantillas predeterminadas, es probable que quiera crear plantillas personalizadas para reducir las ocasiones en las que es necesario especificar opciones individuales. Para más información, vea [Configuración de plantillas personalizadas para el servicio Azure Rights Management](../deploy-use/configure-custom-templates.md).

Para los casos en que los usuarios deban aplicar ellos mismos la protección de información, asegúrate de proporcionarles las instrucciones y las directrices sobre cómo y cuándo deben hacerlo. Las instrucciones deberían ser específicas para la aplicación y las versiones que usan y sobre cómo usarlas, y las directrices sobre cuándo y cómo es apropiado para tu negocio aplicar la protección de información. Para más información, vea [Ayuda a los usuarios para proteger archivos mediante Azure Rights Management](../deploy-use/help-users.md).

Para obtener información sobre cómo configurar estas aplicaciones para el servicio Azure Rights Management de Azure Information Protection, vea [Configurar aplicaciones para Azure Rights Management](../deploy-use/configure-applications.md).

> [!TIP]
> Vea ejemplos y capturas de pantalla de aplicaciones que usan el servicio Azure Rights Management en [Azure RMS en acción: Qué ven los administradores y los usuarios](what-admins-users-see.md).

Los servicios de búsqueda se pueden integrar con Rights Management de maneras diferentes. Por ejemplo: 

- Exchange Online y Exchange Server usan la indexación del servicio para que los mensajes de correo electrónico protegidos por RMS de un usuario se muestren automáticamente en los resultados de búsqueda. 

- SharePoint Online y SharePoint Server aplican la protección de Rights Management a los archivos solo durante la descarga, lo que significa que la indexación y los resultados de la búsqueda en SharePoint no se verán afectados por esta solución de protección de documentos. Sin embargo, si tiene un documento que quiere guardar en SharePoint y no se debe devolver en los resultados de la búsqueda, proteja con RMS el archivo antes de cargarlo en SharePoint.

- La búsqueda de escritorio de Windows usa un índice compartido entre distintos usuarios del dispositivo, por lo que para proteger los datos de los documentos protegidos, no indexa los archivos protegidos por RMS. Esto significa que, aunque los resultados de la búsqueda no incluyen los archivos que ha protegido, puede estar seguro de que los archivos que contienen datos confidenciales no se mostrarán en los resultados de la búsqueda de otros usuarios que inicien sesión o se conecten a su equipo. 



## <a name="next-steps"></a>Pasos siguientes

Obtenga más información sobre la compatibilidad de los elementos siguientes con el servicio Azure Rights Management:

-   [Aplicación RMS sharing para Windows y plataformas móviles](sharing-app-support.md)

-   [Aplicaciones y servicios de Office](office-apps-services-support.md)

-   [Servidores de archivos que ejecutan Windows Server y usan Infraestructura de clasificación de archivos (FCI)](file-server-support.md)

-   [Otras aplicaciones compatibles con las API de RMS](api-support.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



<!--HONumber=Feb17_HO2-->


