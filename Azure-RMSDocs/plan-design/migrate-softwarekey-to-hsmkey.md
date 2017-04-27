---
title: "Migración de clave protegida por software a clave protegida por HSM - AIP"
description: "Estas instrucciones forman parte de la ruta de migración de AD RMS a Azure Information Protection y solo son válidas si la clave de AD RMS está protegida por software y quiere migrar a Azure Information Protection con una clave de inquilino protegida por HSM en Azure Key Vault."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/18/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: c5f4c6ea-fd2a-423a-9fcb-07671b3c2f4f
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: bcb0d7ffe9576f02e6388451f16a8341ee4325c2
ms.sourcegitcommit: 237ce3a0cc4921da5a08ed5753e6491403298194
translationtype: HT
---
# <a name="step-2-software-protected-key-to-hsm-protected-key-migration"></a>Paso 2: Migración de clave protegida por software a clave protegida por HSM

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection*


Estas instrucciones forman parte de la [ruta de migración de AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md) y solo son válidas si la clave de AD RMS está protegida por software y quiere migrar a Azure Information Protection con una clave de inquilino protegida por HSM en Azure Key Vault. 

Si no es el escenario de configuración elegido, vuelva al [Paso 4. Exporte los datos de configuración de AD RMS, impórtelos en Azure RMS](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection) y elija una configuración distinta.

Es un procedimiento de cuatro partes para importar la configuración de AD RMS a Azure Information Protection y conseguir que la clave de inquilino de Azure Information Protection la administre el propio usuario (BYOK) en Azure Key Vault.

Primero, deberá extraer la clave del certificado de emisor de licencias de servidor (SLC) a partir de los datos de configuración de AD RMS y transferir la clave a un HSM de Thales local. A continuación, deberá crear el paquete y transferir la clave de HSM a Azure Key Vault. Posteriormente, deberá autorizar el acceso del servicio Azure Rights Management de Azure Information Protection a su almacén de claves y, por último, importar los datos de configuración.

Como Azure Key Vault almacenará y administrará su clave de inquilino de Azure Information Protection, es necesario que esta parte de la migración se administre en Azure Key Vault, además de Azure Information Protection. Si el Almacén de claves de Azure es administrado para la organización por un administrador distinto de su usuario, necesitará coordinarse y trabajar con ese administrador para completar estos procedimientos.

Antes de empezar, asegúrese de que la organización tenga un almacén de claves creado en el Almacén de claves de Azure y que sea compatible con claves protegidas por HSM. Aunque no es necesario, le recomendamos que tenga un almacén de claves dedicado a Azure Information Protection. Este almacén de claves se configurará para permitir que el servicio Azure Rights Management de Azure Information Protection tenga acceso a él, por lo que las claves que almacene este almacén de claves deberán limitarse únicamente a las claves de Azure Information Protection.


> [!TIP]
> Si va a realizar los pasos de configuración para el Almacén de claves de Azure y no está familiarizado con este servicio de Azure, puede que le resulte útil ver primero [Introducción al Almacén de claves de Azure](/azure/key-vault/key-vault-get-started). 


## <a name="part-1-extract-your-slc-key-from-the-configuration-data-and-import-the-key-to-your-on-premises-hsm"></a>Parte 1: extracción de la clave de SLC de los datos de configuración e importar la clave en el HSM local

