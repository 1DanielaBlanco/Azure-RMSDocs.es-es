---
title: Configuración para clientes y servicios en línea de Office 365 para usar Azure RMS desde AIP
description: Información e instrucciones para que los administradores configuren Office 365 para trabajar con el servicio Azure Rights Management de Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/02/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0a6ce612-1b6b-4e21-b7fd-bcf79e492c3b
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ed441ab24517b5d12a1e38ed61a46d4498237636
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259191"
---
# <a name="office365-configuration-for-clients-and-online-services-to-use-the-azure-rights-management-service"></a>Office 365: configuración para clientes y servicios en línea que usan el servicio Azure Rights Management

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Como Office 365 es compatible de forma nativa con el servicio Azure Rights Management desde Azure Information Protection, no se requiere ninguna configuración para equipo cliente para conseguir la compatibilidad con las funciones de Information Rights Management (IRM) para aplicaciones como Word, Excel, PowerPoint, Outlook y Outlook en la Web. Lo único que han de hacer los usuarios es iniciar sesión en sus aplicaciones de Office con sus credenciales de Rights Management. Después ya pueden proteger archivos y correos electrónicos, y usar archivos y correos electrónicos que hayan protegido otros usuarios.

No obstante, se recomienda complementar estas aplicaciones con el cliente de Azure Information Protection, para que los usuarios se beneficien del complemento de Office y de la compatibilidad con tipos de archivos adicionales. Para más información, vea [Cliente de Azure Information Protection: instalación y configuración de clientes](configure-client.md).

