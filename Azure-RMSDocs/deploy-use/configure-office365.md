---
title: "Office 365&colon; Configuración para clientes y servicios en línea | Azure RMS"
description: "Información e instrucciones para que los administradores configuren Office 365 para trabajar con Azure Rights Management (Azure RMS)."
author: cabailey
manager: mbaldwin
ms.date: 09/20/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0a6ce612-1b6b-4e21-b7fd-bcf79e492c3b
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 18498a6d1edac11b20842b0cca0c4559909d681e
ms.openlocfilehash: e8e2abe6006f40f5c2e34ef0d4ac3f1ccaf66516


---

# Office 365: Configuración para clientes y servicios en línea

>*Se aplica a: Azure Rights Management, Office 365*

Como Office 365 es compatible de forma nativa con Azure RMS, no se requiere ninguna configuración para equipo cliente para conseguir la compatibilidad con las funciones de Information Rights Management (IRM) para aplicaciones como Word, Excel, PowerPoint, Outlook y la aplicación web de Outlook. Todo lo que tienen que hacer los usuarios es iniciar sesión en sus aplicaciones Office con sus credenciales de [!INCLUDE[o365_1](../includes/o365_1_md.md)] y pueden proteger archivos y correos electrónicos, así como usar los que hayan sido protegidos por otros usuarios.

Sin embargo, se recomienda que complemente estas aplicaciones con la aplicación de uso compartido Rights Management, para que los usuarios obtengan los beneficios del complemento de Office. Para más información, consulte la sección [Aplicación de uso compartido Rights Management: Instalación y configuración para clientes](configure-sharing-app.md).

