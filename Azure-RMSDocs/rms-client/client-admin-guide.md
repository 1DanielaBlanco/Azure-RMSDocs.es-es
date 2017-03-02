---
title: "Guía del administrador de cliente de Azure Information Protection"
description: "Instrucciones e información para administradores de una red empresarial que son responsables de implementar el cliente de Azure Information Protection para Windows."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: b6a8477078a333aa23ccfe5904af3582216a1e96
ms.lasthandoff: 02/24/2017


---


# <a name="azure-information-protection-client-administrator-guide"></a>Guía para administradores del cliente de Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8 y Windows 7 con SP1*


Use la información siguiente si es el responsable del cliente de Azure Information Protection en una red empresarial o si desea obtener más información técnica de la contenida en la [Guía del usuario de Azure Information Protection](client-user-guide.md).

El cliente de Azure Information Protection incluye:

- Un complemento de Office, que instala la barra de Azure Information Protection para que los usuarios seleccionen etiquetas de clasificación y un botón **proteger** en la cinta para ofrecer otras opciones.

- Explorador de archivos de Windows, opciones de menú contextual para que los usuarios apliquen etiquetas de clasificación y la protección de los archivos.

- Un visor para mostrar los archivos protegidos cuando una aplicación nativa no puede abrirlo.

- Un módulo de PowerShell para aplicar y quitar etiquetas de clasificación y protección en los archivos.

- El cliente de Rights Management que se comunica con Azure Rights Management (Azure RMS) o Active Directory Rights Management Services (AD RMS).