## <a name="exchangeonline-irm-configuration"></a>Exchange Online: Configuración de IRM
Para obtener información sobre cómo funciona Exchange Online IRM con el servicio Azure Rights Management, vea la sección [Exchange Online y Exchange Server](office-apps-services-support.md#exchange-online-and-exchange-server) de [Cómo las aplicaciones y los servicios de Office admiten Azure Rights Management](office-apps-services-support.md).

Puede que Exchange Online ya esté habilitado para su uso con el servicio Azure Rights Management. Para comprobarlo, ejecute los comandos siguientes:

1. Si es la primera vez que ha usado Windows PowerShell para Exchange Online en el equipo, debe configurar Windows PowerShell para ejecutar scripts firmados. Inicie una sesión de Windows PowerShell mediante la opción **Ejecutar como administrador** y, luego, escriba:
    
        Set-ExecutionPolicy RemoteSigned
    
    Presione **Y** para confirmar.

2. En la sesión de Windows PowerShell, inicie sesión en Exchange Online con una cuenta que está habilitada para el acceso al shell remoto. De manera predeterminada, todas las cuentas que se crean en Exchange Online están habilitadas para el acceso remoto al shell, pero esto se puede deshabilitar (y habilitar) con el comando [Set-User &lt;UserIdentity&gt; -RemotePowerShellEnabled](https://technet.microsoft.com/library/jj984292%28v=exchg.160%29.aspx).
    
    Para iniciar sesión, primero escriba:
    
        $Cred = Get-Credential
   
    Después, en el cuadro de diálogo **Solicitud de credenciales para Windows PowerShell**, proporcione el nombre de usuario y la contraseña de Office 365.

3. Conecte con el servicio Exchange Online. Para ello, establezca primero una variable:
    
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
    
    Después, ejecuta el comando siguiente:
    
        Import-PSSession $Session

4. Ejecute el comando [Get-IRMConfiguration](https://technet.microsoft.com/library/dd776120(v=exchg.160).aspx) para ver la configuración de Exchange Online para el servicio de protección:
    
        Get-IRMConfiguration
    
    En la salida, busque el valor **AzureRMSLicensingEnabled**:
    
    - Si AzureRMSLicensingEnabled está establecido en **True**, significa que Exchange Online ya está habilitado para el servicio Azure Rights Management. 
    
    - Si AzureRMSLicensingEnabled está establecido en **True**, ejecute el siguiente comando para habilitar Exchange Online para el servicio Azure Rights Management: `Set-IRMConfiguration -AzureRMSLicensingEnabled $true`.

5. Para probar que Exchange Online está configurado correctamente, ejecute el siguiente comando:
    ```
    Test-IRMConfiguration -Sender <user email address>
    ```
    Por ejemplo: <strong>Test-IRMConfiguration -Sender  adams@contoso.com</strong>
    
    Este comando ejecuta una serie de comprobaciones que incluyen la comprobación de la conectividad con el servicio y la recuperación de la configuración, los URI, las licencias y las plantillas. En la sesión de Windows PowerShell verá los resultados de cada uno y, al final, si todo pasa estas comprobaciones: **RESULTADO GLOBAL: CORRECTO**

Cuando Exchange Online está habilitado para utilizar el servicio Azure Rights Management, se pueden configurar características que apliquen protección de la información automáticamente, tales como [reglas de flujo de correo](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8), [directivas de prevención de pérdida de datos (DLP)](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx) y [correo de voz protegido](https://technet.microsoft.com/library/dn198211%28v=exchg.150%29.aspx) (mensajería unificada).

## <a name="sharepointonline-and-onedrive-for-business-irm-configuration"></a>SharePoint Online y OneDrive para la Empresa: Configuración de IRM

Para obtener más información sobre cómo funciona IRM de SharePoint Online con el servicio Azure Rights Management, vea [SharePoint Online y SharePoint Server](office-apps-services-support.md#sharepoint-online-and-sharepoint-server) en la sección **Protección de Rights Management** de esta documentación.

Para configurar SharePoint Online y OneDrive para la Empresa de forma que sean compatibles con el servicio Azure Rights Management, primero debe habilitar el servicio Information Rights Management (IRM) para SharePoint Online mediante el centro de administración de SharePoint. Luego, los propietarios de sitios pueden proteger con IRM sus listas y bibliotecas de documentos de SharePoint, y los usuarios pueden proteger con IRM su biblioteca de OneDrive para la Empresa, de modo que los documentos que están guardados ahí, y que se comparten con otros, estén protegidos automáticamente con Azure Rights Management.

> [!NOTE]
> Las bibliotecas protegidas con IRM para SharePoint y OneDrive para la Empresa requieren la última versión del nuevo cliente de sincronización de OneDrive (OneDrive.exe) y la versión del [cliente de RMS del Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=38396). Instale esta versión del cliente de RMS incluso si ha instalado el cliente de Azure Information Protection. Para más información sobre este escenario de implementación, vea [Implementar el nuevo cliente de sincronización de OneDrive en un entorno empresarial](https://support.office.com/article/Deploy-the-new-OneDrive-sync-client-in-an-enterprise-environment-3f3a511c-30c6-404a-98bf-76f95c519668).

Para habilitar el servicio Information Rights Management (IRM) para SharePoint Online, consulte las siguientes instrucciones en la documentación de Office:

- [Configuración de Information Rights Management (IRM) en el centro de administración de SharePoint](/office365/securitycompliance/set-up-irm-in-sp-admin-center)

Esta configuración se realiza mediante el administrador de Office 365.

### <a name="configuring-irm-for-libraries-and-lists"></a>Configuración de IRM para listas y bibliotecas
Después de haber habilitado el servicio IRM para SharePoint, los propietarios de sitios pueden proteger con IRM sus listas y bibliotecas de documentos de SharePoint. Para obtener instrucciones, vea los recursos siguientes en el sitio web de Office:

- [Aplicar Information Rights Management a una lista o biblioteca](https://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)

Esta configuración se realiza mediante el administrador de sitios de SharePoint.

### <a name="configuring-irm-for-onedrive-for-business"></a>Configuración de IRM para OneDrive para la Empresa
Una vez habilitado el servicio IRM para SharePoint Online, las carpetas o la biblioteca de documentos de OneDrive para la Empresa de los usuarios se pueden configurar para la protección de Rights Management. Los usuarios pueden configurarlo por sí mismos en su sitio web de OneDrive. Aunque los administradores no pueden configurar esta protección mediante el centro de administración de SharePoint, pueden hacerlo con Windows PowerShell.

> [!NOTE]
> Para más información acerca de cómo configurar OneDrive para la Empresa, consulte la documentación de Office, [Configurar OneDrive para el negocio en Office 365](https://support.office.com/article/Set-up-OneDrive-for-Business-in-Office-365-3e21f8f0-e0a1-43be-aa3e-8c0236bf11bb).

#### <a name="configuration-for-users"></a>Configuración de los usuarios
Proporcione a los usuarios las siguientes instrucciones para que puedan configurar OneDrive para la Empresa y proteger sus archivos de empresa.

1. Inicie sesión en Office 365 con su cuenta profesional o educativa y vaya al [sitio web de OneDrive](https://portal.office.com/onedrive).

2. En el panel de navegación, en la parte inferior, seleccione **Volver a la versión clásica de OneDrive**.

3. Seleccione el icono **Configuración**. En el panel **Configuración**, si la **cinta de opciones** está **desactivada**, seleccione esta opción para activarla.

4. Para configurar la protección de todos los archivos de OneDrive para la Empresa, seleccione la pestaña **BIBLIOTECA** de la cinta de opciones y, después, seleccione **Configuración de la biblioteca**.

5. En la página **Documentos > Configuración**, en la sección **Permisos y administración**, seleccione **Information Rights Management**.

6. En la página **Configuración de Information Rights Management**, seleccione la casilla de verificación **Restringir permisos en esta biblioteca al descargarlos**. Especifique el nombre y la descripción que quiera para los permisos y, de manera opcional, haga clic en **MOSTRAR OPCIONES** para aplicar configuraciones opcionales. Luego, haga clic en **Aceptar**.

    Para obtener más información sobre las opciones de configuración, consulte las instrucciones que se indican en [Aplicación de Information Rights Management a una lista o biblioteca](https://support.office.com/article/Apply-Information-Rights-Management-to-a-list-or-library-3bdb5c4e-94fc-4741-b02f-4e7cc3c54aa1) de la documentación de Office.

Dado que esta configuración se basa en los usuarios, y no en el administrador, para proteger con IRM sus archivos de OneDrive para la Empresa, muestre a los usuarios las ventajas de proteger sus archivos y cómo hacerlo. Por ejemplo, explique que cuando comparten un documento de OneDrive para la Empresa, solo las personas que ellos autorizan pueden tener a él acceso con cualquier restricción que configuren, incluso si se cambia el nombre del archivo o se copia en otra parte.

#### <a name="configuration-for-administrators"></a>Configuración para administradores
Aunque IRM no se puede configurar para OneDrive para la Empresa de los usuarios mediante el centro de administración de SharePoint, se puede hacer con Windows PowerShell. Para habilitar IRM en estas bibliotecas, siga estos pasos:

1. Descargue e instale el [SDK de componentes del cliente de SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=42038).

2. Descargue e instale el [shell de administración de SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588).

3. Copie el contenido del siguiente script y denomine Set-IRMOnOneDriveForBusiness.ps1 al archivo en el equipo.

   *&#42;&#42;Declinación de responsabilidades&#42;&#42;*: Este script de ejemplo no es compatible en ningún servicio o programa de soporte estándar de Microsoft. Este script de ejemplo se proporciona TAL CUAL sin garantía de ningún tipo.

   ```
   # Requires Windows PowerShell version 3

   <#
     Description:

       Configures IRM policy settings for OneDrive for Business and can also be used for SharePoint Online libraries and lists

    Script Installation Requirements:

      SharePoint Online Client Components SDK
      https://www.microsoft.com/en-us/download/details.aspx?id=42038

      SharePoint Online Management Shell
      https://www.microsoft.com/en-us/download/details.aspx?id=35588

   ======
   #>

   # URL will be in the format https://<tenant-name>-admin.sharepoint.com
   $sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com"

   $tenantAdmin = "admin@contoso.com"

   $webUrls = @("https://contoso-my.sharepoint.com/personal/user1_contoso_com",
                "https://contoso-my.sharepoint.com/personal/user2_contoso_com",
                "https://contoso-my.sharepoint.com/personal/user3_contoso_com")

   <# As an alternative to specifying the URLs as an array, you can import them from a CSV file (no header, single value per row).
      Then, use: $webUrls = Get-Content -Path "File_path_and_name.csv"

   #>

   $listTitle = "Documents"

   function Load-SharePointOnlineClientComponentAssemblies
   {
       [cmdletbinding()]
       param()

       process
       {
           # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI
           try
           {
               Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               return $true
           }
           catch
           {
               if($_.Exception.Message -match "Could not load file or assembly")
               {
                   Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: https://www.microsoft.com/en-us/download/details.aspx?id=42038"
               }
               else
               {
                   Write-Error -Exception $_.Exception
               }
               return $false
           }
       }
   }

   function Load-SharePointOnlineModule
   {
       [cmdletbinding()]
       param()

       process
       {
           do
           {
               # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell
               $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue

               if(-not $spoModule)
               {
                   try
                   {
                       Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking
                       return $true
                   }
                   catch
                   {
                       if($_.Exception.Message -match "Could not load file or assembly")
                       {
                           Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: https://www.microsoft.com/en-us/download/details.aspx?id=35588"
                       }
                       else
                       {
                           Write-Error -Exception $_.Exception
                       }
                       return $false
                   }
               }
               else
               {
                   return $true
               }
           }
           while(-not $spoModule)
       }
   }

   function Set-IrmConfiguration
   {
       [cmdletbinding()]
       param(
           [parameter(Mandatory=$true)][Microsoft.SharePoint.Client.List]$List,
           [parameter(Mandatory=$true)][string]$PolicyTitle,
           [parameter(Mandatory=$true)][string]$PolicyDescription,
           [parameter(Mandatory=$false)][switch]$IrmReject,
           [parameter(Mandatory=$false)][DateTime]$ProtectionExpirationDate,
           [parameter(Mandatory=$false)][switch]$DisableDocumentBrowserView,
           [parameter(Mandatory=$false)][switch]$AllowPrint,
           [parameter(Mandatory=$false)][switch]$AllowScript,
           [parameter(Mandatory=$false)][switch]$AllowWriteCopy,
           [parameter(Mandatory=$false)][int]$DocumentAccessExpireDays,
           [parameter(Mandatory=$false)][int]$LicenseCacheExpireDays,
           [parameter(Mandatory=$false)][string]$GroupName
       )

       process
       {
           Write-Verbose "Applying IRM Configuration on '$($List.Title)'"

           # reset the value to the default settings
           $list.InformationRightsManagementSettings.Reset()

           $list.IrmEnabled = $true

           # IRM Policy title and description

               $list.InformationRightsManagementSettings.PolicyTitle       = $PolicyTitle
               $list.InformationRightsManagementSettings.PolicyDescription = $PolicyDescription

           # Set additional IRM library settings

               # Do not allow users to upload documents that do not support IRM
               $list.IrmReject = $IrmReject.IsPresent

               $parsedDate = Get-Date
               if([DateTime]::TryParse($ProtectionExpirationDate, [ref]$parsedDate))
               {
                   # Stop restricting access to the library at <date>
                   $list.IrmExpire = $true
                   $list.InformationRightsManagementSettings.DocumentLibraryProtectionExpireDate = $ProtectionExpirationDate
               }

               # Prevent opening documents in the browser for this Document Library
               $list.InformationRightsManagementSettings.DisableDocumentBrowserView = $DisableDocumentBrowserView.IsPresent

           # Configure document access rights

               # Allow viewers to print
               $list.InformationRightsManagementSettings.AllowPrint = $AllowPrint.IsPresent

               # Allow viewers to run script and screen reader to function on downloaded documents
               $list.InformationRightsManagementSettings.AllowScript = $AllowScript.IsPresent

               # Allow viewers to write on a copy of the downloaded document
               $list.InformationRightsManagementSettings.AllowWriteCopy = $AllowWriteCopy.IsPresent

               if($DocumentAccessExpireDays)
               {
                   # After download, document access rights will expire after these number of days (1-365)
                   $list.InformationRightsManagementSettings.EnableDocumentAccessExpire = $true
                   $list.InformationRightsManagementSettings.DocumentAccessExpireDays   = $DocumentAccessExpireDays
               }

           # Set group protection and credentials interval

               if($LicenseCacheExpireDays)
               {
                   # Users must verify their credentials using this interval (days)
                   $list.InformationRightsManagementSettings.EnableLicenseCacheExpire = $true
                   $list.InformationRightsManagementSettings.LicenseCacheExpireDays   = $LicenseCacheExpireDays
               }

               if($GroupName)
               {
                   # Allow group protection. Default group:
                   $list.InformationRightsManagementSettings.EnableGroupProtection = $true
                   $list.InformationRightsManagementSettings.GroupName             = $GroupName
               }
       }
       end
       {
           if($list)
           {
               Write-Verbose "Committing IRM configuration settings on '$($list.Title)'"
               $list.InformationRightsManagementSettings.Update()
               $list.Update()
               $script:clientContext.Load($list)
               $script:clientContext.ExecuteQuery()
           }
       }
   }

   function Get-CredentialFromCredentialCache
   {
       [cmdletbinding()]
       param([string]$CredentialName)

       #if( Test-Path variable:\global:CredentialCache )
       if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue )
       {
           if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName))
           {
               Write-Verbose "Credential Cache Hit: $CredentialName"
               return $global:O365TenantAdminCredentialCache[$CredentialName]
           }
       }
       Write-Verbose "Credential Cache Miss: $CredentialName"
       return $null
   }

   function Add-CredentialToCredentialCache
   {
       [cmdletbinding()]
       param([System.Management.Automation.PSCredential]$Credential)

       if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue))
       {
           Write-Verbose "Initializing the Credential Cache"
           $global:O365TenantAdminCredentialCache = @{}
       }

       Write-Verbose "Adding Credential to the Credential Cache"
       $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential
   }

   # load the required assemblies and Windows PowerShell modules

       if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return }

   # Add the credentials to the client context and SharePoint Online service connection

       # check for cached credentials to use
       $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin

       if(-not $o365TenantAdminCredential)
       {
           # when credentials are not cached, prompt for the tenant admin credentials
           $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin"

           if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 )
           {
               Write-Error -Message "Could not validate the supplied tenant admin credentials"
               return
           }

           # add the credentials to the cache
           Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential
       }

   # connect to Office365 first, required for SharePoint Online cmdlets to run

       Connect-SPOService -Url $sharepointAdminCenterUrl -Credential $o365TenantAdminCredential

   # enumerate each of the specified site URLs

       foreach($webUrl in $webUrls)
       {
           $grantedSiteCollectionAdmin = $false

           try
           {
               # establish the client context and set the credentials to connect to the site
               $script:clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($webUrl)
               $script:clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password)

               # initialize the site and web context
               $script:clientContext.Load($script:clientContext.Site)
               $script:clientContext.Load($script:clientContext.Web)
               $script:clientContext.ExecuteQuery()

               # load and ensure the tenant admin user account if present on the target SharePoint site
               $tenantAdminUser = $script:clientContext.Web.EnsureUser($o365TenantAdminCredential.UserName)
               $script:clientContext.Load($tenantAdminUser)
               $script:clientContext.ExecuteQuery()

               # check if the tenant admin is a site admin
               if( -not $tenantAdminUser.IsSiteAdmin )
               {
                   try
                   {
                       # grant the tenant admin temporary admin rights to the site collection
                       Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $true | Out-Null
                       $grantedSiteCollectionAdmin = $true
                   }
                   catch
                   {
                       Write-Error $_.Exception
                       return
                   }
               }

               try
               {
                   # load the list orlibrary using CSOM

                   $list = $null
                   $list = $script:clientContext.Web.Lists.GetByTitle($listTitle)
                   $script:clientContext.Load($list)
                   $script:clientContext.ExecuteQuery()

                   # **************  ADMIN INSTRUCTIONS  **************
                   # If necessary, modify the following Set-IrmConfiguration parameters to match your required values
                   # The supplied options and values are for example only
                   # Example that shows the Set-IrmConfiguration command with all parameters: Set-IrmConfiguration -List $list -PolicyTitle "Protected Files" -PolicyDescription "This policy restricts access to authorized users" -IrmReject -ProtectionExpirationDate $(Get-Date).AddDays(180) -DisableDocumentBrowserView -AllowPrint -AllowScript -AllowWriteCopy -LicenseCacheExpireDays 25 -DocumentAccessExpireDays 90

                   Set-IrmConfiguration -List $list -PolicyTitle "Protected Files" -PolicyDescription "This policy restricts access to authorized users"  
               }
               catch
               {
                   Write-Error -Message "Error setting IRM configuration on site: $webUrl.`nError Details: $($_.Exception.ToString())"
               }
          }
          finally
          {
               if($grantedSiteCollectionAdmin)
               {
                   # remove the temporary admin rights to the site collection
                   Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $false | Out-Null
               }
          }
       }

   Disconnect-SPOService -ErrorAction SilentlyContinue
   ```

4. Revise el script y realice los cambios siguientes:

   1. Busque `$sharepointAdminCenterUrl` y reemplace el valor de ejemplo con su propia dirección URL del centro de administración de SharePoint.

      Este valor aparecerá como URL base al entrar en el centro de administración de SharePoint y tendrá el siguiente formato: https://<em>&lt;nombre_inquilino>&gt;</em>-admin.sharepoint.com

      Por ejemplo, si el nombre del inquilino es "contoso", debería especificar: **https://contoso-admin.sharepoint.com**

   2. Busque `$tenantAdmin` y reemplace el valor de ejemplo por su propia cuenta de administrador global completa para Office 365.

      Este valor es el mismo que se usa para iniciar sesión en el portal de administración de Office 365 como administrador global y tiene el siguiente formato: nombre_usuario@*&lt;nombre_de_dominio_de inquilino&gt;*.com

      Por ejemplo, si el nombre de usuario de administrador global de Office 365 es "admin" en el dominio de inquilino "contoso.com", especificaría: <strong>admin@contoso.com</strong>

   3. Busque `$webUrls` y reemplace los valores del ejemplo por las direcciones URL de la página web de OneDrive para la Empresa de los usuarios y agregue o elimine tantas entradas como necesite.

      Como alternativa, vea los comentarios del script sobre cómo reemplazar esta matriz mediante la importación de un archivo .CSV que contiene todas las direcciones URL que es preciso configurar.  Hemos proporcionado otro script de ejemplo para buscar y extraer automáticamente las direcciones URL para rellenar este archivo .CSV. Cuando esté a punto, vea la sección [Script adicional para enviar todas las direcciones URL de OneDrive para la Empresa a un archivo .CSV](#additional-script-to-output-all-onedrive-for-business-urls-to-a-csv-file) justo después de estos pasos.

      La dirección URL de OneDrive para la Empresa del usuario tiene el siguiente formato: https://<em>&lt;nombre de inquilino&gt;</em>-my.sharepoint.com/personal/*&lt;nombre_usuario&gt;*_*&lt;nombre de inquilino&gt;*_com

      Por ejemplo, si el usuario del inquilino contoso tiene el nombre de usuario "rsimone", especificaría: **https://contoso-my.sharepoint.com/personal/rsimone_contoso_com**

   4. Dado que vamos a usar el script para configurar OneDrive para la Empresa, no cambie el valor de **Documentos** en la variable`$listTitle`.

   5. Busque `ADMIN INSTRUCTIONS`. Si no realiza cambios en esta sección, OneDrive para la Empresa del usuario se configurará para IRM con el título de directiva "Archivos protegidos" y la descripción "Esta directiva restringe el acceso a usuarios autorizados".  No se configurarán otras opciones de IRM, ya que es probable que sea lo más apropiado para la mayoría de los entornos. Sin embargo, es posible cambiar tanto el título de la directiva como la descripción sugeridos, así como agregar otras opciones de IRM que sean apropiadas para su entorno. Consulte el ejemplo comentado en el script, ya que le ayudará a construir su propio conjunto de parámetros para el comando Set-IrmConfiguration.

5. Guarde el script y fírmelo. Si no firma el script (más seguro), Windows PowerShell debe estar configurado en el equipo para ejecutar scripts sin firmar. Para ello, ejecute una sesión de Windows PowerShell con la opción **Ejecutar como administrador** y escriba: **Set-ExecutionPolicy Unrestricted**. Sin embargo, esta configuración permite la ejecución de todos los scripts sin firmar (menos seguro).

   Para obtener más información acerca de la firma de scripts de Windows PowerShell, consulte [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) en la biblioteca de documentación de PowerShell.

6. Ejecute el script y si se le solicita, especifique la contraseña de la cuenta de administrador de Office 365. Si modifica el script y lo ejecuta en la misma sesión de Windows PowerShell, no se le pedirán credenciales.

> [!TIP]
> Este script también se puede utilizar para configurar IRM para una biblioteca de SharePoint Online. Para esta configuración, es probable que desee habilitar la opción adicional **No permitir a los usuarios cargar documentos que no admitan IRM**, con el fin de asegurarse de que la biblioteca solo contiene documentos protegidos.    Para ello, agregue el parámetro `-IrmReject` al comando Set-IrmConfiguration del script.
>
> También tendría que modificar la variable `$webUrls` (por ejemplo, **https://contoso.sharepoint.com**) y la variable `$listTitle` (por ejemplo, **$Reports**).

Si tiene que deshabilitar IRM para las bibliotecas de OneDrive para la Empresa, consulte la sección [Script para deshabilitar IRM en OneDrive para la Empresa](#script-to-disable-irm-for-onedrive-for-business).

##### <a name="additional-script-to-output-all-onedrive-for-business-urls-to-a-csv-file"></a>Script adicional para enviar todas las direcciones URL de OneDrive para la Empresa a un archivo .CSV
En el paso 4c, puede utilizar el siguiente script de Windows PowerShell para extraer las direcciones URL de las bibliotecas de OneDrive para la Empresa de todos los usuarios, que después podrá comprobar, editar si es necesario e importar en el script principal.

Este script también requiere tanto el [SDK de componentes del cliente de SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=42038) como el [shell de administración de SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588). Siga las mismas instrucciones para copiarlo y pegarlo, guarde el archivo localmente (por ejemplo, "Report-OneDriveForBusinessSiteInfo.ps1"), modifique los valores `$sharepointAdminCenterUrl` y `$tenantAdmin` como antes y, a continuación, ejecute el script.

*&#42;&#42;Declinación de responsabilidades&#42;&#42;*: Este script de ejemplo no es compatible en ningún servicio o programa de soporte estándar de Microsoft. Este script de ejemplo se proporciona TAL CUAL sin garantía de ningún tipo.

```
# Requires Windows PowerShell version 3

<#
  Description:

    Queries the search service of an Office 365 tenant to retrieve all OneDrive for Business sites.  
    Details of the discovered sites are written to a .CSV file (by default,"OneDriveForBusinessSiteInfo_<date>.csv").

 Script Installation Requirements:

   SharePoint Online Client Components SDK
   https://www.microsoft.com/en-us/download/details.aspx?id=42038

   SharePoint Online Management Shell
   https://www.microsoft.com/en-us/download/details.aspx?id=35588

======
#>

# URL will be in the format https://<tenant-name>-admin.sharepoint.com
$sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com"

$tenantAdmin = "admin@contoso.onmicrosoft.com"                           

$reportName = "OneDriveForBusinessSiteInfo_$((Get-Date).ToString("yyyy-MM-dd_hh.mm.ss")).csv"

$oneDriveForBusinessSiteUrls= @()
$resultsProcessed = 0

function Load-SharePointOnlineClientComponentAssemblies
{
    [cmdletbinding()]
    param()

    process
    {
        # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI
        try
        {
            Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            return $true
        }
        catch
        {
            if($_.Exception.Message -match "Could not load file or assembly")
            {
                Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: https://www.microsoft.com/en-us/download/details.aspx?id=42038"
            }
            else
            {
                Write-Error -Exception $_.Exception
            }
            return $false
        }
    }
}

function Load-SharePointOnlineModule
{
    [cmdletbinding()]
    param()

    process
    {
        do
        {
            # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell
            $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue

            if(-not $spoModule)
            {
                try
                {
                    Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking
                    return $true
                }
                catch
                {
                    if($_.Exception.Message -match "Could not load file or assembly")
                    {
                        Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: https://www.microsoft.com/en-us/download/details.aspx?id=35588"
                    }
                    else
                    {
                        Write-Error -Exception $_.Exception
                    }
                    return $false
                }
            }
            else
            {
                return $true
            }
        }
        while(-not $spoModule)
    }
}

function Get-CredentialFromCredentialCache
{
    [cmdletbinding()]
    param([string]$CredentialName)

    #if( Test-Path variable:\global:CredentialCache )
    if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue )
    {
        if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName))
        {
            Write-Verbose "Credential Cache Hit: $CredentialName"
            return $global:O365TenantAdminCredentialCache[$CredentialName]
        }
    }
    Write-Verbose "Credential Cache Miss: $CredentialName"
    return $null
}

function Add-CredentialToCredentialCache
{
    [cmdletbinding()]
    param([System.Management.Automation.PSCredential]$Credential)

    if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue))
    {
        Write-Verbose "Initializing the Credential Cache"
        $global:O365TenantAdminCredentialCache = @{}
    }

    Write-Verbose "Adding Credential to the Credential Cache"
    $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential
}

# load the required assemblies and Windows PowerShell modules

    if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return }

# Add the credentials to the client context and SharePoint Online service connection

    # check for cached credentials to use
    $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin

    if(-not $o365TenantAdminCredential)
    {
        # when credentials are not cached, prompt for the tenant admin credentials
        $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin"

        if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 )
        {
            Write-Error -Message "Could not validate the supplied tenant admin credentials"
            return
        }

        # add the credentials to the cache
        Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential
    }