## Exchange Online: Configuración de IRM
Para configurar Exchange Online para que sea compatible con Azure RMS, debe configurar el servicio Information Rights Management (IRM) para Exchange Online. Para ello, use Windows PowerShell (no es preciso instalar un módulo independiente) y ejecute los [comandos de PowerShell para Exchange Online](https://technet.microsoft.com/library/jj200677.aspx).

> [!NOTE]
> Actualmente, no se puede configurar Exchange Online para admitir Azure RMS si usa una clave de inquilino administrada por el cliente (BYOK) con Azure RMS, en lugar de la configuración predeterminada de una clave de inquilino administrada por Microsoft. Para más información, consulte [Precio y restricciones de BYOK](../plan-design/byok-price-restrictions.md).
>
> Si intenta configurar Exchange Online cuando Azure RMS usa BYOK, el comando para importar la clave (paso 5, en el siguiente procedimiento) generará un error con el mensaje **[FailureCategory=Cmdlet-FailedToGetTrustedPublishingDomainFromRmsOnlineException]**.

Los pasos siguientes proporcionan un conjunto típico de comandos que se ejecutarían para permitir que Exchange Online usara Azure RMS:

1.  Si es la primera vez que ha usado Windows PowerShell para Exchange Online en el equipo, debe configurar Windows PowerShell para ejecutar scripts firmados. Inicie una sesión de Windows PowerShell mediante la opción **Ejecutar como administrador** y, luego, escriba:

    ```
    Set-ExecutionPolicy RemoteSigned
    ```

2.  En la sesión de Windows PowerShell, inicie sesión en Exchange Online con una cuenta que está habilitada para el acceso al shell remoto. De forma predeterminada, todas las cuentas que se crean en Exchange Online están habilitadas para el acceso remoto al shell, pero esto se puede deshabilitar (y habilitar) con el comando [Set-User &lt;UserIdentity&gt; -RemotePowerShellEnabled](https://technet.microsoft.com/library/jj984292%28v=exchg.160%29.aspx).

    Para iniciar sesión, escriba:

    ```
    $Cred = Get-Credential
    ```
    En el cuadro de diálogo **Solicitud de credenciales para Windows PowerShell** , proporcione el nombre de usuario y la contraseña de Office 365.

3.  Conecte con el servicio Exchange Online mediante la ejecución de los dos comandos siguientes:

    ```
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
    ```

    ```
    Import-PSSession $Session
    ```

4.  Especifique la ubicación de la clave de inquilino de Azure RMS, según dónde se creara el inquilino de su organización:

    Para América del Norte:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.na.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    Para Europa:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.eu.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    Para Asia:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.ap.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    Para Sudamérica:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.sa.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    Para Office 365 Administración Pública (nube de la comunidad de administración pública):

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.govus.aadrm.com/TenantManagement/ServicePartner.svc"
    ```

5.  Importe datos de configuración de Azure RMS en Exchange Online, en forma del dominio de publicación de confianza (TPD). Esto incluye la clave de inquilino y las plantillas de Azure RMS:

    ```
    Import-RMSTrustedPublishingDomain -RMSOnline -name "RMS Online"
    ```
    En este comando hemos usado el nombre de **RMS Online** como nombre base de TDP para Azure RMS en Exchange Online. Una vez importado el TPD, se denomina **RMS Online - 1** en Exchange Online.

6.  Habilite la funcionalidad de Azure RMS para que las características de IRM estén disponibles para Exchange Online:

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $true
    ```
    Después de ejecutar este comando, Rights Management se habilita automáticamente para el cliente de Outlook, la aplicación web de Outlook y Exchange Active Sync.

7.  Opcionalmente, pruebe que esta configuración es correcta mediante el siguiente comando:

    ```
    Test-IRMConfiguration -Sender <user email address>
    ```
    Por ejemplo: **Test-IRMConfiguration -Sender  adams@contoso.com**

    Este comando ejecuta una serie de comprobaciones que incluyen la comprobación de la conectividad con el servicio y la recuperación de la configuración, los URI, las licencias y las plantillas. En la sesión de Windows PowerShell verá los resultados de cada uno y, al final, si todo pasa estas comprobaciones: **RESULTADO GLOBAL: CORRECTO**

8.  Desconecte la sesión remota de PowerShell:

    ```
    Remove-PSSession $Session
    ```

Los usuarios pueden proteger ahora sus mensajes de correo electrónico mediante el uso de Azure RMS. Por ejemplo, en la aplicación web de Outlook, seleccione **Establecer permisos** en el menú extendido (**...**) y, luego, elija **No reenviar** o una de las plantillas disponibles para aplicar la protección de la información al mensaje de correo electrónico y los datos adjuntos. Sin embargo, dado que la aplicación web de Outlook almacena en caché de interfaz de usuario durante un día, espere a que transcurra ese período de tiempo antes de intentar aplicar la protección de la información a los mensajes de correo electrónico y después de ejecutar estos comandos de configuración. Antes de que las actualizaciones de la interfaz de usuario reflejen la nueva configuración, no verá ninguna de las opciones del menú **Establecer permisos** .

> [!IMPORTANT]
> Si crea nuevas [plantillas personalizadas](configure-custom-templates.md) para Azure RMS o actualiza las plantillas cada vez, debe ejecutar el siguiente comando de PowerShell para Exchange Online (si es necesario, ejecute primero los pasos 2 y 3) para sincronizar dichos cambios con Exchange Online: `Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates –RMSOnline`

Como administrador de Exchange, ahora puede configurar las características que aplican automáticamente protección de la información, como [reglas de transporte](https://technet.microsoft.com/library/dd302432.aspx), [directivas de prevención de pérdida de datos (DLP)](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx)y [correo de voz protegido](https://technet.microsoft.com/library/dn198211%28v=exchg.150%29.aspx) (mensajería unificada).

Para obtener instrucciones detalladas para configurar Exchange Online para permitir la funcionalidad de IRM, vea la documentación de la biblioteca de Exchange. Por ejemplo:

-   [Conexión a Exchange Online mediante PowerShell remoto](https://technet.microsoft.com/library/jj984289%28v=exchg.160%29.aspx)

-   [Configuración de IRM para usar Azure Rights Management](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx)

### Cifrado de mensajes de Office 365
Ejecute los mismos pasos que se documentan en la sección anterior, pero si no desea que se muestren las plantillas, antes del paso 6, ejecute el comando siguiente para evitar que las plantillas de IRM estén disponible la aplicación web de Outlook y el cliente de Outlook: `Set-IRMConfiguration -ClientAccessServerEnabled $false`

Ya está listo para configurar [reglas de transporte](https://technet.microsoft.com/library/dd302432.aspx) con el objeto de modificar automáticamente la seguridad de los mensajes cuando los destinatarios se encuentran fuera de la organización y seleccionar la opción **Aplicar el cifrado de mensajes de Office 365** .

Para obtener más información sobre el cifrado de mensajes, vea [Cifrado en Office 365](https://technet.microsoft.com/library/dn569286.aspx) en la biblioteca de Exchange.

## SharePoint Online y OneDrive para la Empresa: Configuración de IRM
Para configurar SharePoint Online y OneDrive para la Empresa de forma que sean compatibles con Azure RMS, primero debe habilitar el servicio Information Rights Management (IRM) para SharePoint Online mediante el centro de administración de SharePoint. Luego, los propietarios de sitios pueden proteger con IRM sus listas y bibliotecas de documentos de SharePoint, y los usuarios pueden proteger con IRM su biblioteca de OneDrive para la Empresa, de modo que los documentos que están guardados ahí, y que se comparten con otros, estén protegidos automáticamente con Azure RMS.

Para habilitar el servicio Information Rights Management (IRM) para SharePoint Online, vea las siguientes instrucciones en el sitio web de Office:

-   [Configuración de Information Rights Management (IRM) en el centro de administración de SharePoint](http://office.microsoft.com/office365-sharepoint-online-enterprise-help/set-up-information-rights-management-irm-insharepoint-online-HA102895193.aspx)

Esta configuración se realiza mediante el administrador de Office 365.

### Configuración de IRM para listas y bibliotecas
Después de haber habilitado el servicio IRM para SharePoint, los propietarios de sitios pueden proteger con IRM sus listas y bibliotecas de documentos de SharePoint. Para obtener instrucciones, vea los recursos siguientes en el sitio web de Office:

-   [Aplicación de Information Rights Management a una lista o biblioteca](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)

Esta configuración se realiza mediante el administrador de sitios de SharePoint.

### Configuración de IRM para OneDrive para la Empresa
Después de haber habilitado el servicio IRM para SharePoint Online, la biblioteca de documentos OneDrive para la Empresa de los usuarios se puede configurar para la protección de Rights Management.  Los usuarios pueden configurarlo por sí mismos con el icono **Configuración** de su OneDrive. Aunque los administradores no pueden configurar Rights Management para OneDrive para la Empresa mediante el centro de administración de SharePoint, pueden hacerlo con Windows PowerShell.

> [!NOTE]
> Para más información acerca de cómo configurar OneDrive para la Empresa, consulte la documentación de Office, [Configurar OneDrive para el negocio en Office 365](https://support.office.com/article/Set-up-OneDrive-for-Business-in-Office-365-3e21f8f0-e0a1-43be-aa3e-8c0236bf11bb).

#### Configuración de los usuarios
Dé a los usuarios estas instrucciones para que puedan configurar su OneDrive para la Empresa y para proteger mediante IRM los archivos de su empresa.

1.  En OneDrive, haga clic en el icono **Configuración** para abrir el menú de configuración y, luego, haga clic en **Contenido del sitio**.

2.  Mantenga el mouse sobre el icono **Documentos** , elija el botón de puntos suspensivos (**...**) y, luego, haga clic en **CONFIGURACIÓN**.

3.  En la página **Configuración** , en la sección **Permisos y administración** , haga clic en **Information Rights Management**.

4.  En la página **Configuración de Information Rights Management** , seleccione la casilla **Limitar permisos de descarga de esta biblioteca** , especifique la elección del nombre y una descripción de los permisos y, si lo desea, haga clic en **MOSTRAR OPCIONES** para realizar configuraciones opcionales. A continuación, haga clic en **Aceptar**.

    Para obtener más información sobre las opciones de configuración, consulte las instrucciones que se indican en [Aplicación de Information Rights Management a una lista o biblioteca](https://support.office.com/article/Apply-Information-Rights-Management-to-a-list-or-library-3bdb5c4e-94fc-4741-b02f-4e7cc3c54aa1) de la documentación de Office.

Dado que esta configuración confía en los usuarios, en lugar de en el administrador, para proteger con IRM su biblioteca OneDrive para la Empresa, muestre a los usuarios las ventajas de proteger sus archivos y cómo hacerlo. Por ejemplo, explique que cuando comparten un documento de OneDrive para la Empresa, solo las personas que ellos autorizan pueden tener a él acceso con cualquier restricción que configuren, incluso si se cambia el nombre del archivo o se copia en otra parte.

#### Configuración para administradores
Aunque IRM no se puede configurar para OneDrive para la Empresa de los usuarios mediante el centro de administración de SharePoint, se puede hacer con Windows PowerShell. Para habilitar IRM en estas bibliotecas, siga estos pasos:

1.  Descargue e instale el [SDK de componentes del cliente de SharePoint Online](http://www.microsoft.com/en-us/download/details.aspx?id=42038).

2.  Descargue e instale el [shell de administración de SharePoint Online](http://www.microsoft.com/en-us/download/details.aspx?id=35588).

3.  Copie el contenido del siguiente script y denomine Set-IRMOnOneDriveForBusiness.ps1 al archivo en el equipo.

    *&#42;&#42;Aviso de declinación de responsabilidades&#42;&#42;:* este script de ejemplo no es compatible con ningún servicio o programa de soporte técnico Standard de Microsoft. Este script de ejemplo se proporciona TAL CUAL sin garantía de ningún tipo.

    ```
    # Requires Windows PowerShell version 3

    <#
      Description:

        Configures IRM policy settings for OneDrive for Business and can also be used for SharePoint Online libraries and lists

     Script Installation Requirements:

       SharePoint Online Client Components SDK
       http://www.microsoft.com/en-us/download/details.aspx?id=42038

       SharePoint Online Management Shell
       http://www.microsoft.com/en-us/download/details.aspx?id=35588

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
                    Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038"
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
                            Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588"
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

4.  Revise el script y realice los cambios siguientes:

    1.  Busque `$sharepointAdminCenterUrl` y reemplace el valor de ejemplo con su propia dirección URL del centro de administración de SharePoint.

        Este valor aparecerá como URL base al entrar en el centro de administración de SharePoint y tendrá el siguiente formato: https://*&lt;nombre_inquilino>&gt;*-admin.sharepoint.com

        Por ejemplo, si el nombre de inquilino es "contoso", debería especificar: **https://contoso-admin.sharepoint.com**.

    2.  Busque `$tenantAdmin` y reemplace el valor de ejemplo por su propia cuenta de administrador global completa para Office 365.

        Este valor es el mismo que se usa para iniciar sesión en el portal de administración de Office 365 como administrador global y tiene el siguiente formato: nombre_usuario@*&lt;nombre_de_dominio_de inquilino&gt;*.com

        Por ejemplo, si el nombre de usuario de administrador global de Office 365 fuese "admin" en el dominio de inquilino "contoso.com", especificaría: **admin@contoso.com**.

    3.  Busque `$webUrls` y reemplace los valores del ejemplo por las direcciones URL de la página web de OneDrive para la Empresa de los usuarios y agregue o elimine tantas entradas como necesite.

        Como alternativa, vea los comentarios del script sobre cómo reemplazar esta matriz mediante la importación de un archivo .CSV que contiene todas las direcciones URL que es preciso configurar.  Hemos proporcionado otro script de ejemplo para buscar y extraer automáticamente las direcciones URL para rellenar este archivo .CSV. Cuando esté a punto, vea la sección [Script adicional para enviar todas las direcciones URL de OneDrive para la Empresa a un archivo .CSV](#additional-script-to-output-all-onedrive-for-business-urls-to-a-csv-file) justo después de estos pasos.

        La dirección URL de OneDrive para la Empresa del usuario tiene el siguiente formato: https://*&lt;nombre de inquilino&gt;*-my.sharepoint.com/personal/*&lt;nombre_usuario&gt;*_*&lt;nombre de inquilino&gt;*_com

        Por ejemplo, si el usuario del inquilino contoso tiene el nombre de usuario "rsimone", especificaría: **https://contoso-my.sharepoint.com/personal/rsimone_contoso_com**.

    4.  Dado que vamos a usar el script para configurar OneDrive para la Empresa, no cambie el valor de **Documentos** en la variable`$listTitle`.

    5.  Busque `ADMIN INSTRUCTIONS`. Si no realiza cambios en esta sección, OneDrive para la Empresa del usuario se configurará para IRM con el título de directiva "Archivos protegidos" y la descripción "Esta directiva restringe el acceso a usuarios autorizados".  No se configurarán otras opciones de IRM, ya que es probable que sea lo más apropiado para la mayoría de los entornos. Sin embargo, es posible cambiar tanto el título de la directiva como la descripción sugeridos, así como agregar otras opciones de IRM que sean apropiadas para su entorno. Consulte el ejemplo comentado en el script, ya que le ayudará a construir su propio conjunto de parámetros para el comando Set-IrmConfiguration.

5.  Guarde el script y fírmelo. Si no firma el script (más seguro), Windows PowerShell debe estar configurado en el equipo para ejecutar scripts sin firmar. Para hacerlo, ejecute una sesión de Windows PowerShell mediante la opción **Ejecutar como administrador** y escriba: **Set-ExecutionPolicy Unrestricted**. Sin embargo, esta configuración permite la ejecución de todos los scripts sin firmar (menos seguro).

    Para obtener más información acerca de la firma de scripts de Windows PowerShell, consulte [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) en la biblioteca de documentación de PowerShell.

6.  Ejecute el script y si se le solicita, especifique la contraseña de la cuenta de administrador de Office 365. Si modifica el script y lo ejecuta en la misma sesión de Windows PowerShell, no se le pedirán credenciales.

> [!TIP]
> Este script también se puede utilizar para configurar IRM para una biblioteca de SharePoint Online. Para esta configuración, es probable que desee habilitar la opción adicional **No permitir a los usuarios cargar documentos que no admitan IRM**, con el fin de asegurarse de que la biblioteca solo contiene documentos protegidos.    Para ello, agregue el parámetro `-IrmReject` al comando Set-IrmConfiguration del script.
>
> También tendría que modificar la variable `$webUrls` (por ejemplo, **https://contoso.sharepoint.com**) y la variable `$listTitle` (por ejemplo, **$Reports**).

Si tiene que deshabilitar IRM para las bibliotecas de OneDrive para la Empresa, consulte la sección [Script para deshabilitar IRM en OneDrive para la Empresa](#script-to-disable-irm-for-onedrive-for-business).

##### Script adicional para enviar todas las direcciones URL de OneDrive para la Empresa a un archivo .CSV
En el paso 4c, puede utilizar el siguiente script de Windows PowerShell para extraer las direcciones URL de las bibliotecas de OneDrive para la Empresa de todos los usuarios, que después podrá comprobar, editar si es necesario e importar en el script principal.

Este script también requiere tanto el [SDK de componentes del cliente de SharePoint Online](http://www.microsoft.com/en-us/download/details.aspx?id=42038) como el [shell de administración de SharePoint Online](http://www.microsoft.com/en-us/download/details.aspx?id=35588). Siga las mismas instrucciones para copiarlo y pegarlo, guarde el archivo localmente (por ejemplo, "Report-OneDriveForBusinessSiteInfo.ps1"), modifique los valores `$sharepointAdminCenterUrl` y `$tenantAdmin` como antes y, a continuación, ejecute el script.

*&#42;&#42;Aviso de declinación de responsabilidades&#42;&#42;:* este script de ejemplo no es compatible con ningún servicio o programa de soporte técnico Standard de Microsoft. Este script de ejemplo se proporciona TAL CUAL sin garantía de ningún tipo.

```
# Requires Windows PowerShell version 3

<#
  Description:

    Queries the search service of an Office 365 tenant to retrieve all OneDrive for Business sites.  
    Details of the discovered sites are written to a .CSV file (by default,"OneDriveForBusinessSiteInfo_<date>.csv").

 Script Installation Requirements:

   SharePoint Online Client Components SDK
   http://www.microsoft.com/en-us/download/details.aspx?id=42038

   SharePoint Online Management Shell
   http://www.microsoft.com/en-us/download/details.aspx?id=35588

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
                Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038"
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
                        Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588"
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

##### Script para deshabilitar IRM en OneDrive para la Empresa
Utilice el siguiente script de ejemplo si necesita deshabilitar IRM en OneDrive para la Empresa de los usuarios.

Este script también requiere tanto el [SDK de componentes del cliente de SharePoint Online](http://www.microsoft.com/en-us/download/details.aspx?id=42038) como el [shell de administración de SharePoint Online](http://www.microsoft.com/en-us/download/details.aspx?id=35588). Copie y pegue el contenido, guarde el archivo localmente (por ejemplo, "Disable-IRMOnOneDriveForBusiness.ps1") y modifique los valores `$sharepointAdminCenterUrl` y `$tenantAdmin`. Especifique manualmente las direcciones URL de OneDrive para la Empresa o use el script de la sección anterior para poder importarlas y, a continuación, ejecute el script.

*&#42;&#42;Aviso de declinación de responsabilidades&#42;&#42;:* este script de ejemplo no es compatible con ningún servicio o programa de soporte técnico Standard de Microsoft. Este script de ejemplo se proporciona TAL CUAL sin garantía de ningún tipo.

```
# Requires Windows PowerShell version 3

<#
  Description:

    Disables IRM for OneDrive for Business and can also be used for SharePoint Online libraries and lists

 Script Installation Requirements:

   SharePoint Online Client Components SDK
   http://www.microsoft.com/en-us/download/details.aspx?id=42038

   SharePoint Online Management Shell
   http://www.microsoft.com/en-us/download/details.aspx?id=35588

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
                Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038"
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
                        Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588"
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




<!--HONumber=Sep16_HO3-->


