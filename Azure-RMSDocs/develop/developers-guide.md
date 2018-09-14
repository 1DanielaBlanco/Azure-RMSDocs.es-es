---
title: Guía del desarrollador de Azure Information Protection
description: Los desarrolladores pueden usar Azure Information Protection para proteger y administrar todo tipo de archivos
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 10/11/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: a53c2df2-a0a2-4f1f-995b-75ba55e4489b
ms.suite: ems
ms.reviewer: kartikk
ms.openlocfilehash: 21564a219a05efb0d47a12755d4334cc9ac2a559
ms.sourcegitcommit: 26a2c1becdf3e3145dc1168f5ea8492f2e1ff2f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2018
ms.locfileid: "44150354"
---
# <a name="azure-information-protection-developers-guide"></a>Guía del desarrollador de Azure Information Protection

Esta guía le orienta sobre las herramientas para ampliar el servicio de administración de derechos de Information Protection e realizar la integración con él.

>El SDK de Azure Information Protection actual tiene el componente de administración de derechos. Un componente de clasificación y etiquetado está en desarrollo.

## <a name="service-applications"></a>Aplicaciones de servicio

Las aplicaciones de servicio proporcionan funcionalidades para proteger la información que se exporta desde el sistema de administración de contenido empresarial, una aplicación de negocios o una solución empresarial basada en la nube. Prevención de pérdida de datos (DLP) y Cloud Application Security (CAS) son ejemplos de aplicaciones de servicio. Nuestro SDK para el desarrollo de aplicaciones de servicio está disponible mediante dos modelos de programación.

