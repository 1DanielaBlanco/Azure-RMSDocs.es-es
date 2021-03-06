---
title: Guía del administrador de cliente de Azure Information Protection
description: Instrucciones e información para administradores de una red empresarial que son responsables de implementar el cliente de Azure Information Protection para Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 01/18/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 33a5982f-7125-4031-92c2-05daf760ced1
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: a0addbf7d4e613ab49ea29e750fd67a3b8ef1793
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56254584"
---
# <a name="azure-information-protection-client-administrator-guide"></a>Guía para administradores del cliente de Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2*

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

- Un complemento de Office, que instala la barra de Azure Information Protection para que los usuarios seleccionen etiquetas de clasificación y un botón **Proteger** en la cinta para ofrecer otras opciones. Para Outlook, también está disponible un botón **No reenviar** en la cinta.

- Explorador de archivos de Windows, opciones de menú contextual para que los usuarios apliquen etiquetas de clasificación y la protección de los archivos.

- Un visor para mostrar los archivos protegidos cuando una aplicación nativa no puede abrirlo.

- Un módulo de PowerShell para aplicar y quitar etiquetas de clasificación y protección en los archivos. 
    
    Este módulo incluye cmdlets para instalar y configurar el [analizador de Azure Information Protection](../deploy-aip-scanner.md) que se ejecuta como un servicio en Windows Server. Este servicio le permite detectar, clasificar y proteger archivos en almacenes de datos como recursos compartidos de red y bibliotecas de SharePoint Server.

- El cliente de Rights Management que se comunica con Azure Rights Management (Azure RMS) o Active Directory Rights Management Services (AD RMS).

El cliente de Azure Information Protection resulta ideal para trabajar con sus servicios de Azure; Azure Information Protection y su servicio de protección de datos, Azure Rights Management. Sin embargo, con algunas limitaciones, el cliente de Azure Information Protection también funciona con la versión local de Rights Management, AD RMS. Para ver una comparación exhaustiva de las características que admiten Azure Information Protection y AD RMS, consulte [Comparación entre Azure Information Protection y AD RMS](../compare-on-premise.md). 

Si tiene AD RMS y quiere migrar a Azure Information Protection, consulte [Migración desde AD RMS a Azure Information Protection](../migrate-from-ad-rms-to-azure-rms.md).


## <a name="should-you-deploy-the-azure-information-protection-client"></a>¿Debe implementar el cliente de Azure Information Protection?

Implemente el cliente de Azure Information Protection si se aplica alguna de las siguientes condiciones:

- Desea clasificar (y, opcionalmente, proteger) documentos y mensajes de correo electrónico mediante la selección de etiquetas desde las aplicaciones de Office (Word, Excel, PowerPoint y Outlook).

- Desea clasificar (y, opcionalmente, proteger) archivos mediante el Explorador de archivos, que admite tipos de archivos adicionales a los que admite Office, selección múltiple y carpetas.

- Desea ejecutar scripts que clasifican (y, opcionalmente, protegen) documentos mediante los comandos de PowerShell.

- Desea ejecutar un servicio que detecta, clasifica (y, opcionalmente, protege) archivos almacenados localmente.

- Desea ver documentos protegidos cuando una aplicación nativa para mostrar el archivo no está instalada o no puede abrir estos documentos.

- Solo desea proteger archivos con el Explorador de archivos o con los comandos de PowerShell.

- Desea que los usuarios y administradores puedan realizar un seguimiento de los documentos protegidos y revocarlos.

- Desea quitar el cifrado de archivos y contenedores (desproteger) en masa para fines de recuperación de datos.

- Ejecutar Office 2010 y proteger documentos y mensajes de correo electrónico mediante el servicio Azure Rights Management.

Ejemplo que muestra el complemento del cliente de Azure Information Protection para una aplicación de Office, mostrando las etiquetas de clasificación para su organización y el nuevo botón **Proteger** en la cinta:

![Barra de Azure Information Protection con la directiva predeterminada](../media/word2016-calloutsv2.png)

## <a name="installing-and-supporting-the-azure-information-protection-client"></a>Instalación y soporte técnico del cliente de Azure Information Protection

