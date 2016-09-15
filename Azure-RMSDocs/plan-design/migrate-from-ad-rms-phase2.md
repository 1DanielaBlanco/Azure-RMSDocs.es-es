---
title: "Migración desde AD RMS a Azure Rights Management - Fase 2 | Azure RMS"
description: "Fase 2 de la migración de AD RMS a Azure Rights Management (Azure RMS), que abarca el paso 5 descrito en Migración desde AD RMS a Azure Rights Management."
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ada00b6f6298e7d359c73eb38dfdac169eacb708
ms.openlocfilehash: d03c61ae5a2b0f74259e177d0f15dd2262465754


---
# Fase 2 de migración: Configuración del lado cliente

>*Se aplica a: Active Directory Rights Management Services, Azure Rights Management*

Use la siguiente información para la fase 2 de migración desde AD RMS a Azure Rights Management (Azure RMS). Estos procedimientos incluyen el paso 5 del tema [Migración desde AD RMS a Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).


## Paso 5. Vuelva a configurar los clientes para usar Azure RMS.
Para los clientes de Windows:

1.  [Descargue los scripts de migración](https://go.microsoft.com/fwlink/?LinkId=524619):

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    Estos scripts restablecen la configuración en los equipos de Windows para que usen el servicio de Azure RMS en lugar de AD RMS.

2.  Siga las instrucciones del script de redireccionamiento (Redirect_OnPrem.cmd) para modificarlo de forma que apunte al nuevo inquilino de Azure RMS.

    > [!IMPORTANT]
    > Las instrucciones incluyen reemplazar las direcciones de ejemplo de **adrms** y **adrms.contoso.com** con las direcciones de sus propios servidores de AD RMS. Al hacerlo, asegúrese de que no haya ningún espacio adicional antes o después de las direcciones, ya que interrumpirá el script de migración y es muy difícil de identificar como la causa principal del problema. Algunas herramientas de edición agregan automáticamente un espacio después de pegar texto.

3. Si los usuarios tienen Office 2016: aún no se han actualizado los scripts para incluir la configuración de Office 2016, por lo que, si los usuarios tienen esta versión de Office, debe actualizar manualmente los scripts:

    - Para **CleanUpRMS.cmd**: busque la línea `reg delete HKCU\Software\Microsoft\Office\15.0\Common\DRM /f` e, inmediatamente después de ella, agregue la siguiente línea:

            reg delete HKCU\Software\Microsoft\Office\16.0\Common\DRM /f

    - Para **Redirect_Onprem.cmd**: busque la línea `reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM" /t REG_SZ /v "DefaultServer" /d "%CloudRMS%" /F1` e, inmediatamente después de ella, agregue las siguientes dos líneas:

            reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\DRM" /t REG_SZ /v "DefaultServerUrl" /d "https://%CloudRMS%/_wmcs/licensing" /F 

            reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\DRM" /t REG_SZ /v "DefaultServer" /d "%CloudRMS%" /F

    Opcional: los scripts no hacen referencia a Office 2016 en los comentarios. Si quiere actualizar los comentarios para reflejar estas adiciones para Office 2016, realice los siguientes cambios para **Redirect_Onprem.cmd**:

    - Busque `::     or MSIPC (Office 2013) with on-premises AD RMS` y reemplácelo con lo siguiente:
    
            ::     or MSIPC (Office 2013 and 2016) with on-premises AD RMS

    - Busque `echo Redirect SCP for Office 2013` y reemplácelo con lo siguiente:
    
            echo Redirect SCP for Office versions based on MSIPC

    - Busque `echo Redirect MSIPC for Office 2013` y reemplácelo con lo siguiente:
    
            echo Redirect MSIPC for Office versions based on MSIPC

4.  En equipos Windows:

    - Ejecute estos scripts con privilegios elevados en el contexto del usuario.

    Para clientes de dispositivos móviles y equipos Mac:

    -  Quite los registros de DNS SRV que creó cuando implementó la [extensión de AD RMS para dispositivos móviles](http://technet.microsoft.com/library/dn673574.aspx).

#### Cambios realizados por los scripts de migración
En esta sección se documentan los cambios que hacen los scripts de migración. Puede utilizar esta información sólo con fines de referencia o para solucionar problemas o si prefiere hacer estos cambios usted mismo.

CleanUpRMS_RUN_Elevated.cmd:

-   Elimine el contenido de las carpetas %userprofile%\AppData\Local\Microsoft\DRM y %userprofile%\AppData\Local\Microsoft\MSIPC, incluidas todas las subcarpetas y los archivos con nombres de archivo largos.

-   Elimine el contenido de las claves del Registro siguientes:

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\SOFTWARE\WoW6432Node\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation

-   Agregue los siguientes valores del Registro:

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServerURL

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServer

Redirect_OnPrem.cmd:

-   Cree los siguientes valores del Registro para cada dirección URL proporcionada como un parámetro en cada una de las siguientes ubicaciones:

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\LicensingRedirection

    Cada entrada tiene un valor REG_SZ de **https://DirecciónURLAntiguaServidorRMS/_wmcs/licensing** con los datos en el siguiente formato: **https://&lt;DirecciónURLInquilino&gt;/_wmcs/licensing**.

    > [!NOTE]
    > *&lt;DirecciónURLInquilino&gt;* tiene el formato siguiente: **{GUID}.rms.[Region].aadrm.com**.
    > 
    > Por ejemplo: 5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
    > 
    > Para encontrar este valor, identifique el valor **RightsManagementServiceId** cuando ejecute el cmdlet [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) para Azure RMS.


## Pasos siguientes
Para continuar con la migración, vaya a [Fase 3: Configuración de servicios auxiliares](migrate-from-ad-rms-phase3.md).


<!--HONumber=Aug16_HO4-->


