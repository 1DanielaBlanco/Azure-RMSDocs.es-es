---
# required metadata

title: ¿Cómo admiten las aplicaciones Azure Rights Management? | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ¿Cómo admiten las aplicaciones Azure Rights Management?
Use la información siguiente para tratar de comprender cómo la mayoría de las aplicaciones de usuario final usadas habitualmente (como las aplicaciones de Office, Word, Excel, PowerPoint y Outlook) y los servicios (como Exchange y SharePoint) pueden utilizar Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] con la idea de proteger los datos de su organización. 
> [!NOTE]
> Para comprobar las aplicaciones y versiones que son compatibles con [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS), consulte [Requisitos de Azure Rights Management](../get-started/requirements-azure-rms.md).

En algunos casos, la protección de la información se aplica de manera automática, según lo previsto en las directivas que tú mismo configuras. Por ejemplo, este es el caso con bibliotecas de SharePoint, archivos clasificados y reglas de transporte de Exchange. En otros casos, los usuarios deben aplicar ellos mismos la protección de la información desde sus aplicaciones, ya sea seleccionando una plantilla o unas opciones específicas. Por ejemplo, este es el caso cuando los usuarios comparten un archivo por correo electrónico, o protegen un archivo in situ restringiendo el acceso o el uso a usuarios seleccionados o a usuarios externos a la organización.

Las plantillas facilitan a los usuarios (y a los administradores que configuran las directivas) la aplicación del nivel de protección adecuado y restringen el acceso a personas de dentro de la organización. Aunque [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] se presenta con dos plantillas predeterminadas, probablemente querrás crear plantillas personalizadas a fin de reducir las veces en que se tienen que especificar opciones individuales. Para más información, consulte [Configuración de plantillas personalizadas para Azure Rights Management](../deploy-use/configure-custom-templates.md).

Para los casos en que los usuarios deban aplicar ellos mismos la protección de información, asegúrate de proporcionarles las instrucciones y las directrices sobre cómo y cuándo deben hacerlo. Las instrucciones deberían ser específicas para la aplicación y las versiones que usan y sobre cómo usarlas, y las directrices sobre cuándo y cómo es apropiado para tu negocio aplicar la protección de información. Para más información, consulte [Ayuda a los usuarios para proteger archivos mediante Azure Rights Management](../deploy-use/help-users.md).

Para obtener información sobre cómo configurar estas aplicaciones para Azure RMS, consulte [Configuración de aplicaciones para Azure Rights Management](../deploy-use/configure-applications.md).

> [!TIP]
> Para obtener ejemplos y capturas de pantalla de aplicaciones con Azure RMS, consulte [Azure RMS en acción: Qué ven los administradores y los usuarios](what-admins-users-see.md).


## Pasos siguientes

Obtenga más información sobre cómo admiten RMS cada uno de los siguientes elementos:

-   [Aplicación de uso compartido RMS para Windows y plataformas móviles](sharing-app-support.md)

-   [Aplicaciones y servicios de Office](office-apps-services-support.md)

-   [Servidores de archivos que ejecutan Windows Server y usan Infraestructura de clasificación de archivos (FCI)](file-server-support.md)

-   [Otras aplicaciones compatibles con las API de RMS](api-support.md)



<!--HONumber=Apr16_HO4-->


