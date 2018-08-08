---
title: Guía del administrador de cliente de Azure Information Protection
description: Instrucciones e información para administradores de una red empresarial que son responsables de implementar el cliente de Azure Information Protection para Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 33a5982f-7125-4031-92c2-05daf760ced1
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 74cb6b6cd03621f52860012331fbf4cf518459dc
ms.sourcegitcommit: 949bf02d5d12bef8e26d89ad5d6a0d5cc7826135
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39473974"
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
    
    Este módulo incluye cmdlets para instalar y configurar el [analizador de Azure Information Protection](../deploy-use/deploy-aip-scanner.md) que se ejecuta como un servicio en Windows Server. Este servicio le permite detectar, clasificar y proteger archivos en almacenes de datos como recursos compartidos de red y bibliotecas de SharePoint Server.

- El cliente de Rights Management que se comunica con Azure Rights Management (Azure RMS) o Active Directory Rights Management Services (AD RMS).

El cliente de Azure Information Protection resulta ideal para trabajar con sus servicios de Azure; Azure Information Protection y su servicio de protección de datos, Azure Rights Management. Sin embargo, con algunas limitaciones, el cliente de Azure Information Protection también funciona con la versión local de Rights Management, AD RMS. Para ver una comparación exhaustiva de las características que admiten Azure Information Protection y AD RMS, consulte [Comparación entre Azure Information Protection y AD RMS](../compare-on-premise.md). 

Si tiene AD RMS y quiere migrar a Azure Information Protection, consulte [Migración desde AD RMS a Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).


## <a name="should-you-deploy-the-azure-information-protection-client"></a>¿Debe implementar el cliente de Azure Information Protection?

Implemente el cliente de Azure Information Protection si se aplica alguna de las siguientes condiciones:

- Desea clasificar (y, opcionalmente, proteger) documentos y mensajes de correo electrónico mediante la selección de etiquetas desde las aplicaciones de Office (Word, Excel, PowerPoint y Outlook).

- Desea clasificar (y, opcionalmente, proteger) documentos y mensajes de correo electrónico mediante el Explorador de archivos, que admite tipos de archivos adicionales, la selección múltiple y carpetas.

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

Puede instalar el cliente de Azure Information Protection mediante Windows Update, un archivo ejecutable o un archivo instalador de Windows. Para obtener más información sobre cada opción, así como instrucciones, consulte [Instalación del cliente de Azure Information Protection para los usuarios](client-admin-guide-install.md).  

Utilice las secciones siguientes para obtener información de soporte técnico sobre cómo instalar el cliente. 

### <a name="installation-checks-and-troubleshooting"></a>Comprobaciones de instalación y solución de problemas

Cuando el cliente esté instalado, utilice la opción **Ayuda y comentarios** para abrir el cuadro de diálogo **Microsoft Azure Information Protection**:

- Desde una aplicación de Office: En la pestaña **Inicio**, en el grupo **Protección**, seleccione **Proteger** y luego **Ayuda y comentarios**.

- Desde el Explorador de archivos: Mediante el botón derecho, seleccione uno o varios archivos o una carpeta, elija **Clasificar y proteger** y luego seleccione **Ayuda y comentarios**. 

#### <a name="help-and-feedback-section"></a>Sección **Ayuda y comentarios**

El vínculo **Más información** dirige, de forma predeterminada, al sitio web de [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection), pero lo puede configurar con una dirección URL personalizada como uno de los valores de [configuración de directivas](../deploy-use/configure-policy-settings.md) en la directiva de Azure Information Protection.

