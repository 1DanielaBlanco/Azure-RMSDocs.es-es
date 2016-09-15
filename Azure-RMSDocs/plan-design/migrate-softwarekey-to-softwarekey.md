---
title: "Paso 2&colon; Migración entre claves protegidas por software | Azure RMS"
description: "Estas instrucciones son parte de la ruta de acceso de la migración de AD RMS a Azure Rights Management, y se aplican solo si la clave de AD RMS está protegida por software y desea migrar a Azure Rights Management con una clave de inquilino protegida por software."
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ada00b6f6298e7d359c73eb38dfdac169eacb708
ms.openlocfilehash: 5ec3d2b275521807c6fd8f9ccfe1136db97d5d79


---


# Paso 2: Migración entre claves protegidas por software

>*Se aplica a: Active Directory Rights Management Services, Azure Rights Management*


Estas instrucciones son parte de la [ruta de acceso de la migración de AD RMS a Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md), y se aplican solo si la clave de AD RMS está protegida por software y desea migrar a Azure Rights Management con una clave de inquilino protegida por software. 

Si no es el escenario de configuración elegido, vuelva al [paso 2. Exporte los datos de configuración de AD RMS, impórtelos en Azure RMS](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms) y elija una configuración distinta.

Utilice el siguiente procedimiento para importar la configuración de AD RMS a Azure RMS, que resulta en que la clave del inquilino de Azure RMS la administre Microsoft.

## Para importar los datos de configuración a Azure RMS

1.  En una estación de trabajo conectada a Internet, descargue e instale el módulo de Windows PowerShell para Azure RMS (versión mínima 2.5.0.0), donde se incluye el cmdlet [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx).

    > [!TIP]
    > Si ya ha descargado e instalado el módulo anteriormente, compruebe el número de versión. Para ello, ejecute: `(Get-Module aadrm -ListAvailable).Version`

    Para obtener instrucciones de instalación, consulte [Instalación de Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md).

2.  Inicie Windows PowerShell con la opción **Ejecutar como administrador** y use el cmdlet [Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx) para conectarse al servicio de Azure RMS:

    ```
    Connect-AadrmService
    ```
    Cuando se le pida, escriba las credenciales de administrador de inquilinos de [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (normalmente, usará una cuenta de administrador global de Office 365 o Azure Active Directory).

3.  Use el cmdlet [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) para cargar el primer archivo del dominio de publicación de confianza (.xml) exportado. Si tiene más de un archivo .xml porque tenía varios dominios de publicación de confianza, elija el archivo que contenga el dominio de publicación de confianza exportado que desee usar en Azure RMS para proteger el contenido después de la migración. Use el siguiente comando:

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -Active $True -Verbose
    ```
    Por ejemplo: **Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword -Active $true -Verbose**

    Cuando se le pida, escriba la contraseña que especificó anteriormente y confirme que desea realizar esta acción.

4.  Cuando se complete el comando, repita el paso 3 por cada archivo .xml restante que haya creado al exportar los dominios de publicación de confianza. Sin embargo, en el caso de estos archivos, establezca **-Active** en **false** al ejecutar el comando Import. Por ejemplo: **Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword -Active $false -Verbose**

5.  Use el cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx) para desconectarse del servicio Azure RMS:

    ```
    Disconnect-AadrmService
    ```


Ahora puede ir al [paso 3. Active el inquilino de RMS](migrate-from-ad-rms-phase1.md#step-3-activate-your-rms-tenant).





<!--HONumber=Aug16_HO4-->


