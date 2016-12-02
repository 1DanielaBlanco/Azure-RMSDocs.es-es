---
title: "Paso 2&colon; Migración entre claves protegidas por software | Azure Information Protection"
description: "Estas instrucciones forman parte de la ruta de migración de AD RMS a Azure Information Protection y solo se aplican si la clave de AD RMS está protegida por software y quiere migrar a Azure Rights Management con una clave de inquilino protegida por software."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/23/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 5aac7b9fae12642c9846a70c5d271c7600af4096
ms.openlocfilehash: 07b2a94625f006c07f72c543488f69d4cae3a9ec


---


# <a name="step-2-software-protected-key-to-software-protected-key-migration"></a>Paso 2: Migración entre claves protegidas por software

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Office 365*


Estas instrucciones forman parte de la [ruta de migración de AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md) y solo se aplican si la clave de AD RMS está protegida por software y quiere migrar a Azure Rights Management con una clave de inquilino protegida por software. 

Si no es el escenario de configuración elegido, vuelva al [paso 2. Exporte los datos de configuración de AD RMS, impórtelos en Azure RMS](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection) y elija una configuración distinta.

Siga el procedimiento siguiente para importar la configuración de AD RMS en Azure Information Protection, para generar la clave de inquilino de Azure Information Protection administrada por Microsoft.

## <a name="to-import-the-configuration-data-to-azure-information-protection"></a>Para importar los datos de configuración en Azure Information Protection

1.  En una estación de trabajo conectada a Internet, descargue e instale el módulo de Windows PowerShell para Azure Rights Management (versión mínima 2.5.0.0), donde se incluye el cmdlet [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx). El servicio Azure Rights Management (Azure RMS) proporciona el servicio de protección para Azure Information Protection.

    > [!TIP]
    > Si ya descargó e instaló el módulo, compruebe el número de versión. Para ello, ejecute: `(Get-Module aadrm -ListAvailable).Version`

    Para obtener instrucciones de instalación, consulte [Instalación de Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md).

2.  Inicie Windows PowerShell con la opción **Ejecutar como administrador** y use el cmdlet [Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx) para conectarse al servicio de Azure RMS:

    ```
    Connect-AadrmService
    ```
    Cuando se le pida, escriba las credenciales de administrador de inquilinos de [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (normalmente, usará una cuenta de administrador global de Office 365 o Azure Active Directory).

3.  Use el cmdlet [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) para cargar el primer archivo del dominio de publicación de confianza (.xml) exportado. Si tiene más de un archivo .xml porque tenía varios dominios de publicación de confianza, elija el archivo que contenga el dominio de publicación de confianza exportado que quiera usar con Azure Information Protection para proteger el contenido después de la migración. Use el siguiente comando:

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword <secure string> -Active $True -Verbose
    ```
    Puede usar [ConvertTo-SecureString -AsPlaintext](https://technet.microsoft.com/library/hh849818.aspx) o [Read-Host](https://technet.microsoft.com/library/hh849945.aspx) para especificar la contraseña como una cadena segura. Cuando utilice ConvertTo-SecureString y la contraseña tiene caracteres especiales, escriba la contraseña entre comillas simples o con caracteres especiales de escape.
    
    Por ejemplo: ejecute primero **$TPD_Password = Read-Host -AsSecureString** y escriba la contraseña que especificó anteriormente. Después, ejecute **Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword $TPD_Password -Active $true -Verbose**. Cuando se le pida, confirme que desea realizar esta acción.
    
4.  Cuando se complete el comando, repita el paso 3 por cada archivo .xml restante que haya creado al exportar los dominios de publicación de confianza. Por ejemplo, debe tener al menos un archivo adicional para importar si actualizó su clúster de AD RMS para el modo criptográfico 2. Sin embargo, en el caso de estos archivos, establezca **-Active** en **false** al ejecutar el comando Import. Por ejemplo: **Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword $TPD_Password -Active $false -Verbose**

5.  Use el cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx) para desconectarse del servicio Azure Rights Management:

    ```
    Disconnect-AadrmService
    ```


Ahora puede ir al [paso 3. Active el inquilino de Azure Information Protection](migrate-from-ad-rms-phase1.md#step-3-activate-your-azure-information-protection-tenant).





<!--HONumber=Nov16_HO4-->


