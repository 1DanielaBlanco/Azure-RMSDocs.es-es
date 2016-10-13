---
title: "Instalación del cliente de Azure Information Protection | Azure Information Protection"
description: "Instrucciones para instalar el cliente que agrega una barra de Information Protection a las aplicaciones de Office para que pueda seleccionar etiquetas de clasificación de los documentos y correos electrónicos."
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4445adff-4c5a-450f-aff8-88bf5bd4ca78
translationtype: Human Translation
ms.sourcegitcommit: 003e76733657bb97c5447e2cdc44049d111d33fa
ms.openlocfilehash: 2892b091e300b0ef15ca09524d233474bd5de193


---

# Instalación del cliente de Azure Information Protection

>*Se aplica a: Azure Information Protection*

Para clasificar documentos y mensajes de correo electrónico mediante Azure Information Protection, primero debe instalar el cliente de Azure Information Protection. Esta instalación agrega una barra de Information Protection a las aplicaciones de Office (Word, Excel, PowerPoint, Outlook) que muestra las etiquetas de clasificación de la organización, además de un nuevo grupo **Protección** en la pestaña **Inicio** (Word, Excel, PowerPoint), que tiene un botón llamado **Proteger**:

La siguiente imagen muestra esta barra de protección de Information Protection y las etiquetas de la [directiva predeterminada](../deploy-use/configure-policy-default.md):

![Barra de Azure Information Protection con la directiva predeterminada](../media/info-protect-bar-default.png)

Descargue el cliente de Azure Information Protection del [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Antes de instalar el cliente, compruebe que tiene las versiones necesarias de sistema operativo y aplicaciones para el cliente de Azure Information Protection: [Requisitos para Azure Information Protection](../get-started/requirements-azure-rms.md).


## Para instalar el cliente de Azure Information Protection manualmente

1. Cuando haya [descargado el cliente](https://www.microsoft.com/en-us/download/details.aspx?id=53018), ejecute **AZInfoProtection.exe** y siga los mensajes para instalar el cliente. Esta instalación requiere permisos administrativos locales.

    Si no puede conectarse a Office 365 o Azure Active Directory, pero desea ver y experimentar el lado cliente de Azure Information Protection mediante una directiva local con fines de demostración, seleccione la opción para instalar una directiva de demostración. Cuando el cliente se conecta a un servicio de Azure Information Protection, esta directiva de demostración se reemplaza por la directiva de Azure Information Protection de su organización. 

2. Para empezar a usar el cliente de Azure Information Protection: si su equipo ejecuta Office 2010, reinicie el equipo. Para otras versiones de Office, reinicie las aplicaciones de Office.

## Para instalar el cliente de Azure Information Protection para los usuarios

Puede incluir y automatizar la instalación del cliente de Azure Information Protection mediante las opciones de la línea de comandos. Para ver las opciones de instalación, ejecute `AzInfoProtection.exe /help`.

Por ejemplo, para instalar el cliente de forma silenciosa: `AzInfoProtection.exe /passive | quiet`

## Para desinstalar el cliente de Azure Information Protection

Puede usar una de estas opciones:

- Utilice el Panel de Control para desinstalar un programa: haga clic en **Microsoft Azure Information Protection** > **Desinstalar**

- Vuelva a ejecutar **AzInfoProtection.exe** y, desde la página **Modificar instalación**, haga clic en **Desinstalar**. 

- Ejecutar `AzInfoProtection.exe /uninstall`


## Para comprobar la instalación, el estado de la conexión o informar de un problema

1. Abra una aplicación de Office y, en la pestaña **Inicio**, en el grupo **Protección**, haga clic en **Proteger** y luego en **Ayuda y comentarios**.

2. En el cuadro de diálogo **Microsoft Azure Information Protection**, anote lo siguiente:

    - El valor de **Última conexión** que identifica cuándo se conectó por última vez el cliente al servicio de Azure Information Protection de su organización. Cuando el cliente se conecta al servicio, se descarga automáticamente la directiva más reciente si encuentra cambios con respecto a su directiva actual. Si ha realizado cambios en la directiva con posterioridad al tiempo mostrado, cierre y vuelva a abrir la aplicación de Office.

    - El nombre de usuario mostrado que identifica la cuenta que se usa para autenticarle en Azure Information Protection. Este nombre de usuario debe coincidir con una cuenta que se usa para Office 365 o Azure Active Directory.

    - La versión del cliente de Azure Information Protection.

    - El vínculo **Enviar comentarios**, que se puede usar para adjuntar automáticamente los registros de cliente a un mensaje de correo electrónico que se puede enviar al equipo de Information Protection para que lo investiguen.

## Métodos abreviados de teclado para la barra Azure Information Protection

Para acceder a la barra Azure Information Protection mediante el uso de métodos abreviados de teclado, utilice la combinación de teclas siguiente:

- Presione **Ctrl** + **Mayús** + **~** 

A continuación, utilice la tecla de tabulación para seleccionar las etiquetas y otros controles en la barra (el icono **Ocultar etiquetas** y el icono **Quitar etiqueta**) y la tecla Intro para seleccionarlos.


## Ubicaciones de archivos

Archivos de cliente:   

- Para los sistemas operativos de 64 bits: **\Archivos de programa (x86)\Microsoft Azure Information Protection**

- Para los sistemas operativos de 32 bits: **\Archivos de programa\Microsoft Azure Information Protection**

Archivos de registros de cliente y archivos de directiva actualmente instalado:

- Para los sistemas operativos de 32 y 64 bits: **%localappdata%\Microsoft\MSIP**


## Pasos siguientes

Para cambiar las etiquetas en la barra de Information Protection, debe configurar la directiva de Azure Information Protection. Para más información, consulte [Configuración de la directiva de Azure Information Protection](../deploy-use/configure-policy.md).

Para ver un ejemplo de cómo personalizar la directiva predeterminada y ver el comportamiento resultante en una aplicación de Office, pruebe el [tutorial de inicio rápido de Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md). 



<!--HONumber=Sep16_HO4-->

