---
title: Aplicación RMS sharing para Windows y plataformas móviles - AIP
description: Cómo la aplicación RMS sharing admite Azure RMS como una aplicación gratuita y descargable que es necesaria para ofrecer compatibilidad con Office 2010, pero también se recomienda para equipos con Windows, equipos con Mac y dispositivos móviles.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 16/01/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1da6e372-2b3f-4af7-80f7-6b9073dff7f5
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 2ffe55eeecaea82929a6439cfcf5695e4c93424e
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39371805"
---
# <a name="rms-sharing-application-for-windows-and-mobile-platforms"></a>Aplicación de uso compartido RMS para Windows y plataformas móviles

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!IMPORTANT]
> **Finalización de notificación de compatibilidad**: la aplicación Rights Management sharing para Windows se va a sustituir por el [cliente de Azure Information Protection](../rms-client/aip-client.md). La aplicación anterior dejará de ser compatible el 31 de enero de 2019. 
 
La aplicación RMS sharing es una aplicación descargable que admite Office 2010 para equipos con Windows y que suele recomendarse para todos los dispositivos móviles y equipos con Windows. Todavía se recomienda para equipos Mac y dispositivos con Windows Phone. Una de sus ventajas es que puede aplicar protección genérica en aplicaciones y archivos que de forma nativa no son compatibles con el servicio Azure Rights Management, lo que significa que se pueden proteger todos los archivos. Para más información sobre los distintos niveles de protección, consulte la sección [Niveles de protección: nativa y genérica](../rms-client/sharing-app-admin-guide-technical.md#levels-of-protection--native-and-generic) en la [Guía del administrador de la aplicación Microsoft Rights Management sharing](../rms-client/sharing-app-admin-guide.md).

Cuando los usuarios protegen sus archivos mediante la aplicación de uso compartido de RMS, también pueden realizar el seguimiento de los documentos que han protegido y, si es necesario, revocar el acceso a ellos. Para ello, pueden utilizar el [sitio de seguimiento de documentos](http://go.microsoft.com/fwlink/?LinkId=529562).

Para ordenadores con Windows, la aplicación de uso compartido RMS se integra de forma discreta con las aplicaciones que los usuarios ya usan y las mejora:

-   Se instala un completo de Office para Word, Excel, PowerPoint y Outlook. De este modo, los usuarios disponen del botón **Uso compartido seguro** en la cinta de opciones, que abre un sencillo cuadro de diálogo de configuración que se usa normalmente para proteger archivos que se enviarán por correo electrónico. Este botón también proporciona una forma rápida de obtener acceso al sitio de seguimiento de documentos.

-   Una nueva opción con un clic en el botón secundario para el Explorador de archivos. De este modo, los usuarios disponen de la opción **Proteger en contexto**, que abre un sencillo cuadro de diálogo de configuración que se usa normalmente para proteger archivos almacenados en un disco.

-   Un visor para abrir archivos protegidos por el servicio Azure Rights Management. Este visor se invoca automáticamente cuando no hay otra aplicación instalada que pueda abrir el archivo protegido.

-   Configuración de back-end para Office 2010, lo que permite que las correspondientes versiones de Word, Excel, PowerPoint y Outlook funcionen perfectamente con el servicio Azure Rights Management.

Aunque la aplicación para uso compartido de RMS para Windows puede descargarse e instalarse en un solo equipo desde la [página de Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970), también admite una implementación empresarial para la instalación silenciosa y la configuración personalizada. Para obtener más información, vea los recursos siguientes:

-   [Guía del administrador de la aplicación Rights Management sharing](../rms-client/sharing-app-admin-guide.md)

-   [Guía de usuario de la aplicación Rights Management sharing](../rms-client/sharing-app-user-guide.md)

La aplicación de uso compartido RMS para dispositivos móviles admite los dispositivos móviles más usados, como iPad e iPhone, Android, Windows Phone y Windows RT. Los usuarios pueden descargar esta aplicación desde la tienda pertinente, y se pueden encontrar enlaces a estas desde la [página de Rights Management de Microsoft](http://go.microsoft.com/fwlink/?LinkId=303970).

**Si tiene Microsoft Intune**: Dado que la aplicación RMS sharing incluye el Kit de desarrollo de software para aplicaciones de Microsoft Intune, puede utilizar las siguientes opciones:

-   Implemente y administre la aplicación para dispositivos iOS y Android inscritos por Intune.

-   Implemente y administre la aplicación para dispositivos iOS y Android no inscritos por Intune.


## <a name="next-steps"></a>Pasos siguientes
Para conocer otras aplicaciones y servicios compatibles con el servicio Azure Rights Management de Azure Information Protection, vea [Compatibilidad de aplicaciones con el servicio Azure Rights Management](applications-support.md).

