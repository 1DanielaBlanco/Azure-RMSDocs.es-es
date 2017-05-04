---
title: "Guía del administrador de cliente de Azure Information Protection"
description: "Instrucciones e información para administradores de una red empresarial que son responsables de implementar el cliente de Azure Information Protection para Windows."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/26/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 74abbe0db07a155afe500388810945a3ff5a35a5
ms.sourcegitcommit: 3ff6c072a228994308402778c493727cc682c6b7
translationtype: HT
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

El cliente de Azure Information Protection resulta ideal para trabajar con sus servicios de Azure; Azure Information Protection y su servicio de protección de datos, Azure Rights Management. Sin embargo, con algunas limitaciones, el cliente de Azure Information Protection también funciona con la versión local de Rights Management, AD RMS. Para ver una comparación exhaustiva de las características que admiten Azure Information Protection y AD RMS, consulte [Comparación entre Azure Information Protection y AD RMS](../understand-explore/compare-azure-rms-ad-rms.md). 

Si tiene AD RMS y quiere migrar a Azure Information Protection, consulte [Migración desde AD RMS a Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

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

![Barra de Azure Information Protection con la directiva predeterminada](../media/word2016-calloutsv2.png)

## <a name="how-to-install-the-azure-information-protection-client-for-users"></a>Instalación del cliente de Azure Information Protection para los usuarios

Antes de instalar el cliente, compruebe que tiene las versiones necesarias de sistema operativo y aplicaciones para el cliente de Azure Information Protection: [Requisitos para Azure Information Protection](../get-started/requirements-azure-rms.md). 

Requisitos previos adicionales para el cliente de Azure Information Protection:

- De forma predeterminada, la instalación completa del cliente de Azure Information Protection requiere una versión mínima de Microsoft .NET Framework 4.6.2 y, en su defecto, el instalador intenta descargar e instalar este requisito previo. Cuando este requisito previo se instala como parte de la instalación de cliente, es necesario reiniciar el equipo. Aunque no se recomienda, puede omitir este requisito previo con un parámetro de instalación personalizada.

- Si el visor de Azure Information Protection se instala por separado, se requiere una versión mínima de Microsoft .NET Framework 4.5.2 y, en su defecto, el instalador no lo descarga ni lo instala.

- El módulo de PowerShell requiere Windows PowerShell versión 4.0, que quizá deba instalarse en sistemas operativos anteriores. Para obtener más información consulte [How to Install Windows PowerShell 4.0](http://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx) (Instalación de Windows PowerShell 4.0). El instalador no comprueba ni instala este requisito previo para usted. Para confirmar la versión de Windows PowerShell que ejecuta, escriba **$PSVersionTable** en una sesión de PowerShell.

- Los equipos que ejecutan Windows 7 Service Pack 1 requieren KB 2533623. Para más información sobre esta actualización, consulte [Aviso de seguridad de Microsoft: la carga de una biblioteca no segura podría permitir la ejecución remota de código](https://support.microsoft.com/en-us/kb/2533623). Es posible que tenga que instalar directamente esta actualización o podría reemplazarla otra actualización que la instale por usted.
    
    Si la actualización es necesaria y no está instalada, la instalación del cliente mostrará una advertencia que lo señale. Esta actualización se puede instalar después de instalar el cliente, pero algunas acciones estarán bloqueadas y se volverá a mostrar el mensaje.  

> [!NOTE]
> La instalación requiere permisos administrativos locales.

El cliente de Azure Information Protection también se incluye en el catálogo de Microsoft Update, para que pueda instalar y actualizar al cliente mediante el uso de cualquier servicio de actualización de software que use el catálogo. 

1. Descargue el cliente de Azure Information Protection del [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 
    
    Si hay una versión preliminar disponible, manténgala solo para pruebas. No está diseñada para usuarios finales en un entorno de producción. 

2. En una instalación predeterminada, simplemente ejecute el archivo ejecutable, por ejemplo, **AzInfoProtection.exe**. No obstante, para ver las opciones de instalación, primero ejecute el archivo ejecutable con **/help**: `AzInfoProtection.exe /help`

    Ejemplo para instalar el cliente de forma silenciosa: `AzInfoProtection.exe /quiet`
    
    Ejemplo para instalar de forma silenciosa solo los cmdlets de PowerShell: `AzInfoProtection.exe  PowerShellOnly=true /quiet`
    
    Parámetros adicionales que no aparecen en la pantalla de ayuda:
    
    - **ServiceLocation**: Utilice este parámetro si va a instalar el cliente en equipos que ejecutan Office 2010 y los usuarios no son administradores locales en sus equipos o no quiere que se les pregunte. [Más información](#more-information-about-the-servicelocation-installation-parameter). 
    
    - **DowngradeDotNetRequirement**: Utilice este parámetro para omitir el requisito de .NET Framework de Microsoft versión 4.6.2. [Más información](#more-information-about-the-downgradedotnetrequirement-installation-parameter).

3. Si va a realizar la instalación de forma interactiva, seleccione la opción para instalar una **directiva de demostración**, si no puede conectarse a Office 365 o Azure Active Directory, pero quiere ver y experimentar el lado cliente de Azure Information Protection mediante una directiva local con fines de demostración. Cuando el cliente se conecta a un servicio de Azure Information Protection, esta directiva de demostración se reemplaza por la directiva de Azure Information Protection de su organización.
    
4. Para completar la instalación: 

    - Si su equipo ejecuta Office 2010, reinicie el equipo. 
        
        Si el cliente no se ha instalado con el parámetro ServiceLocation, la primera vez que abre una de las aplicaciones de Office que usan la barra de Azure Information Protection (por ejemplo, Word), debe confirmar las solicitudes de actualización del registro para la primera vez que se usa. La [detección de servicios](../rms-client/client-deployment-notes.md#rms-service-discovery) se usa para rellenar las claves del Registro. 
    
    - Para otras versiones de Office, reinicie todas las aplicaciones de Office y todas las instancias del Explorador de archivos. 
        
5. Puede confirmar que la instalación se completó correctamente consultando el archivo de registro de la instalación, que se crea de forma predeterminada en la carpeta %temp%. Puede cambiar esta ubicación con el parámetro de instalación **/log** . 
 
    Este archivo tiene el formato de nomenclatura siguiente: `Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`.
    
    Por ejemplo: **Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**
    
    En este archivo de registro, busque la siguiente cadena: **Product: Microsoft Azure Information Protection -- Installation completed successfully.** Si se produce un error en la instalación, este archivo de registro contiene detalles que le ayudarán a identificar y resolver los problemas.

### <a name="more-information-about-the-servicelocation-installation-parameter"></a>Más información sobre el parámetro de instalación ServiceLocation

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


### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>Más información sobre el parámetro de instalación DowngradeDotNetRequirement

Para admitir actualizaciones automáticas mediante Windows Update y para la integración confiable con aplicaciones de Office, el cliente de Azure Information Protection usa Microsoft .NET Framework versión 4.6.2. De forma predeterminada, la instalación busca esta versión e intenta instalarla si no está. A continuación, la instalación requerirá el reinicio del equipo.

Si la instalación de esta versión posterior de Microsoft .NET Framework no resulta práctica, puede instalar el cliente con el parámetro y valor **DowngradeDotNetRequirement = True**, que omite este requisito si está instalado Microsoft .NET Framework versión 4.5.1.

Por ejemplo: `AzInfoProtection.exe DowngradeDotNetRequirement=True`

Se recomienda utilizar este parámetro con precaución y sabiendo que se ha informado de problemas relacionados con el bloqueo de aplicaciones de Office cuando se utiliza el cliente de Azure Information Protection con esta versión anterior de Microsoft .NET Framework. Si experimenta problemas de bloqueo, actualice a la versión recomendada antes de intentar otros tipos de solución de problemas. 

Recuerde también que si usa Windows Update para mantener actualiza el cliente de Azure Information Protection, necesitará otro mecanismo de implementación de software para actualizar el cliente a versiones posteriores.

## <a name="additional-checks-and-troubleshooting"></a>Comprobaciones adicionales y solución de problemas

Utilice la opción **Ayuda y comentarios** para abrir el cuadro de diálogo **Microsoft Azure Information Protection**:

- Desde una aplicación de Office: En la pestaña **Inicio**, en el grupo **Protección**, seleccione **Proteger** y luego **Ayuda y comentarios**.

- Desde el Explorador de archivos: Mediante el botón derecho, seleccione uno o varios archivos o una carpeta, elija **Clasificar y proteger** y luego seleccione **Ayuda y comentarios**. 

### <a name="help-and-feedback-section"></a>Sección **Ayuda y comentarios**

El vínculo **Más información** dirige, de forma predeterminada, al sitio web de [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection), pero se puede configurar con una dirección URL personalizada como uno de los valores de [configuración de directivas](../deploy-use/configure-policy-settings.md) en la directiva de Azure Information Protection.

Use el vínculo **Envíenos sus comentarios** para enviar sugerencias o solicitudes al equipo de Information Protection. No utilice esta opción para obtener soporte técnico, pero, en su lugar, vea [Opciones de soporte y recursos de la comunidad](../get-started/information-support.md#support-options-and-community-resources). 

**Exportar registros** se utiliza para recopilar y adjuntar archivos de registro para el cliente de Azure Information Protection si se le ha pedido que los envíe al soporte técnico de Microsoft. Los usuarios finales también puede utilizar esta opción para enviar estos archivos de registro a su departamento de soporte técnico.

Para información de diagnóstico y restablecer el cliente, seleccione **Ejecutar diagnósticos**. Al finalizar las pruebas de los diagnósticos, haga clic en **Copiar resultados** para pegar la información en un correo electrónico que puede enviar al soporte técnico de Microsoft; asimismo, los usuarios finales pueden enviarla a su departamento de soporte técnico. Cuando finalicen las pruebas, también puede restablecer al cliente.

Más información acerca de la opción **Restablecer**:

- No tiene que ser un administrador local para usar esta opción, y esta acción no se registra en el Visor de eventos. 

- A menos que los archivos estén bloqueados, esta acción elimina todos los archivos de **%localappdata%\Microsoft\MSIPC**, que es donde se almacenan las plantillas de certificados de cliente y administración de derechos. No se elimina la directiva de Azure Information Protection, ni los archivos de registro de cliente, ni se cierra la sesión del usuario.

- La clave de registro y las configuraciones siguientes se eliminan: **HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC**. Si establece la configuración de esta clave del registro (por ejemplo, configuración de redireccionamiento para el inquilino de Azure Information Protection porque ya está migrando de AD RMS y aún tiene un punto de conexión de servicio en la red), debe volver a configurar la configuración del registro después de restablecer al cliente.

- Después de restablecer el cliente, debe volver a inicializar el entorno de usuario, con lo cual se descargarán los certificados para el cliente y las plantillas más recientes. Para ello, cierre todas las instancias de Office y, después, reinicie una aplicación de Office. Esta acción también comprobará que ha descargado la directiva de Azure Information Protection más reciente. No vuelva a ejecutar las pruebas de diagnóstico hasta que haya realizado esta acción.


### <a name="client-status-section"></a>Sección **Estado del cliente**

Utilice el valor **Conectado como** para confirmar que el nombre de usuario mostrado identifica la cuenta que se va a utilizar para la autenticación de Azure Information Protection. Este nombre de usuario debe coincidir con una cuenta usada para Office 365 o Azure Active Directory y que pertenezca a un inquilino que esté configurado para Azure Information Protection.

Si necesita iniciar sesión como un usuario diferente al que se muestra, consulte la sección [Inicio de sesión como un usuario diferente](#sign-in-as-a-different-user) en esta página.

**Última conexión** muestra cuándo el cliente se conectó por última vez al servicio de Azure Information Protection de su organización y se puede utilizar con la fecha y hora de la opción **La directiva de Information Protection se instaló el día**  para confirmar cuándo se instaló o actualizó por última vez la directiva de Azure Information Protection. Cuando el cliente se conecta al servicio, se descarga automáticamente la directiva más reciente si encuentra cambios con respecto a su directiva actual, y también cada 24 horas. Si ha realizado cambios en la directiva con posterioridad al tiempo mostrado, cierre y vuelva a abrir la aplicación de Office.

Si ve **Este cliente no tiene licencia de Office Professional Plus**, significa que el cliente de Azure Information Protection ha detectado que la edición instalada de Office no admite la aplicación de la protección de Rights Management. Cuando se realiza esta detección, las etiquetas que aplican protección no se muestran en la barra de Azure Information Protection.

Utilice la información de **Versión** para confirmar qué versión del cliente está instalada. Puede comprobar si se trata de versión más reciente, así como las correcciones correspondientes y las nuevas características haciendo clic en el vínculo **Novedades** para leer el [historial de versiones](client-version-release-history.md) del cliente.

## <a name="custom-configurations"></a>Configuraciones personalizadas

Utilice la siguiente información para configuraciones avanzadas que podría necesitar para escenarios específicos o un subconjunto de usuarios. 

### <a name="prevent-sign-in-prompts-for-ad-rms-only-computers"></a>Evitar solicitudes de inicio de sesión solo para equipos AD RMS

De forma predeterminada, el cliente de Azure Information Protection intenta conectarse automáticamente al servicio Azure Information Protection. Para equipos que solo se comunican con AD RMS, esto puede producir una solicitud de inicio de sesión para los usuarios que no es necesaria. Se puede evitar esta solicitud de inicio de sesión modificando el registro:

Busque el siguiente nombre de valor y después establezca los datos del valor en **0**:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Independientemente de esta configuración, el cliente de Azure Information Protection sigue el [proceso de detección del servicio de RMS](../rms-client/client-deployment-notes.md#rms-service-discovery) estándar para buscar su clúster de AD RMS.

### <a name="sign-in-as-a-different-user"></a>Inicio de sesión como un usuario diferente

En un entorno de producción, los usuarios normalmente no necesitarán iniciar sesión como un usuario diferente cuando estén utilizando el cliente de Azure Information Protection. Sin embargo, tendrá que hacerlo como administrador si tiene varios inquilinos. Por ejemplo, en caso de que tenga un inquilino de prueba además del inquilino de Office 365 o Azure que usa la organización.

Puede comprobar con qué cuenta ha iniciado sesión en el cuadro de diálogo **Microsoft Azure Information Protection**: abra una aplicación de Office y, en la pestaña **Inicio** del grupo **Protección**, haga clic en **Proteger** y finalmente en **Ayuda y comentarios**. El nombre de cuenta se muestra en la sección **Estado del cliente**.

Especialmente si está usando una cuenta de administrador, asegúrese de comprobar el nombre de dominio de la cuenta con la sesión iniciada que aparece. Por ejemplo, si tiene una cuenta de "administrador" en dos inquilinos diferentes, puede ser fácil pasar por alto que se ha iniciado sesión con el nombre de cuenta correcto pero con el dominio incorrecto. Esto se traduciría en que no se podría descargar la directiva de Azure Information Protection o no se verían las etiquetas de comportamiento esperadas.

Para iniciar sesión como un usuario diferente:

1. Mediante un editor del Registro, vaya a **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP** y elimine el valor **TokenCache** (y sus datos de valores asociados).

2. Reinicie todas las aplicaciones de Office abiertas e inicie sesión con su cuenta de usuario diferente. Si no ve un mensaje en la aplicación de Office para iniciar sesión en el servicio Azure Information Protection, vuelva al cuadro de diálogo **Microsoft Azure Information Protection** y haga clic en **Iniciar sesión** desde la sección **Estado del cliente** actualizada.

Además:

- Si utiliza el inicio de sesión único, debe cerrar la sesión de Windows e iniciar sesión con su cuenta de usuario diferente después de editar el registro. El cliente Azure Information Protection se autenticará automáticamente mediante la cuenta de usuario que tiene iniciada sesión actualmente.

- Si desea reinicializar el entorno para el servicio de Azure Rights Management (también conocido como arranque), puede hacerlo mediante la opción **Restablecer** de la [herramienta RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437).

- Si desea eliminar la directiva actualmente descargada de Azure Information Protection, elimine el archivo **Policy.msip** de la carpeta **%localappdata%\Microsoft\MSIP**.

### <a name="hide-the-classify-and-protect-menu-option-in-windows-file-explorer"></a>Ocultación de la opción de menú Clasificar y Proteger en el Explorador de archivos de Windows

Puede configurar esta configuración avanzada editando el Registro cuando tenga la versión 1.3.0.0 del cliente de Azure Information Protection o una versión superior. 

Cree el siguiente nombre de valor DWORD (con cualquier datos de valor):

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

### <a name="support-for-disconnected-computers"></a>Soporte técnico para equipos desconectados

De forma predeterminada, el cliente de Azure Information Protection intenta conectarse automáticamente al servicio Azure Information Protection para descargar la directiva más reciente de Azure Information Protection. Si tiene un equipo que sabe que no se podrá conectar a Internet durante un período de tiempo, puede impedir que el cliente intente conectarse al servicio editando el Registro. Busque el siguiente nombre de valor y establezca los datos del valor en **0**:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Asegúrese de que el cliente tiene un archivo de directiva válido denominado **Policy.msip**, en la carpeta **%localappdata%\Microsoft\MSIP**. Si es necesario, puede exportar la directiva desde Azure Portal y copiar el archivo exportado en el equipo cliente. También puede utilizar este método para reemplazar un archivo de directiva no actualizado con la directiva publicada más reciente.

## <a name="to-uninstall-the-azure-information-protection-client"></a>Para desinstalar el cliente de Azure Information Protection

Puede usar una de estas opciones:

- Utilice el Panel de Control para desinstalar un programa: haga clic en **Microsoft Azure Information Protection** > **Desinstalar**

- Vuelva a ejecutar el archivo ejecutable (por ejemplo, **AzInfoProtection.exe**) y, en la página, **Modificar instalación**, haga clic en **Desinstalar**. 

- Ejecute el archivo ejecutable con **/uninstall**. Por ejemplo: `AzInfoProtection.exe /uninstall`

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha instalado el cliente de Azure Information Protection, vea la siguiente información adicional que puede necesitar para la compatibilidad con este cliente:

- [Archivos de cliente y registro de uso](client-admin-guide-files-and-logging.md)

- [Seguimiento de documentos](client-admin-guide-document-tracking.md)

- [Tipos de archivos admitidos](client-admin-guide-file-types.md)

- [Comandos de PowerShell](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
