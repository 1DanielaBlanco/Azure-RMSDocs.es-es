---
# required metadata

title: Aplicación RMS sharing para plataformas Windows y móviles | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1da6e372-2b3f-4af7-80f7-6b9073dff7f5

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Aplicación de uso compartido RMS para Windows y plataformas móviles

*Se aplica a: Azure Rights Management, Office 365*

La aplicación de uso compartido RMS es una aplicación gratuita y descargable que es necesaria para admitir Office 2010, pero también se recomienda para equipos con Windows, equipos con Mac y dispositivos móviles. Una de sus ventajas es que puede aplicar protección genérica para aplicaciones y archivos que no son admiten de forma nativa [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], lo que significa que se pueden proteger todos los archivos. Para obtener más información sobre los distintos niveles de protección, consulte la sección [Level of protection – native and generic](../rms-client/sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic) (Niveles de protección: nativo y genérico) en la [Rights Management sharing application administrator guide](../rms-client/sharing-app-admin-guide.md) (Guía de administrador de la aplicación Rights Management sharing)..

Cuando los usuarios protegen sus archivos mediante la aplicación de uso compartido de RMS, también pueden realizar el seguimiento de los documentos que han protegido y, si es necesario, revocar el acceso a ellos. Para ello, pueden usar el [sitio de seguimiento de documentos](http://go.microsoft.com/fwlink/?LinkId=529562)..

Para ordenadores con Windows, la aplicación de uso compartido RMS se integra de forma discreta con las aplicaciones que los usuarios ya usan y las mejora:

-   Se instala un completo de Office para Word, Excel, PowerPoint y Outlook. De este modo, los usuarios disponen del botón **Uso compartido seguro** en la cinta de opciones, que abre un sencillo cuadro de diálogo de configuración que se usa normalmente para proteger archivos que se enviarán por correo electrónico. Este botón también proporciona una forma rápida de obtener acceso al sitio de seguimiento de documentos.

-   Una nueva opción con un clic en el botón secundario para el Explorador de archivos. De este modo, los usuarios disponen de la opción **Proteger en contexto**, que abre un sencillo cuadro de diálogo de configuración que se usa normalmente para proteger archivos almacenados en un disco.

-   Un visor para abrir archivos que se hayan protegido mediante [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]. Este visor de invoca automáticamente cuando no hay otra aplicación instalada que pueda abrir el archivo protegido.

-   Configuración de back-end para Office 2010 que permite que Word, Excel, PowerPoint y Outlook funcionen sin problemas con [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

Aunque la aplicación para uso compartido de RMS para Windows puede descargarse e instalarse en un solo equipo desde la [página de Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970), también admite una implementación empresarial para la instalación silenciosa y la configuración personalizada. Para obtener más información, vea los recursos siguientes:

-   [Guía del administrador de la aplicación de uso compartido de Rights Management](../rms-client/sharing-app-admin-guide.md)

-   [Guía de usuario de la aplicación de uso compartido Rights Management](../rms-client/sharing-app-user-guide.md)

La aplicación de uso compartido RMS para dispositivos móviles admite los dispositivos móviles más usados, como iPad e iPhone, Android, Windows Phone y Windows RT. Los usuarios pueden descargar esta aplicación desde la tienda pertinente, y se pueden encontrar enlaces a estas desde la [página de Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970)..

**Si tiene Microsoft Intune**: Dado que la aplicación RMS sharing incluye el Kit de desarrollo de software para aplicaciones de Microsoft Intune, puede utilizar las siguientes opciones:

-   Implemente y administre la aplicación para dispositivos iOS y Android inscritos por Intune.

-   Implemente y administre la aplicación para dispositivos iOS y Android no inscritos por Intune.


## Pasos siguientes
Para ver la compatibilidad de otras aplicaciones y servicios con Azure Rights Management, consulte [How applications support Azure Rights Management](applications-support.md) (Compatibilidad de las aplicaciones con Azure Rights Management)..



<!--HONumber=Apr16_HO4-->


