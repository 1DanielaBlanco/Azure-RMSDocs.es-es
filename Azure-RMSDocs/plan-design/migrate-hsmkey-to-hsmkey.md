---
# required metadata

title: Paso 2; Migración entre claves protegidas por HSM | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5bbf37e-f1bf-4010-a60f-37177c9e9b39

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Paso 2: Migración entre claves protegidas por HSM

Estas instrucciones son parte de la [ruta de acceso de la migración de AD RMS a Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md), y se aplican solo si la clave de AD RMS está protegida por HSM y desea migrar a Azure Rights Management con una clave de inquilino protegida por HSM. 

Si no es el escenario de configuración elegido, vuelva al [paso 2. Exporte los datos de configuración de AD RMS e impórtelos en Azure RMS](migrate-from-ad-rms-to-azure-rms.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms) y elija una configuración distinta.

> [!NOTE]
> Estas instrucciones asumen que su clave de AD RMS tiene la protección del módulo. Se trata del caso común. Si la clave de AD RMS tiene la protección de OCS, póngase en contacto con [AskIPTeam@microsoft.com](mailto: askipteam@microsoft.com?subject=AD%20RMS%20migration%20with%20OCS-protected%20key) antes de seguir estas instrucciones.

Es un procedimiento de dos partes para importar la clave HSM y la configuración de AD RMS a Azure RMS, que tiene como resultado la clave de inquilino de Azure RMS que administra el propio usuario (BYOK).

Primero debe empaquetar su clave HSM para prepararla para transferirla a Azure RMS y, luego, importarla con los datos de configuración.

## Parte 1: Empaquetar la clave HSM para que esté preparada para transferirla a Azure RMS

1.  Siga los pasos de la sección [Implementación de "Aporte su propia clave" (BYOK)](plan-implement-tenant-key.md#BKMK_ImplementBYOK) de [Planeamiento e implementación de la clave de inquilino de Azure Rights Management](plan-implement-tenant-key.md). Para ello, use el procedimiento **Generar y transferir su clave de inquilino a través de Internet** con las siguientes excepciones:

    -   No siga los pasos que se indican en **Generar su clave de inquilino**, porque ya tiene el equivalente por su implementación de AD RMS. Debe identificar la clave utilizada por el servidor de AD RMS de la instalación de Thales y usar esta clave durante la migración. Los archivos de claves cifradas de Thales suelen denominarse **key_(keyAppName)_(keyIdentifier)** de forma local en el servidor.

    -   No siga los pasos para **Transferir su clave de inquilino a Azure RMS**, que usa el comando Add-AadrmKey.  En su lugar, transferirá la clave HSM preparada cuando se cargue el dominio de publicación de confianza exportado, mediante el comando Import-AadrmTpd.

2.  En la estación de trabajo conectada a Internet, en la sesión de Windows PowerShell, vuelva a conectar con el servicio de Azure RMS.

Ahora que ha preparado su clave HSM para Azure RMS, está listo para importar el archivo de clave HSM y los datos de configuración de AD RMS.

## Part 2: Importar la clave HSM y los datos de configuración a Azure RMS

1.  En la estación de trabajo conectada a Internet y en la sesión de Windows PowerShell, cargue el primer archivo del dominio de publicación de confianza exportado (.xml). Si tiene más de un archivo .xml porque tenía varios dominios de publicación de confianza, elija el archivo que contenga el dominio de publicación de confianza exportado que corresponda a la clave HSM que desee usar en Azure RMS para proteger el contenido después de la migración. Use el siguiente comando:

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToBYOKPackage> -Active $True -Verbose
    ```
    Por ejemplo: **Import -TpdFile E:\no_key_tpd_contosokey1.xml  -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $true -Verbose**

    Cuando se le pida, escriba la contraseña que especificó anteriormente y confirme que desea realizar esta acción.

2.  Cuando se haya completado el comando, repita el paso 1 en cada archivo .xml restante que se creó mediante la exportación de los dominios de publicación de confianza. Sin embargo, en el caso de estos archivos, establezca **-Active** en **false** al ejecutar el comando Import.  Por ejemplo: **Import -TpdFile E:\contosokey2.xml -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $false -Verbose**

3.  Use el cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) para desconectarse del servicio Azure RMS:

    ```
    Disconnect-AadrmService
    ```

Ahora puede ir al [paso 3. Active el inquilino de RMS](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration).



<!--HONumber=Apr16_HO3-->


