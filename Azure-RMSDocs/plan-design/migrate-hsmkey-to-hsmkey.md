---
title: "Paso 2&colon; Migración entre claves protegidas por HSM | Azure Information Protection"
description: "Instrucciones que forman parte de la ruta de migración de AD RMS a Azure Information Protection y que solo son válidas si la clave de AD RMS está protegida por HSM y quiere migrar a Azure Information Protection con una clave de inquilino protegida con HSM en Azure Key Vault."
author: cabailey
manager: mbaldwin
ms.date: 11/04/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: c5bbf37e-f1bf-4010-a60f-37177c9e9b39
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 1fcebaaa2fbe1479e83c232d51013341977796fc
ms.openlocfilehash: 3f5982b94f1de83ec66860946c46b9acbf45f479


---

# <a name="step-2-hsmprotected-key-to-hsmprotected-key-migration"></a>Paso 2: Migración entre claves protegidas por HSM

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection*


Estas instrucciones forman parte de la [ruta de migración de AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md) y solo son válidas si la clave de AD RMS está protegida por HSM y quiere migrar a Azure Information Protection con una clave de inquilino protegida con HSM en Azure Key Vault. 

Si no es el escenario de configuración elegido, vuelva al [paso 2. Exporte los datos de configuración de AD RMS, impórtelos en Azure RMS](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection) y elija una configuración distinta.

> [!NOTE]
> Estas instrucciones asumen que su clave de AD RMS tiene la protección del módulo. Este es el caso de uso más habitual. 

Es un procedimiento de dos partes para importar la clave de HSM y la configuración de AD RMS en Azure Information Protection, para generar la clave de inquilino de Azure Information Protection administrada por el usuario (BYOK).

Como Azure Key Vault almacenará y administrará la clave de inquilino de Azure Information Protection, es necesario que esta parte de la migración se administre en Azure Key Vault, además de Azure Information Protection. Si el Almacén de claves de Azure es administrado para la organización por un administrador distinto de su usuario, necesitará coordinarse y trabajar con ese administrador para completar estos procedimientos.

Antes de empezar, asegúrese de que la organización tenga un almacén de claves creado en el Almacén de claves de Azure y que sea compatible con claves protegidas por HSM. Aunque no es necesario, se recomienda que tenga un almacén de claves dedicado para Azure Information Protection. Este almacén de claves se configurará para permitir que el servicio Azure Rights Management pueda acceder a este, de forma que las claves almacenadas en este almacén de estén limitadas solo a las claves de Azure Information Protection.


> [!TIP]
> Si va a realizar los pasos de configuración para el Almacén de claves de Azure y no está familiarizado con este servicio de Azure, puede que le resulte útil ver primero [Introducción al Almacén de claves de Azure](https://azure.microsoft.com/documentation/articles/key-vault-get-started/). 


## <a name="part-1-transfer-your-hsm-key-to-azure-key-vault"></a>Parte 1: Transferir la clave de HSM al Almacén de claves de Azure

El administrador del Almacén de claves de Azure realiza estos procedimientos.

1.  Siga las instrucciones de la documentación del Almacén de claves de Azure con [Implementación del método Aportar tu propia clave (BYOK) en el Almacén de claves de Azure](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azure-key-vault) con la excepción siguiente:

    - Como ya tiene el equivalente de la implementación de AD RMS, no siga los pasos que se indican en **Generar su clave de inquilino**. En su lugar, identifique la clave usada por el servidor de AD RMS de la instalación de Thales y use esa clave durante la migración. Los archivos de claves cifradas de Thales suelen denominarse **key<*nombreDeAplicaciónDeClave*><*identificadorDeClave*>** de forma local en el servidor.

    Cuando se cargue la clave en el Almacén de claves de Azure, se mostrarán las propiedades de la clave, incluido el identificador de clave. Será similar a https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333. Anote esta URL, ya que el administrador de Azure Information Protection necesitará indicar al servicio Azure Rights Management que use esta clave para su clave de inquilino.

2. En la estación de trabajo conectada a Internet, en una sesión de PowerShell, use el cmdlet [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/es-es/library/mt603625(v=azure.300\).aspx) para autorizar a la entidad de servicio llamada Microsoft.Azure.RMS a acceder al almacén de claves que almacenará la clave de inquilino de Azure Information Protection. Los permisos necesarios son decrypt, encrypt, unwrapkey, wrapkey, verify y sign.
    
    Por ejemplo, si el almacén de claves que ha creado para Azure Information Protection tiene el nombre contoso-byok-ky y su grupo de recursos se llama contoso-byok-rg, ejecute el comando siguiente:
    
        Set-AzureRmKeyVaultAccessPolicy -VaultName "contoso-byok-kv" -ResourceGroupName "contoso-byok-rg" -ServicePrincipalName Microsoft.Azure.RMS -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign,get


Ahora que ya ha preparado la clave de HSM en Azure Key Vault para el servicio Azure Rights Management de Azure Information Protection, está preparado para importar los datos de configuración de AD RMS.

## <a name="part-2-import-the-configuration-data-to-azure-information-protection"></a>Parte 2: Importar los datos de configuración en Azure Information Protection

El administrador necesita realizar estos procedimientos para Azure Information Protection.

1.  En la estación de trabajo conectada a Internet y en la sesión de PowerShell, conéctese al servicio Azure Rights Management con el cmdlet [Connnect-AadrmService](https://msdn.microsoft.com/library/dn629415.aspx).
    
    Después, use el cmdlet [Import-AadrmTpd](https://msdn.microsoft.com/library/dn857523.aspx) para cargar el primer archivo del dominio de publicación de confianza (.xml) exportado. Si tiene más de un archivo .xml porque tenía varios dominios de publicación de confianza, elija el archivo que contenga el dominio de publicación de confianza exportado que corresponda a la clave HSM que desee usar en Azure RMS para proteger el contenido después de la migración. 
    
    Para ejecutar este cmdlet, necesitará la URL para la clave que se ha identificado en el paso anterior.
    
    Por ejemplo, si usa el valor de la URL de clave del paso anterior y un archivo TPD de C:\contoso-tpd1.xml, ejecutaría lo siguiente:
    
    ```
    Import-AadrmTpd -TpdFile "C:\contoso-tpd1.xml" -ProtectionPassword –KeyVaultStringUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Active $True -Verbose
    ```
    
    Cuando se le pida, escriba la contraseña que especificó anteriormente y confirme que desea realizar esta acción.

2.  Cuando se haya completado el comando, repita el paso 1 en cada archivo .xml restante que se creó mediante la exportación de los dominios de publicación de confianza. Sin embargo, en el caso de estos archivos, establezca **-Active** en **false** al ejecutar el comando Import.  

3.  Use el cmdlet [Disconnect-AadrmService](https://msdn.microsoft.com/library/azure/dn629416.aspx) para desconectarse del servicio Azure Rights Management:

    ```
    Disconnect-AadrmService
    ```

    > [!NOTE]
    > Si posteriormente necesita confirmar la clave de inquilino de Azure Information Protection que se usa en Azure Key Vault, use el cmdlet [Get-AadrmKeys](https://msdn.microsoft.com/library/dn629420.aspx) de Azure RMS.

Ahora puede ir al [paso 3. Active el inquilino de Azure Information Protection](migrate-from-ad-rms-phase1.md#step-3-activate-your-azure-information-protection-tenant).




<!--HONumber=Nov16_HO1-->