El cliente de Azure Information Protection resulta ideal para trabajar con sus servicios de Azure; Azure Information Protection y su servicio de protección de datos, Azure Rights Management. Sin embargo, con algunas limitaciones, el cliente de Azure Information Protection también funciona con la versión local de Rights Management, AD RMS. Para ver una comparación exhaustiva de las características que admiten Azure Information Protection y AD RMS, consulte [Comparación entre Azure Information Protection y AD RMS](../understand-explore/compare-azure-rms-ad-rms.md). Si tiene AD RMS y quiere migrar a Azure Information Protection, consulte [Migración desde AD RMS a Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

**¿Tiene alguna pregunta que no se trata en esta documentación?** Visite el [sitio de Yammer sobre Azure Information Protection](https://www.yammer.com/AskIPTeam). 


## <a name="should-you-deploy-the-azure-information-protection-client"></a>¿Debe implementar el cliente de Azure Information Protection?

Implemente el cliente de Azure Information Protection si se aplica alguna de las siguientes condiciones:

- Desea clasificar (y, opcionalmente, proteger) documentos y mensajes de correo electrónico mediante la selección de etiquetas desde las aplicaciones de Office (Word, Excel, PowerPoint y Outlook).

- Desea clasificar (y, opcionalmente, proteger) documentos y mensajes de correo electrónico mediante el Explorador de archivos, que admite tipos de archivos adicionales, la selección múltiple y carpetas.

- Desea ejecutar scripts que clasifican (y, opcionalmente, protegen) documentos mediante los comandos de PowerShell.

- Desea ver documentos protegidos cuando una aplicación nativa para mostrar el archivo no está instalada o no puede abrir estos documentos.

- Solo desea proteger archivos con el Explorador de archivos o con los comandos de PowerShell.

- Desea que los usuarios y administradores puedan realizar un seguimiento de los documentos protegidos y revocarlos.

- Desea quitar el cifrado de archivos y contenedores (desproteger) en masa para fines de recuperación de datos.

- Ejecutar Office 2010 y proteger documentos y mensajes de correo electrónico mediante el servicio Azure Rights Management.

Ejemplo que muestra el complemento del cliente de Azure Information Protection en una aplicación de Office, mostrando las etiquetas de clasificación para su organización y el nuevo botón **Proteger** en la cinta:

![Barra de Azure Information Protection con la directiva predeterminada](../media/info-protect-bar-default.png)

## <a name="how-to-install-the-azure-information-protection-client-for-users"></a>Instalación del cliente de Azure Information Protection para los usuarios

Antes de instalar el cliente, compruebe que tiene las versiones necesarias de sistema operativo y aplicaciones para el cliente de Azure Information Protection: [Requisitos para Azure Information Protection](../get-started/requirements-azure-rms.md). 

Además:

- La instalación completa del cliente de Azure Information Protection requiere una versión mínima de Microsoft .NET Framework 4.6.2 y, en su defecto, el instalador intenta descargar e instalar este requisito previo. Cuando este requisito previo se instala como parte de la instalación de cliente, es necesario reiniciar el equipo.

- Si el visor de Azure Information Protection se instala por separado, se requiere una versión mínima de Microsoft .NET Framework 4.5.2 y, en su defecto, el instalador no lo descarga ni lo instala.

- El módulo de PowerShell requiere Windows PowerShell versión 4.0, que quizá deba instalarse en sistemas operativos anteriores. Para obtener más información consulte [How to Install Windows PowerShell 4.0](http://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx) (Instalación de Windows PowerShell 4.0). Para confirmar la versión de Windows PowerShell que ejecuta, escriba **$PSVersionTable** en una sesión de PowerShell.

- Los equipos que ejecutan Windows 7 Service Pack 1 requieren [KB 2533623](https://support.microsoft.com/en-us/kb/2533623), que se puede instalar después de instalar el cliente. Si esta actualización es necesaria y no se ha instalado, se le pide que lo haga.

> [!NOTE]
> La instalación requiere permisos administrativos locales.

Además de usar las siguientes instrucciones, el cliente de Azure Information Protection también se incluye en el catálogo de Microsoft Update para que pueda instalar y actualizar al cliente mediante cualquier servicio de actualización de software que use el catálogo. 

1. Descargue el cliente de Azure Information Protection del [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 

2. En una instalación predeterminada, simplemente ejecute el archivo ejecutable, **AzInfoProtection.exe**. No obstante, para ver las opciones de instalación, primero ejecute el archivo ejecutable con **/help**: `AzInfoProtection.exe /help`

   Ejemplo para instalar el cliente de forma silenciosa: `AzInfoProtection.exe /quiet`
   
   Ejemplo para instalar de forma silenciosa solo los cmdlets de PowerShell: `AzInfoProtection.exe  PowerShellOnly=true /quiet`
   
   Además, si va a instalar el cliente en equipos que ejecutan Office 2010, debe especificar el parámetro **ServiceLocation** (no incluido en la pantalla de ayuda) si los usuarios no son administradores locales en sus equipos. Para obtener más información, consulte la sección siguiente.

3. Si va a realizar la instalación de forma interactiva, seleccione la opción para instalar una **directiva de demostración**, si no puede conectarse a Office 365 o Azure Active Directory, pero quiere ver y experimentar el lado cliente de Azure Information Protection mediante una directiva local con fines de demostración. Cuando el cliente se conecta a un servicio de Azure Information Protection, esta directiva de demostración se reemplaza por la directiva de Azure Information Protection de su organización.
    
4. Para completar la instalación: 

    - Si su equipo ejecuta Office 2010, reinicie el equipo. 
        
        Si el cliente no se ha instalado con el parámetro ServiceLocation, la primera vez que abre una de las aplicaciones de Office que usan la barra de Azure Information Protection (por ejemplo, Word), debe confirmar las solicitudes de actualización del registro para la primera vez que se usa. La [detección de servicios](../rms-client/client-deployment-notes.md#rms-service-discovery) se usa para rellenar las claves del Registro. 
    
    - Para otras versiones de Office, reinicie todas las aplicaciones de Office y todas las instancias del Explorador de archivos. 
        
5. Puede confirmar que la instalación se completó correctamente consultando el archivo de registro de la instalación en la carpeta %temp%. El nombre del archivo tiene el formato siguiente:`Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`. Por ejemplo: **Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**
    
    En este archivo de registro, busque la siguiente cadena: **Product: Microsoft Azure Information Protection -- Installation completed successfully.**

### <a name="additional-instructions-for-office-2010-only"></a>Instrucciones adicionales solo para Office 2010

Si instala el cliente para usuarios que tienen Office 2010 y no tienen permisos administrativos locales, especifique el parámetro ServiceLocation y la dirección URL para el servicio Azure Rights Management. El parámetro y el valor permiten crear y establecer las claves del Registro siguientes:

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


## <a name="to-verify-installation-connection-status-or-send-feedback"></a>Para verificar la instalación, el estado de la conexión o enviar comentarios

1. Abra una aplicación de Office y, en la pestaña **Inicio**, en el grupo **Protección**, haga clic en **Proteger** y luego en **Ayuda y comentarios**.

2. En el cuadro de diálogo **Microsoft Azure Information Protection**, anote lo siguiente:

    - En la sección del **estado de cliente**: use el valor de la **versión** para comprobar que la instalación se realizó correctamente. Además, puede ver cuándo el cliente se ha conectado por última vez al servicio de Azure Information Protection de su organización y cuándo la directiva de dicho servicio se ha instalado o actualizado por última vez. Cuando el cliente se conecta al servicio, se descarga automáticamente la directiva más reciente si encuentra cambios con respecto a su directiva actual. Si ha realizado cambios en la directiva con posterioridad al tiempo mostrado, cierre y vuelva a abrir la aplicación de Office.
    
        También puede ver el nombre de usuario mostrado que identifica la cuenta que se usa para autenticarlo en Azure Information Protection. Este nombre de usuario debe coincidir con una cuenta que utilice para Office 365 o Azure Active Directory y que pertenezca a un inquilino que esté configurado para Azure Information Protection.

    - En la sección **Ayuda y comentarios**: el vínculo **Más información** dirige, de forma predeterminada, al sitio web de [Azure Information Protection](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection), pero se puede configurar con una dirección URL personalizada como uno de los valores de [configuración de directivas](../deploy-use/configure-policy-settings.md) en la directiva de Azure Information Protection.
        
        Use el vínculo **Enviar comentarios** para enviar sugerencias o solicitudes al equipo de Information Protection. No utilice esta opción para obtener soporte técnico, pero, en su lugar, vea [Opciones de soporte y recursos de la comunidad](../get-started/information-support.md#support-options-and-community-resources). 
    
        Para obtener información de diagnóstico y restablecer el cliente, haga clic en **Ejecutar diagnósticos**. Al finalizar las pruebas de los diagnósticos, haga clic en **Copiar resultados** para pegar la información en un correo electrónico que puede enviar a su departamento de soporte técnico o al soporte técnico de Microsoft. Cuando finalicen las pruebas, también puede restablecer al cliente.
        
        Más información acerca de la opción **Restablecer**:
        
        - No tiene que ser un administrador local para usar esta opción, y esta acción no se registra en el Visor de eventos. 
        
        - A menos que los archivos estén bloqueados, esta acción elimina todos los archivos de **%localappdata%\Microsoft\MSIPC**, que es donde se almacenan las plantillas de certificados de cliente y administración de derechos. No se elimina la directiva de Azure Information Protection, ni los archivos de registro de cliente, ni se cierra la sesión del usuario.
        
        - La clave de registro y las configuraciones siguientes se eliminan: **HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC**. Si establece la configuración de esta clave del registro (por ejemplo, configuración de redireccionamiento para el inquilino de Azure Information Protection porque ya está migrando de AD RMS y aún tiene un punto de conexión de servicio en la red), debe volver a configurar la configuración del registro después de restablecer al cliente.
        
        - Después de restablecer al cliente, debe volver a inicializar el entorno de usuario (también conocido como "arranque"), con lo cual se descargarán los certificados para el cliente y las plantillas más recientes. Para ello, cierre todas las instancias de Office y, después, reinicie una aplicación de Office. Esta acción también comprobará que ha descargado la directiva de Azure Information Protection más reciente. No vuelva a ejecutar las pruebas de diagnóstico hasta que haya realizado esta acción.


## <a name="next-steps"></a>Pasos siguientes
Ahora que ha instalado el cliente de Azure Information Protection, vea la siguiente información adicional que puede necesitar para la compatibilidad con este cliente:

- [Archivos de cliente y registro de uso](client-admin-guide-files-and-logging.md)

- [Seguimiento de documentos](client-admin-guide-document-tracking.md)

- [Tipos de archivos admitidos](client-admin-guide-file-types.md)

- [Comandos de PowerShell](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]

