---
title: Migración entre claves protegidas por software - AIP
description: Estas instrucciones forman parte de la ruta de migración de AD RMS a Azure Information Protection y solo se aplican si la clave de AD RMS está protegida por software y quiere migrar a Azure Rights Management con una clave de inquilino protegida por software.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/11/2018
ms.topic: article
ms.service: information-protection
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: e33b31150d769ea32ebab19002fb6fb5a5c3b2ae
ms.sourcegitcommit: 7ba9850e5bb07b14741bb90ebbe98f1ebe057b10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2018
ms.locfileid: "42808463"
---
# <a name="step-2-software-protected-key-to-software-protected-key-migration"></a>Paso 2: migración entre claves protegidas por software

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Estas instrucciones forman parte de la [ruta de migración de AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md) y solo se aplican si la clave de AD RMS está protegida por software y quiere migrar a Azure Rights Management con una clave de inquilino protegida por software. 

Si no es el escenario de configuración elegido, vuelva al [Paso 4. Exporte los datos de configuración de AD RMS, impórtelos en Azure RMS](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection) y elija una configuración distinta.

Siga el procedimiento siguiente para importar la configuración de AD RMS en Azure Information Protection, para generar la clave de inquilino de Azure Information Protection administrada por Microsoft.

## <a name="to-import-the-configuration-data-to-azure-information-protection"></a>Para importar los datos de configuración en Azure Information Protection

1. En una estación de trabajo conectada a Internet, use el cmdlet [Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice) para conectarse al servicio de Azure Rights Management:

    ```
    Connect-AadrmService
    ```
    Cuando se le pida, escriba las credenciales de administrador de inquilinos de Azure Rights Management (normalmente, usará una cuenta de administrador global de Office 365 o Azure Active Directory).

2. Use el cmdlet [Import-AadrmTpd](/powershell/aadrm/vlatest/import-aadrmtpd) para cargar cada archivo del dominio de publicación de confianza (.xml) exportado. Por ejemplo, debe tener al menos un archivo adicional para importar si actualizó su clúster de AD RMS para el modo criptográfico 2. 
    
    Para ejecutar este cmdlet, necesitará la contraseña que especificó anteriormente para cada archivo de datos de configuración. 
    
    Por ejemplo, primero ejecute lo siguiente para almacenar la contraseña:
    
        $TPD_Password = Read-Host -AsSecureString
    
    Escriba la contraseña que especificó para exportar el primer archivo de datos de configuración. A continuación, use E:\contosokey1.xml como ejemplo para ese archivo de configuración, ejecute el siguiente comando y confirme que desea realizar esta acción:
    ```
    Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword $TPD_Password -Verbose
    ```
    
3. Cuando haya cargado cada archivo, ejecute [AadrmKeyProperties Set](/powershell/module/aadrm/set-aadrmkeyproperties) para identificar la clave importada que coincida con la clave SLC actualmente activa de AD RMS. Esta clave se convertirá en la clave del inquilino activo para el servicio Azure Rights Management.

4.  Use el cmdlet [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice) para desconectarse del servicio Azure Rights Management:

    ```
    Disconnect-AadrmService
    ```

Ahora puede ir al [Paso 5. Activación del servicio de Azure Rights Management](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service).


