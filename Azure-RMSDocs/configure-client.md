---
title: 'Cliente de Azure Information Protection: instalación y configuración'
description: Información para administradores sobre la implementación del cliente de Azure Information Protection en dispositivos móviles y equipos con Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/05/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b1a19ae7-db26-40da-9e21-6620af3d0b02
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 79d4dbb1d6339f0261d57b32cf77addee9ca9744
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56258933"
---
# <a name="azure-information-protection-client-installation-and-configuration-for-clients"></a>Cliente de Azure Information Protection: Instalación y configuración para clientes

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Los equipos que ejecutan Office 2010 requieren el cliente de Azure Information Protection para autenticarse en el servicio Azure Rights Management y en el servicio Azure Information Protection. Este cliente también se recomienda para todos los equipos con Windows y dispositivos iOS y Android que admiten el servicio Azure Rights Management y Azure Information Protection. 

El cliente de Azure Information Protection se integra con aplicaciones de Office mediante la instalación de un complemento de Office para que los usuarios puedan etiquetar y proteger fácilmente documentos y correos electrónicos directamente desde la cinta de opciones de Office. Este cliente también ofrece etiquetado y protección para tipos de archivo que no son compatibles de forma nativa con el servicio Azure Rights Management, un visor de archivos protegidos y un sitio de seguimiento de documentos para que los usuarios controlen y revoquen los archivos que hayan protegido.

## <a name="the-azure-information-protection-client-for-windows-installation-and-configuration"></a>El cliente de Azure Information Protection para Windows: Instalación y configuración

Para una instalación empresarial y la configuración del cliente para Windows, vea [Azure Information Protection administrator guide](./rms-client/client-admin-guide.md) (Guía para administradores de Azure Information Protection).

> [!TIP]
> Si desea instalar y probar rápidamente el cliente de Azure Information Protection en un solo equipo, vea [Descarga e instalación del cliente de Azure Information Protection](./rms-client/install-client-app.md) de la [Guía del usuario de Azure Information Protection](./rms-client/client-user-guide.md).

## <a name="the-azure-information-protection-client-for-ios-and-android-installation-and-management"></a>El cliente de Azure Information Protection para iOS y Android: Instalación y administración

Para instalar el cliente de Azure Information Protection en estas plataformas móviles populares, puede descargar la aplicación correspondiente con los vínculos de la [página de Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970). No es necesario realizar ninguna configuración.

> [!NOTE]
> Para equipos Mac, los vínculos de esta página descargan la aplicación RMS sharing. Estos equipos no admiten el cliente de Azure Information Protection.

### <a name="integration-with-intune"></a>Integración con Intune

Como la aplicación Azure Information Protection usa el kit de desarrollo de software de aplicaciones de Microsoft Intune, cuando los dispositivos iOS y Android están inscritos mediante Intune, puede implementar y administrar la aplicación Azure Information Protection para estos dispositivos:

1. [Adición de la aplicación Azure Information Protection a Intune](/intune/apps-add) 

2. Realice una de las acciones siguientes o ambas:
    
    - Implementar la aplicación [asignándola a los usuarios](/intune/apps-deploy)
    
    - Administrar la aplicación mediante el uso de [directivas de protección de aplicaciones](/intune/app-protection-policies)

Información adicional para cuando agregue la aplicación Azure Information Protection a Intune:

- Para iOS: busque y agregue la aplicación de Intune.

- Para Android: al agregar la aplicación, use la siguiente **dirección URL de Appstore**:
        
        https://play.google.com/store/apps/details?id=com.microsoft.ipviewer

Después de configurar la aplicación de Azure Information Protection para una directiva de protección de aplicación para dispositivos Android, además de abrir texto, imágenes y documentos PDF protegidos, esta aplicación también podrá abrir archivos de audio y vídeo. Para obtener más información, vea [Visualización de archivos multimedia con la aplicación de Azure Information Protection](/intune/end-user-mam-apps-android#view-media-files-with-the-azure-information-protection-app).

## <a name="next-steps"></a>Pasos siguientes

Una vez que haya instalado y configurado el cliente de Azure Information Protection, necesita obtener más información sobre cómo el cliente interpreta los distintos derechos de uso que pueden usarse para proteger documentos y correos electrónicos. Para más información, consulte [Configuración de los derechos de uso para Azure Rights Management](configure-usage-rights.md).
