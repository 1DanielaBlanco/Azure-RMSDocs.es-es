---
title: "Instalación del cliente de Azure Information Protection | Azure Information Protection"
description: "Instrucciones para instalar el cliente que agrega una barra de Information Protection a las aplicaciones de Office para que pueda seleccionar etiquetas de clasificación de los documentos y correos electrónicos."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/01/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4445adff-4c5a-450f-aff8-88bf5bd4ca78
translationtype: Human Translation
ms.sourcegitcommit: 2f1930f4657278d25ef6dd369866f16e4ba71644
ms.openlocfilehash: 5e36d046d53b0fdfb6796f2a00e8d0d1325f30c3


---

# <a name="installing-the-azure-information-protection-client"></a>Instalación del cliente de Azure Information Protection

>*Se aplica a: Azure Information Protection*

Para clasificar documentos y mensajes de correo electrónico mediante Azure Information Protection, primero debe instalar el cliente de Azure Information Protection. Esta instalación agrega una barra de Information Protection a las aplicaciones de Office (Word, Excel, PowerPoint, Outlook) que muestra las etiquetas de clasificación de la organización, además de un nuevo grupo **Protección** en la pestaña **Inicio** (Word, Excel, PowerPoint), que tiene un botón llamado **Proteger**:

La siguiente imagen muestra esta barra de protección de Information Protection y las etiquetas de la [directiva predeterminada](../deploy-use/configure-policy-default.md):

![Barra de Azure Information Protection con la directiva predeterminada](../media/info-protect-bar-default.png)