Use el vínculo **Envíenos sus comentarios** para enviar sugerencias o solicitudes al equipo de Information Protection. No utilice esta opción para obtener soporte técnico, pero, en su lugar, vea [Opciones de soporte y recursos de la comunidad](../information-support.md#support-options-and-community-resources). 

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

Si ve **Este cliente no tiene licencia de Office Professional Plus**, significa que el cliente de Azure Information Protection ha detectado que la edición instalada de Office no admite la aplicación de la protección de Rights Management. Cuando se realiza esta detección, las etiquetas que aplican protección no se muestran en la barra de Azure Information Protection.

Utilice la información de **Versión** para confirmar qué versión del cliente está instalada. Puede comprobar si se trata de versión más reciente, así como las correcciones correspondientes y las nuevas características haciendo clic en el vínculo **Novedades** para leer el [historial de versiones](client-version-release-history.md) del cliente.

## <a name="support-for-multiple-languages"></a>Compatibilidad con varios idiomas

El cliente de Azure Information Protection admite los mismos idiomas que Office 365. Para obtener una lista de estos idiomas, vea la sección **Office 365, Exchange Online Protection y Power BI** de la página [Disponibilidad internacional](https://products.office.com/business/international-availability) de Office.

Para estos idiomas, las opciones de menú, los cuadros de diálogo y los mensajes del cliente de Azure Information Protection se muestran en el idioma del usuario. Hay un instalador único que detecta el idioma, por lo que no necesita ninguna configuración adicional para instalar el cliente de Azure Information Protection en distintos idiomas. 

Pero los nombres y descripciones de etiqueta que especifique no se traducen automáticamente al configurar las etiquetas en la directiva de Azure Information Protection. A partir del 30 de agosto de 2017, la [directiva predeterminada](../deploy-use/configure-policy-default.md) actual incluye compatibilidad con algunos idiomas. Para que los usuarios puedan ver las etiquetas en su idioma preferido, proporcione sus propias traducciones y configure la directiva de Azure Information Protection para que use dichas traducciones. Para obtener más información, consulte [Configuración de etiquetas para distintos idiomas en Azure Information Protection](../deploy-use/configure-policy-languages.md). Las marcas visuales no se traducen y no admiten más de un idioma.

## <a name="post-installation-tasks"></a>Tareas posteriores a la instalación

Después de instalar el cliente de Azure Information Protection, asegúrese de brindar a los usuarios las instrucciones sobre cómo etiquetar los documentos y correos electrónicos, además de orientación sobre qué etiquetas elegir para escenarios específicos. Por ejemplo:

- Instrucciones en línea para el usuario: [Guía del usuario de Azure Information Protection](client-user-guide.md)

- Descargue una guía del usuario personalizable: [Guía de adopción de Azure Information Protection para el usuario final](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf)

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

Use el [historial de publicación de versiones y directiva de soporte técnico](../rms-client/client-version-release-history.md) para comprender la directiva de soporte técnico del cliente de Azure Information Protection, qué versiones son compatibles actualmente y qué novedades y modificaciones existen para las versiones compatibles. 

### <a name="upgrading-the-azure-information-protection-scanner"></a>Actualización del analizador de Azure Information Protection

Para actualizar el analizador de Azure Information Protection, instale la versión más reciente del cliente de Azure Information Protection. Lleve a cabo una de las siguientes acciones únicas:

Para la versión actual de disponibilidad general (GA): 

- Si la versión instalada previamente del cliente era 1.26.6.0 o anterior, vuelva a ejecutar el comando de instalación del analizador con[Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner). Se conservarán las opciones de configuración para el analizador y los repositorios. La reinstalación del analizador concede al servicio del analizador permisos de eliminación de cuenta para la base de datos del analizador, que se necesitarán para los informes.

Para la versión preliminar: 

- Si la versión instalada previamente del cliente era 1.26.6.0 o anterior, ejecute [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner) después de instalar el cliente. Se conservarán las opciones de configuración para el analizador y los repositorios. Se requiere la ejecución de este cmdlet para actualizar el esquema de base de datos del analizador y, en caso necesario, también se conceden permisos de eliminación en la base de datos del analizador a la cuenta de servicio del analizador. Hasta que se ejecute este cmdlet de actualización, el analizador no se ejecutará.

## <a name="uninstalling-the-azure-information-protection-client"></a>Desinstalación del cliente de Azure Information Protection

Puede usar cualquiera de las opciones siguientes para desinstalar el cliente:

- Utilice el Panel de Control para desinstalar un programa: haga clic en **Microsoft Azure Information Protection** > **Desinstalar**

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


