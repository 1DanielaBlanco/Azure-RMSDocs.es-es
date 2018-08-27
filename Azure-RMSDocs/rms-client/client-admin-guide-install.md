---
title: Instalación del cliente de Azure Information Protection para los usuarios
description: Instrucciones e información para administradores para implementar el cliente de Azure Information Protection para Windows en redes empresariales.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/21/2018
ms.topic: article
ms.service: information-protection
ms.assetid: ea3ec965-3720-4614-8564-3ecfe60bc175
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 5a56836d8a77cc65c633cdb6777f1666d24b5777
ms.sourcegitcommit: 7ba9850e5bb07b14741bb90ebbe98f1ebe057b10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2018
ms.locfileid: "42805597"
---
# <a name="admin-guide-install-the-azure-information-protection-client-for-users"></a>Guía del administrador: Instalación del cliente de Azure Information Protection para los usuarios

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2*

Antes de instalar el cliente de Azure Information Protection en su red empresarial, compruebe que los equipos tienen las versiones necesarias de sistema operativo y aplicaciones para Azure Information Protection: [Requisitos para Azure Information Protection](../requirements.md). 

Luego, compruebe los requisitos previos adicionales que puede necesitar el cliente de Azure Information Protection, tal como se documenta en la sección siguiente. El programa de instalación no comprueba todos los requisitos previos.

## <a name="additional-prerequisites-for-the-azure-information-protection-client"></a>Requisitos previos adicionales para el cliente de Azure Information Protection