Descargue el cliente de Azure Information Protection del [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Antes de instalar el cliente, compruebe que tiene las versiones necesarias de sistema operativo y aplicaciones para el cliente de Azure Information Protection: [Requisitos para Azure Information Protection](../get-started/requirements-azure-rms.md).


## <a name="to-install-the-azure-information-protection-client-manually"></a>Para instalar el cliente de Azure Information Protection manualmente

1. Cuando haya [descargado el cliente](https://www.microsoft.com/en-us/download/details.aspx?id=53018), ejecute **AZInfoProtection.exe** y siga los mensajes para instalar el cliente. Esta instalación requiere permisos administrativos locales.

    Si no puede conectarse a Office 365 o Azure Active Directory, pero desea ver y experimentar el lado cliente de Azure Information Protection mediante una directiva local con fines de demostración, seleccione la opción para instalar una directiva de demostración. Cuando el cliente se conecta a un servicio de Azure Information Protection, esta directiva de demostración se reemplaza por la directiva de Azure Information Protection de su organización. 

2. Para empezar a usar el cliente de Azure Information Protection: si su equipo ejecuta Office 2010, reinicie el equipo. Para otras versiones de Office, reinicie las aplicaciones de Office.

## <a name="to-install-the-azure-information-protection-client-for-users"></a>Para instalar el cliente de Azure Information Protection para los usuarios

Puede incluir y automatizar la instalación del cliente de Azure Information Protection mediante las opciones de la línea de comandos. Para ver las opciones de instalación, ejecute `AzInfoProtection.exe /help`.

Por ejemplo, para instalar el cliente de forma silenciosa: `AzInfoProtection.exe /passive | quiet`

El cliente de Azure Information Protection también se incluye en el catálogo de Microsoft Update, para que pueda instalar y actualizar al cliente mediante el uso de cualquier servicio de actualización de software que use el catálogo.

## <a name="to-uninstall-the-azure-information-protection-client"></a>Para desinstalar el cliente de Azure Information Protection

Puede usar una de estas opciones:

- Utilice el Panel de Control para desinstalar un programa: haga clic en **Microsoft Azure Information Protection** > **Desinstalar**

- Vuelva a ejecutar **AzInfoProtection.exe** y, desde la página **Modificar instalación**, haga clic en **Desinstalar**. 

- Ejecute `AzInfoProtection.exe /uninstall`:


## <a name="to-verify-installation-connection-status-or-report-a-problem"></a>Para comprobar la instalación, el estado de la conexión o informar de un problema

1. Abra una aplicación de Office y, en la pestaña **Inicio**, en el grupo **Protección**, haga clic en **Proteger** y luego en **Ayuda y comentarios**.

2. En el cuadro de diálogo **Microsoft Azure Information Protection**, anote lo siguiente:

    - En la sección del **estado de cliente**: use el valor de la **versión** para comprobar que la instalación se realizó correctamente. Además, puede ver cuándo el cliente se ha conectado por última vez al servicio de Azure Information Protection de su organización y cuándo la directiva de dicho servicio se ha instalado o actualizado por última vez. Cuando el cliente se conecta al servicio, se descarga automáticamente la directiva más reciente si encuentra cambios con respecto a su directiva actual. Si ha realizado cambios en la directiva con posterioridad al tiempo mostrado, cierre y vuelva a abrir la aplicación de Office.
    
        También puede ver el nombre de usuario mostrado que identifica la cuenta que se usa para autenticarlo en Azure Information Protection. Este nombre de usuario debe coincidir con una cuenta que se usa para Office 365 o Azure Active Directory.

    - En la sección **Ayuda y comentarios**: use el vínculo **Enviar comentarios** para adjuntar automáticamente los registros de cliente a un mensaje de correo electrónico que se puede enviar al equipo de Information Protection para que investiguen si hay algún problema. 
    
        Para obtener información de diagnóstico y restablecer el cliente, haga clic en **Ejecutar diagnósticos**. Al finalizar las pruebas de los diagnósticos, haga clic en **Copiar resultados** para pegar la información en un correo electrónico que puede enviar a su departamento de soporte técnico o al soporte técnico de Microsoft. Cuando finalicen las pruebas, también puede restablecer al cliente.
        
        Más información acerca de la opción **Restablecer**:
        
        - No tiene que ser un administrador local para usar esta opción, y esta acción no se registra en el Visor de eventos. 
        
        - A menos que los archivos estén bloqueados, esta acción elimina todos los archivos de **%localappdata%\Microsoft\MSIPC**, que es donde se almacenan las plantillas de certificados de cliente y administración de derechos. No se elimina la directiva de Azure Information Protection, ni los archivos de registro de cliente, ni se cierra la sesión del usuario.
        
        - La clave de registro y las configuraciones siguientes se eliminan: **HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC**. Si establece la configuración de esta clave del registro (por ejemplo, configuración de redireccionamiento para el inquilino de Azure Information Protection porque ya está migrando de AD RMS y aún tiene un punto de conexión de servicio en la red), debe volver a configurar la configuración del registro después de restablecer al cliente.
        
        - Después de restablecer al cliente, debe volver a inicializar el entorno de usuario (también conocido como "arranque"), con lo cual se descargarán los certificados para el cliente y las plantillas más recientes. Para ello, cierre todas las instancias de Office y, después, reinicie una aplicación de Office. Esta acción también comprobará que ha descargado la directiva de Azure Information Protection más reciente. No vuelva a ejecutar las pruebas de diagnóstico hasta que haya realizado esta acción.

## <a name="keyboard-shortcuts-for-the-azure-information-protection-bar"></a>Métodos abreviados de teclado para la barra Azure Information Protection

Para acceder a la barra Azure Information Protection mediante el uso de métodos abreviados de teclado, utilice la combinación de teclas siguiente:

- Presione **Ctrl** + **Mayús** + **~** 

A continuación, utilice la tecla de tabulación para seleccionar las etiquetas y otros controles en la barra (el icono **Ocultar etiquetas** y el icono **Quitar etiqueta**) y la tecla Intro para seleccionarlos.


## <a name="file-locations"></a>Ubicaciones de archivos

Archivos de cliente:   

- Para los sistemas operativos de 64 bits: **\Archivos de programa (x86)\Microsoft Azure Information Protection**

- Para los sistemas operativos de 32 bits: **\Archivos de programa\Microsoft Azure Information Protection**

Archivos de registros de cliente y archivos de directiva actualmente instalado:

- Para los sistemas operativos de 32 y 64 bits: **%localappdata%\Microsoft\MSIP**


## <a name="next-steps"></a>Pasos siguientes

Para cambiar las etiquetas en la barra de Information Protection, debe configurar la directiva de Azure Information Protection. Para más información, consulte [Configuración de la directiva de Azure Information Protection](../deploy-use/configure-policy.md).

Para ver un ejemplo de cómo personalizar la directiva predeterminada y ver el comportamiento resultante en una aplicación de Office, pruebe el [tutorial de inicio rápido de Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md).

Para comprobar la información de versión de lanzamiento para el cliente, consulte el [Historial de publicación de versiones](client-version-release-history.md).



<!--HONumber=Nov16_HO1-->