- [C++](https://www.microsoft.com/download/details.aspx?id=38397)
- [API administrada en C#](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/IpcManagedAPI)

### <a name="examples-of-service-applications"></a>Ejemplos de aplicaciones de servicio

- [IpcDlp](https://github.com/Azure-Samples/active-directory-dotnet-rms) es un ejemplo de aplicación DLP habilitada para RMS que le guía por los pasos básicos que deben realizar este tipo de aplicaciones mediante la API de archivo de RMS para proteger y consumir contenido restringido.
- [IpcAzureApp](https://github.com/Azure-Samples/active-directory-dotnet-rms) es un ejemplo que muestra cómo usar el SDK de RMS en aplicaciones de Azure para proteger los datos en una instancia de Azure Blob Storage.
- [RmsFileWatcher](https://github.com/Azure-Samples/active-directory-dotnet-rms) es un ejemplo que muestra cómo compilar una aplicación de Windows que inspecciona directorios del sistema de archivos y aplica directivas de protección de RMS en cada cambio, por ejemplo, cuando se agrega o modifica un archivo.
- [ProtectFilesInDir](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/ProtectFilesInDir) es un ejemplo de aplicación de consola simple que toma un directorio como entrada y protege todos los archivos de ese directorio únicamente, sin recursión.

## <a name="powershell-guides"></a>Guías de PowerShell

Los cdmlets de PowerShell, utilizados por los administradores de Azure Rights Management, también son útiles para desarrollar y probar las aplicaciones de servicio. Para más información, vea [Uso de PowerShell con el cliente de Azure Information Protection](/azure/information-protection/rms-client/client-admin-guide-powershell).

## <a name="user-applications"></a>Aplicaciones de usuario

Se pueden crear aplicaciones de usuario con el SDK 2.1 o 4.2 de RMS.
La versión 4.2 es un cliente de REST basado en API específicas del sistema operativo para varias plataformas conocidas: iOS/OSX, Android, Linux, Windows. La versión 2.1 se usa para crear aplicaciones Windows nativas.

### <a name="user-application-development-guides"></a>Guías de desarrollo de aplicaciones de usuario

- [Desarrollo de la aplicación](developing-your-application.md)
- [Prueba de la aplicación](how-to-set-up-your-test-environment.md)
- [Implementación de una aplicación](deploying-your-application.md)

### <a name="user-application-samples"></a>Ejemplos de aplicaciones de usuario

- [AzureIP Test](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/AzureIP_Test) es un ejemplo de aplicación de consola que le permite cifrar documentos con una directiva ad-hoc o una plantilla de Azure.
- [IPCNotepad](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/AzureIP_Test) es un ejemplo de aplicación habilitada para RMS que le guía por los pasos básicos que debe realizar este tipo de aplicaciones al proteger y consumir contenido restringido.
- [RmsDocumentInspector](https://github.com/Azure-Samples/active-directory-dotnet-rms) es una herramienta que puede proporcionar información sobre cualquier archivo protegido por RMS, como los derechos de usuario o el identificador de contenido.

## <a name="development-environment-setup"></a>Configuración del entorno de desarrollo

Las guías siguientes le llevan por los pasos de configuración específicos del sistema operativo en un entorno de desarrollo de aplicaciones mediante herramientas comunes.

[![Configuración de iOS/OSX](../media/develop/ios-icon.png)](ios-sdk.md)
[![Configuración de Android](../media/develop/android-icon.png)](android-sdk.md)
[![Configuración de Windows Phone](../media/develop/windows-phone-icon.png)](windows-phone-apps.md)
[![Configuración del servicio de Windows](../media/develop/windows-icon.png)](install-the-rms-sdk.md)
[![Configuración de Linux](../media/develop/linux-icon.png)](linux-setup.md)


## <a name="how-tos"></a>Procedimientos

Cada uno de los siguientes temas presenta instrucciones específicas sobre un aspecto de implementación de la aplicación. Las aplicaciones de servicio se crean con el SDK 2.x de RMS. Las aplicaciones de usuario se crean mediante el SDK 4.x de RMS. El vínculo del artículo se atribuye al tipo de aplicación; servicio, usuario.

### <a name="general"></a>General

- [Habilitación de la revocación y el seguimiento de documentos (servicio)](tracking-content.md)
- [Implementación de un cliente](../rms-client/client-deployment-notes.md)
- [Implementación de la aplicación de servicio en otro inquilino] (how-to-deploy-app.md)
- [Instalación y configuración de un servidor RMS (servicio)](how-to-install-and-configure-an-rms-server.md)
- [Uso del seguimiento de documentos (usuario)](how-to-use-document-tracking.md)
- [Renovación de una clave simétrica en Azure Information Protection](how-to-renew-symmetric-key.md)

### <a name="security-and-authentication"></a>Seguridad y autenticación

- [Configuración de la aplicación de App Service para usar el inicio de sesión de Azure Active Directory](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication)
- [Uso de la autenticación de Azure Active Directory (ADAL)](how-to-use-adal-authentication.md)
- [Configuración de Azure RMS para la autenticación (servicio)](adal-auth.md)
- [Establecimiento del modo de seguridad de API (servicio)](setting-the-api-security-mode-api-mode.md)
- [Habilitación de las aplicaciones para usar Azure RMS (servicio)](how-to-use-file-api-with-aadrm-cloud.md)
- [Cómo registrar y habilitar para RMS la aplicación con Azure AD (usuario)](authentication-integration.md)

### <a name="configuration-and-performance-management"></a>Administración de configuración y rendimiento

- [Incorporación de derechos de propiedad explícitos (servicio)](add-explicit-owner-rights.md)
- [Configuración de la API de archivo (servicio)](file-api-configuration.md)
- [Cómo usar los derechos integrados (usuario)](built-in-rights-usage-restriction-reference.md)
- [Procedimiento para habilitar el registro de rendimiento y errores (usuario)](enabling-logging.md)

## <a name="introduction-and-datasheets"></a>Introducción y hojas de datos

[Introducción a Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection)

## <a name="other-resources"></a>Otros recursos

- [Guía de procedimientos de seguridad](security-guidelines.md)
- [Esquina del desarrollador de RMS (blog)](https://blogs.msdn.microsoft.com/rms/)
- [Preguntas más frecuentes sobre Azure Information Protection](https://docs.microsoft.com/information-protection/get-started/faqs)

### <a name="support-articles"></a>Artículos de soporte técnico

- [Formatos de archivo compatibles](supported-file-formats.md)
- [Plataformas compatibles](supported-platforms.md)
- [Descripción de las restricciones de uso](understanding-usage-restrictions.md)

### <a name="message-protocol-and-file-formats"></a>Protocolo de mensajes y formatos de archivo

- [Protocolo de cliente a servidor](https://msdn.microsoft.com/library/cc243191.aspx)
- [Protocolo de objetos de correo electrónico administrado con derechos](https://msdn.microsoft.com/library/cc463909(v=EXCHG.80).aspx)
- [Formato de archivo compuesto y archivo binario](https://msdn.microsoft.com/library/dd942138.aspx)

#### <a name="rights-managed-email-message"></a>Mensaje de correo electrónico administrado con derechos

- [Formato de archivo .MSG (parte 1)](https://blogs.msdn.microsoft.com/openspecification/2009/11/06/msg-file-format-part-1/)
- [Formato de archivo .MSG (parte 2)](https://blogs.msdn.microsoft.com/openspecification/2010/06/20/msg-file-format-rights-managed-email-message-part-2/)

### <a name="api-reference"></a>Referencia de API

- [Referencia de la API de Windows](https://msdn.microsoft.com/library/hh535292.aspx)
  - [Códigos de error del SDK de Windows](https://msdn.microsoft.com/library/hh535248.aspx)
- [Referencia de API de la Tienda Windows y Windows Phone](https://msdn.microsoft.com/library/dn891914.aspx)
- [Referencia de API de iOS/OSX](https://msdn.microsoft.com/library/dn758306.aspx)
- [Referencia de API de Android](https://msdn.microsoft.com/library/dn758245.aspx)
- [Referencia de la API de Linux](http://azuread.github.io/rms-sdk-for-cpp/annotated.html)

### <a name="previous-versions"></a>Versiones anteriores

- El [SDK de AD RMS](https://msdn.microsoft.com/library/cc530379.aspx) es la primera versión del SDK de RMS.
- La [herramienta de scripting de AD RMS](https://msdn.microsoft.com/library/bb968797.aspx) es una herramienta administrativa para una instalación de AD RMS.

### <a name="see-also"></a>Vea también

- [Terminología de desarrollador](terms.md)
- [Terminología de Azure Information Protection: profesionales de TI](../terminology.md)