Puede instalar el cliente de Azure Information Protection mediante un archivo ejecutable o un archivo instalador de Windows. Para obtener más información sobre cada opción, así como instrucciones, consulte [Instalación del cliente de Azure Information Protection para los usuarios](client-admin-guide-install.md).  

Utilice las secciones siguientes para obtener información de soporte técnico sobre cómo instalar el cliente. 

### <a name="installation-checks-and-troubleshooting"></a>Comprobaciones de instalación y solución de problemas

Cuando el cliente esté instalado, utilice la opción **Ayuda y comentarios** para abrir el cuadro de diálogo **Microsoft Azure Information Protection**:

- Desde una aplicación de Office: en la pestaña **Inicio**, en el grupo **Protección**, seleccione **Proteger** y luego **Ayuda y comentarios**.

- Desde el Explorador de archivos: mediante el botón derecho, seleccione uno o varios archivos o una carpeta, elija **Clasificar y proteger** y luego seleccione **Ayuda y comentarios**. 

#### <a name="help-and-feedback-section"></a>Sección **Ayuda y comentarios**

El vínculo **Más información** dirige, de forma predeterminada, al sitio web de [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection), pero lo puede configurar con una dirección URL personalizada como uno de los valores de [configuración de directivas](../configure-policy-settings.md) en la directiva de Azure Information Protection.

