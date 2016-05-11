---
# required metadata

title: Guía del desarrollador de RMS | Azure RMS
description: Hay tres generaciones de Rights Management SDK.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0510ead4-2fe7-4269-885b-fe16bcc69888

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Guía del desarrollador de RMS

## Información general ##
Actualmente hay disponibles tres generaciones del SDK de Rights Management: **Microsoft Rights Management SDK 4.2** para Android, iOS/OS X, dispositivos Windows y Linux, **Microsoft Rights Management SDK 2.1** para Windows Desktop Client y el ya reemplazado **AD RMS SDK**.

## Kits de desarrollo de software ##
| SDK | Descripción |
|------|---------|
| [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) | Conjunto de herramientas simplificadas y de próxima generación que proporciona una experiencia de desarrollo ligero para habilitar aplicaciones de dispositivos Android, iOS, Mac OS X, Windows Phone/RT y Linux/C++ con protección de la información a través de servicios de Microsoft Rights Management. |
| [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) | Una oferta de SDK eficaz para los desarrolladores de aplicaciones de escritorio de Windows y proveedores de soluciones basadas en servidor para habilitar sus productos administración de derechos.|
|[SDK de AD RMS]()|** Nota **: La funcionalidad de aprovechamiento de AD RMS SDK expuesta por el cliente en Msdrm.dll está disponible para su uso en Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7, Windows Server 2008 y Windows Vista. En versiones posteriores podría modificarse o no estar disponible. En su lugar, use Microsoft Rights Management Services SDK 2.1, que aprovecha la funcionalidad expuesta por el cliente en Msipc.dll.|
|[AD RMS Scripting API]()| Se usa para crear scripts para administrar una instalación de AD RMS.|

## Ejemplos de código y herramientas ##
Esta colección de herramientas de soporte para desarrolladores y de ejemplos de código RMS suministrados por Microsoft abarca todos los sistemas operativos compatible: Android, iOS/OS X, Windows Phone y escritorio de Windows. Se actualiza periódicamente para mantener compatibilidad con su correspondiente SDK.

| Elemento | Sistema operativo | Versión de SDK compatible | Descripción |
|------|------------------|------------------------|-------------|
| [Read PFILE protected PDF](https://blogs.msdn.microsoft.com/rms/2015/11/09/reading-a-pfile-protected-pdf/) | Escritorio de Windows| [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) y versiones posteriores de los SDK 2.x | **Read PFILE protected PDF** (Leer un PDF protegido por PFILE) es un ejemplo de código sencillo incluido en nuestro blog para desarrolladores de RMS que usa la API de archivo MSIPC para descifrar y abrir un documento PDF protegido por PFILE.|
| [IpcManagedAPI](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Escritorio de Windows | [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) y versiones posteriores de los SDK 2.x | **IpcManagedAPI** es una representación .NET (C#) de RMS SDK 2.1 que facilita que su aplicación administrada pueda habilitarse para RMS.|
| [IPCNotepad](https://code.msdn.microsoft.com/ipcnotepad-sample-f67dae80) | Escritorio de Windows | [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) y versiones posteriores de los SDK 2.x| **IPCNotepad** es un ejemplo de aplicación habilitada para RMS que le guiará por los pasos básicos que deben realizar este tipo de aplicaciones al proteger y consumir contenido restringido.|
| [IpcDlp](https://github.com/Azure-Samples/active-directory-dotnet-rms)|Escritorio de Windows|[RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) y versiones posteriores de los SDK 2.x|**IpcDlp** es un ejemplo de aplicación de protección de pérdida de datos (DLP) habilitada para RMS que le guiará por los pasos básicos que deben realizar este tipo de aplicaciones mediante la API de archivo para proteger y consumir contenido restringido.|
| [IpcAzureApp](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Escritorio de Windows|[RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) y versiones posteriores de los SDK 2.x|**IpcAzureApp** es un ejemplo que muestra cómo usar RMS SDK en la aplicación de Azure para proteger los datos en el almacenamiento de blobs de Azure.|
| [RmsDocumentInspector](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Escritorio de Windows|[RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) y versiones posteriores de los SDK 2.x|**RmsDocumentInspector** es una herramienta que puede proporcionar información sobre cualquier archivo protegido por RMS, como los derechos de usuario o el identificador de contenido.|
| [RmsFileWatcher](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Escritorio de Windows|[RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) y versiones posteriores de los SDK 2.x|**RmsFileWatcher** es un ejemplo que muestra cómo compilar una aplicación de Windows que inspecciona los directorios del sistema de archivos y aplica las directivas de protección de RMS en cada cambio, por ejemplo, cuando se agrega o se modifica un archivo.|
| [Escenarios de uso iOS/OS X](https://msdn.microsoft.com/en-us/library/dn758307(v=vs.85).aspx) |iOS / OS X|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) y versiones posteriores de los SDK 4.x|**Ejemplos de código Objective C** que representan escenarios de desarrollo importante para irse habituando a RMS SDK. Entre los ejemplos se incluye el uso del formato de archivo protegido de Microsoft, formatos de archivos protegidos personalizados y controles de interfaz de usuario personalizados.|
| [Aplicación de ejemplo y la biblioteca de interfaz de usuario](https://github.com/AzureAD/rms-sdk-ui-for-ios) |iOS|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) y versiones posteriores de los SDK 4.x|**Bibliotecas de interfaz de usuario y aplicaciones de ejemplo para iOS** en GitHub, para que pueda empezar a trabajar rápidamente y volver a usar la interfaz de usuario estándar en sus aplicaciones.|
| [Aplicación de ejemplo y la biblioteca de interfaz de usuario](https://github.com/AzureAD/rms-sdk-ui-for-android) |Android|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) y versiones posteriores de los SDK 4.x|**Bibliotecas de interfaz de usuario y aplicaciones de ejemplo para Android** en GitHub, para que pueda empezar a trabajar rápidamente y volver a usar la interfaz de usuario estándar en sus aplicaciones.|
| [Escenarios de uso de Android](https://msdn.microsoft.com/en-us/library/dn758246(v=vs.85).aspx) |Android|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) y versiones posteriores de los SDK 4.x|**Ejemplos de código Java** que representan escenarios de desarrollo importante para irse habituando a RMS SDK. Entre los ejemplos se incluye el uso del formato de archivo protegido de Microsoft, formatos de archivos protegidos personalizados y controles de interfaz de usuario personalizados.|


<!--HONumber=Apr16_HO3-->