# establish the client context and set the credentials to connect to the site

    $clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($sharepointAdminCenterUrl)
    $clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password)

# run a query against the Office 365 tenant search service to retrieve all OneDrive for Business URLs

    do
    {
        # build the query object
        $query = New-Object Microsoft.SharePoint.Client.Search.Query.KeywordQuery($clientContext)
        $query.TrimDuplicates        = $false
        $query.RowLimit              = 500
        $query.QueryText             = "SPSiteUrl:'/personal/' AND contentclass:STS_Site"
        $query.StartRow              = $resultsProcessed
        $query.TotalRowsExactMinimum = 500000

        # run the query
        $searchExecutor = New-Object Microsoft.SharePoint.Client.Search.Query.SearchExecutor($clientContext)
        $queryResults = $searchExecutor.ExecuteQuery($query)
        $clientContext.ExecuteQuery()

        # enumerate the search results and store the site URLs
        $queryResults.Value[0].ResultRows | % {
            $oneDriveForBusinessSiteUrls += $_.Path
            $resultsProcessed++
        }
    }
    while($resultsProcessed -lt $queryResults.Value.TotalRows)

$oneDriveForBusinessSiteUrls | Out-File -FilePath $reportName
```

##### <a name="script-to-disable-irm-for-onedrive-for-business"></a>Script para deshabilitar IRM en OneDrive para la Empresa
Utilice el siguiente script de ejemplo si necesita deshabilitar IRM en OneDrive para la Empresa de los usuarios.

Este script también requiere tanto el [SDK de componentes del cliente de SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=42038) como el [shell de administración de SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588). Copie y pegue el contenido, guarde el archivo localmente (por ejemplo, "Disable-IRMOnOneDriveForBusiness.ps1") y modifique los valores `$sharepointAdminCenterUrl` y `$tenantAdmin`. Especifique manualmente las direcciones URL de OneDrive para la Empresa o use el script de la sección anterior para poder importarlas y, a continuación, ejecute el script.

*&#42;&#42;Declinación de responsabilidades&#42;&#42;*: Este script de ejemplo no es compatible en ningún servicio o programa de soporte estándar de Microsoft. Este script de ejemplo se proporciona TAL CUAL sin garantía de ningún tipo.

```
# Requires Windows PowerShell version 3

