---
title: "Guía del administrador de cliente de Azure Information Protection"
description: "Instrucciones e información para administradores de una red empresarial que son responsables de implementar el cliente de Azure Information Protection para Windows."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/25/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 33a5982f-7125-4031-92c2-05daf760ced1
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 9359d83ec2ee85edeef6a3d2680f95633d22546e
ms.sourcegitcommit: 7bec3dfe3ce61793a33d53691046c5b2bdba3fb9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/27/2017
---
# <a name="azure-information-protection-client-administrator-guide"></a>Guía para administradores del cliente de Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Use la información que aparece en esta guía si es el responsable del cliente de Azure Information Protection en una red empresarial o si desea obtener más información técnica de la contenida en la [Guía del usuario de Azure Information Protection](client-user-guide.md). 

Por ejemplo:

- Descripción de los distintos componentes de este cliente y si debe instalarlo

- Instalación del cliente para los usuarios, con información sobre requisitos previos, opciones y parámetros de instalación, y comprobaciones

- Adaptación de las configuraciones personalizadas que a menudo requieren editar el registro

- Ubicación de los archivos de cliente y los registros de uso

- Identificación de los tipos de archivo compatibles con el cliente

- Configuración y uso del sitio de seguimiento de documentos para los usuarios

- Uso del cliente con PowerShell para control de la línea de comandos

