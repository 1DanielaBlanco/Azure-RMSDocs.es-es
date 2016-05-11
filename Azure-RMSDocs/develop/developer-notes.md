---
# required metadata

title: Notas para el desarrollador | Azure RMS
description: En este tema se incluyen instrucciones específicas para varios escenarios de desarrollo importantes. 
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 65c2f3d1-0852-41fa-a95a-53dcec787680

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿# Notas para el desarrollador

En esta sección se incluyen instrucciones específicas para varios escenarios de desarrollo importantes. Los escenarios de esta sección son específicos de esta versión de Rights Management Services SDK 2.1 y podrían modificarse en versiones posteriores.

- [Agregar derechos de propiedad explícitos](add-explicit-owner-rights.md): su aplicación debe agregar explícitamente derechos de &quot;propietario;Owner&quot; al crear una licencia desde el principio ([IpcCreateLicenseFromScratch](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)).
- [Condiciones de error comunes y soluciones](common-error-conditions-and-solutions.md): los mensajes de error más comunes que pueden surgir al usar las herramientas para desarrolladores del SDK 2.1 de RMS.
- [Habilitación de notificaciones por correo electrónico](how-to-enable-email-notification.md): las notificaciones por correo electrónico permiten que el propietario de contenido protegido reciba una notificación cuando se acceda a su contenido.
- [Configuración de la API de archivos](file-api-configuration.md): el comportamiento de la API de archivos se puede configurar mediante el Registro.
- [Aplicación de ejemplo IPCHelloWorld](how-to-build-your-first-application.md): este tema contiene instrucciones para crear una aplicación de ejemplo habilitada para derechos.
- [Configuración del modo de seguridad de la API](setting-the-api-security-mode-api-mode.md): puede elegir en qué modo de seguridad se ejecutará su aplicación de API de archivo mediante la función [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty).
- [Formatos de archivo compatibles](supported-file-formats.md): la API de archivo admite formato Pfile y nativo.
- [Seguimiento de contenido](tracking-content.md): en este tema se abordan las instrucciones básicas para implementar el seguimiento de documentos con contenido protegido con el SDK 2.1 de RMS.
- [El cifrado](working-with-encryption.md): este tema le orienta sobre nuestros paquetes de cifrado y muestra el uso de algunos fragmentos de código.

 

## Temas relacionados ##
* [Información general](ad-rms-overview.md)
* [Procedimiento](how-to-use-msipc.md)
 

 


<!--HONumber=Apr16_HO3-->


