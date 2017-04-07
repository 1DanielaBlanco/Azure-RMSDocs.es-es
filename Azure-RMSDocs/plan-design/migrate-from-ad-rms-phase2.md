---
title: "Migración de AD RMS-Azure Information Protection: fase 2"
description: "La fase 2 de la migración desde AD RMS a Azure Information Protection, donde se describe el paso 5 de la migración de AD RMS a Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 6e3f0bf46886c27620f8b7c836d0c67aafb61d37
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="migration-phase-2---client-side-configuration"></a>Fase 2 de migración: Configuración del lado cliente

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Office 365*

Use la información siguiente para la fase 2 de la migración desde AD RMS a Azure Information Protection. En estos procedimientos se describe el paso 5 de la [Migración desde AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).


## <a name="step-5-reconfigure-clients-to-use-azure-information-protection"></a>Paso 5. Volver a configurar los clientes para usar Azure Information Protection
Para los clientes de Windows:

1.  [Descargue los scripts de migración](https://go.microsoft.com/fwlink/?LinkId=524619):

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    Estos scripts restablecen la configuración en los equipos Windows para que usen el servicio Azure Information Protection en lugar de AD RMS.

2.  Siga las instrucciones del script de redireccionamiento (Redirect_OnPrem.cmd) para modificarlo de forma que apunte al nuevo inquilino de Azure Information Protection.

    > [!IMPORTANT]
    > Las instrucciones incluyen reemplazar las direcciones de ejemplo de **adrms** y **adrms.contoso.com** con las direcciones de sus propios servidores de AD RMS. Al hacerlo, asegúrese de que no haya ningún espacio adicional antes o después de las direcciones, ya que interrumpirá el script de migración y es muy difícil de identificar como la causa principal del problema. Algunas herramientas de edición agregan automáticamente un espacio después de pegar texto.
    >
    > Además, si los servidores de AD RMS usan certificados de servidor SSL/TLS, compruebe si los valores de la dirección URL de administración de licencias incluyen el número de puerto **443** en la cadena. Por ejemplo: https:// rms.treyresearch.net:443/_wmcs/licensing. Para encontrar esta información en la consola de Active Directory Rights Management Services, haga clic en el nombre del clúster y vea la información de **Detalles del clúster**. Si ve el número de puerto 443 incluido en la dirección URL, incluya este valor cuando modifique el script. Por ejemplo, https://rms.treyresearch.net**:443**.

3. Si los usuarios tienen Office 2016: aún no se han actualizado los scripts para incluir la configuración de Office 2016, por lo que, si los usuarios tienen esta versión de Office, debe actualizar manualmente los scripts:

    - Para **CleanUpRMS.cmd**: busque la línea `reg delete HKCU\Software\Microsoft\Office\15.0\Common\DRM /f` e, inmediatamente después de ella, agregue la siguiente línea:

            reg delete HKCU\Software\Microsoft\Office\16.0\Common\DRM /f

    - Para **Redirect_Onprem.cmd**: busque la línea `reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM" /t REG_SZ /v "DefaultServer" /d "%CloudRMS%" /F` e, inmediatamente después de ella, agregue las siguientes dos líneas:

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

#### <a name="changes-made-by-the-migration-scripts"></a>Cambios realizados por los scripts de migración
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


## <a name="next-steps"></a>Pasos siguientes
Para continuar con la migración, vaya a [Fase 3: Configuración de servicios auxiliares](migrate-from-ad-rms-phase3.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]