**¿Tiene alguna pregunta que no se trata en esta documentación?** Visite el [sitio de Yammer sobre Azure Information Protection](https://www.yammer.com/AskIPTeam). 

## <a name="technical-overview-of-the-azure-information-protection-client"></a>Información general técnica sobre el cliente de Azure Information Protection

El cliente de Azure Information Protection incluye:

- Un complemento de Office, que instala la barra de Azure Information Protection para que los usuarios seleccionen etiquetas de clasificación y un botón **proteger** en la cinta para ofrecer otras opciones.

- Explorador de archivos de Windows, opciones de menú contextual para que los usuarios apliquen etiquetas de clasificación y la protección de los archivos.

- Un visor para mostrar los archivos protegidos cuando una aplicación nativa no puede abrirlo.

- Un módulo de PowerShell para aplicar y quitar etiquetas de clasificación y protección en los archivos.

- El cliente de Rights Management que se comunica con Azure Rights Management (Azure RMS) o Active Directory Rights Management Services (AD RMS).

El cliente de Azure Information Protection resulta ideal para trabajar con sus servicios de Azure; Azure Information Protection y su servicio de protección de datos, Azure Rights Management. Sin embargo, con algunas limitaciones, el cliente de Azure Information Protection también funciona con la versión local de Rights Management, AD RMS. Para ver una comparación exhaustiva de las características que admiten Azure Information Protection y AD RMS, consulte [Comparación entre Azure Information Protection y AD RMS](../understand-explore/compare-azure-rms-ad-rms.md). 

Si tiene AD RMS y quiere migrar a Azure Information Protection, consulte [Migración desde AD RMS a Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).


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

![Barra de Azure Information Protection con la directiva predeterminada](../media/word2016-calloutsv2.png)

## <a name="how-to-install-the-azure-information-protection-client-for-users"></a>Instalación del cliente de Azure Information Protection para los usuarios

Antes de instalar el cliente, compruebe que los equipos tienen las versiones necesarias de sistema operativo y aplicaciones para el cliente de Azure Information Protection: [Requisitos para Azure Information Protection](../get-started/requirements-azure-rms.md). 

Luego, compruebe los requisitos previos adicionales que puede necesitar el cliente de Azure Information Protection.

### <a name="additional-prerequisites-for-the-azure-information-protection-client"></a>Requisitos previos adicionales para el cliente de Azure Information Protection

- Microsoft .NET Framework 4.6.2
    
    De forma predeterminada, la instalación completa del cliente de Azure Information Protection requiere una versión mínima de Microsoft .NET Framework 4.6.2 y, en su defecto, el instalador intenta descargar e instalar este requisito previo. Cuando este requisito previo se instala como parte de la instalación de cliente, es necesario reiniciar el equipo. Aunque no se recomienda, puede omitir este requisito previo con un [parámetro de instalación personalizada](#more-information-about-the-downgradedotnetrequirement-installation-parameter).

- Microsoft .NET Framework 4.5.2
    
    Si el visor de Azure Information Protection se instala por separado, se requiere una versión mínima de Microsoft .NET Framework 4.5.2 y, en su defecto, el instalador no lo descarga ni lo instala.

- Windows PowerShell versión 4.0
    
    El módulo de PowerShell para el cliente requiere Windows PowerShell versión 4.0, que quizá deba instalarse en sistemas operativos anteriores. Para obtener más información consulte [How to Install Windows PowerShell 4.0](http://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx) (Instalación de Windows PowerShell 4.0). El instalador no comprueba ni instala este requisito previo para usted. Para confirmar la versión de Windows PowerShell que ejecuta, escriba `$PSVersionTable` en una sesión de PowerShell.

- Microsoft Online Services - Ayudante para el inicio de sesión 7.250.4303.0
    
    Los equipos que ejecutan Office 2010 requiere Microsoft Online Services - Ayudante para el inicio de sesión versión 7.250.4303.0. Esta versión está incluida en la instalación del cliente. Si tiene una versión posterior del Asistente para el inicio de sesión, desinstálela antes de instalar el cliente de Azure Information Protection. Por ejemplo, compruebe la versión y desinstale el Asistente para el inicio de sesión en **Panel de control** > **Programas y características** > **Desinstalar o cambiar un programa**.

- KB 2533623
    
    Los equipos que ejecutan Windows 7 Service Pack 1 requieren KB 2533623. Para más información sobre esta actualización, consulte [Aviso de seguridad de Microsoft: la carga de una biblioteca no segura podría permitir la ejecución remota de código](https://support.microsoft.com/en-us/kb/2533623). Es posible que tenga que instalar directamente esta actualización o podría reemplazarla otra actualización que la instale por usted.
    
    Si la actualización es necesaria y no está instalada, la instalación del cliente mostrará una advertencia que lo señale. Esta actualización se puede instalar después de instalar el cliente, pero algunas acciones estarán bloqueadas y se volverá a mostrar el mensaje.  

- No deshabilite el complemento **Microsoft Azure Information Protection** para las aplicaciones de Office.
    
    Si ha configurado la opción de directivas de grupo **Lista de complementos administrados**, agregue el complemento Microsoft Azure Information Protection para aplicaciones de Office especificando los siguientes identificadores programáticos (ProgID) para Azure Information Protection y establezca la opción en **1: El complemento siempre está habilitado**.
    
    - Para Outlook: `MSIP.OutlookAddin`
    
    - Para Word: `MSIP.WordAddin`
    
    - Para Excel:`MSIP.ExcelAddin`
    
    - Para PowerPoint: `MSIP.PowerPointAddin`
    
    Incluso si no ha configurado esta opción de directiva de grupo **Lista de complementos administrados**, puede que necesite configurarla si recibe algún informe en el que se indique que el complemento de Microsoft Azure Information Protection se va a deshabilitar. Al deshabilitar este complemento, los usuarios no verán la barra de Azure Information Protection en la aplicación de Office.
    
    Para obtener más información sobre esta configuración de directiva de grupo, consulte [No Add-ins loaded due to group policy settings for Office 2013 and Office 2016 programs](https://support.microsoft.com/help/2733070/no-add-ins-loaded-due-to-group-policy-settings-for-office-2013-and-off) (No se ha cargado ningún complemento debido a la configuración de directivas de grupo para Office 2013 y Office 2016).

> [!IMPORTANT]
> La instalación del cliente de Azure Information Protection requiere permisos administrativos locales.


### <a name="options-to-install-the-azure-information-protection-client-for-users"></a>Opciones para instalar el cliente de Azure Information Protection para los usuarios

Hay tres opciones de instalación del cliente para los usuarios:

**Windows Update**: el cliente de Azure Information Protection se incluye en el catálogo de Microsoft Update, para que pueda instalar y actualizar este cliente mediante el uso de cualquier servicio de actualización de software que use el catálogo.

**Ejecutar la versión ejecutable (.exe) del cliente**: el método de instalación recomendado que se puede ejecutar de manera interactiva o silenciosa. Este método es el más flexible y se recomienda porque el instalador comprueba muchos de los requisitos previos y puede instalar automática los requisitos previos que faltan. [Instrucciones](#to-install-the-azure-information-protection-client-by-using-the-executable-installer)

**Implementación de la versión de Windows Installer (.msi) del cliente**: compatible solo con instalaciones silenciosas que usan un mecanismo de implementación central, como directiva de grupo, Configuration Manager y Microsoft Intune. Este método es necesario para los equipos con Windows 10 administrados mediante Intune y administración de dispositivos móviles (MDM) porque, en estos equipos, no se admiten los archivos ejecutables para la instalación. Sin embargo, cuando usa este método de instalación debe comprobar manualmente e instalar o desinstalar el software dependiente que el instalador del ejecutable realizaría para cada equipo. [Instrucciones](#to-install-the-azure-information-protection-client-by-using-the-msi-installer)

### <a name="to-install-the-azure-information-protection-client-by-using-the-executable-installer"></a>Para instalar el cliente de Azure Information Protection con el instalador ejecutable

Use las instrucciones siguientes para instalar el cliente cuando no usa el catálogo de Microsoft Update ni implementa el archivo .msi mediante un método de implementación central, como Intune.

1. Descargue la versión ejecutable del cliente de Azure Information Protection del [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 
    
    Si hay una versión preliminar disponible, manténgala solo para pruebas. No está diseñada para usuarios finales en un entorno de producción. 

2. En una instalación predeterminada, simplemente ejecute el archivo ejecutable, por ejemplo, **AzInfoProtection.exe**. No obstante, para ver las opciones de instalación, primero ejecute el archivo ejecutable con **/help**: `AzInfoProtection.exe /help`

    Ejemplo para instalar el cliente de forma silenciosa: `AzInfoProtection.exe /quiet`
    
    Ejemplo para instalar de forma silenciosa solo los cmdlets de PowerShell: `AzInfoProtection.exe  PowerShellOnly=true /quiet`
    
    Parámetros adicionales que no aparecen en la pantalla de ayuda:
    
    - **ServiceLocation**: Utilice este parámetro si va a instalar el cliente en equipos que ejecutan Office 2010 y los usuarios no son administradores locales en sus equipos o no quiere que se les pregunte. [Más información](#more-information-about-the-servicelocation-installation-parameter). 
    
    - **DowngradeDotNetRequirement**: Utilice este parámetro para omitir el requisito de .NET Framework de Microsoft versión 4.6.2. [Más información](#more-information-about-the-downgradedotnetrequirement-installation-parameter).
    
    - **AllowTelemetry=0**: utilice este parámetro para deshabilitar la opción de instalación **Enviar estadísticas de uso a Microsoft para ayudar a mejorar Azure Information Protection**. 
    
3. Si va a realizar la instalación de forma interactiva, seleccione la opción para instalar una **directiva de demostración**, si no puede conectarse a Office 365 o Azure Active Directory, pero quiere ver y experimentar el lado cliente de Azure Information Protection mediante una directiva local con fines de demostración. Cuando el cliente se conecta a un servicio de Azure Information Protection, esta directiva de demostración se reemplaza por la directiva de Azure Information Protection de su organización.
    
4. Para completar la instalación: 

    - Si su equipo ejecuta Office 2010, reinicie el equipo. 
        
        Si el cliente no se ha instalado con el parámetro ServiceLocation, la primera vez que abre una de las aplicaciones de Office que usan la barra de Azure Information Protection (por ejemplo, Word), debe confirmar las solicitudes de actualización del registro para la primera vez que se usa. La [detección de servicios](../rms-client/client-deployment-notes.md#rms-service-discovery) se usa para rellenar las claves del Registro. 
    
    - Para otras versiones de Office, reinicie todas las aplicaciones de Office y todas las instancias del Explorador de archivos. 
        
5. Puede confirmar que la instalación se completó correctamente consultando el archivo de registro de la instalación, que se crea de forma predeterminada en la carpeta %temp%. Puede cambiar esta ubicación con el parámetro de instalación **/log** . 
 
    Este archivo tiene el formato de nomenclatura siguiente: `Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`.
    
    Por ejemplo: **Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**
    
    En este archivo de registro, busque la siguiente cadena: **Product: Microsoft Azure Information Protection -- Installation completed successfully.** Si se produce un error en la instalación, este archivo de registro contiene detalles que le ayudarán a identificar y resolver los problemas.

#### <a name="more-information-about-the-servicelocation-installation-parameter"></a>Más información sobre el parámetro de instalación ServiceLocation

Si instala el cliente para usuarios que tienen Office 2010 y no tienen permisos administrativos locales, especifique el parámetro ServiceLocation y la dirección URL para el servicio Azure Rights Management. El parámetro y el valor permiten crear y establecer las claves del Registro siguientes:

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

Utilice el procedimiento siguiente para identificar el valor que se especificará para el parámetro ServiceLocation. 

##### <a name="to-identify-the-value-to-specify-for-the-servicelocation-parameter"></a>Para identificar el valor que se especificará para el parámetro ServiceLocation

1. Desde una sesión de PowerShell, ejecute [Connect-AadrmService](https://docs.microsoft.com/powershell/aadrm/vlatest/connect-aadrmservice) y especifique sus credenciales de administrador para conectarse al servicio de Azure Rights Management. Ejecute a continuación [Get-AadrmConfiguration](https://docs.microsoft.com/powershell/aadrm/vlatest/get-aadrmconfiguration). 
 
    Si aún no ha instalado el módulo de PowerShell para el servicio Azure Rights Management, consulte [Instalación de Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md).

2. En la salida, identifique el valor **LicensingIntranetDistributionPointUrl** .

    Por ejemplo: **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. En el valor, quite **/_wmcs/licensing** de esta cadena. Por ejemplo: **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**.

    La cadena restante es el valor que se especificará para el parámetro ServiceLocation.

Ejemplo para instalar el cliente de Office 2010 y Azure RMS de forma silenciosa: `AzInfoProtection.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


#### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>Más información sobre el parámetro de instalación DowngradeDotNetRequirement

Para admitir actualizaciones automáticas mediante Windows Update y para la integración confiable con aplicaciones de Office, el cliente de Azure Information Protection usa Microsoft .NET Framework versión 4.6.2. De forma predeterminada, la instalación busca esta versión e intenta instalarla si no está. A continuación, la instalación requiere el reinicio del equipo.

Si la instalación de esta versión posterior de Microsoft .NET Framework no resulta práctica, puede instalar el cliente con el parámetro y valor **DowngradeDotNetRequirement = True**, que omite este requisito si está instalado Microsoft .NET Framework versión 4.5.1.

Por ejemplo: `AzInfoProtection.exe DowngradeDotNetRequirement=True`

Se recomienda utilizar este parámetro con precaución y sabiendo que se ha informado de problemas relacionados con el bloqueo de aplicaciones de Office cuando se utiliza el cliente de Azure Information Protection con esta versión anterior de Microsoft .NET Framework. Si experimenta problemas de bloqueo, actualice a la versión recomendada antes de intentar otros tipos de solución de problemas. 

Recuerde también que, si usa Windows Update para mantener actualizado el cliente de Azure Information Protection, necesita otro mecanismo de implementación de software para actualizar el cliente a versiones posteriores.

### <a name="to-install-the-azure-information-protection-client-by-using-the-msi-installer"></a>Para instalar el cliente de Azure Information Protection con el instalador .msi

Para la implementación central, use la información siguiente que es específica para la versión de instalación de .msi del cliente de Azure Information Protection. 

Si usa Intune como el método de implementación de software, use estas instrucciones junto con [Agregar aplicaciones con Microsoft Intune](/intune/deploy-use/add-apps).

1. Descargue la versión .msi del cliente de Azure Information Protection del [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 
    
    Si hay una versión preliminar disponible, manténgala solo para pruebas. No está diseñada para usuarios finales en un entorno de producción. 

2. Para cada equipo que ejecute el archivo .msi, debe asegurarse de que estén implementadas las siguientes dependencias de software. Por ejemplo, empaquételas con la versión .msi del cliente o solo impleméntelas en equipos que cumplan con estas dependencias:
    
    |Versión de Office|Sistema operativo|Software|Acción|
    |--------------------|--------------|----------------|---------------------|
    |Office 2013|Todas las versiones compatibles|[KB 3054941](https://www.microsoft.com/en-us/download/details.aspx?id=49337)<br /><br /> Número de versión incluido en el nombre de archivo: v3|Instalar|
    |Office 2010|Todas las versiones compatibles|[Microsoft Online Services - Ayudante para el inicio de sesión](https://www.microsoft.com/en-us/download/details.aspx?id=28177)<br /><br /> Versión: 2.1|Instalar|
    |Office 2010|Windows 8.1 y Windows Server 2012 R2|[KB 2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> Número de versión incluido en el nombre de archivo: v3|Se debe instalar si no están instalados KB 2843630 ni KB 2919355|
    |Office 2010|Windows 8 y Windows Server 2012|[KB 2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> Número de versión incluido en el nombre de archivo: v3|Instalar|
    |Office 2010|Windows 7|[KB 2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41709)<br /><br /> Número de versión incluido en el nombre de archivo: v3|Se debe instalar si no está instalado KB 3125574|
    |No aplicable|Windows 7|KB 2627273 <br /><br /> Número de versión incluido en el nombre de archivo: v4|Desinstalar|

3. Para una instalación predeterminada, ejecute .msi con **/quiet**, por ejemplo, `AzInfoProtection.msi /quiet`. Sin embargo, es posible que tenga que especificar parámetros de instalación adicionales que están documentados en las [instrucciones del instalador ejecutable](#to-install-the-azure-information-protection-client-by-using-the-executable-installer).  

## <a name="additional-checks-and-troubleshooting"></a>Comprobaciones adicionales y solución de problemas

Utilice la opción **Ayuda y comentarios** para abrir el cuadro de diálogo **Microsoft Azure Information Protection**:

- Desde una aplicación de Office: En la pestaña **Inicio**, en el grupo **Protección**, seleccione **Proteger** y luego **Ayuda y comentarios**.

- Desde el Explorador de archivos: Mediante el botón derecho, seleccione uno o varios archivos o una carpeta, elija **Clasificar y proteger** y luego seleccione **Ayuda y comentarios**. 

### <a name="help-and-feedback-section"></a>Sección **Ayuda y comentarios**

El vínculo **Más información** dirige, de forma predeterminada, al sitio web de [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection), pero lo puede configurar con una dirección URL personalizada como uno de los valores de [configuración de directivas](../deploy-use/configure-policy-settings.md) en la directiva de Azure Information Protection.

Use el vínculo **Envíenos sus comentarios** para enviar sugerencias o solicitudes al equipo de Information Protection. No utilice esta opción para obtener soporte técnico, pero, en su lugar, vea [Opciones de soporte y recursos de la comunidad](../get-started/information-support.md#support-options-and-community-resources). 

La opción **Exportar registros** se utiliza para recopilar y adjuntar archivos de registro para el cliente de Azure Information Protection si se le ha pedido que los envíe al soporte técnico de Microsoft. Los usuarios finales también puede utilizar esta opción para enviar estos archivos de registro a su departamento de soporte técnico.

Para información de diagnóstico y restablecer el cliente, seleccione **Ejecutar diagnósticos**. Al finalizar las pruebas de los diagnósticos, haga clic en **Copiar resultados** para pegar la información en un correo electrónico que puede enviar al soporte técnico de Microsoft; asimismo, los usuarios finales pueden enviarla a su departamento de soporte técnico. Cuando finalicen las pruebas, también puede restablecer al cliente.

> [!NOTE]
> En la versión preliminar del cliente, se quitó la opción **Ejecutar diagnóstico** y se reemplazó por **Restablecer configuración**. Además, el comportamiento de esta opción ha [cambiado](#more-information-about-the-reset-option-for-the-current-preview-version-of-the-azure-information-protection-client).

#### <a name="more-information-about-the-reset-option-for-the-general-availability-ga-version-of-the-azure-information-protection-client"></a>Más información acerca de la opción de restablecimiento de la versión de disponibilidad general (GA) del cliente de Azure Information Protection

- No tiene que ser un administrador local para usar esta opción, y esta acción no se registra en el Visor de eventos. 

- A menos que los archivos estén bloqueados, esta acción elimina todos los archivos de **%LocalAppData%\Microsoft\MSIPC**, que es donde se almacenan los certificados de cliente y las plantillas de Rights Management. No se elimina la directiva de Azure Information Protection, ni los archivos de registro de cliente, ni se cierra la sesión del usuario.

- La clave de registro y las configuraciones siguientes se eliminan: **HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC**. Si ha establecido la configuración de esta clave del Registro, tiene que volver a configurarla después de restablecer el cliente. Por ejemplo, ha establecido la configuración de redireccionamiento para el inquilino de Azure Information Protection porque ya está migrando de AD RMS y aún tiene un punto de conexión de servicio en la red.

- Después de restablecer el cliente, debe volver a inicializar el entorno de usuario, con lo cual se descargarán los certificados para el cliente y las plantillas más recientes. Para ello, cierre todas las instancias de Office y, después, reinicie una aplicación de Office. Esta acción también comprueba que haya descargado la directiva de Azure Information Protection más reciente. No vuelva a ejecutar las pruebas de diagnóstico hasta que haya realizado esta acción.

#### <a name="more-information-about-the-reset-option-for-the-current-preview-version-of-the-azure-information-protection-client"></a>Más información acerca de la opción de restablecimiento de la versión preliminar actual del cliente de Azure Information Protection

- No tiene que ser un administrador local para usar esta opción, y esta acción no se registra en el Visor de eventos. 

- A menos que los archivos estén bloqueados, esta acción elimina todos los archivos de las siguientes ubicaciones. Estos archivos incluyen certificados de cliente, plantillas de Rights Management, la directiva de Azure Information Protection y las credenciales de usuario almacenadas en caché. Los archivos de registro del cliente no se eliminan.
    
    - %LocalAppData%\Microsoft\DRM
    
    - %LocalAppData%\Microsoft\MSIPC
    
    - %LocalAppData%\Microsoft\MSIP\Policy.msip
    
    - %LocalAppData%\Microsoft\MSIP\TokenCache

- La configuración y las claves del Registro siguientes se eliminan. Si estableció la configuración de alguna de estas claves del Registro, deberá volver a configurarlas después de restablecer el cliente. Por ejemplo, estableció la configuración de redireccionamiento al inquilino de Azure Information Protection porque ya está migrando de AD RMS y aún tiene un punto de conexión de servicio en la red:
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\15.0\Common\Identity
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\15.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\16.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Classes\Local Settings\Software\Microsoft\MSIPC    

- Se cerrará la sesión del usuario que tiene iniciada una sesión actualmente.

### <a name="client-status-section"></a>Sección **Estado del cliente**

Utilice el valor **Conectado como** para confirmar que el nombre de usuario mostrado identifica la cuenta que se va a utilizar para la autenticación de Azure Information Protection. Este nombre de usuario debe coincidir con una cuenta que se usa para Office 365 o Azure Active Directory. La cuenta también debe pertenecer a un inquilino que esté configurado para Azure Information Protection.

Si necesita iniciar sesión como un usuario diferente al que se muestra, consulte la personalización [Inicio de sesión como un usuario diferente](client-admin-guide-customizations.md#sign-in-as-a-different-user).

El valor de **Última conexión** muestra cuándo se ha conectado por última vez el cliente al servicio de Azure Information Protection de su organización. Puede utilizar esta información con la **directiva de Information Protection que se haya instalado en** una fecha y una hora concretas para confirmar la última vez que se ha instalado o actualizado la directiva de Azure Information Protection. Cuando el cliente se conecta al servicio, se descarga automáticamente la directiva más reciente si encuentra cambios con respecto a su directiva actual, y también cada 24 horas. Si ha realizado cambios en la directiva con posterioridad al tiempo mostrado, cierre y vuelva a abrir la aplicación de Office.

Si ve **Este cliente no tiene licencia de Office Professional Plus**, significa que el cliente de Azure Information Protection ha detectado que la edición instalada de Office no admite la aplicación de la protección de Rights Management. Cuando se realiza esta detección, las etiquetas que aplican protección no se muestran en la barra de Azure Information Protection.

Utilice la información de **Versión** para confirmar qué versión del cliente está instalada. Puede comprobar si se trata de versión más reciente, así como las correcciones correspondientes y las nuevas características haciendo clic en el vínculo **Novedades** para leer el [historial de versiones](client-version-release-history.md) del cliente.

## <a name="support-for-multiple-languages"></a>Compatibilidad con varios idiomas

El cliente de Azure Information Protection admite todos los idiomas que incluye Office. Por ejemplo, las opciones del menú, los cuadros de diálogo y los mensajes se muestran en el idioma del usuario. Hay un instalador único que detecta el idioma, por lo que no necesita realizar ninguna configuración adicional para instalar el cliente en distintos idiomas. 

Sin embargo, los nombres de las etiquetas que ven los usuarios no se traducen automáticamente, ni en el caso de la [directiva predeterminada](../deploy-use/configure-policy-default.md) ni en el de los nombres de etiquetas que especifique. Para que los usuarios puedan ver las etiquetas en varios idiomas, debe proporcionar sus propias traducciones y configurar la directiva de Azure Information Protection para que use dichas traducciones. Para obtener más información, consulte [Configuración de etiquetas para distintos idiomas en Azure Information Protection](../deploy-use/configure-policy-languages.md).

## <a name="to-uninstall-the-azure-information-protection-client"></a>Para desinstalar el cliente de Azure Information Protection

Puede usar una de estas opciones:

- Utilice el Panel de Control para desinstalar un programa: haga clic en **Microsoft Azure Information Protection** > **Desinstalar**

- Vuelva a ejecutar el archivo ejecutable (por ejemplo, **AzInfoProtection.exe**) y, en la página, **Modificar instalación**, haga clic en **Desinstalar**. 

- Ejecute el archivo ejecutable con **/uninstall**. Por ejemplo: `AzInfoProtection.exe /uninstall`

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha instalado el cliente de Azure Information Protection, vea la siguiente información adicional que puede necesitar para la compatibilidad con este cliente:

- [Customizations](client-admin-guide-customizations.md) (Personalizaciones)

- [Archivos de cliente y registro de uso](client-admin-guide-files-and-logging.md)

- [Seguimiento de documentos](client-admin-guide-document-tracking.md)

- [Tipos de archivos admitidos](client-admin-guide-file-types.md)

- [Comandos de PowerShell](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
