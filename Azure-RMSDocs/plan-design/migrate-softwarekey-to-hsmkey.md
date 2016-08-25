---
title: "Paso 2&colon; Migración de clave protegida por software a clave protegida por HSM | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 08/17/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5f4c6ea-fd2a-423a-9fcb-07671b3c2f4f
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 437afd88efebd9719a3db98f8ab0ae07403053f7
ms.openlocfilehash: bd93e781da7dc34c18e236a90a03dbc8fb012a1c


---

# Paso 2: Migración de clave protegida por software a clave protegida por HSM

*Se aplica a: Active Directory Rights Management Services, Azure Rights Management*


Estas instrucciones forman parte de la [ruta de migración de AD RMS a Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) y solo son válidas si la clave de AD RMS está protegida por software y quiere migrar a Azure Rights Management con una clave de inquilino protegida por HSM en el Almacén de claves de Azure. 

Si no es el escenario de configuración elegido, vuelva al [paso 2. Exporte los datos de configuración de AD RMS, impórtelos en Azure RMS](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms) y elija una configuración distinta.

Es un procedimiento de cuatro partes para importar la configuración de AD RMS a Azure RMS y conseguir que la clave de inquilino de Azure RMS la administre el propio usuario (BYOK) en el Almacén de claves de Azure.

Primero necesita extraer la clave del certificado de emisor de licencias de servidor (SLC) a partir de los datos de configuración de AD RMS y transferir la clave a un HSM de Thales local, después crear el paquete y transferir la clave de HSM a un Almacén de claves de Azure, a continuación autorizar el acceso de Azure RMS al almacén de claves y, por último, importar los datos de configuración.

Como el Almacén de claves de Azure almacenará y administrará la clave de inquilino de Azure RMS, es necesario que esta parte de la migración se administre en el Almacén de claves de Azure, además del RMS de claves de Azure. Si el Almacén de claves de Azure es administrado para la organización por un administrador distinto de su usuario, necesitará coordinarse y trabajar con ese administrador para completar estos procedimientos.

Antes de empezar, asegúrese de que la organización tenga un almacén de claves creado en el Almacén de claves de Azure y que sea compatible con claves protegidas por HSM. Aunque no es necesario, se recomienda que tenga un almacén de claves dedicado para Azure RMS. Este almacén de claves se configurará para permitir que Azure RMS pueda obtener acceso a este, de forma que las claves guardadas en este almacén de claves se limiten a Azure RMS únicamente.


