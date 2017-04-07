---
title: "Actualización de plantillas de Azure RMS - AIP"
description: "Cuando usa el servicio Azure Rights Management, se descargan de forma automática plantillas a los ordenadores cliente para que los usuarios puedan seleccionarlas desde sus aplicaciones. Sin embargo, es posible que tengas que tomar medidas adicionales si quieres efectuar cambios en las plantillas."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/27/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8c2064f0-dd71-4ca5-9040-1740ab8876fb
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 77bd9e7bedf4a319f8f911782c995066a26a7055
ms.sourcegitcommit: 8ae83a9fc03bf2ee39ea758835ef52156f19784d
translationtype: HT
---
# <a name="refreshing-templates-for-users"></a>Actualización de plantillas para usuarios

>*Se aplica a: Azure Information Protection, Office 365*

Cuando usa el servicio Azure Rights Management de Azure Information Protection, se descargan de forma automática plantillas a los ordenadores cliente para que los usuarios puedan seleccionarlas desde sus aplicaciones. Sin embargo, es posible que tengas que tomar medidas adicionales si quieres efectuar cambios en las plantillas:

|Aplicación o servicio|Cómo se actualizan las plantillas tras los cambios|
|--------------------------|---------------------------------------------|
|Exchange Online|Configuración manual precisa para actualizar plantillas.<br /><br />En los pasos de configuración, consulte la sección siguiente, [Solamente Exchange Online: Cómo configurar Exchange para descargar las plantillas personalizadas que se han cambiado](#exchange-online-only-how-to-configure-exchange-to-download-changed-custom-templates).|
|Cliente de Azure Information Protection|Se actualiza automáticamente cada vez que la directiva de Azure Information Protection se actualiza en el cliente:<br /><br /> - Cuando se abre una aplicación de Office que admite la barra de Azure Information Protection. <br /><br /> - Cuando hace clic con el botón derecho para clasificar y proteger un archivo o carpeta. <br /><br /> - Cuando ejecuta cmdlets de PowerShell para etiquetado y protección (Get-AIPFileStatus y Set-AIPFileLabel).<br /><br /> - Cada 24 horas.<br /><br /> Además, dado que el cliente de Azure Information Protection está estrechamente integrado con Office, cualquier plantillas actualizada para Office 2016 u Office 2013 también se actualizará para el cliente de Azure Information Protection.|
|Office 2016 y Office 2013<br /><br />Aplicaciones de uso compartido de RMS para Windows|Actualización automática: programada:<br /><br />- Para estas versiones posteriores de Office: el intervalo de actualización predeterminado es cada 7 días.<br /><br />- Para la aplicación RMS sharing para Windows: a partir de la versión 1.0.1784.0, el intervalo de actualización predeterminado es cada día. Las versiones anteriores tienen un intervalo de actualización predeterminado de 7 días.<br /><br />Para exigir una actualización antes de esta programación, consulte la sección [Office 2016, Office 2013 y la aplicación RMS sharing para Windows: Cómo forzar una actualización de una plantilla personalizada que se ha cambiado](#office-2016--office-2013-and-rms-sharing-application-for-windows-how-to-force-a-refresh-for-a-changed-custom-template).|
|Office 2010|Se actualiza automáticamente cuando los usuarios cierran la sesión de Windows, vuelven a iniciarla y esperan hasta 1 hora.|
|Office 2016 para Mac|Actualización automática: no se requieren pasos adicionales.|
|Aplicación RMS sharing para dispositivos móviles|Actualización automática: no se requieren pasos adicionales.|


## <a name="exchange-online-only-how-to-configure-exchange-to-download-changed-custom-templates"></a>Solamente Exchange Online: Cómo configurar Exchange para descargar las plantillas personalizadas que se han cambiado
Si ya has configurado Information Rights Management (IRM) para Exchange Online, no se descargarán plantillas personalizadas para usuarios hasta que realices los cambios siguientes mediante Windows PowerShell en Exchange Online.

> [!NOTE]
> Para más información sobre cómo usar Windows PowerShell en Exchange Online, consulte [Usar PowerShell con Exchange Online](https://technet.microsoft.com/library/jj200677%28v=exchg.160%29.aspx).

Debes efectuar este procedimiento cada vez que cambies una plantilla.

### <a name="to-update-templates-for-exchange-online"></a>Para actualizar plantillas para Exchange Online

1.  Conéctese al servicio mediante Windows PowerShell en Exchange Online:

    1.  Especifique el nombre de usuario y la contraseña de Office 365:

        ```
        $UserCredential = Get-Credential
        ```

    2.  Conecte con el servicio Exchange Online mediante la ejecución de los dos comandos siguientes:

        ```
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection
        ```

        ```
        Import-PSSession $Session
        ```

2.  Use el cmdlet [Import-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200724%28v=exchg.160%29.aspx) para volver a importar el Dominio de publicación de confianza (TPD) desde Azure RMS:

    ```
    Import-RMSTrustedPublishingDomain -Name "<TPD name>" -RefreshTemplates -RMSOnline
    ```
    Por ejemplo, si el nombre del TPD es **RMS Online - 1** (un nombre habitual en muchas organizaciones), escriba: **Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates -RMSOnline**

    > [!NOTE]
    > Para comprobar el nombre del TPD, puede usar el cmdlet [Get-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200707%28v=exchg.160%29.aspx).

3.  Para confirmar que se han importado correctamente las plantillas, espere unos minutos y después ejecute el cmdlet [Get-RMSTemplate](http://technet.microsoft.com/library/dd297960%28v=exchg.160%29.aspx) y establezca Tipo en Todas. Por ejemplo:

    ```
    Get-RMSTemplate -TrustedPublishingDomain "RMS Online - 1" -Type All
    ```
    > [!TIP]
    > Es útil conservar una copia de la salida, con el fin de poder copiar fácilmente los nombres de plantilla o los GUID si posteriormente se archiva una plantilla.

4.  Por cada plantilla importada que desea que esté disponible en Outlook Web App, debe usar el cmdlet [Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) y establecer Tipo en Distribuido:

    ```
    Set-RMSTemplate -Identity "<name  or GUID of the template>" -Type Distributed
    ```
    Dado que Outlook Web Access almacena en caché la interfaz de usuario durante las 24 horas, es posible que los usuarios no puedan ver la plantilla nueva hasta un día después.

Además, si archivas una plantilla (personalizada o predeterminada) y usas Exchange Online con Office 365, los usuarios continuarán viendo las plantillas archivadas si usan la aplicación web de Outlook o dispositivos móviles que usen el protocolo Exchange ActiveSync.

Para que los usuarios ya no vean estas plantillas, conéctese al servicio mediante Windows PowerShell en Exchange Online y después use el cmdlet [Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) ejecutando el comando siguiente:

```
Set-RMSTemplate -Identity "<name or GUID of the template>" -Type Archived
```

## <a name="office-2016--office-2013-and-rms-sharing-application-for-windows-how-to-force-a-refresh-for-a-changed-custom-template"></a>Office 2016, Office 2013 y la aplicación RMS sharing para Windows: Cómo forzar una actualización de una plantilla personalizada que se ha cambiado
Si modifica el Registro de los equipos que ejecutan Office 2016, Office 2013 o la aplicación Rights Management (RMS) sharing, puede cambiar la programación automática para que las plantillas cambiadas se actualicen en los equipos con más frecuencia que la indicada en sus valores predeterminados. También puede forzar una actualización inmediata eliminando los datos existentes en un valor del Registro.

> [!WARNING]
> Si usas el Editor del Registro de forma incorrecta, es posible que ocasiones problemas serios que puedan hacer preciso que reinstales el sistema operativo. Microsoft no puede garantizar que pueda resolver problemas ocasionados por un uso incorrecto del Editor del Registro. Usa el Editor del Registro bajo tu propia responsabilidad.

### <a name="to-change-the-automatic-schedule"></a>Para cambiar la programación automática

1.  Con un editor del Registro, cree y establezca uno de los valores del Registro siguientes:

    - Para establecer una frecuencia de actualización en días (mínimo de 1 día):  cree un nuevo valor del Registro denominado **TemplateUpdateFrequency** y defina un valor entero para los datos, que especifique la frecuencia en días para descargar los cambios en una plantilla descargada. Use la información siguiente para localizar la ruta de acceso del Registro y crear este nuevo valor del Registro.

        **Ruta de acceso del Registro:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **Escriba:** REG_DWORD

        **Valor:** TemplateUpdateFrequency

    - Para establecer una frecuencia de actualización en segundos (mínimo de 1 segundo):  cree un nuevo valor del Registro denominado **TemplateUpdateFrequencyInSeconds** y defina un valor entero para los datos, que especifique la frecuencia en segundos para descargar los cambios en una plantilla descargada. Use la información siguiente para localizar la ruta de acceso del Registro y crear este nuevo valor del Registro.

        **Ruta de acceso del Registro:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **Escriba:** REG_DWORD

        **Valor:** TemplateUpdateFrequencyInSeconds

    Asegúrese de crear y establecer uno de estos valores del Registro, no ambos. Si ambos están presentes, **TemplateUpdateFrequency** se omite.

2.  Si desea forzar una actualización inmediata de las plantillas, vaya al procedimiento siguiente. En caso contrario, reinicie ahora las aplicaciones de Office y las instancias del Explorador de archivos.

### <a name="to-force-an-immediate-refresh"></a>Para forzar una actualización inmediata

1.  Con un editor del Registro, elimine los datos del valor **LastUpdatedTime** . Por ejemplo, en los datos puede aparecer **2015-04-20T15:52**. Elimine 2015-04-20T15:52 para que no se muestre ningún dato. Use la información siguiente para localizar la ruta de acceso del Registro y eliminar estos datos del valor del Registro.

    **Ruta de acceso del registro:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\<*MicrosoftRMS_FQDN*>\Template

    **Tipo:** REG_SZ

    **Valor:** LastUpdatedTime

    > [!TIP]
        > En la ruta de acceso del Registro, <*MicrosoftRMS_FQDN*> hace referencia al FQDN de servicio de Microsoft RMS. Si desea comprobar este valor:

    > 1.  Ejecute el cmdlet [Get-AadrmConfiguration](https://msdn.microsoft.com/library/windowsazure/dn629410.aspx) para Azure RMS. Si aún no ha instalado el módulo de Windows PowerShell para Azure RMS, consulte [Instalación de Windows PowerShell para Azure Rights Management](install-powershell.md).
    > 2.  En la salida, identifique el valor **LicensingIntranetDistributionPointUrl** .
    > 
    >     Por ejemplo: **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**
    > 3.  En el valor, quite **https://** y **/_wmcs/licensing** de esta cadena. El valor restante es el FQDN de servicio de Microsoft RMS. En nuestro ejemplo, el FQDN de servicio de Microsoft RMS sería el valor siguiente:
    > 
    >     **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

2.  Elimine la carpeta siguiente y todos los archivos que contenga: **%localappdata%\Microsoft\MSIPC\Templates**

3.  Reinicie las aplicaciones de Office y las instancias del Explorador de archivos.


## <a name="see-also"></a>Véase también
[Configuración de plantillas personalizadas para Azure Rights Management](configure-custom-templates.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]