<#
  Description:

    Disables IRM for OneDrive for Business and can also be used for SharePoint Online libraries and lists

 Script Installation Requirements:

   SharePoint Online Client Components SDK
   https://www.microsoft.com/en-us/download/details.aspx?id=42038

   SharePoint Online Management Shell
   https://www.microsoft.com/en-us/download/details.aspx?id=35588

======
#>

$sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com"

$tenantAdmin = "admin@contoso.com"

$webUrls = @("https://contoso-my.sharepoint.com/personal/user1_contoso_com",
             "https://contoso-my.sharepoint.com/personal/user2_contoso_com",
             "https://contoso-my.sharepoint.com/personal/person3_contoso_com")

<# As an alternative to specifying the URLs as an array, you can import them from a CSV file (no header, single value per row).
   Then, use: $webUrls = Get-Content -Path "File_path_and_name.csv"

#>

$listTitle = "Documents"

function Load-SharePointOnlineClientComponentAssemblies
{
    [cmdletbinding()]
    param()

    process
    {
        # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI
        try
        {
            Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            return $true
        }
        catch
        {
            if($_.Exception.Message -match "Could not load file or assembly")
            {
                Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: https://www.microsoft.com/en-us/download/details.aspx?id=42038"
            }
            else
            {
                Write-Error -Exception $_.Exception
            }
            return $false
        }
    }
}

