---
title: "Paso 2&colon; Migración de clave protegida por software a clave protegida por HSM | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5f4c6ea-fd2a-423a-9fcb-07671b3c2f4f
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7a9c8b531ec342e7d5daf0cbcacd6597a79e6a55
ms.openlocfilehash: 173641b9dada2673b48a1c210419cb933cdd9f13


---

# Paso 2: Migración de clave protegida por software a clave protegida por HSM

*Se aplica a: Active Directory Rights Management Services, Azure Rights Management*


Estas instrucciones son parte de la [ruta de acceso de la migración de AD RMS a Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md), y se aplican solo si la clave de AD RMS está protegida por software y desea migrar a Azure Rights Management con una clave de inquilino protegida por HSM. 

Si no es el escenario de configuración elegido, vuelva al [paso 2. Exporte los datos de configuración de AD RMS, impórtelos en Azure RMS](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms) y elija una configuración distinta.

Es un procedimiento de tres partes para importar la configuración de AD RMS a Azure RMS, que resulta en que la clave del inquilino de Azure RMS la administre el propio usuario (BYOK).

Debe extraer la clave del primer certificado emisor de licencias de servidor (SLC) de los datos de configuración y transferir la clave a un HSM de Thales local, empaquetar y transferir la clave de HSM a Azure RMS y, a continuación, importe los datos de configuración.

## Parte 1: Extraer el SLC de los datos de configuración e importar la clave al HSM local

1.  Siga los pasos de la sección [Implementación del método Aportar tu propia clave (BYOK)](plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key) de [Planeamiento e implementación de la clave de inquilino de Azure Rights Management](plan-implement-tenant-key.md). Para ello, use el procedimiento **Generar y transferir su clave de inquilino a través de Internet** con las siguientes excepciones:

    -   **Generación y transferencia de la clave de inquilino a través de Internet**: **preparar la estación de trabajo conectada a Internet.**

    -   **Generar y transferir su clave de inquilino a través de Internet**: **Prepare su estación de trabajo desconectada.**

    Debe seguir los pasos para generar la clave de inquilino, puesto que ya tiene el equivalente en el archivo de datos de configuración exportado (.xml). En su lugar, se ejecutará un comando para extraer esta clave del archivo e importarla en el HSM local.

2.  En la estación de trabajo desconectada, ejecute el siguiente comando:

    ```
    KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath <TPD> -ProtectionPassword -KeyIdentifier <KeyID> -ExchangeKeyPackage <BYOK-KEK-pka-Region> -NewSecurityWorldPackage <BYOK-SecurityWorld-pkg-Region>
    ```
    Por ejemplo, para Norteamérica: **KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath E:\contosokey1.xml -ProtectionPassword -KeyIdentifier contosorms1key –- -ExchangeKeyPackage &lt;BYOK-KEK-pka-NA-1&gt; -NewSecurityWorldPackage &lt;BYOK-SecurityWorld-pkg-NA-1&gt;**

    Información adicional:

    -   El parámetro ImportRmsCentrallyManagedKey indica que la operación es importar la clave de SLC.

    -   Si no especifica la contraseña en el comando, se le pedirá que la especifique.

    -   El parámetro KeyIdentifier es un nombre descriptivo de clave que crea el nombre del archivo de clave. Debe utilizar únicamente caracteres en minúsculas ASCII.

    -   El parámetro ExchangeKeyPackage especifica un paquete de claves de intercambio de claves (KEK) específico de la región cuyo nombre comienza por BYOK-KEK-pkg-.

    -   El parámetro NewSecurityWorldPackage especifica un paquete internacional de seguridad específico de la región cuyo nombre comienza por BYOK-SecurityWorld-pkg-.

    Este comando genera lo siguiente:

    -   Un archivo de clave de HSM: %NFAST_KMDATA%\local\key_mscapi_&lt;KeyID&gt;

    -   Archivo de datos de configuración de RMS con el SLC quitado: %NFAST_KMDATA%\local\no_key_tpd_&lt;KeyID&gt;.xml

3.  Si tiene más de un archivo de datos de configuración de RMS, repita el paso 2 para el resto de estos archivos.

Ahora que se ha extraído el SLC para que sea una clave de HSM, está listo para empaquetar y transferirla a Azure RMS.

## Part 2: Empaquetar y transferir su clave de HSM a Azure RMS

1.  Siga los pasos de la sección [Implementación del método Aportar tu propia clave (BYOK)](plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key) de [Planeamiento e implementación de la clave de inquilino de Azure Rights Management](plan-implement-tenant-key.md):

    -   **Generar y transferir su clave de inquilino a través de Internet**: **Preparar su clave de inquilino para transferirla**

    -   **Generar y transferir su clave de inquilino a través de Internet**: **Transferir su clave de inquilino a Azure RMS**

Ahora que ha transferido su clave de HSM a Azure RMS, está listo para importar los datos de configuración de AD RMS, que contienen solo un puntero a la clave del inquilino recién transferido.

## Part 3: Importar los datos de configuración a Azure RMS

1.  Aún en la estación de trabajo conectada a Internet y en la sesión de Windows PowerShell, copie los archivos de configuración de RMS con el SLC quitado (desde la estación de trabajo desconectada, %NFAST_KMDATA%\local\no_key_tpd_&lt;KeyID&gt;.xml)

2.  Cargue el primer archivo. Si tiene más de un archivo .xml porque tenía varios dominios de publicación de confianza, elija el archivo que contenga el dominio de publicación de confianza exportado que corresponda a la clave HSM que desee usar en Azure RMS para proteger el contenido después de la migración. Use el siguiente comando:

    ```
    Import-AadrmTpd -TpdFile <PathToNoKeyTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToKeyTransferPackage> -Active $true -Verbose
    ```
    Por ejemplo: **Import -TpdFile E:\no_key_tpd_contosorms1key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $true -Verbose**

    Cuando se le pida, escriba la contraseña que especificó anteriormente y confirme que desea realizar esta acción.

3.  Cuando se haya completado el comando, repita el paso 2 en cada archivo .xml restante que se creó mediante la exportación de los dominios de publicación de confianza. Sin embargo, en el caso de estos archivos, establezca **-Active** en **false** al ejecutar el comando Import. Por ejemplo: **Import -TpdFile E:\no_key_tpd_contosorms2key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $false -Verbose**

4.  Use el cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) para desconectarse del servicio Azure RMS:

    ```
    Disconnect-AadrmService
    ```

Ahora puede ir al [paso 3. Active el inquilino de RMS](migrate-from-ad-rms-phase1.md#step-3-activate-your-rms-tenant).





<!--HONumber=Jul16_HO3-->


