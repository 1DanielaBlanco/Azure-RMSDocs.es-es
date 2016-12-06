---
title: "Guía del desarrollador | Azure RMS"
description: "Información general del uso de las herramientas para desarrolladores; SDK, bibliotecas adicionales y ejemplos de código."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 11/15/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a22e6bd0-8ce8-45b4-9a32-273126ab831e
audience: developer
ms.reviewer: kartikk
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 329dce4c8bb5a6de3ecb7bbd7e734b4acbf339c9
ms.openlocfilehash: bbf266512a80ece05253cbfab7b9ab40505f3f67


---

# <a name="developers-guide"></a>guía del desarrollador

## <a name="overview"></a>Información general ##
En esta guía se describe un conjunto cada vez mayor de herramientas y ejemplos de código que abarcan todas las plataformas soportadas, un conjunto de herramientas de administración de SDK de Rights Management y de PowerShell.

[**Herramientas y ejemplos de código**](#code-samples-and-tools): abarcan todos los sistemas operativos compatibles, Android, iOS/OS X, cliente Windows y teléfono.

[**Orientación de PowerShell**](#powershell-guidance): para las operaciones de protección masiva y de administración de Rights Management.

[**Kits de desarrollo de software**](#software-development-kits): proporcionan soporte para varios sistemas operativos de dispositivos móviles, incluidos Android e iOS, así como una amplia compatibilidad con el cliente Windows.


---

## <a name="code-samples-and-tools"></a>Ejemplos de código y herramientas

Esta colección de herramientas de soporte para desarrolladores y ejemplos de código de RMS suministrados por Microsoft abarca todos los sistemas operativos compatibles: Android, iOS/OS X, Windows Phone y escritorio de Windows y se actualiza periódicamente para mantener la compatibilidad con su correspondiente SDK.

### <a name="android"></a>Android

Ejecute lo siguiente en sistemas Android compatibles con el [SDK 4.2 de RMS](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) y versiones posteriores de los SDK 4.x.

- [Biblioteca de interfaz de usuario y aplicación de ejemplo](https://github.com/AzureAD/rms-sdk-ui-for-android) en GitHub, para que pueda empezar a trabajar rápidamente y volver a usar la interfaz de usuario estándar en sus aplicaciones.
- [Escenarios de uso de Android](https://msdn.microsoft.com/en-us/library/dn758246(v=vs.85).aspx) en Java, representan escenarios de desarrollo importantes para familiarizarse con el SDK de RMS. Entre los ejemplos se incluye el uso del formato de archivo protegido de Microsoft, formatos de archivos protegidos personalizados y controles de interfaz de usuario personalizados.

### <a name="ios-os-x"></a>iOS/OS X

Lo siguiente se ejecuta en sistemas iOS/OS X compatibles con el [SDK 4.2 de RMS](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) y versiones posteriores de los SDK 4.x.

- [Escenarios de uso de iOS/OS X](https://msdn.microsoft.com/en-us/library/dn758307(v=vs.85).aspx) en Objective C, representan escenarios de desarrollo importantes para familiarizarse con el SDK de RMS. Entre los ejemplos se incluye el uso del formato de archivo protegido de Microsoft, formatos de archivos protegidos personalizados y controles de interfaz de usuario personalizados.
- [Biblioteca de interfaz de usuario y aplicación de ejemplo](https://github.com/AzureAD/rms-sdk-ui-for-ios) en GitHub, para que pueda empezar a trabajar rápidamente y volver a usar la interfaz de usuario estándar en sus aplicaciones. Se admite **solo en iOS**.

### <a name="windows-desktop"></a>Escritorio de Windows

Lo siguiente se ejecuta en el escritorio de Windows compatible con el [SDK 2.1 de RMS](microsoft-information-protection-and-control-client-portal.md) y versiones posteriores del SDK 2.x.

- [PDF protegido con PFILE de lectura](https://blogs.msdn.microsoft.com/rms/2015/11/09/reading-a-pfile-protected-pdf/) es un ejemplo de código sencillo incluido en nuestro blog para desarrolladores de RMS que usa la API de archivo MSIPC para descifrar y abrir un documento PDF protegido con PFILE.
- [IpcManagedAPI](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/IpcManagedAPI) es una representación .NET (C#) del SDK 2.1 de RMS que permite habilitar con facilidad su aplicación administrada para RMS.
- [IPCNotepad](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/IpcNotepad) es un ejemplo de aplicación habilitada para RMS que le guiará por los pasos básicos que deben realizar este tipo de aplicaciones al proteger y consumir contenido restringido.
- [IpcDlp](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/IpcDlpApp) es un ejemplo de aplicación de protección de pérdida de datos (DLP) habilitada para RMS que le guiará por los pasos básicos que deben realizar este tipo de aplicaciones mediante la API de archivo para proteger y consumir contenido restringido.
- [IpcAzureApp](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/IpcAzureApp) es un ejemplo que muestra cómo utilizar el SDK de RMS en la aplicación de Azure para proteger los datos en el Almacenamiento de blobs de Azure.
- [RmsDocumentInspector](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/RmsDocumentInspector) es una herramienta que puede proporcionar información sobre cualquier archivo protegido por RMS, como los derechos de usuario o el identificador de contenido.
- [RmsFileWatcher](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/RmsFileWatcher) es un ejemplo que muestra cómo compilar una aplicación de Windows que inspecciona directorios del sistema de archivos y aplica directivas de protección de RMS en cada cambio, por ejemplo, cuando se agrega o modifica un archivo.

### <a name="windows-store-and-phone"></a>Tienda Windows y Windows Phone

- [Biblioteca de interfaz de usuario para la Tienda Windows](https://github.com/AzureAD/rms-sdk-ui-for-windowsstore): una biblioteca de interfaz de usuario para el SDK v4.1 de Microsoft RMS destinada a aplicaciones de la Tienda Windows. Esta biblioteca es opcional y los desarrolladores pueden optar por crear su propia interfaz de usuario mediante el SDK v4.1 de Microsoft RMS.

- [Biblioteca de interfaz de usuario para Windows Phone](https://github.com/AzureAD/rms-sdk-ui-for-winphone): una biblioteca de interfaz de usuario para el SDK v4.1 de Microsoft RMS destinada a aplicaciones de Windows Phone. Esta biblioteca es opcional y los desarrolladores pueden optar por crear su propia interfaz de usuario mediante el SDK v4.1 de Microsoft RMS.

- [Aplicación de ejemplo](https://github.com/Azure-Samples/active-directory-dotnet-rms-windowsstore): el ejemplo del SDK v4.1 de Microsoft RMS para aplicaciones de la Tienda Windows proporciona un ejemplo básico de consumo de documentos para la plataforma.

---

## <a name="powershell-guidance"></a>Guía de PowerShell
Contamos con cmdlets de PowerShell para las operaciones de protección masiva y de administración de Rights Management.

[Los cmdlets de Azure Rights Management](https://msdn.microsoft.com/library/azure/dn629398.aspx) le permiten administrar Azure RMS desde la línea de comandos. Aunque esto le permite automatizar, también ofrece procesos fiables y repetidos para ayudar a reducir las sobrecargas administrativas. Además, algunas configuraciones y operaciones avanzadas de Azure RMS requieren Azure PowerShell.

[Los cmdlets de protección de RMS](https://msdn.microsoft.com/library/azure/mt433195.aspx) se pueden usar con la protección de datos de Azure Rights Management (Azure RMS) que proporciona Azure Information Protection, o con Active Directory Rights Management Services (AD RMS), y complementar otros módulos de PowerShell para estas implementaciones de Rights Management. Puede usar estos cmdlets de protección de RMS para proteger y desproteger en masa archivos de cualquier tipo.

---

## <a name="software-development-kits"></a>Kits de desarrollo de software


Las tres generaciones de RMS SDK que están disponibles se describen en la tabla siguiente.

| SDK | Descripción |
|------|---------|
| [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) | Conjunto de herramientas simplificado de próxima generación que proporciona una experiencia de desarrollo ligera que permite que sus aplicaciones de dispositivos Android, iOS, Mac OS X, Windows Phone/RT y Linux/C++ reciban protección de la información mediante Microsoft Rights Management. |
| [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) | Una oferta de SDK eficaz para los desarrolladores de aplicaciones de escritorio de Windows y proveedores de soluciones basadas en servidor que permite que sus productos tengan administración de derechos.|
|[AD RMS SDK](https://msdn.microsoft.com/library/cc530379.aspx)|** NOTA **: La funcionalidad de aprovechamiento de AD RMS SDK expuesta por el cliente en Msdrm.dll está disponible para su uso en Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7, Windows Server 2008 y Windows Vista. En versiones posteriores podría modificarse o no estar disponible. En su lugar, use Microsoft Rights Management Services SDK 2.1, que aprovecha la funcionalidad expuesta por el cliente en Msipc.dll.|
|[API de script de AD RMS](https://msdn.microsoft.com/en-us/library/bb968797.aspx)| Se usa para crear scripts para administrar una instalación de AD RMS.|



<!--HONumber=Nov16_HO3-->


