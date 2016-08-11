---
title: "Instalación del cliente de Azure Information Protection | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4445adff-4c5a-450f-aff8-88bf5bd4ca78
translationtype: Human Translation
ms.sourcegitcommit: 93444affe94b280db2c9e4e2960c6902e491dec6
ms.openlocfilehash: c8a7c7d7182df7b525b3425ab378126feb389d9f


---

# Instalación del cliente de Azure Information Protection

>*Se aplica a: Azure Information Protection (versión preliminar)*

**[Esta información es preliminar y está sujeta a cambios. ]**

Para clasificar documentos y mensajes de correo electrónico mediante Azure Information Protection, primero debe instalar el cliente de Azure Information Protection. Esta instalación agrega una barra de Information Protection a las aplicaciones de Office (Word, Excel, PowerPoint, Outlook) que muestra las etiquetas de clasificación de la organización, además de un nuevo grupo **Protección** en la pestaña **Inicio** (Word, Excel, PowerPoint), que tiene un botón llamado **Proteger**:

La siguiente imagen muestra esta barra de protección de Information Protection y las etiquetas de la [directiva predeterminada](configure-policy-default.md):

![Barra de Azure Information Protection con la directiva predeterminada](../media/info-protect-bar-default.png)

Descargue el cliente de Azure Information Protection del [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Antes de instalar el cliente, compruebe que tiene las versiones necesarias de sistema operativo y aplicaciones: [Requisitos para Azure Information Protection](requirements-azure-infoprotect.md).


## Para instalar el cliente de Azure Information Protection manualmente

1. Cuando haya [descargado el cliente](https://www.microsoft.com/en-us/download/details.aspx?id=53018), ejecute **AZInfoProtection.exe** y siga los mensajes para instalar el cliente. Esta instalación requiere permisos administrativos locales.

    Si no puede conectarse a Office 365 o Azure Active Directory, pero desea ver y experimentar el lado cliente de Azure Information Protection mediante una directiva local con fines de demostración, seleccione la opción para instalar una directiva de demostración. Cuando el cliente se conecta a un servicio de Azure Information Protection, esta directiva de demostración se reemplaza por la directiva de Azure Information Protection de su organización. 

2. Para empezar a usar el cliente de Azure Information Protection: si su equipo ejecuta Office 2010, reinicie el equipo. Para otras versiones de Office, reinicie las aplicaciones de Office.

## Para instalar el cliente de Azure Information Protection para los usuarios

- Puede generar scripts y automatizar la instalación del cliente de Azure Information Protection; para ello, empaquete AZInfoProtection.exe y use [opciones de línea de comandos estándar de Windows Installer (msiexec)](https://technet.microsoft.com/library/cc759262(v=ws.10).aspx).

    Por ejemplo, si la versión empaquetada que se crea se denomina InfoProtect.msi y desea instalar el cliente de forma silenciosa: `msiexec /qn InfoProtection.msi`


## Para desinstalar el cliente de Azure Information Protection

- Utilice el Panel de Control para desinstalar un programa: haga clic en **Microsoft Azure Information Protection** > **Desinstalar**

## Para comprobar la instalación, el estado de la conexión o informar de un problema

1. Abra una aplicación de Office y, en la pestaña **Inicio**, en el grupo **Protección**, haga clic en **Proteger** y luego en **Ayuda y comentarios**.

2. En el cuadro de diálogo **Microsoft Azure Information Protection**, anote lo siguiente:

    - El valor de **Última conexión** que identifica cuándo se conectó por última vez el cliente al servicio de Azure Information Protection de su organización. Cuando el cliente se conecta al servicio, se descarga automáticamente la directiva más reciente si encuentra cambios con respecto a su directiva actual. Si ha realizado cambios en la directiva con posterioridad al tiempo mostrado, cierre y vuelva a abrir la aplicación de Office.

    - El nombre de usuario mostrado que identifica la cuenta que se usa para autenticarle en Azure Information Protection. Este nombre de usuario debe coincidir con una cuenta que se usa para Office 365 o Azure Active Directory.

    - La versión del cliente de Azure Information Protection.

    - El vínculo **Enviar comentarios**, que se puede usar para adjuntar automáticamente los registros de cliente a un mensaje de correo electrónico que se puede enviar al equipo de Information Protection para que lo investiguen.

    - El vínculo **Ejecutar diagnósticos**: esta funcionalidad no está actualmente implementada.

## Ubicaciones de archivos

Archivos de cliente:   

- Para los sistemas operativos de 64 bits: **\Archivos de programa (x86)\Microsoft Azure Information Protection**

- Para los sistemas operativos de 32 bits: **\Archivos de programa\Microsoft Azure Information Protection**

Archivos de registros de cliente y archivos de directiva actualmente instalado:

- Para los sistemas operativos de 32 y 64 bits: **%localappdata%\Microsoft\MSIP**


## Pasos siguientes

Para cambiar las etiquetas en la barra de Information Protection, debe configurar la directiva de Azure Information Protection. Para más información, consulte [Configuración de la directiva de Azure Information Protection](configure-policy.md).

Para ver un ejemplo de cómo personalizar la directiva predeterminada y ver el comportamiento resultante en una aplicación de Office, pruebe el [tutorial de inicio rápido de Azure Information Protection](infoprotect-quick-start-tutorial.md). 



<!--HONumber=Jul16_HO5-->


