---
title: "Instalación del cliente de Azure Information Protection | Azure Information Protection"
description: "Instrucciones para instalar el cliente que agrega una barra de Information Protection a las aplicaciones de Office para que pueda seleccionar etiquetas de clasificación de los documentos y correos electrónicos."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/13/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4445adff-4c5a-450f-aff8-88bf5bd4ca78
translationtype: Human Translation
ms.sourcegitcommit: bd3cbea29183c39abaa66aa5dcec8a14ad0b0757
ms.openlocfilehash: bccddf228b33bcd8d36ef6af55dea9015cad34d0


---

# <a name="installing-the-azure-information-protection-client"></a>Instalación del cliente de Azure Information Protection

>*Se aplica a: Azure Information Protection*

Para clasificar documentos y mensajes de correo electrónico mediante Azure Information Protection, primero debe instalar el cliente de Azure Information Protection. Esta instalación agrega una barra de Information Protection a las aplicaciones de Office (Word, Excel, PowerPoint, Outlook) que muestra las etiquetas de clasificación de la organización, además de un nuevo grupo **Protección** en la pestaña **Inicio** (Word, Excel, PowerPoint), que tiene un botón llamado **Proteger**:

La siguiente imagen muestra esta barra de protección de Information Protection y las etiquetas de la [directiva predeterminada](../deploy-use/configure-policy-default.md):

![Barra de Azure Information Protection con la directiva predeterminada](../media/info-protect-bar-default.png)

