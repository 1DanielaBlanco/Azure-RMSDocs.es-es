---
title: Configurar IRM de Exchange Online para el servicio Azure Rights Management de Azure Information Protection
description: Información e instrucciones para que los administradores configuren Exchange Online para el servicio Azure Rights Management cuando el inquilino de Office 365 no admite las nuevas capacidades de cifrado de mensajes de Office 365.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/11/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ''
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: e452f5ac4e3297106a54a2034d64f57d8f6d5302
ms.sourcegitcommit: affda7572064edaf9e3b63d88f4a18d0d6932b13
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="exchange-online-irm-configuration-to-import-a-trusted-publishing-domain"></a>Configuración de IRM de Exchange Online para importar un dominio de publicación de confianza

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Utilice estas instrucciones solo si su inquilino no puede utilizar las nuevas funcionalidades del cifrado de mensajes de Office 365. Para confirmar, ejecute el comando de Exchange Online [Get-IRMConfiguration](https://technet.microsoft.com/library/dd776120(v=exchg.160\).aspx) y compruebe si tiene un parámetro **AzureRMSLicensingEnabled**. Si ve este parámetro, el inquilino puede utilizar las nuevas funcionalidades del cifrado de mensajes de Office 365:

- Si **AzureRMSLicensingEnabled** se establece en **True**, el inquilino ya utiliza las nuevas funcionalidades de cifrado de mensajes de Office 365 y no debe utilizar las instrucciones que aparecen en la sección siguiente.

- Si **AzureRMSLicensingEnabled** se establece **False**, el inquilino admite las nuevas funcionalidades de cifrado de mensajes de Office 365 pero todavía no se ha configurado para ello. Para configurar al inquilino para esas nuevas funcionalidades del cifrado de mensajes consulte [Set up new Office 365 Message Encryption capabilities built on top of Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e) (Configuración de las nuevas funcionalidades del cifrado de mensajes de Office 365 basadas en Azure Information Protection). 

Solo si el inquilino no es compatible con las nuevas funcionalidades del cifrado de mensajes de Office 365, siga las instrucciones que se indican a continuación.

## <a name="exchange-online-irm-configuration"></a>Configuración de IRM de Exchange Online

Para configurar IRM de Exchange Online, use Windows PowerShell (no es preciso instalar un módulo independiente) y ejecute los [comandos de PowerShell para Exchange Online](https://technet.microsoft.com/library/jj200677.aspx).

> [!NOTE]
> Hasta que Microsoft migre el inquilino de Office 365 para admitir nuevas funcionalidades, no se puede configurar Exchange Online para que admita el servicio Azure Rights Management si usa una clave de inquilino administrada por el cliente (BYOK) para Azure Information Protection, en lugar de la configuración predeterminada de una clave de inquilino administrada por Microsoft.
>
> Si intenta configurar Exchange Online cuando el servicio Azure Rights Management usa BYOK, el comando para importar la clave (paso 5, en el siguiente procedimiento) generará un error con el mensaje **[FailureCategory=Cmdlet-FailedToGetTrustedPublishingDomainFromRmsOnlineException]**.

Los pasos siguientes proporcionan un conjunto típico de comandos que se ejecutarían para habilitar IRM de Exchange Online:

1.  Si es la primera vez que ha usado Windows PowerShell para Exchange Online en el equipo, debe configurar Windows PowerShell para ejecutar scripts firmados. Inicie una sesión de Windows PowerShell mediante la opción **Ejecutar como administrador** y, luego, escriba:

    ```
    Set-ExecutionPolicy RemoteSigned
    ```

2.  En la sesión de Windows PowerShell, inicie sesión en Exchange Online con una cuenta que está habilitada para el acceso al shell remoto. De manera predeterminada, todas las cuentas que se crean en Exchange Online están habilitadas para el acceso remoto al shell, pero esto se puede deshabilitar (y habilitar) con el comando [Set-User &lt;UserIdentity&gt; -RemotePowerShellEnabled](https://technet.microsoft.com/library/jj984292%28v=exchg.160%29.aspx).

    Para iniciar sesión, escriba:

    ```
    $UserCredential = Get-Credential
    ```
    En el cuadro de diálogo **Solicitud de credenciales para Windows PowerShell** , proporcione el nombre de usuario y la contraseña de Office 365.

3.  Conecte con el servicio Exchange Online mediante la ejecución de los dos comandos siguientes:

    ```
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection
    ```

    ```
    Import-PSSession $Session
    ```

4.  Especifique la ubicación de la clave de inquilino de Azure Information Protection, según dónde se ha creado el inquilino de su organización:

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

5.  Importe datos de configuración desde el servicio Azure Rights Management en Exchange Online, en forma del dominio de publicación de confianza (TPD). Esto incluye la clave de inquilino de Azure Information Protection y plantillas de Azure Rights Management:

    ```
    Import-RMSTrustedPublishingDomain -RMSOnline -name "RMS Online"
    ```
    En este comando hemos usado el nombre de **RMS Online** como nombre base de TDP para Azure Rights Management en Exchange Online. Una vez importado el TPD, se denomina **RMS Online - 1** en Exchange Online.

6.  Habilite la funcionalidad de Azure Rights Management para que las características de IRM estén disponibles para Exchange Online:

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

Los usuarios pueden proteger ahora sus mensajes de correo electrónico mediante el uso del servicio Azure Rights Management. Por ejemplo, en Outlook Web App, seleccione **Establecer permisos** en el menú extendido (**...**) y, luego, elija **No reenviar** o una de las plantillas disponibles para aplicar la protección de la información al mensaje de correo y los datos adjuntos. Sin embargo, dado que la aplicación web de Outlook almacena en caché de interfaz de usuario durante un día, espere a que transcurra ese período de tiempo antes de intentar aplicar la protección de la información a los mensajes de correo electrónico y después de ejecutar estos comandos de configuración. Antes de que las actualizaciones de la interfaz de usuario reflejen la nueva configuración, no verá ninguna de las opciones del menú **Establecer permisos** .

> [!IMPORTANT]
> Si crea nuevas [plantillas personalizadas](configure-custom-templates.md) para Azure Rights Management o actualiza las plantillas, deberá ejecutar cada vez el siguiente comando de PowerShell para Exchange Online (si es necesario, ejecute primero los pasos 2 y 3) para sincronizar esos cambios con Exchange Online: `Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates –RMSOnline`

Como administrador de Exchange, ahora puede configurar las características que aplican automáticamente protección de la información, como [reglas de transporte](https://technet.microsoft.com/library/dd302432.aspx), [directivas de prevención de pérdida de datos (DLP)](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx)y [correo de voz protegido](https://technet.microsoft.com/library/dn198211%28v=exchg.150%29.aspx) (mensajería unificada).


### <a name="office-365-message-encryption"></a>Cifrado de mensajes de Office 365
Siga los mismos pasos de la sección anterior pero, si no quiere que se muestren las plantillas, antes de realizar el paso 6 ejecute el comando siguiente para evitar que las plantillas de IRM estén disponibles en Outlook Web App y el cliente de Outlook: `Set-IRMConfiguration -ClientAccessServerEnabled $false`

Ya está listo para configurar [reglas de transporte](https://technet.microsoft.com/library/dd302432.aspx) con el objeto de modificar automáticamente la seguridad de los mensajes cuando los destinatarios se encuentran fuera de la organización y seleccionar la opción **Aplicar el cifrado de mensajes de Office 365** .

Para obtener más información sobre el cifrado de mensajes, vea [Cifrado en Office 365](https://technet.microsoft.com/library/dn569286.aspx) en la biblioteca de Exchange.


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