1.  Administrador de Azure Key Vault: para cada clave SLC exportada que desee almacenar en Azure Key Vault, utilice los pasos siguientes de la sección [Implementación del método Aportar tu propia clave (BYOK) en el Almacén de claves de Azure](/azure/key-vault/key-vault-hsm-protected-keys#implementing-bring-your-own-key-byok-for-azure-key-vault) de la documentación de Azure Key Vault:

    -   **Generación y transferencia de una clave a un HSM del Almacén de claves de Azure**: [Paso 1: preparación de la estación de trabajo conectada a Internet](/azure/key-vault-hsm-protected-keys/#step-1-prepare-your-internet-connected-workstation)

    -   **Generación y transferencia de una clave de inquilino a través de Internet**: [Paso 2: preparación de la estación de trabajo desconectada](/azure/key-vault-hsm-protected-keys/#step-2-prepare-your-disconnected-workstation)

    Debe seguir los pasos para generar la clave de inquilino, puesto que ya tiene el equivalente en el archivo de datos de configuración exportado (.xml). En su lugar, ejecutará una herramienta para extraer la clave del archivo e importarla en el HSM local. Esta herramienta crea dos archivos al ejecutarla:

    - Un nuevo archivo de datos de configuración sin la clave, que se podrá importar al inquilino de Azure Information Protection.

    - Un archivo PEM (contenedor de claves) con la clave, que se puede importar en el HSM local.

2. Administrador de Azure Information Protection o administrador de Azure Key Vault: en la estación de trabajo desconectada, ejecute la herramienta TpdUtil desde el [kit de herramientas de migración de Azure RMS](https://go.microsoft.com/fwlink/?LinkId=524619). Por ejemplo, si la herramienta está instalada en la unidad E, donde copia el archivo de datos de configuración llamado ContosoTPD.xml:

    ```
        E:\TpdUtil.exe /tpd:ContosoTPD.xml /otpd:ContosoTPD.xml /opem:ContosoTPD.pem
    ```

    Si tiene más de un archivo de datos de configuración de RMS, ejecute esta herramienta para el resto de los archivos.

    Para ver la ayuda de esta herramienta, donde se incluye una descripción, instrucciones de uso y ejemplos, ejecute TpdUtil.exe sin parámetros

    Información adicional sobre este comando:

    - **/tpd**: especifica la ruta de acceso completa y el nombre del archivo de datos de configuración exportado de AD RMS. El nombre de parámetro completo es **TpdFilePath**.

    - **/otpd**: especifica el nombre del archivo de salida del archivo de datos de configuración sin la clave. El nombre de parámetro completo es **OutPfxFile**. Si no especifica este parámetro, el archivo de salida será, de forma predeterminada, el nombre del archivo original con el sufijo **_keyless** y se almacenará en la carpeta actual.

    - **/opem**: especifica el nombre del archivo de salida del archivo PEM, que contiene la clave extraída. El nombre de parámetro completo es **OutPemFile**. Si no especifica este parámetro, el archivo de salida será, de forma predeterminada, el nombre del archivo original con el sufijo **_key** y se almacenará en la carpeta actual.

    - Si no especifica una contraseña al ejecutar este comando (con el nombre de parámetro completo **TpdPassword** o con el nombre de parámetro abreviado, **pwd**), se le pedirá que lo especifique.

3. En la misma estación de trabajo desconectada, conecte y configure el HSM de Thales según la documentación de Thales. Ahora puede importar la clave en el HSM de Thales conectado con el comando siguiente, donde tendrá que sustituir su propio nombre de archivo por ContosoTPD.pem:

        generatekey --import simple pemreadfile=e:\ContosoTPD.pem plainname=ContosoBYOK protect=module ident=contosobyok type=RSA

    > [!NOTE]
    >Si tiene más de un archivo, elija el archivo que se corresponda con la clave de HSM que quiera usar en Azure RMS para proteger el contenido después de la migración.

    Esto generará una pantalla de resultados similar a la siguiente:

    **parámetros de generación de claves:**

    **operación &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Operación a ejecutar &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; importación**

    **aplicación &nbsp;&nbsp;&nbsp;&nbsp;Aplicación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; simple**

    **verificar &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Verificar la seguridad de la clave de configuración&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; sí**

    **tipo &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Tipo de clave &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; RSA**

    **pemreadfile &nbsp;&nbsp; Archivo PEM que contiene una clave RSA &nbsp;&nbsp; e:\ContosoTPD.pem**

    **identificador &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Identificador de clave &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; contosobyok**

    **plainname &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Nombre de clave &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ContosoBYOK**

    **La clave se ha importado correctamente.**

    **Ruta de la clave: C:\ProgramData\nCipher\Key Management Data\local\key_simple_contosobyok**

Este resultado confirma que la clave privada se ha migrado al dispositivo HSM de Thales local con una copia cifrada guardada en una clave (en el ejemplo anterior, "key_simple_contosobyok"). 

Después de extraer la clave de SLC e importarla en el HSM local, puede crear un paquete de la clave protegida por HSM y transferirlo al Almacén de claves de Azure.

> [!IMPORTANT]
> Después de completar este paso, borre de forma segura estos archivos PEM de la estación de trabajo desconectada para evitar que usuarios no autorizados puedan obtener acceso a ellos. Por ejemplo, ejecute "cipher /w:E" para eliminar de forma segura todos los archivos de la unidad E.

## <a name="part-2-package-and-transfer-your-hsm-key-to-azure-key-vault"></a>Parte 2: creación del paquete y transferencia de la clave de HSM al Almacén de claves de Azure

Administrador de Azure Key Vault: para cada clave SLC exportada que desee almacenar en Azure Key Vault, utilice los pasos siguientes de la sección [Implementación del método Aportar tu propia clave (BYOK) en el Almacén de claves de Azure](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azure-key-vault) de la documentación de Azure Key Vault:

- [Paso 4: preparación de la clave para la transferencia](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-4-prepare-your-key-for-transfer)

- [Paso 5: transferencia de la clave a Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-5-transfer-your-key-to-azure-key-vault)

Como ya tiene la clave, no siga los pasos para generar el par de claves. En su lugar, ejecute un comando para transferir esta clave (en el ejemplo anterior, el parámetro KeyIdentifier usa "contosobyok") del HSM local.

Antes de transferir la clave al Almacén de claves de Azure, asegúrese de que la utilidad KeyTransferRemote.exe devuelva **Result: SUCCESS** al crear una copia de la clave con permisos reducidos (paso 4.1) y al cifrar la clave (paso 4.3).

Cuando se cargue la clave en el Almacén de claves de Azure, se mostrarán las propiedades de la clave, incluido el identificador de clave. Será similar a **https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333**. Anote esta URL porque el administrador de Azure Information Protection necesitará indicar al servicio Azure Rights Management de Azure Information Protection que use esta clave para su clave de inquilino.

A continuación, utilice el cmdlet [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) para autorizar a la entidad del servicio Azure Rights Management a acceder al almacén de claves. Los permisos necesarios son decrypt, encrypt, unwrapkey, wrapkey, verify y sign.

Por ejemplo, si el almacén de claves que ha creado para Azure Information Protection tiene el nombre contosorms-byok-kv y su grupo de recursos se llama contosorms-byok-rg, ejecute el comando siguiente:
    
    Set-AzureRmKeyVaultAccessPolicy -VaultName "contosorms-byok-kv" -ResourceGroupName "contosorms-byok-rg" -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign,get

Después de transferir la clave de HSM al Almacén de claves de Azure, estará preparado para importar los datos de configuración de AD RMS.

## <a name="part-3-import-the-configuration-data-to-azure-information-protection"></a>Parte 3: importación de los datos de configuración a Azure Information Protection

1. Administrador de Azure Information Protection: en la estación de trabajo conectada a Internet y en la sesión de PowerShell, copie los nuevos archivos de datos de configuración (.xml) de los que se haya quitado la clave SLC después de ejecutar la herramienta TpdUtil.

2. Cargue cada archivo .xml con el cmdlet [Import-AadrmTpd](/powershell/aadrm/vlatest/import-aadrmtpd). Por ejemplo, debe tener al menos un archivo adicional para importar si actualizó su clúster de AD RMS para el modo criptográfico 2.

    Para ejecutar este cmdlet, necesitará la contraseña que especificó anteriormente para el archivo de datos de configuración y la dirección URL para la clave que se identificó en el paso anterior.

    Por ejemplo, en caso de usar el archivo de datos de configuración C:\contoso_keyless.xml y el valor de la dirección URL de clave del paso anterior, ejecute primero lo siguiente para almacenar la contraseña:
    
    ```
    $TPD_Password = Read-Host -AsSecureString
    ```
    
   Escriba la contraseña que especificó para exportar el archivo de datos de configuración. A continuación, ejecute el siguiente comando y confirme que desea realizar esta acción:

    ```
    Import-AadrmTpd -TpdFile "C:\contoso_keyless.xml" -ProtectionPassword $TPD_Password –KeyVaultStringUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Verbose
    ```

    Como parte de esta importación, la clave de SLC se importa y se establece automáticamente como archivada.

3. Cuando haya cargado cada archivo, ejecute [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) para especificar la clave importada que coincida con la clave de SLC actualmente activa del clúster de AD RMS.

4. Use el cmdlet [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice) para desconectarse del servicio Azure Rights Management:

    ```
    Disconnect-AadrmService
    ```

Si posteriormente necesita confirmar la clave de inquilino de Azure Information Protection que se usa en Azure Key Vault, use el cmdlet [Get-AadrmKeys](/powershell/aadrm/vlatest/get-aadrmkeys) de Azure RMS.


Ahora puede ir al [Paso 5. Activación del servicio de Azure Rights Management](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