Descargue el cliente de Azure Information Protection del [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). Actualmente, puede instalar la versión de disponibilidad general (GA) y la versión preliminar. La versión preliminar incluye nueva funcionalidad con fines de evaluación y está sujeta a cambios. Para más información, consulte la entrada de blog de [anuncio de disponibilidad de la versión preliminar de Azure Information Protection en diciembre](https://blogs.technet.microsoft.com/enterprisemobility/2016/12/07/azure-information-protection-december-preview-now-available/).

Antes de instalar el cliente, compruebe que tiene las versiones necesarias de sistema operativo y aplicaciones para el cliente de Azure Information Protection: [Requisitos para Azure Information Protection](../get-started/requirements-azure-rms.md). Además, para la versión preliminar del cliente, los equipos que ejecutan Windows 7 SP1 requieren [KB 2533623](https://support.microsoft.com/en-us/kb/2533623), que se puede instalar después de la instalación del cliente. Si esta actualización es necesaria y no se ha instalado, se le pedirá que lo haga.


## <a name="to-install-the-azure-information-protection-client-manually"></a>Para instalar el cliente de Azure Information Protection manualmente

> [!NOTE]
> Esta instalación requiere permisos administrativos locales.

    
1. Cuando haya [descargado el cliente](https://www.microsoft.com/en-us/download/details.aspx?id=53018), ejecute el ejecutable, como **AzInfoProtection.exe** y siga las indicaciones para instalar el cliente.
    
    Si no puede conectarse a Office 365 o Azure Active Directory, pero quiere ver y experimentar el lado cliente de Azure Information Protection mediante una directiva local con fines de demostración, seleccione la opción para instalar una **directiva de demostración**. Cuando el cliente se conecta a un servicio de Azure Information Protection, esta directiva de demostración se reemplaza por la directiva de Azure Information Protection de su organización.
    
    Para obtener más información sobre lo que se instala:

    - La versión de disponibilidad general instala la barra de Azure Information Protection para las aplicaciones de Office. 
    
    - La última versión preliminar del cliente instala la barra de Azure Information Protection para las aplicaciones de Office, las opciones de clic derecho para el Explorador de archivos, un visor para archivos protegidos y cmdlets de Windows PowerShell para clasificar y proteger archivos en masa. 
        
        Tenga en cuenta que puede instalar solo el módulo de PowerShell (RMSProtection) especificando el parámetro **PowerShellOnly=true**. Por ejemplo: `AzInfoProtection_PREVIEW_1.3.98.0.exe  PowerShellOnly=true`

2. Para completar la instalación: 

    - Si su equipo ejecuta Office 2010, reinicie el equipo. 
        
        **En caso de haber instalado la versión preliminar del cliente**: además de reiniciar el equipo, abra una de las aplicaciones de Office que utilizan la barra de Azure Information Protection (por ejemplo, Word) y confirme las solicitudes para actualizar el Registro para la primera vez que se usa. La [detección de servicios](../rms-client/client-deployment-notes.md#rms-service-discovery) se usa para rellenar las claves del Registro. 
    
    - Para otras versiones de Office, reinicie las aplicaciones de Office. 
        
        **En caso de haber instalado la versión preliminar del cliente**: además de reiniciar las aplicaciones de Office, cierre y vuelva a iniciar el Explorador de archivos.

## <a name="to-install-the-azure-information-protection-client-for-users"></a>Para instalar el cliente de Azure Information Protection para los usuarios

Puede incluir y automatizar la instalación del cliente de Azure Information Protection mediante las opciones de la línea de comandos. Para ver las opciones de instalación, ejecute el archivo ejecutable con **/help**. Por ejemplo: `AzInfoProtection.exe /help`

Ejemplo para instalar la versión de disponibilidad general del cliente de forma silenciosa: `AzInfoProtection.exe /quiet`

Ejemplo para instalar el módulo de PowerShell, con el cliente de versión preliminar, de forma silenciosa: `AzInfoProtection_PREVIEW_1.3.98.0.exe  PowerShellOnly=true /quiet`

Si va a instalar la versión preliminar del cliente en equipos que ejecutan Office 2010, especifique el parámetro **ServiceLocation** si los usuarios no son administradores locales en sus equipos. Para obtener más información, consulte la sección siguiente.

La versión de disponibilidad general del cliente de Azure Information Protection también se incluye en el catálogo de Microsoft Update para que pueda instalar y actualizar al cliente mediante cualquier servicio de actualización de software que use el catálogo. Las versiones preliminares del cliente no se incluyen en el catálogo de Microsoft Update.

### <a name="preview-version-and-office-2010-only"></a>Solo versión preliminar y Office 2010

Para la versión preliminar del cliente y Office 2010, al instalar el cliente para usuarios, especifique el parámetro ServiceLocation y la URL para su servicio de Azure Rights Management. El parámetro y el valor permiten crear y establecer las claves del Registro siguientes:

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

Utilice el procedimiento siguiente para identificar el valor que se especificará para el parámetro ServiceLocation. 

#### <a name="to-identify-the-value-to-specify-for-the-servicelocation-parameter"></a>Para identificar el valor que se especificará para el parámetro ServiceLocation

1. Desde una sesión de PowerShell, ejecute [Connect-AadrmService](https://docs.microsoft.com/powershell/aadrm/vlatest/connect-aadrmservice) y especifique sus credenciales de administrador para conectarse al servicio de Azure Rights Management. Ejecute a continuación [Get-AadrmConfiguration](https://docs.microsoft.com/powershell/aadrm/vlatest/get-aadrmconfiguration). 
 
    Si aún no ha instalado el módulo de PowerShell para el servicio Azure Rights Management, consulte [Instalación de Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md).

2. En la salida, identifique el valor **LicensingIntranetDistributionPointUrl** .

    Por ejemplo: **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. En el valor, quite **/_wmcs/licensing** de esta cadena. Por ejemplo: **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**.

    La cadena restante es el valor que se especificará para el parámetro ServiceLocation.

Ejemplo para instalar el cliente de Office 2010 y Azure RMS de forma silenciosa: `AzInfoProtection.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


## <a name="to-uninstall-the-azure-information-protection-client"></a>Para desinstalar el cliente de Azure Information Protection

Puede usar una de estas opciones:

- Utilice el Panel de Control para desinstalar un programa: haga clic en **Microsoft Azure Information Protection** > **Desinstalar**

- Vuelva a ejecutar el archivo ejecutable (por ejemplo, **AzInfoProtection.exe**) y, en la página, **Modificar instalación**, haga clic en **Desinstalar**. 

- Ejecute el archivo ejecutable con **/uninstall**. Por ejemplo: `AzInfoProtection.exe /uninstall`


## <a name="to-verify-installation-connection-status-or-report-a-problem"></a>Para comprobar la instalación, el estado de la conexión o informar de un problema

1. Abra una aplicación de Office y, en la pestaña **Inicio**, en el grupo **Protección**, haga clic en **Proteger** y luego en **Ayuda y comentarios**.

2. En el cuadro de diálogo **Microsoft Azure Information Protection**, anote lo siguiente:

    - En la sección del **estado de cliente**: use el valor de la **versión** para comprobar que la instalación se realizó correctamente. Además, puede ver cuándo el cliente se ha conectado por última vez al servicio de Azure Information Protection de su organización y cuándo la directiva de dicho servicio se ha instalado o actualizado por última vez. Cuando el cliente se conecta al servicio, se descarga automáticamente la directiva más reciente si encuentra cambios con respecto a su directiva actual. Si ha realizado cambios en la directiva con posterioridad al tiempo mostrado, cierre y vuelva a abrir la aplicación de Office.
    
        También puede ver el nombre de usuario mostrado que identifica la cuenta que se usa para autenticarlo en Azure Information Protection. Este nombre de usuario debe coincidir con una cuenta que utilice para Office 365 o Azure Active Directory y que pertenezca a un inquilino que esté configurado para Azure Information Protection.

    - En la sección **Ayuda y comentarios**: el vínculo **Más información** dirige, de forma predeterminada, al sitio web de [Azure Information Protection](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection), pero se puede configurar con una dirección URL personalizada como uno de los valores de [configuración de directivas](../deploy-use/configure-policy-settings.md) en la directiva de Azure Information Protection.
        
        Utilice el vínculo **Enviar comentarios** para adjuntar automáticamente los registros de cliente a un mensaje de correo electrónico que se puede enviar al equipo de Information Protection para investigar un problema. 
    
        Para obtener información de diagnóstico y restablecer el cliente, haga clic en **Ejecutar diagnósticos**. Al finalizar las pruebas de los diagnósticos, haga clic en **Copiar resultados** para pegar la información en un correo electrónico que puede enviar a su departamento de soporte técnico o al soporte técnico de Microsoft. Cuando finalicen las pruebas, también puede restablecer al cliente.
        
        Más información acerca de la opción **Restablecer**:
        
        - No tiene que ser un administrador local para usar esta opción, y esta acción no se registra en el Visor de eventos. 
        
        - A menos que los archivos estén bloqueados, esta acción elimina todos los archivos de **%localappdata%\Microsoft\MSIPC**, que es donde se almacenan las plantillas de certificados de cliente y administración de derechos. No se elimina la directiva de Azure Information Protection, ni los archivos de registro de cliente, ni se cierra la sesión del usuario.
        
        - La clave de registro y las configuraciones siguientes se eliminan: **HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC**. Si establece la configuración de esta clave del registro (por ejemplo, configuración de redireccionamiento para el inquilino de Azure Information Protection porque ya está migrando de AD RMS y aún tiene un punto de conexión de servicio en la red), debe volver a configurar la configuración del registro después de restablecer al cliente.
        
        - Después de restablecer al cliente, debe volver a inicializar el entorno de usuario (también conocido como "arranque"), con lo cual se descargarán los certificados para el cliente y las plantillas más recientes. Para ello, cierre todas las instancias de Office y, después, reinicie una aplicación de Office. Esta acción también comprobará que ha descargado la directiva de Azure Information Protection más reciente. No vuelva a ejecutar las pruebas de diagnóstico hasta que haya realizado esta acción.


## <a name="usage-logging"></a>Registro de uso

**[Esta característica requiere la versión preliminar del cliente y está sujeta a cambios.]**

En la versión preliminar del cliente de Azure Information Protection, el cliente registra la actividad del usuario en el registro de eventos local de Windows **Aplicaciones y servicios**, **Azure Information Protection**. Los eventos incluyen la siguiente información:

- Fecha, versión de cliente, id. de directiva

- Nombre de usuario de inicio de sesión, nombre de equipo

- Nombre y ubicación del archivo

- Acción:

    - Definir etiqueta: id. de información 101
    
    - Definir etiqueta (inferior): id. de información 102
    
    - Definir etiqueta (superior): id. de información 103
    
    - Quitar etiqueta: id. de información 104
   
    - Sugerencia recomendada: información 105
    
    - Aplicar protección personalizada: id. de información 201
    
    - Quitar protección personalizada: id. de información 202
    
    - Inicio de sesión (operativo): id. de información 902
    
    - Descargar directiva (operativo): id. de información 901
    
- Origen de la acción:
    
    - Manual 
    
    - Recomendado
    
    - Automático  
    
    - Sistema (para iniciar sesión y descargar la directiva)
    
- Etiqueta antes y después de la acción 
    
- Protección antes y después de la acción
    
- Justificación de usuario (si procede)
    

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

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO2-->