function Load-SharePointOnlineModule
{
    [cmdletbinding()]
    param()

    process
    {
        do
        {
            # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell
            $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue

            if(-not $spoModule)
            {
                try
                {
                    Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking
                    return $true
                }
                catch
                {
                    if($_.Exception.Message -match "Could not load file or assembly")
                    {
                        Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: https://www.microsoft.com/en-us/download/details.aspx?id=35588"
                    }
                    else
                    {
                        Write-Error -Exception $_.Exception
                    }
                    return $false
                }
            }
            else
            {
                return $true
            }
        }
        while(-not $spoModule)
    }
}

function Remove-IrmConfiguration
{
    [cmdletbinding()]
    param(
        [parameter(Mandatory=$true)][Microsoft.SharePoint.Client.List]$List
    )

    process
    {
        Write-Verbose "Disabling IRM Configuration on '$($List.Title)'"

        $List.IrmEnabled = $false
        $List.IrmExpire  = $false
        $List.IrmReject  = $false
        $List.InformationRightsManagementSettings.Reset()
    }
    end
    {
        if($List)
        {
            Write-Verbose "Committing IRM configuration settings on '$($list.Title)'"
            $list.InformationRightsManagementSettings.Update()
            $list.Update()
            $script:clientContext.Load($list)
            $script:clientContext.ExecuteQuery()
        }
    }
}

