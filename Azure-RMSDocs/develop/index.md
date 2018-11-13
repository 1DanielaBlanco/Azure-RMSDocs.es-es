---
title: Guía del desarrollador de RMS | Azure RMS
description: Hay tres generaciones de Rights Management SDK.
keywords: ''
author: bryanla
manager: mbaldwin
ms.date: 09/07/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 0510ead4-2fe7-4269-885b-fe16bcc69888
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 6f964c6a6cf36cbd6f78cf58096f8c912fb0ff68
ms.sourcegitcommit: 26a2c1becdf3e3145dc1168f5ea8492f2e1ff2f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2018
ms.locfileid: "51527935"
---
# <a name="rms-developers-guide"></a>Guía del desarrollador de RMS

## <a name="overview"></a>Introducción ##
Actualmente hay disponibles tres generaciones del SDK de Rights Management: **SDK 4.2 de Microsoft Rights Management** para Android, iOS/OS X, dispositivos Windows y Linux, **SDK 2.1 de Microsoft Rights Management** para Windows Desktop Client y el ya reemplazado **SDK de AD RMS**.

## <a name="software-development-kits"></a>Kits de desarrollo de software ##
| SDK | Descripción |
|------|---------|
| [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) | Conjunto de herramientas simplificado de próxima generación que proporciona una experiencia de desarrollo ligera que permite que sus aplicaciones de dispositivos Android, iOS, Mac OS X, Windows Phone/RT y Linux/C++ reciban protección de la información mediante Microsoft Rights Management. |
| [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) | Una oferta de SDK eficaz para los desarrolladores de aplicaciones de escritorio de Windows y proveedores de soluciones basadas en servidor que permite que sus productos tengan administración de derechos.|
|[AD RMS SDK]()|** Nota **: La funcionalidad de aprovechamiento de AD RMS SDK expuesta por el cliente en Msdrm.dll está disponible para su uso en Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7, Windows Server 2008 y Windows Vista. En versiones posteriores podría modificarse o no estar disponible. En su lugar, use Microsoft Rights Management Services SDK 2.1, que aprovecha la funcionalidad expuesta por el cliente en Msipc.dll.|
|[API de script de AD RMS]()| Se usa para crear scripts para administrar una instalación de AD RMS.|

## <a name="code-samples-and-tools"></a>Ejemplos de código y herramientas ##
Esta colección de herramientas de soporte para desarrolladores y de ejemplos de código RMS suministrados por Microsoft abarca todos los sistemas operativos compatible: Android, iOS/OS X, Windows Phone y escritorio de Windows. Se actualiza periódicamente para mantener compatibilidad con su correspondiente SDK.

| Elemento | Sistema operativo | Versión de SDK compatible | Descripción |
|------|------------------|------------------------|-------------|
| [Read PFILE protected PDF](https://blogs.msdn.microsoft.com/rms/2015/11/09/reading-a-pfile-protected-pdf/) | Escritorio de Windows| [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) y versiones posteriores de los SDK 2.x | **PDF protegido con PFILE de lectura** es un ejemplo de código sencillo incluido en nuestro blog para desarrolladores de RMS que usa la API de archivo MSIPC para descifrar y abrir un documento PDF protegido con PFILE.|
| [IpcManagedAPI](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Escritorio de Windows | [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) y versiones posteriores de los SDK 2.x | **IpcManagedAPI** es una representación .NET (C#) del SDK 2.1 de RMS que permite habilitar con facilidad su aplicación administrada para RMS.|
| [IPCNotepad](https://code.msdn.microsoft.com/ipcnotepad-sample-f67dae80) | Escritorio de Windows | [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) y versiones posteriores de los SDK 2.x| **IPCNotepad** es un ejemplo de aplicación habilitada para RMS que le guiará por los pasos básicos que deben realizar este tipo de aplicaciones al proteger y consumir contenido restringido.|
| [IpcDlp](https://github.com/Azure-Samples/active-directory-dotnet-rms)|Escritorio de Windows|[RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) y versiones posteriores de los SDK 2.x|**IpcDlp** es un ejemplo de aplicación de protección de pérdida de datos (DLP) habilitada para RMS que le guiará por los pasos básicos que deben realizar este tipo de aplicaciones mediante la API de archivo para proteger y consumir contenido restringido.|
| [IpcAzureApp](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Escritorio de Windows|[RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) y versiones posteriores de los SDK 2.x|**IpcAzureApp** es un ejemplo que muestra cómo utilizar el SDK de RMS en la aplicación de Azure para proteger los datos en el Almacenamiento de blobs de Azure.|
| [RmsDocumentInspector](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Escritorio de Windows|[RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) y versiones posteriores de los SDK 2.x|**RmsDocumentInspector** es una herramienta que puede proporcionar información sobre cualquier archivo protegido por RMS, como los derechos de usuario o el identificador de contenido.|
| [RmsFileWatcher](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Escritorio de Windows|[RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) y versiones posteriores de los SDK 2.x|**RmsFileWatcher** es un ejemplo que muestra cómo compilar una aplicación de Windows que inspecciona directorios del sistema de archivos y aplica directivas de protección de RMS en cada cambio, por ejemplo, cuando se agrega o modifica un archivo.|
| [Escenarios de uso iOS/OS X](https://msdn.microsoft.com/library/dn758307(v=vs.85).aspx) |iOS/OS X|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) y versiones posteriores de los SDK 4.x|**Ejemplos de código Objective C** que representan escenarios de desarrollo importante para irse habituando a RMS SDK. Entre los ejemplos se incluye el uso del formato de archivo protegido de Microsoft, formatos de archivos protegidos personalizados y controles de interfaz de usuario personalizados.|
| [Aplicación de ejemplo y la biblioteca de interfaz de usuario](https://github.com/AzureAD/rms-sdk-ui-for-ios) |iOS|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) y versiones posteriores de los SDK 4.x|**Bibliotecas de interfaz de usuario y aplicaciones de ejemplo para iOS** en GitHub, para que pueda empezar a trabajar rápidamente y volver a usar la interfaz de usuario estándar en sus aplicaciones.|
| [Aplicación de ejemplo y la biblioteca de interfaz de usuario](https://github.com/AzureAD/rms-sdk-ui-for-android) |Android|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) y versiones posteriores de los SDK 4.x|**Bibliotecas de interfaz de usuario y aplicaciones de ejemplo para Android** en GitHub, para que pueda empezar a trabajar rápidamente y volver a usar la interfaz de usuario estándar en sus aplicaciones.|
| [Escenarios de uso de Android](https://msdn.microsoft.com/en-us/library/dn758246(v=vs.85).aspx) |Android|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) y versiones posteriores de los SDK 4.x|**Ejemplos de código Java** que representan escenarios de desarrollo importante para irse habituando a RMS SDK. Entre los ejemplos se incluye el uso del formato de archivo protegido de Microsoft, formatos de archivos protegidos personalizados y controles de interfaz de usuario personalizados.|