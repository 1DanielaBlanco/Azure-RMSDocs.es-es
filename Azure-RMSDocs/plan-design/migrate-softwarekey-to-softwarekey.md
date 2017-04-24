---
title: "Migración entre claves protegidas por software - AIP"
description: "Estas instrucciones forman parte de la ruta de migración de AD RMS a Azure Information Protection y solo se aplican si la clave de AD RMS está protegida por software y quiere migrar a Azure Rights Management con una clave de inquilino protegida por software."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/06/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 60370cc34184b28f5cdecf6ad51f9ba58dd4816a
ms.sourcegitcommit: 77b0936bea2700eb12b580e5738e077d447d5686
translationtype: HT
---
# <a name="step-2-software-protected-key-to-software-protected-key-migration"></a>Paso 2: migración entre claves protegidas por software

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Office 365*


Estas instrucciones forman parte de la [ruta de migración de AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md) y solo se aplican si la clave de AD RMS está protegida por software y quiere migrar a Azure Rights Management con una clave de inquilino protegida por software. 

Si no es el escenario de configuración elegido, vuelva al [Paso 4. Exporte los datos de configuración de AD RMS, impórtelos en Azure RMS](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection) y elija una configuración distinta.

Siga el procedimiento siguiente para importar la configuración de AD RMS en Azure Information Protection, para generar la clave de inquilino de Azure Information Protection administrada por Microsoft.

## <a name="to-import-the-configuration-data-to-azure-information-protection"></a>Para importar los datos de configuración en Azure Information Protection

1. En una estación de trabajo conectada a Internet, use el cmdlet [Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice) para conectarse al servicio de Azure Rights Management:

    ```
    Connect-AadrmService
    ```
    Cuando se le pida, escriba las credenciales de administrador de inquilinos de [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (normalmente, usará una cuenta de administrador global de Office 365 o Azure Active Directory).

2. Use el cmdlet [Import-AadrmTpd](/powershell/aadrm/vlatest/import-aadrmtpd) para cargar el primer archivo del dominio de publicación de confianza (.xml) exportado. Si tiene más de un archivo .xml porque tenía varios dominios de publicación de confianza, elija el archivo que contenga el dominio de publicación de confianza exportado que quiera usar con Azure Information Protection para proteger el contenido después de la migración. Use el siguiente comando:

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword <secure string> -Active $True -Verbose
    ```
    Puede usar [ConvertTo-SecureString -AsPlaintext](https://technet.microsoft.com/library/hh849818.aspx) o [Read-Host](https://technet.microsoft.com/library/hh849945.aspx) para especificar la contraseña como una cadena segura. Cuando utilice ConvertTo-SecureString y la contraseña tiene caracteres especiales, escriba la contraseña entre comillas simples o con caracteres especiales de escape.
    
    Por ejemplo: ejecute primero **$TPD_Password = Read-Host -AsSecureString** y escriba la contraseña que especificó anteriormente. Después, ejecute **Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword $TPD_Password -Active $true -Verbose**. Cuando se le pida, confirme que desea realizar esta acción.
    
3.  Cuando se complete el comando, repita el paso 3 por cada archivo .xml restante que haya creado al exportar los dominios de publicación de confianza. Por ejemplo, debe tener al menos un archivo adicional para importar si actualizó su clúster de AD RMS para el modo criptográfico 2. Sin embargo, en el caso de estos archivos, establezca **-Active** en **false** al ejecutar el comando Import. Por ejemplo: **Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword $TPD_Password -Active $false -Verbose**

4.  Use el cmdlet [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice) para desconectarse del servicio Azure Rights Management:

    ```
    Disconnect-AadrmService
    ```


Ahora puede ir al [Paso 5. Active el inquilino de Azure Information Protection](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