function Get-CredentialFromCredentialCache
{
    [cmdletbinding()]
    param([string]$CredentialName)

    #if( Test-Path variable:\global:CredentialCache )
    if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue )
    {
        if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName))
        {
            Write-Verbose "Credential Cache Hit: $CredentialName"
            return $global:O365TenantAdminCredentialCache[$CredentialName]
        }
    }
    Write-Verbose "Credential Cache Miss: $CredentialName"
    return $null
}

function Add-CredentialToCredentialCache
{
    [cmdletbinding()]
    param([System.Management.Automation.PSCredential]$Credential)

    if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue))
    {
        Write-Verbose "Initializing the Credential Cache"
        $global:O365TenantAdminCredentialCache = @{}
    }

    Write-Verbose "Adding Credential to the Credential Cache"
    $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential
}

# load the required assemblies and Windows PowerShell modules

    if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return }

# Add the credentials to the client context and SharePoint Online service connection

    # check for cached credentials to use
    $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin

    if(-not $o365TenantAdminCredential)
    {
        # when credentials are not cached, prompt for the tenant admin credentials
        $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin"

        if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 )
        {
            Write-Error -Message "Could not validate the supplied tenant admin credentials"
            return
        }

        # add the credentials to the cache
        Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential
    }

# connect to Office365 first, required for SharePoint Online cmdlets to run

    Connect-SPOService -Url $sharepointAdminCenterUrl -Credential $o365TenantAdminCredential

