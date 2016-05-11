---
# required metadata

title: Migración desde AD RMS a Azure Rights Management - Fase 2 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793


# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
# Fase 2 de migración: Configuración del lado cliente
Use la siguiente información para la fase 2 de migración desde AD RMS a Azure Rights Management (Azure RMS). Estos procedimientos incluyen el paso 5 del tema [Migración desde AD RMS a Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).


## Paso 5. Vuelva a configurar los clientes para usar Azure RMS.
Para los clientes de Windows:

1.  [Descargue los scripts de migración](http://go.microsoft.com/fwlink/?LinkId=524619):

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    Estos scripts restablecen la configuración en los equipos de Windows para que usen el servicio de Azure RMS en lugar de AD RMS.

2.  Siga las instrucciones del script de redireccionamiento (Redirect_OnPrem.cmd) para modificarlo de forma que apunte al nuevo inquilino de Azure RMS.

3.  En los equipos Windows, ejecute estos scripts con privilegios elevados en el contexto del usuario.

Para clientes de dispositivos móviles y equipos Mac:

-   Quite los registros de DNS SRV que creó cuando implementó la [extensión de AD RMS para dispositivos móviles](http://technet.microsoft.com/library/dn673574.aspx).

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

-   Elimine los siguientes valores del Registro:

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServerURL

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServer

Redirect_OnPrem.cmd:

-   Cree los siguientes valores del Registro para cada dirección URL proporcionada como un parámetro en cada una de las siguientes ubicaciones:

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\LicensingRedirection

    Cada entrada tiene un valor REG_SZ de **https://OldRMSserverURL/_wmcs/licensing** con los datos en el siguiente formato: **https://&lt;YourTenantURL&gt;/_wmcs/licensing**.

    > [!NOTE]
    > *&lt;YourTenantURL&gt;* tiene el formato siguiente: **{GUID}.rms.[Region].aadrm.com**.
    > 
    > Por ejemplo: 5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
    > 
    > Para encontrar este valor, identifique el valor **RightsManagementServiceId** cuando ejecute el cmdlet [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) para Azure RMS.


## Pasos siguientes
Para continuar con la migración, vaya a [Fase 3: Configuración de servicios auxiliares](migrate-from-ad-rms-phase3.md).

<!--HONumber=Apr16_HO3-->


