---
title: "Instrucciones e información para desarrolladores | Azure RMS"
description: "En este tema se incluyen instrucciones específicas para varios escenarios de desarrollo importantes."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 10/18/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5A9F04FD-0FCD-482F-8671-36FE93B783B0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: 93ed9760d79f2f38d4bee302ebb5c7c6368b1bbe


---

# <a name="developer-guidance-and-information"></a>Instrucciones e información para desarrolladores

En esta sección se incluyen instrucciones específicas para varios escenarios de desarrollo importantes, así como información general sobre el desarrollo con este SDK. Los escenarios de esta sección son específicos de esta versión de Rights Management Services SDK 2.1 y podrían modificarse en versiones posteriores.
- [Uso de la autenticación ADAL](how-to-use-adal-authentication.md): autenticación con Azure RMS para una aplicación que use la biblioteca de autenticación de Azure Active Directory (ADAL).
- [Incorporación de derechos de propiedad explícitos](add-explicit-owner-rights.md): la aplicación debe agregar explícitamente derechos "Owner" al crear una licencia desde el principio ([IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx)).
- [Depuración de una aplicación con derechos habilitados](debugging-applications-that-use-ad-rms.md): en este tema se muestra cómo depurar la aplicación y usar el registro de eventos de Windows.
- [Habilitación de la revocación y el seguimiento de documentos](tracking-content.md): en este tema se abordan las instrucciones básicas para implementar el seguimiento de documentos, así como código de ejemplo para las actualizaciones de metadatos y para la creación de un botón **Hacer seguimiento de uso** para la aplicación.
- [Habilitación de la notificación por correo electrónico](how-to-enable-email-notification.md): las notificaciones por correo electrónico permiten que el propietario de contenido protegido reciba una notificación cuando se acceda a su contenido.
- [Habilitación de la aplicación de servicio para que funcione con RMS basado en la nube](how-to-use-file-api-with-aadrm-cloud.md): en este tema se describe cómo configurar la aplicación de servicio para que use Azure Rights Management.
- [Instalación y configuración de un servidor RMS](how-to-install-and-configure-an-rms-server.md): en este tema se explica cómo conectar con un servidor RMS o Azure RMS para probar la aplicación con derechos habilitados.
- [Establecimiento del modo de seguridad de API](setting-the-api-security-mode-api-mode.md): puede elegir en qué modo de seguridad se ejecutará la aplicación de API de archivo mediante la función [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx).
- [Trabajo con la configuración de cifrado](working-with-encryption.md): en este tema se le orienta sobre nuestros paquetes de cifrado y se muestra el uso de algunos fragmentos de código.
- [Tipos de aplicación](application-types.md): en este tema se cubren los tipos de aplicaciones que puede elegir crear como aplicaciones con derechos habilitados.
- [Configuración de la API de archivos](file-api-configuration.md): el comportamiento de la API de archivos se puede configurar mediante el Registro.
- [Formatos de archivo compatibles](supported-file-formats.md): la API de archivo admite formato Pfile y nativo.
- [Plataformas compatibles](supported-platforms.md): en este tema se identifican las plataformas de cliente y servidor compatibles con RMS SDK 2.1.
- [Descripción de las restricciones de uso](understanding-usage-restrictions.md): todas las aplicaciones habilitadas para RMS deben aplicar restricciones de uso.
- [Referencia de restricción de uso](usage-restriction-reference.md): las restricciones de uso se definen mediante las constantes indicadas en este tema.

 
## <a name="related-topics"></a>Temas relacionados
* [Información general](ad-rms-overview.md)
 

 



<!--HONumber=Nov16_HO2-->