# enumerate each of the specified site URLs

    foreach($webUrl in $webUrls)
    {
        $grantedSiteCollectionAdmin = $false

        try
        {
            # establish the client context and set the credentials to connect to the site
            $script:clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($webUrl)
            $script:clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password)

            # initialize the site and web context
            $script:clientContext.Load($script:clientContext.Site)
            $script:clientContext.Load($script:clientContext.Web)
            $script:clientContext.ExecuteQuery()

            # load and ensure the tenant admin user account if present on the target SharePoint site
            $tenantAdminUser = $script:clientContext.Web.EnsureUser($o365TenantAdminCredential.UserName)
            $script:clientContext.Load($tenantAdminUser)
            $script:clientContext.ExecuteQuery()

            # check if the tenant admin is a site admin
            if( -not $tenantAdminUser.IsSiteAdmin )
            {
                try
                {
                    # grant the tenant admin temporary admin rights to the site collection
                    Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $true | Out-Null
                    $grantedSiteCollectionAdmin = $true
                }
                catch
                {
                    Write-Error $_.Exception
                    return
                }
            }

            try
            {
                # load the list orlibrary using CSOM

                $list = $null
                $list = $script:clientContext.Web.Lists.GetByTitle($listTitle)
                $script:clientContext.Load($list)
                $script:clientContext.ExecuteQuery()

               Remove-IrmConfiguration -List $list                 
            }
            catch
            {
                Write-Error -Message "Error setting IRM configuration on site: $webUrl.`nError Details: $($_.Exception.ToString())"
            }
       }
       finally
       {
            if($grantedSiteCollectionAdmin)
            {
                # remove the temporary admin rights to the site collection
                Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $false | Out-Null
            }
       }
    }

Disconnect-SPOService -ErrorAction SilentlyContinue
```

