---
title: "Migración de clave protegida por software a clave protegida por HSM - AIP"
description: "Estas instrucciones forman parte de la ruta de migración de AD RMS a Azure Information Protection y solo son válidas si la clave de AD RMS está protegida por software y quiere migrar a Azure Information Protection con una clave de inquilino protegida por HSM en Azure Key Vault."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: c5f4c6ea-fd2a-423a-9fcb-07671b3c2f4f
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 4126bd34615307347d387217b8ad4f39ba69cad8
ms.lasthandoff: 02/24/2017


---

# <a name="step-2-software-protected-key-to-hsm-protected-key-migration"></a>Paso 2: Migración de clave protegida por software a clave protegida por HSM

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection*


Estas instrucciones forman parte de la [ruta de migración de AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md) y solo son válidas si la clave de AD RMS está protegida por software y quiere migrar a Azure Information Protection con una clave de inquilino protegida por HSM en Azure Key Vault. 

Si no es el escenario de configuración elegido, vuelva al [paso 2. Exporte los datos de configuración de AD RMS, impórtelos en Azure RMS](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection) y elija una configuración distinta.

Es un procedimiento de cuatro partes para importar la configuración de AD RMS a Azure Information Protection y conseguir que la clave de inquilino de Azure Information Protection la administre el propio usuario (BYOK) en Azure Key Vault.

Primero, deberá extraer la clave del certificado de emisor de licencias de servidor (SLC) a partir de los datos de configuración de AD RMS y transferir la clave a un HSM de Thales local. A continuación, deberá crear el paquete y transferir la clave de HSM a Azure Key Vault. Posteriormente, deberá autorizar el acceso del servicio Azure Rights Management de Azure Information Protection a su almacén de claves y, por último, importar los datos de configuración.

Como Azure Key Vault almacenará y administrará su clave de inquilino de Azure Information Protection, es necesario que esta parte de la migración se administre en Azure Key Vault, además de Azure Information Protection. Si el Almacén de claves de Azure es administrado para la organización por un administrador distinto de su usuario, necesitará coordinarse y trabajar con ese administrador para completar estos procedimientos.

Antes de empezar, asegúrese de que la organización tenga un almacén de claves creado en el Almacén de claves de Azure y que sea compatible con claves protegidas por HSM. Aunque no es necesario, le recomendamos que tenga un almacén de claves dedicado a Azure Information Protection. Este almacén de claves se configurará para permitir que el servicio Azure Rights Management de Azure Information Protection tenga acceso a él, por lo que las claves que almacene este almacén de claves deberán limitarse únicamente a las claves de Azure Information Protection.