El vínculo **Notificar un problema** muestra solo si especifica una [configuración de cliente avanzada](client-admin-guide-customizations.md#add-report-an-issue-for-users). Al configurar esta opción, se especifica un vínculo HTTP, como la dirección de correo electrónico del departamento.

La opción **Exportar registros** se utiliza para recopilar y adjuntar archivos de registro para el cliente de Azure Information Protection si se le ha pedido que los envíe al soporte técnico de Microsoft. Los usuarios finales también puede utilizar esta opción para enviar estos archivos de registro a su departamento de soporte técnico.

La opción **Restablecer configuración** cierra la sesión del usuario, elimina la directiva de Azure Information Protection descargada y restablece la configuración del usuario para el servicio Azure Rights Management.

##### <a name="more-information-about-the-reset-settings-option"></a>Más información sobre la opción Restablecer configuración

- No tiene que ser un administrador local para usar esta opción, y esta acción no se registra en el Visor de eventos. 

- A menos que los archivos estén bloqueados, esta acción elimina todos los archivos de las siguientes ubicaciones. Estos archivos incluyen certificados de cliente, plantillas de Rights Management, la directiva de Azure Information Protection y las credenciales de usuario almacenadas en caché. Los archivos de registro del cliente no se eliminan.
    
    - %LocalAppData%\Microsoft\DRM
    
    - %LocalAppData%\Microsoft\MSIPC
    
    - %LocalAppData%\Microsoft\MSIP\Policy.msip
    
    - %LocalAppData%\Microsoft\MSIP\TokenCache

- La configuración y las claves del Registro siguientes se eliminan. Si la configuración de alguna de estas claves del Registro tiene valores personalizados, tendrá que volver a configurarlos después de restablecer el cliente. 
    
    Normalmente para las redes empresariales, estas opciones se configuran mediante la directiva de grupo, en cuyo caso se aplican automáticamente cuando se actualiza la directiva de grupo en el equipo. Pero es posible que algunas opciones se configuren una vez con un script o se configuren de forma manual. En estos casos, debe realizar pasos adicionales para volver a configurar estas opciones. Por ejemplo, es posible que los equipos ejecuten un script una vez para configurar opciones de redireccionamiento para Azure Information Protection porque está migrando de AD RMS y aún tiene un punto de conexión de servicio en la red. Después de restablecer al cliente, el equipo debe volver a ejecutar este script.
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\15.0\Common\Identity
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\15.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\16.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Classes\Local Settings\Software\Microsoft\MSIPC    

- Se cerrará la sesión del usuario que tiene iniciada una sesión actualmente.

#### <a name="client-status-section"></a>Sección **Estado del cliente**

Utilice el valor **Conectado como** para confirmar que el nombre de usuario mostrado identifica la cuenta que se va a utilizar para la autenticación de Azure Information Protection. Este nombre de usuario debe coincidir con una cuenta que se usa para Office 365 o Azure Active Directory. La cuenta también debe pertenecer a un inquilino que esté configurado para Azure Information Protection.

Si necesita iniciar sesión como un usuario diferente al que se muestra, consulte la personalización [Inicio de sesión como un usuario diferente](client-admin-guide-customizations.md#sign-in-as-a-different-user).

El valor de **Última conexión** muestra cuándo se ha conectado por última vez el cliente al servicio de Azure Information Protection de su organización. Puede utilizar esta información con la **directiva de Information Protection que se haya instalado en** una fecha y una hora concretas para confirmar la última vez que se ha instalado o actualizado la directiva de Azure Information Protection. Cuando el cliente se conecta al servicio, se descarga automáticamente la directiva más reciente si encuentra cambios con respecto a su directiva actual, y también cada 24 horas. Si ha realizado cambios en la directiva con posterioridad al tiempo mostrado, cierre y vuelva a abrir la aplicación de Office.

Si ve **Este cliente no tiene licencia de Office Professional Plus**: el cliente de Azure Information Protection ha detectado que la edición instalada de Office no admite la aplicación de la protección de Rights Management. Cuando se realiza esta detección, las etiquetas que aplican protección no se muestran en la barra de Azure Information Protection.

Utilice la información de **Versión** para confirmar qué versión del cliente está instalada. Puede comprobar si se trata de versión más reciente, así como las correcciones correspondientes y las nuevas características haciendo clic en el vínculo **Novedades** para leer el [historial de versiones](client-version-release-history.md) del cliente.

## <a name="support-for-multiple-languages"></a>Compatibilidad con varios idiomas

El cliente de Azure Information Protection admite los mismos idiomas que Office 365. Para obtener una lista de estos idiomas, vea la sección **Office 365, Exchange Online Protection y Power BI** de la página [Disponibilidad internacional](https://products.office.com/business/international-availability) de Office.

Para estos idiomas, las opciones de menú, los cuadros de diálogo y los mensajes del cliente de Azure Information Protection se muestran en el idioma del usuario. Hay un instalador único que detecta el idioma, por lo que no necesita ninguna configuración adicional para instalar el cliente de Azure Information Protection en distintos idiomas. 

Pero los nombres y descripciones de etiqueta que especifique no se traducen automáticamente al configurar las etiquetas en la directiva de Azure Information Protection. A partir del 30 de agosto de 2017, la [directiva predeterminada](../configure-policy-default.md) actual incluye compatibilidad con algunos idiomas. Para que los usuarios puedan ver las etiquetas en su idioma preferido, proporcione sus propias traducciones y configure la directiva de Azure Information Protection para que use dichas traducciones. Para obtener más información, consulte [Configuración de etiquetas para distintos idiomas en Azure Information Protection](../configure-policy-languages.md). Las marcas visuales no se traducen y no admiten más de un idioma.

## <a name="post-installation-tasks"></a>Tareas posteriores a la instalación

Después de instalar el cliente de Azure Information Protection, asegúrese de brindar a los usuarios las instrucciones sobre cómo etiquetar los documentos y correos electrónicos, además de orientación sobre qué etiquetas elegir para escenarios específicos. Por ejemplo:

- Instrucciones para usuarios en línea: [Guía del usuario de Azure Information Protection](client-user-guide.md)

- Descargue una guía de usuario personalizable: [Guía de adopción del usuario final de Azure Information Protection](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf)

### <a name="update-macros-in-excel-spreadsheets"></a>Actualización de macros en hojas de cálculo de Excel

Si tiene hojas de cálculo de Excel que contengan macros, edite las macros de la siguiente manera para asegurarse de que sigan funcionando según lo esperado una vez que se instale el cliente de Azure Information Protection:

1. Al inicio de la macro, agregue:

        Application.EnableEvents = False

2. Al final de la macro, agregue:

        Application.EnableEvents = True

Para más información, consulte la [propiedad Application.EnableEvents (Excel)](https://msdn.microsoft.com/vba/excel-vba/articles/application-enableevents-property-excel).

## <a name="upgrading-and-maintaining-the-azure-information-protection-client"></a>Actualización y mantenimiento del cliente de Azure Information Protection

El equipo de Azure Information Protection actualiza de forma periódica el cliente de Azure Information Protection para implementar correcciones y agregar nuevas funciones. Los anuncios se publican en el [sitio de Yammer](https://www.yammer.com/AskIPTeam) del equipo.

Si usa Windows Update, el cliente de Azure Information Protection actualiza automáticamente la versión de disponibilidad general del cliente, con independencia de cómo se instaló el cliente. Las nuevas versiones de cliente se publican en el catálogo unas semanas después del lanzamiento.

Como alternativa, puede actualizar manualmente el cliente mediante la descarga de la nueva versión desde el [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). A continuación, instale la nueva versión para actualizar el cliente. Debe usar este método para actualizar las versiones preliminares.

Si actualiza manualmente, desinstale la versión anterior en primer lugar solo si va a cambiar el método de instalación. Por ejemplo, cambie de la versión del archivo ejecutable (.exe) del cliente a la versión de Windows Installer (.msi) del cliente. O bien, si necesita instalar una versión anterior del cliente. Por ejemplo, tiene la versión preliminar actual instalada para pruebas y ahora necesita volver a la versión actual de disponibilidad general.

Use el [historial de publicación de versiones y directiva de soporte técnico](client-version-release-history.md) para comprender la directiva de soporte técnico del cliente de Azure Information Protection, qué versiones son compatibles actualmente y qué novedades y modificaciones existen para las versiones compatibles. 

### <a name="upgrading-the-azure-information-protection-scanner"></a>Actualización del analizador de Azure Information Protection

La forma de actualizar el analizador depende de si la actualización se realiza a la versión de disponibilidad general actual o a la versión preliminar actual.

#### <a name="to-upgrade-the-scanner-to-the-current-ga-version"></a>Para actualizar el analizador a la versión de disponibilidad general actual

Para actualizar el analizador de Azure Information Protection, instale la versión más reciente del cliente de Azure Information Protection. Luego realice la siguiente acción única. Después de hacerlo, no tendrá que volver a examinar los archivos que ya están analizados.

- Ejecute [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner) una vez que haya actualizado el cliente de Azure Information Protection. Se conservarán las opciones de configuración para el analizador y los repositorios. Se requiere la ejecución de este cmdlet para actualizar el esquema de base de datos del analizador y, en caso necesario, también se conceden permisos de eliminación en la base de datos del analizador a la cuenta de servicio del analizador. 
    
    Hasta que se ejecuta este cmdlet de actualización, el analizador no se ejecuta y normalmente verá el identificador de evento **1000** en el registro de eventos de Windows con el siguiente mensaje de error: **Nombre de objeto "ScannerStatus" no válido**.

#### <a name="to-upgrade-the-scanner-to-the-current-preview-version"></a>Para actualizar el analizador a la versión preliminar actual

> [!IMPORTANT]
> Para obtener una ruta de actualización sencilla, no instale la versión preliminar del cliente de Azure Information Protection en el equipo que ejecuta el analizador como primer paso para actualizarlo. En su lugar, utilice las siguientes instrucciones de actualización.

Para la versión preliminar actual del analizador, el proceso de actualización es distinto al de las versiones anteriores. La actualización automática del analizador lo cambia para que obtenga sus opciones de configuración de Azure Portal. Además, se actualiza el esquema para la base de datos de configuración del analizador, y también se cambia el nombre de AzInfoProtection de esta base de datos:

- Si no especifica su propio nombre de perfil, se cambia el nombre de la base de datos de configuración por **AIPScanner_\<computer_name>**. 

- Si especifica su propio nombre de perfil, se cambia el nombre de la base de datos de configuración por **AIPScanner_\<profile_name>**.

Aunque es posible actualizar el analizador en un orden diferente, se recomiendan los pasos siguientes:

1. Use Azure Portal para crear un perfil de analizador que incluya la configuración del el analizador y los repositorios de datos con cualquier configuración que necesiten. Para obtener ayuda con este paso, vea la sección [Configuración del analizador en Azure Portal](../deploy-aip-scanner-preview.md#configure-the-scanner-in-the-azure-portal) de las instrucciones de implementación del analizador en versión preliminar.
    
    Si el equipo que ejecuta el analizador está desconectado de Internet, aun así deberá realizar este paso. A continuación, en Azure Portal, use la opción **Exportar** para exportar el perfil del analizador a un archivo.

2. En el equipo del analizador, detenga el servicio del analizador, **Analizador de Azure Information Protection**.

3. Actualice el cliente de Azure Information Protection mediante la instalación de la versión preliminar actual desde el [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

4. En una sesión de PowerShell, ejecute el comando Update-AIPScanner con el mismo nombre de perfil que especificó en el paso 1. Por ejemplo: `Update-AIPScanner –Profile USWest`

5. Solo si el analizador se ejecuta en un equipo sin conexión: Ahora ejecute [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration) y especifique el archivo que contiene la configuración exportada.

6. Reinicie el servicio Analizador de Azure Information Protection, **Analizador de Azure Information Protection**.

##### <a name="upgrading-in-a-different-order-to-the-recommended-steps"></a>Actualización en un orden diferente a los pasos recomendados

Si no configura el analizador en Azure Portal antes de ejecutar el comando Update-AIPScanner, no tendrá un nombre de perfil para especificar que identifique las opciones de configuración del analizador para el proceso de actualización. 

En este escenario, al configurar el analizador en Azure Portal, debe especificar exactamente el mismo nombre de perfil que usó cuando ejecutó el comando Update-AIPScanner. Si el nombre no coincide, el analizador no se configurará para su perfil. 

> [!TIP]
> Para identificar los analizadores que tienen este error de configuración, use la hoja **Azure Information Protection: Nodos** en Azure Portal.
>  
> Si se trata de analizadores que tienen conectividad a Internet, estos muestran su nombre de equipo con el número de versión preliminar del cliente de Azure Information Protection, pero no aparece ningún nombre de perfil. Solo los analizadores que tienen un número de versión 1.41.51.0 no deberían mostrar ningún nombre de perfil en esta hoja. 

Si no especificó ningún nombre de perfil cuando ejecutó el comando Update-AIPScanner, el nombre de equipo se usa para crear automáticamente el nombre de perfil del analizador.

#### <a name="moving-the-scanner-configuration-database-to-a-different-sql-server-instance"></a>Mover la base de datos de configuración del analizador a otra instancia de SQL Server

En la versión preliminar actual, hay un problema conocido si intenta mover la base de datos de configuración del analizador a una nueva instancia de SQL Server después de ejecutar el comando de actualización.

Si sabe que desea mover la base de datos de configuración del analizador para la versión preliminar, realice lo siguiente:

1. Desinstale el analizador mediante [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner).

2. Si aún no ha actualizado a la versión preliminar del cliente de Azure Information Protection, hágalo ahora.

3. Instale el analizador mediante [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner) y después especifique la nueva instancia de SQL Server y el nombre de perfil.

4. Opcional: Si no desea que el analizador vuelva a examinar todos los archivos, exporte la tabla ScannerFiles e impórtela a la nueva base de datos.

## <a name="uninstalling-the-azure-information-protection-client"></a>Desinstalación del cliente de Azure Information Protection

Puede usar cualquiera de las opciones siguientes para desinstalar el cliente:

- Use el Panel de control para desinstalar un programa: Haga clic en **Microsoft Azure Information Protection** > **Desinstalar**

- Vuelva a ejecutar el archivo ejecutable (por ejemplo, **AzInfoProtection.exe**) y, en la página, **Modificar instalación**, haga clic en **Desinstalar**. 

- Ejecute el archivo ejecutable con **/uninstall**. Por ejemplo: `AzInfoProtection.exe /uninstall`

## <a name="next-steps"></a>Pasos siguientes
Para instalar el cliente, consulte [Instalación del cliente de Azure Information Protection para los usuarios](client-admin-guide-install.md).

Si ya ha instalado el cliente, consulte la siguiente información adicional que puede necesitar para la compatibilidad con este cliente:

- [Personalizaciones](client-admin-guide-customizations.md)

- [Archivos de cliente y registro de uso](client-admin-guide-files-and-logging.md)

- [Seguimiento de documentos](client-admin-guide-document-tracking.md)

- [Tipos de archivos admitidos](client-admin-guide-file-types.md)

- [Comandos de PowerShell](client-admin-guide-powershell.md)