- Microsoft .NET Framework 4.6.2
    
    De forma predeterminada, la instalación completa del cliente de Azure Information Protection requiere una versión mínima de Microsoft .NET Framework 4.6.2 y, en caso de que falte, el asistente para la instalación del instalador ejecutable intenta descargar e instalar este requisito previo. Cuando este requisito previo se instala como parte de la instalación de cliente, es necesario reiniciar el equipo. Aunque no se recomienda, puede omitir este requisito previo al usar el asistente para la instalación con un [parámetro de instalación personalizada](#more-information-about-the-downgradedotnetrequirement-installation-parameter).
    
    Este requisito previo no se instala automáticamente al instalar el cliente en modo silencioso utilizando el instalador ejecutable, Windows Update o el instalador de Windows. Para estos escenarios, debe instalar por separado este requisito previo si es necesario, o se produce un error en la instalación. Puede descargar Microsoft .NET Framework 4.6.2 (instalador sin conexión) desde el [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53344).

- Microsoft .NET Framework 4.5.2
    
    Si el visor de Azure Information Protection se instala por separado, se requiere una versión mínima de Microsoft .NET Framework 4.5.2 y, si falta, el instalador ejecutable no lo descarga ni lo instala.

- Windows PowerShell versión 4.0
    
    El módulo de PowerShell para el cliente requiere Windows PowerShell versión 4.0, que quizá deba instalarse en sistemas operativos anteriores. Para obtener más información consulte [How to Install Windows PowerShell 4.0](http://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx) (Instalación de Windows PowerShell 4.0). El instalador no comprueba ni instala este requisito previo para usted. Para confirmar la versión de Windows PowerShell que ejecuta, escriba `$PSVersionTable` en una sesión de PowerShell.

- Microsoft Online Services - Ayudante para el inicio de sesión 7.250.4303.0
    
    Los equipos que ejecutan Office 2010 requiere Microsoft Online Services - Ayudante para el inicio de sesión versión 7.250.4303.0. Esta versión está incluida en la instalación del cliente. Si tiene una versión posterior del Asistente para el inicio de sesión, desinstálela antes de instalar el cliente de Azure Information Protection. Por ejemplo, compruebe la versión y desinstale el Asistente para el inicio de sesión en **Panel de control** > **Programas y características** > **Desinstalar o cambiar un programa**.

- KB 2533623
    
    Los equipos que ejecutan Windows 7 Service Pack 1 requieren KB 2533623. Para más información sobre esta actualización, consulte [Aviso de seguridad de Microsoft: la carga de una biblioteca no segura podría permitir la ejecución remota de código](https://support.microsoft.com/en-us/kb/2533623). Es posible que tenga que instalar directamente esta actualización o podría reemplazarla otra actualización que la instale por usted.
    
    Si la actualización es necesaria y no está instalada, la instalación del cliente mostrará una advertencia que lo señale. Esta actualización se puede instalar después de instalar el cliente, pero algunas acciones estarán bloqueadas y se volverá a mostrar el mensaje.  

- Visual C++ Redistributable para Visual Studio 2015 (versión de 32 bits)
    
    En el caso de los equipos que ejecuten Windows 7 Service Pack 1, instale **vc_redist.x86.exe** desde la siguiente página de descarga: [Visual C++ Redistributable para Visual Studio 2015](https://www.microsoft.com/en-us/download/details.aspx?id=48145).
    
    La instalación del cliente no comprueba este requisito previo, pero es necesario para que el cliente de Azure Information Protection pueda clasificar y proteger los archivos PDF.

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


## <a name="options-to-install-the-azure-information-protection-client-for-users"></a>Opciones para instalar el cliente de Azure Information Protection para los usuarios

Hay dos opciones de instalación del cliente para los usuarios:

**Ejecutar la versión ejecutable (.exe) del cliente**: el método de instalación recomendado que se puede ejecutar de manera interactiva o silenciosa. Este método es el más flexible y se recomienda porque el instalador comprueba muchos de los requisitos previos y puede instalar automática los requisitos previos que faltan. [Instrucciones](#to-install-the-azure-information-protection-client-by-using-the-executable-installer)

**Implementación de la versión de Windows Installer (.msi) del cliente**: compatible solo con instalaciones silenciosas que usan un mecanismo de implementación central, como directiva de grupo, Configuration Manager y Microsoft Intune. Este método es necesario para los equipos con Windows 10 administrados mediante Intune y administración de dispositivos móviles (MDM) porque, en estos equipos, no se admiten los archivos ejecutables para la instalación. Sin embargo, cuando usa este método de instalación debe comprobar manualmente e instalar o desinstalar el software dependiente que el instalador del ejecutable realizaría para cada equipo. [Instrucciones](#to-install-the-azure-information-protection-client-by-using-the-msi-installer)

Una vez instalado el cliente de Azure Information Protection, puede actualizar este cliente con la repetición del método de instalación elegido o usar Windows Update para mantener el cliente actualizado automáticamente. Para obtener más información sobre la actualización, consulte la sección [Actualización y mantenimiento del cliente de Azure Information Protection](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client).

### <a name="to-install-the-azure-information-protection-client-by-using-the-executable-installer"></a>Para instalar el cliente de Azure Information Protection con el instalador ejecutable

Use las instrucciones siguientes para instalar el cliente cuando no usa el catálogo de Microsoft Update ni implementa el archivo .msi mediante un método de implementación central, como Intune.

1. Descargue la versión ejecutable del cliente de Azure Information Protection del [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 
    
    Si hay una versión preliminar disponible, manténgala solo para pruebas. No está diseñada para usuarios finales en un entorno de producción. 

2. En una instalación predeterminada, simplemente ejecute el archivo ejecutable, por ejemplo, **AzInfoProtection.exe**. No obstante, para ver las opciones de instalación, primero ejecute el archivo ejecutable con **/help**: `AzInfoProtection.exe /help`

    Ejemplo para instalar el cliente de forma silenciosa: `AzInfoProtection.exe /quiet`
    
    Ejemplo para instalar de forma silenciosa solo los cmdlets de PowerShell: `AzInfoProtection.exe  PowerShellOnly=true /quiet`
    
    Parámetros adicionales que no aparecen en la pantalla de ayuda:
    
    - **ServiceLocation**: Utilice este parámetro si va a instalar el cliente en equipos que ejecutan Office 2010 y los usuarios no son administradores locales en sus equipos o no quiere que se les pregunte. [Más información](#more-information-about-the-servicelocation-installation-parameter) 
    
    - **DowngradeDotNetRequirement**: Utilice este parámetro para omitir el requisito de .NET Framework de Microsoft versión 4.6.2. [Más información](#more-information-about-the-downgradedotnetrequirement-installation-parameter)
    
    - **AllowTelemetry=0**: utilice este parámetro para deshabilitar la opción de instalación **Enviar estadísticas de uso a Microsoft para ayudar a mejorar Azure Information Protection**. 
    
3. Si va a realizar la instalación de forma interactiva, seleccione la opción para instalar una **directiva de demostración**, si no puede conectarse a Office 365 o Azure Active Directory, pero quiere ver y experimentar el lado cliente de Azure Information Protection mediante una directiva local con fines de demostración. Cuando el cliente se conecta a un servicio de Azure Information Protection, esta directiva de demostración se reemplaza por la directiva de Azure Information Protection de su organización.
    
4. Para completar la instalación: 

    - Si su equipo ejecuta Office 2010, reinicie el equipo. 
        
        Si el cliente no se ha instalado con el parámetro ServiceLocation, la primera vez que abre una de las aplicaciones de Office que usan la barra de Azure Information Protection (por ejemplo, Word), debe confirmar las solicitudes de actualización del registro para la primera vez que se usa. La [detección de servicios](client-deployment-notes.md#rms-service-discovery) se usa para rellenar las claves del Registro. 
    
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
 
    Si aún no ha instalado el módulo de PowerShell para el servicio de Azure Rights Management, vea [Instalación del módulo de PowerShell para AADRM](../install-powershell.md).

2. En la salida, identifique el valor **LicensingIntranetDistributionPointUrl** .

    Por ejemplo: **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. En el valor, quite **/_wmcs/licensing** de esta cadena. Por ejemplo: **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    La cadena restante es el valor que se especificará para el parámetro ServiceLocation.

Ejemplo para instalar el cliente de Office 2010 y Azure RMS de forma silenciosa: `AzInfoProtection.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


#### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>Más información sobre el parámetro de instalación DowngradeDotNetRequirement

Para admitir actualizaciones automáticas mediante Windows Update y para la integración confiable con aplicaciones de Office, el cliente de Azure Information Protection usa Microsoft .NET Framework versión 4.6.2. De forma predeterminada, la instalación interactiva usa las comprobaciones ejecutables para buscar esta versión e intenta instalarla si no está. A continuación, la instalación requiere el reinicio del equipo.

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
    |Office 2016|Todas las versiones compatibles|64 bits: [KB3178666](https://www.microsoft.com/en-us/download/details.aspx?id=55007)<br /><br />32 bits: [KB3178666](https://www.microsoft.com/en-us/download/details.aspx?id=54999)<br /><br /> Versión: 1.0|Instalar|
    |Office 2013|Todas las versiones compatibles|64 bits: [KB3172523](https://www.microsoft.com/en-us/download/details.aspx?id=54992)<br /><br /> 32 bits: [KB3172523](https://www.microsoft.com/en-us/download/details.aspx?id=54979) <br /><br />Versión: 1.0|Instalar|
    |Office 2010|Todas las versiones compatibles|[Microsoft Online Services - Ayudante para el inicio de sesión](https://www.microsoft.com/en-us/download/details.aspx?id=28177)<br /><br /> Versión: 2.1|Instalar|
    |Office 2010|Windows 8.1 y Windows Server 2012 R2|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> Número de versión incluido en el nombre de archivo: v3|Instalar si KB2843630 o KB2919355 no está instalado|
    |Office 2010|Windows 8 y Windows Server 2012|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> Número de versión incluido en el nombre de archivo: v3|Instalar|
    |Office 2010|Windows 7 y Windows Server 2008 R2|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41709)<br /><br /> Número de versión incluido en el nombre de archivo: v3|Se debe instalar si no está instalado KB3125574|
    |No disponible|Windows 7|[vc_redist.x86.exe](https://www.microsoft.com/en-us/download/details.aspx?id=48145)|Instalar|
    |No disponible|Windows 7|KB2627273 <br /><br /> Número de versión incluido en el nombre de archivo: v4|Desinstalar|

3. Para una instalación predeterminada, ejecute .msi con **/quiet**, por ejemplo, `AzInfoProtection.msi /quiet`. Sin embargo, es posible que tenga que especificar parámetros de instalación adicionales que están documentados en las [instrucciones del instalador ejecutable](#to-install-the-azure-information-protection-client-by-using-the-executable-installer).  


## <a name="how-to-install-the-azure-information-protection-scanner"></a>Cómo instalar el analizador de Azure Information Protection

El módulo de PowerShell incluido con el cliente de Azure Information Protection tiene cmdlets para instalar y configurar el analizador. Pero para usar el analizador debe instalar la versión completa del cliente, no basta con instalar simplemente el módulo de PowerShell.

Para instalar al cliente para el analizador, siga las mismas instrucciones que en las secciones anteriores. A continuación, ya lo tendrá todo a punto para instalar el analizador. Para obtener instrucciones, consulte [Implementación del analizador de Azure Information Protection para clasificar y proteger automáticamente los archivos](../deploy-aip-scanner.md).

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha instalado el cliente de Azure Information Protection, vea la siguiente información adicional que puede necesitar para la compatibilidad con este cliente:

- [Personalizaciones](client-admin-guide-customizations.md)

- [Archivos de cliente y registro de uso](client-admin-guide-files-and-logging.md)

- [Seguimiento de documentos](client-admin-guide-document-tracking.md)

- [Tipos de archivos admitidos](client-admin-guide-file-types.md)

- [Comandos de PowerShell](client-admin-guide-powershell.md)