> [!TIP]
> Si va a realizar los pasos de configuración para el Almacén de claves de Azure y no está familiarizado con este servicio de Azure, puede que le resulte útil ver primero [Introducción al Almacén de claves de Azure](https://azure.microsoft.com/documentation/articles/key-vault-get-started/). 


## Parte 1: Extraer la clave de SLC de los datos de configuración e importar la clave en el HSM local

1.  Administrador del Almacén de claves de Azure: siga este procedimiento de la sección [Implementación del método Aportar tu propia clave (BYOK) en el Almacén de claves de Azure](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azure-key-vault) en la documentación del Almacén de claves de Azure:

    -   **Generación y transferencia de una clave a un HSM del Almacén de claves de Azure**: [Paso 1: preparación de la estación de trabajo conectada a Internet](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-1-prepare-your-internet-connected-workstation)

    -   **Generación y transferencia de una clave de inquilino a través de Internet**: [Paso 2: preparación de la estación de trabajo desconectada](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-2-prepare-your-disconnected-workstation)

    Debe seguir los pasos para generar la clave de inquilino, puesto que ya tiene el equivalente en el archivo de datos de configuración exportado (.xml). En su lugar, ejecutará una herramienta para extraer la clave del archivo e importarla en el HSM local. Esta herramienta crea dos archivos al ejecutarla:

    - Un nuevo archivo de datos de configuración sin la clave, que se puede importar en el inquilino de Azure RMS.

    - Un archivo PEM (contenedor de claves) con la clave, que se puede importar en el HSM local.

2. Administrador de Azure RMS o administrador del Almacén de claves de Azure: en la estación de trabajo desconectada, ejecute la herramienta TpdUtil desde el [kit de herramientas de migración de Azure RMS](https://go.microsoft.com/fwlink/?LinkId=524619). Por ejemplo, si la herramienta está instalada en la unidad E, donde copia el archivo de datos de configuración llamado ContosoTPD.xml:

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

    **key generation parameters:**

    **operation &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Operation to perform &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; import**

    **application &nbsp;&nbsp;&nbsp;&nbsp;Application&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; simple**

    **verify &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Verify security of configration key&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; yes**

    **type &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Key type &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; RSA**

    **pemreadfile &nbsp;&nbsp; PEM file containing RSA key &nbsp;&nbsp; e:\ContosoTPD.pem**

    **ident &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Key identifier &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; contosobyok**

    **plainname &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Key name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ContosoBYOK**

    **Key successfully imported.**

    **Path to key: C:\ProgramData\nCipher\Key Management Data\local\key_simple_contosobyok**

Este resultado confirma que la clave privada se ha migrado al dispositivo HSM de Thales local con una copia cifrada guardada en una clave (en el ejemplo anterior, "key_simple_contosobyok"). 

Después de extraer la clave de SLC e importarla en el HSM local, puede crear un paquete de la clave protegida por HSM y transferirlo al Almacén de claves de Azure.

> [!IMPORTANT]
> Después de completar este paso, borre de forma segura estos archivos PEM de la estación de trabajo desconectada para evitar que usuarios no autorizados puedan obtener acceso a ellos. Por ejemplo, ejecute "cipher /w:E" para eliminar de forma segura todos los archivos de la unidad E.

## Parte 2: Crear el paquete y transferir la clave de HSM al Almacén de claves de Azure

1.  Administrador del Almacén de claves de Azure: siga este procedimiento de la sección [Implementación del método Aportar tu propia clave (BYOK) en el Almacén de claves de Azure](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azure-key-vault) en la documentación del Almacén de claves de Azure:

    -   [Paso 4: preparación de la clave para la transferencia](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-4-prepare-your-key-for-transfer)

    -   [Paso 5: transferencia de la clave al Almacén de claves de Azure](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-5-transfer-your-key-to-azure-key-vault)

    Como ya tiene la clave, no siga los pasos para generar el par de claves. En su lugar, ejecute un comando para transferir esta clave (en el ejemplo anterior, el parámetro KeyIdentifier usa "contosobyok") del HSM local.

    Antes de transferir la clave al Almacén de claves de Azure, asegúrese de que la utilidad KeyTransferRemote.exe devuelva **Result: SUCCESS** al crear una copia de la clave con permisos reducidos (paso 4.1) y al cifrar la clave (paso 4.3).

    Cuando se cargue la clave en el Almacén de claves de Azure, se mostrarán las propiedades de la clave, incluido el identificador de clave. Será similar a **https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333**. Anote esta URL, ya que el administrador de Azure RMS la necesitará para configurar Azure RMS para que use esa clave para la clave de inquilino.

    Después de transferir la clave de HSM al Almacén de claves de Azure, estará preparado para importar los datos de configuración de AD RMS.

## Part 3: Importar los datos de configuración a Azure RMS

1.  Administrador de Azure RMS: en la estación de trabajo conectada a Internet y en la sesión de PowerShell, copie los nuevos archivos de datos de configuración (.xml) de los que se haya quitado la clave de SLC después de ejecutar la herramienta TpdUtil.

2. Cargue el primer archivo .xml con el cmdlet [Import-AadrmTpd](https://msdn.microsoft.com/library/dn857523.aspx). Si tiene más de uno de estos archivos porque tenía varios dominios de publicación de confianza, elija el archivo que se corresponda con la clave de HSM que quiera usar en Azure RMS para proteger el contenido después de la migración.

    Para ejecutar este cmdlet, necesitará la URL para la clave que se ha identificado en el paso anterior.

    Por ejemplo, en caso de usar el valor de la URL de clave del paso anterior y el archivo de datos de configuración C:\contoso_keyless.xml, tendría que ejecutar lo siguiente:

    ```
    Import-AadrmTpd -TpdFile "C:\contoso_keyless.xml" -ProtectionPassword –KeyVaultStringUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Active $True -Verbose
    ```

    Cuando se le pida, escriba la contraseña que haya especificado anteriormente para el archivo de datos de configuración y confirme que quiere realizar esta acción.

    Si tiene más de un archivo de datos de configuración, repita este comando para el resto de los archivos. Sin embargo, en el caso de estos archivos, establezca **-Active** en **false** al ejecutar el comando Import.



3.  Use el cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) para desconectarse del servicio Azure RMS:

    ```
    Disconnect-AadrmService
    ```

    > [!NOTE]
    > Si posteriormente necesita confirmar la clave de inquilino de Azure RMS que se usa en el Almacén de claves de Azure, use el cmdlet [Get-AadrmKeys](https://msdn.microsoft.com/library/dn629420.aspx) de Azure RMS.


Ahora puede ir al [paso 3. Active el inquilino de RMS](migrate-from-ad-rms-phase1.md#step-3-activate-your-rms-tenant).






<!--HONumber=Aug16_HO3-->