> [!TIP]
> Si va a realizar los pasos de configuración para el Almacén de claves de Azure y no está familiarizado con este servicio de Azure, puede que le resulte útil ver primero [Introducción al Almacén de claves de Azure](https://azure.microsoft.com/documentation/articles/key-vault-get-started/). 


## <a name="part-1-extract-your-slc-key-from-the-configuration-data-and-import-the-key-to-your-on-premises-hsm"></a>Parte 1: Extraer la clave de SLC de los datos de configuración e importar la clave en el HSM local

1.  Administrador del Almacén de claves de Azure: siga este procedimiento de la sección [Implementación del método Aportar tu propia clave (BYOK) en el Almacén de claves de Azure](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azure-key-vault) en la documentación del Almacén de claves de Azure:

    -   **Generación y transferencia de una clave a un HSM del Almacén de claves de Azure**: [Paso 1: preparación de la estación de trabajo conectada a Internet](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-1-prepare-your-internet-connected-workstation)

    -   **Generación y transferencia de una clave de inquilino a través de Internet**: [Paso 2: preparación de la estación de trabajo desconectada](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-2-prepare-your-disconnected-workstation)

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

## <a name="part-2-package-and-transfer-your-hsm-key-to-azure-key-vault"></a>Parte 2: Crear el paquete y transferir la clave de HSM al Almacén de claves de Azure

1.  Administrador del Almacén de claves de Azure: siga este procedimiento de la sección [Implementación del método Aportar tu propia clave (BYOK) en el Almacén de claves de Azure](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azure-key-vault) en la documentación del Almacén de claves de Azure:

    -   [Paso 4: Preparar la clave para la transferencia](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-4-prepare-your-key-for-transfer)

    -   [Paso 5: Transferir la clave a Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-5-transfer-your-key-to-azure-key-vault)

    Como ya tiene la clave, no siga los pasos para generar el par de claves. En su lugar, ejecute un comando para transferir esta clave (en el ejemplo anterior, el parámetro KeyIdentifier usa "contosobyok") del HSM local.

    Antes de transferir la clave al Almacén de claves de Azure, asegúrese de que la utilidad KeyTransferRemote.exe devuelva **Result: SUCCESS** al crear una copia de la clave con permisos reducidos (paso 4.1) y al cifrar la clave (paso 4.3).

    Cuando se cargue la clave en el Almacén de claves de Azure, se mostrarán las propiedades de la clave, incluido el identificador de clave. Será similar a **https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333**. Anote esta URL porque el administrador de Azure Information Protection necesitará indicar al servicio Azure Rights Management de Azure Information Protection que use esta clave para su clave de inquilino.

    Después de transferir la clave de HSM al Almacén de claves de Azure, estará preparado para importar los datos de configuración de AD RMS.

## <a name="part-3-import-the-configuration-data-to-azure-information-protection"></a>Parte 3: Importar los datos de configuración a Azure Information Protection

1.  Administrador de Azure Information Protection: en la estación de trabajo conectada a Internet y en la sesión de PowerShell, copie los nuevos archivos de datos de configuración (.xml) de los que se haya quitado la clave SLC después de ejecutar la herramienta TpdUtil.

2. Cargue el primer archivo .xml con el cmdlet [Import-AadrmTpd](https://msdn.microsoft.com/library/dn857523.aspx). Si tiene más de uno de estos archivos porque tenía varios dominios de publicación de confianza, elija el archivo que se corresponda con la clave HSM que quiera usar en Azure Information Protection para proteger el contenido después de la migración.

    Para ejecutar este cmdlet, necesitará la URL para la clave que se ha identificado en el paso anterior.

    Por ejemplo, en caso de usar el valor de la URL de clave del paso anterior y el archivo de datos de configuración C:\contoso_keyless.xml, tendría que ejecutar lo siguiente:

    ```
    Import-AadrmTpd -TpdFile "C:\contoso_keyless.xml" -ProtectionPassword –KeyVaultStringUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Active $True -Verbose
    ```

    Cuando se le pida, escriba la contraseña que haya especificado anteriormente para el archivo de datos de configuración y confirme que quiere realizar esta acción.

    Si tiene más de un archivo de datos de configuración, repita este comando para el resto de los archivos. Por ejemplo, debe tener al menos un archivo adicional para importar si actualizó su clúster de AD RMS para el modo criptográfico 2. Sin embargo, en el caso de estos archivos, establezca **-Active** en **false** al ejecutar el comando Import.



3.  Use el cmdlet [Disconnect-AadrmService](https://msdn.microsoft.com/library/azure/dn629416.aspx) para desconectarse del servicio Azure Rights Management:

    ```
    Disconnect-AadrmService
    ```

    > [!NOTE]
    > Si posteriormente necesita confirmar la clave de inquilino de Azure Information Protection que se usa en Azure Key Vault, use el cmdlet [Get-AadrmKeys](https://msdn.microsoft.com/library/dn629420.aspx) de Azure RMS.


Ahora puede ir al [paso 3. Active el inquilino de Azure Information Protection](migrate-from-ad-rms-phase1.md#step-3-activate-your-azure-information-protection-tenant).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



