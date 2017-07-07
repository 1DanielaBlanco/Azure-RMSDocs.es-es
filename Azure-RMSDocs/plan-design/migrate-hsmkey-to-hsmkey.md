---
title: "Migración entre claves protegidas por HSM - AIP"
description: "Instrucciones que forman parte de la ruta de migración de AD RMS a Azure Information Protection y que solo son válidas si la clave de AD RMS está protegida por HSM y quiere migrar a Azure Information Protection con una clave de inquilino protegida con HSM en Azure Key Vault."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/18/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: c5bbf37e-f1bf-4010-a60f-37177c9e9b39
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: e2f8f92595b21d122dfe76918a604ce7ff21b7ef
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2017
---
# <a name="step-2-hsm-protected-key-to-hsm-protected-key-migration"></a>Paso 2: Migración entre claves protegidas por HSM

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection*


Estas instrucciones forman parte de la [ruta de migración de AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md) y solo son válidas si la clave de AD RMS está protegida por HSM y quiere migrar a Azure Information Protection con una clave de inquilino protegida con HSM en Azure Key Vault. 

Si no es el escenario de configuración elegido, vuelva al [Paso 4. Exporte los datos de configuración de AD RMS, impórtelos en Azure RMS](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection) y elija una configuración distinta.

> [!NOTE]
> Estas instrucciones asumen que su clave de AD RMS tiene la protección del módulo. Este es el caso de uso más habitual. 

Es un procedimiento de dos partes para importar la clave de HSM y la configuración de AD RMS en Azure Information Protection, para generar la clave de inquilino de Azure Information Protection administrada por el usuario (BYOK).

Como Azure Key Vault almacenará y administrará la clave de inquilino de Azure Information Protection, es necesario que esta parte de la migración se administre en Azure Key Vault, además de Azure Information Protection. Si el Almacén de claves de Azure es administrado para la organización por un administrador distinto de su usuario, necesitará coordinarse y trabajar con ese administrador para completar estos procedimientos.

Antes de empezar, asegúrese de que la organización tenga un almacén de claves creado en el Almacén de claves de Azure y que sea compatible con claves protegidas por HSM. Aunque no es necesario, se recomienda que tenga un almacén de claves dedicado para Azure Information Protection. Este almacén de claves se configurará para permitir que el servicio Azure Rights Management pueda acceder a este, de forma que las claves almacenadas en este almacén de estén limitadas solo a las claves de Azure Information Protection.


> [!TIP]
> Si va a realizar los pasos de configuración para el Almacén de claves de Azure y no está familiarizado con este servicio de Azure, puede que le resulte útil ver primero [Introducción al Almacén de claves de Azure](https://azure.microsoft.com/documentation/articles/key-vault-get-started/). 


## <a name="part-1-transfer-your-hsm-key-to-azure-key-vault"></a>Parte 1: transferencia de la clave de HSM al Almacén de claves de Azure

El administrador del Almacén de claves de Azure realiza estos procedimientos.

1. Para cada clave de SLC exportada que desee almacenar en Azure Key Vault, siga las instrucciones de la documentación de Azure Key Vault, utilizando para ello la sección [Implementación del método Aportar tu propia clave (BYOK) en el Almacén de claves de Azure](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azure-key-vault) con la siguiente excepción:

    - Como ya tiene el equivalente de la implementación de AD RMS, no siga los pasos que se indican en **Generar su clave de inquilino**. En su lugar, identifique la clave usada por el servidor de AD RMS de la instalación de Thales y use esa clave durante la migración. Los archivos de claves cifradas de Thales suelen denominarse **key<*nombreDeAplicaciónDeClave*><*identificadorDeClave*>** de forma local en el servidor.

    Cuando se cargue la clave en el Almacén de claves de Azure, se mostrarán las propiedades de la clave, incluido el identificador de clave. Será similar a https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333. Anote esta URL, ya que el administrador de Azure Information Protection necesitará indicar al servicio Azure Rights Management que use esta clave para su clave de inquilino.

2. En la estación de trabajo conectada a Internet, en una sesión de PowerShell, use el cmdlet [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) para autorizar a la entidad de servicio de Azure Rights Management para que obtenga acceso al almacén de claves donde se almacenará la clave de inquilino de Azure Information Protection. Los permisos necesarios son decrypt, encrypt, unwrapkey, wrapkey, verify y sign.
    
    Por ejemplo, si el almacén de claves que ha creado para Azure Information Protection tiene el nombre contoso-byok-ky y su grupo de recursos se llama contoso-byok-rg, ejecute el comando siguiente:
    
        Set-AzureRmKeyVaultAccessPolicy -VaultName "contoso-byok-kv" -ResourceGroupName "contoso-byok-rg" -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign,get


Ahora que ya ha preparado la clave de HSM en Azure Key Vault para el servicio Azure Rights Management de Azure Information Protection, está preparado para importar los datos de configuración de AD RMS.

## <a name="part-2-import-the-configuration-data-to-azure-information-protection"></a>Parte 2: importación de los datos de configuración en Azure Information Protection

El administrador necesita realizar estos procedimientos para Azure Information Protection.

1. En la estación de trabajo conectada a Internet y en la sesión de PowerShell, conéctese al servicio Azure Rights Management con el cmdlet [Connnect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice).
    
    Después, cargue cada archivo del dominio de publicación de confianza (.xml) mediante el cmdlet [Import-AadrmTpd](/powershell/aadrm/vlatest/import-aadrmtpd). Por ejemplo, debe tener al menos un archivo adicional para importar si actualizó su clúster de AD RMS para el modo criptográfico 2.
    
    Para ejecutar este cmdlet, necesitará la contraseña que especificó anteriormente para cada archivo de datos de configuración y la dirección URL para la clave que se identificó en el paso anterior.
    
    Por ejemplo, en caso de usar el archivo de datos de configuración C:\contoso-tpd1.xml y el valor de la dirección URL de clave del paso anterior, ejecute primero lo siguiente para almacenar la contraseña:
    
    ```
    $TPD_Password = Read-Host -AsSecureString
    ```
    
    Escriba la contraseña que especificó para exportar el archivo de datos de configuración. A continuación, ejecute el siguiente comando y confirme que desea realizar esta acción:
    
    ```
    Import-AadrmTpd -TpdFile "C:\contoso-tpd1.xml" -ProtectionPassword $TPD_Password –KeyVaultStringUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Verbose
    ```
    
    Como parte de esta importación, la clave de SLC se importa y se establece automáticamente como archivada.

2.  Cuando haya cargado cada archivo, ejecute [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) para especificar la clave importada que coincida con la clave de SLC actualmente activa del clúster de AD RMS. Esta clave se convertirá en la clave del inquilino activo para el servicio Azure Rights Management.

3.  Use el cmdlet [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice) para desconectarse del servicio Azure Rights Management:

    ```
    Disconnect-AadrmService
    ```

Si posteriormente necesita confirmar la clave de inquilino de Azure Information Protection que se usa en Azure Key Vault, use el cmdlet [Get-AadrmKeys](/powershell/aadrm/vlatest/get-aadrmkeys) de Azure RMS.

Ahora puede ir al [Paso 5. Activación del servicio de Azure Rights Management](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

