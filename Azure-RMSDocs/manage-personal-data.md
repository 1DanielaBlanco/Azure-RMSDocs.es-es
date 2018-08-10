---
title: Administración de datos personales de Azure Information Protection
description: Información sobre los datos personales que usa Azure Information Protection y cómo puede verlos, exportarlos y eliminarlos.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/16/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 99a51862-83e9-4a1e-873a-a84ae1465f07
ms.reviewer: aashishr
ms.suite: ems
ms.openlocfilehash: 17ec391c31285687819fe1a2d1b40baf4c31cd44
ms.sourcegitcommit: 5fdf013fe05b65517b56245e1807875d80be6e70
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2018
ms.locfileid: "39490398"
---
# <a name="manage-personal-data-for-azure-information-protection"></a>Administración de datos personales de Azure Information Protection

Cuando configura y usa Azure Information Protection, las direcciones de correo electrónico y las direcciones IP se almacenan y se utilizan por el servicio Azure Information Protection. Estos datos personales pueden encontrarse en los siguientes elementos:

- La directiva de Azure Information Protection

- Plantillas de protección para el servicio Azure Rights Management

- Superusuarios y administradores delegados para el servicio Azure Rights Management 

- Registros de administración para el servicio Azure Rights Management

- Registros de uso para el servicio Azure Rights Management

- Registros de seguimiento de documentos

- Registros de uso para los clientes Azure Information Protection y RMS 


[!INCLUDE [GDPR-related guidance](./includes/gdpr-intro-sentence.md)]


## <a name="viewing-personal-data-that-azure-information-protection-uses"></a>Visualización de los datos personales que usa Azure Information Protection

Por medio de Azure Portal, un administrador puede especificar direcciones de correo electrónico para directivas con ámbito y la configuración de protección dentro de una configuración de etiqueta. Para obtener más información, vea [Configuración de la directiva de Azure Information Protection para usuarios específicos mediante directivas de ámbito](configure-policy-scope.md) y [Configuración de una etiqueta para la protección de Rights Management](configure-policy-protection.md). 

En el caso de las etiquetas que están configuradas para aplicar la protección desde el servicio Rights Management de Azure, la dirección de correo electrónico también puede encontrarse en las plantillas de protección, mediante el uso de cmdlets de PowerShell desde el [módulo de AADRM](/powershell/module/aadrm). Este módulo de PowerShell también permite a los administradores especificar usuarios mediante la dirección de correo electrónico para convertirlos en [superusuarios](configure-super-users.md) o administradores del servicio Azure Rights Management. 

Cuando se usa Azure Information Protection para clasificar y proteger documentos y mensajes de correo electrónico, las direcciones de correo electrónico y las direcciones IP de los usuarios podrían guardarse en archivos de registro.


### <a name="protection-templates"></a>Plantillas de protección

Ejecute el cmdlet [Get-AadrmTemplate](/powershell/module/aadrm/get-aadrmtemplate) para obtener una lista de las plantillas de protección. Puede usar el identificador de plantilla para obtener detalles de una plantilla específica. El objeto `RightsDefinitions` muestra los datos personales, si existen. 

Ejemplo:
```
PS C:\Users> Get-AadrmTemplate -TemplateId fcdbbc36-1f48-48ca-887f-265ee1268f51 | select *


TemplateId              : fcdbbc36-1f48-48ca-887f-265ee1268f51
Names                   : {1033 -> Confidential}
Descriptions            : {1033 -> This data includes sensitive business information. Exposing this data to
                          unauthorized users may cause damage to the business. Examples for Confidential information
                          are employee information, individual customer projects or contracts and sales account data.}
Status                  : Archived
RightsDefinitions       : {admin@aip500.onmicrosoft.com -> VIEW, VIEWRIGHTSDATA, EDIT, DOCEDIT, PRINT, EXTRACT,
                          REPLY, REPLYALL, FORWARD, EXPORT, EDITRIGHTSDATA, OBJMODEL, OWNER,
                          AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@aip500.onmicrosoft.com -> VIEW,
                          VIEWRIGHTSDATA, EDIT, DOCEDIT, PRINT, EXTRACT, REPLY, REPLYALL, FORWARD, EXPORT,
                          EDITRIGHTSDATA, OBJMODEL, OWNER, admin2@aip500.onmicrosoft.com -> VIEW, VIEWRIGHTSDATA, EDIT,
                          DOCEDIT, PRINT, EXTRACT, REPLY, REPLYALL, FORWARD, EXPORT, EDITRIGHTSDATA, OBJMODEL, OWNER}
ContentExpirationDate   : 1/1/0001 12:00:00 AM
ContentValidityDuration : 0
ContentExpirationOption : Never
LicenseValidityDuration : 7
ReadOnly                : False
LastModifiedTimeStamp   : 1/26/2018 6:17:00 PM
ScopedIdentities        : {}
EnableInLegacyApps      : False
LabelId                 :
```

### <a name="super-users-and-delegated-administrators-for-the-azure-rights-management-service"></a>Superusuarios y administradores delegados para el servicio Azure Rights Management

Ejecute el cmdlet [Get-AadrmSuperUser](/powershell/module/aadrm/get-aadrmsuperuser) y [Get-AadrmRoleBasedAdministrator](/powershell/module/aadrm/get-aadrmrolebasedadministrator) para ver a qué usuarios se les ha asignado el rol de superusuario o administrador global para el servicio Azure Rights Management. Se muestran las direcciones de correo electrónico de los usuarios a los que se haya asignado cualquiera de estos roles.


### <a name="administration-logs-for-the-azure-rights-management-service"></a>Registros de administración para el servicio Azure Rights Management

Ejecute el cmdlet [Get-AadrmAdminLog](/powershell/module/aadrm/get-aadrmadminlog) para obtener un registro de las acciones de administración para el servicio Azure Rights Management, que protege los datos de Azure Information Protection. Este registro incluye datos personales en el formato de direcciones de correo electrónico y direcciones IP. El registro está en texto no cifrado y, después de descargarlo, se pueden buscar los detalles de un administrador específico sin conexión.

Por ejemplo:
```
PS C:\Users> Get-AadrmAdminLog -Path '.\Desktop\admin.log' -FromTime 4/1/2018 -ToTime 4/30/2018 -Verbose
The Rights Management administration log was successfully generated and can be found at .\Desktop\admin.log.
```

### <a name="usage-logs-for-the-azure-rights-management-service"></a>Registros de uso para el servicio Azure Rights Management
Ejecute el cmdlet [Get-AadrmUserLog](/powershell/module/aadrm/get-aadrmuserlog) para recuperar un registro de las acciones de usuario final que usan el servicio Azure Rights Management. Este servicio protege los datos para Azure Information Protection. El registro podría incluir datos personales en el formato de direcciones de correo electrónico y direcciones IP. El registro está en texto no cifrado y, después de descargarlo, se pueden buscar los detalles de un administrador específico sin conexión.

Por ejemplo:
```
PS C:\Users> Get-AadrmUserLog -Path '.\Desktop\' -FromDate 4/1/2018 -ToDate 4/30/2018 -NumberOfThreads 10
Acquiring access to your user log…
Downloading the log for 2018-04-01.
Downloading the log for 2018-04-03.
Downloading the log for 2018-04-06.
Downloading the log for 2018-04-09.
Downloading the log for 2018-04-10.
Downloaded the log for 2018-04-01. The log is available at .\Desktop\rmslog-2018-04-01.log.
Downloaded the log for 2018-04-03. The log is available at .\Desktop\rmslog-2018-04-03.log.
Downloaded the log for 2018-04-06. The log is available at .\Desktop\rmslog-2018-04-06.log.
Downloaded the log for 2018-04-09. The log is available at .\Desktop\rmslog-2018-04-09.log.
Downloaded the log for 2018-04-10. The log is available at .\Desktop\rmslog-2018-04-10.log.
Downloading the log for 2018-04-12.
Downloading the log for 2018-04-13.
Downloading the log for 2018-04-14.
Downloading the log for 2018-04-16.
Downloading the log for 2018-04-18.
Downloaded the log for 2018-04-12. The log is available at .\Desktop\rmslog-2018-04-12.log.
Downloaded the log for 2018-04-13. The log is available at .\Desktop\rmslog-2018-04-13.log.
Downloaded the log for 2018-04-14. The log is available at .\Desktop\rmslog-2018-04-14.log.
Downloaded the log for 2018-04-16. The log is available at .\Desktop\rmslog-2018-04-16.log.
Downloaded the log for 2018-04-18. The log is available at .\Desktop\rmslog-2018-04-18.log.
Downloading the log for 2018-04-24.
Downloaded the log for 2018-04-24. The log is available at .\Desktop\rmslog-2018-04-24.log.
```   

### <a name="document-tracking-logs"></a>Registros de seguimiento de documentos

Ejecute el cmdlet [Get-AadrmDocumentLog](/powershell/module/aadrm/get-aadrmdocumentlog) para recuperar información desde el sitio de seguimiento de documentos acerca de un usuario específico. Para obtener información de seguimiento asociada a los registros de documento, use el cmdlet [Get-AadrmTrackingLog](/powershell/module/aadrm/get-aadrmtrackinglog?view=azureipps).

Por ejemplo:
```
PS C:\Users> Get-AadrmDocumentLog -UserEmail "admin@aip500.onmicrosoft.com"


ContentId             : 6326fcb2-c465-4c24-a7f6-1cace7a9cb6f
Issuer                : admin@aip500.onmicrosoft.com
Owner                 : admin@aip500.onmicrosoft.com
ContentName           :
CreatedTime           : 3/6/2018 10:24:00 PM
Recipients            : {
                        PrimaryEmail: johndoe@contoso.com
                        DisplayName: JOHNDOE@CONTOSO.COM
                        UserType: External,
                        PrimaryEmail: alice@contoso0110.onmicrosoft.com
                        DisplayName: ALICE@CONTOSO0110.ONMICROSOFT.COM
                        UserType: External
                        }
TemplateId            :
PolicyExpires         :
EULDuration           :
SendRegistrationEmail : True
NotificationInfo      : Enabled: False
                        DeniedOnly: False
                        Culture:
                        TimeZoneId:
                        TimeZoneOffset: 0
                        TimeZoneDaylightName:
                        TimeZoneStandardName:

RevocationInfo        : Revoked: False
                        RevokedTime:
                        RevokedBy:


PS C:\Users> Get-AadrmTrackingLog -UserEmail "admin@aip500.onmicrosoft.com"

ContentId            : 6326fcb2-c465-4c24-a7f6-1cace7a9cb6f
Issuer               : admin@aip500.onmicrosoft.com
RequestTime          : 3/6/2018 10:45:57 PM
RequesterType        : External
RequesterEmail       : johndoe@contoso.com
RequesterDisplayName : johndoe@contoso.com
RequesterLocation    : IP: 167.220.1.54
                       Country: US
                       City: redmond
                       Position: 47.6812453974602,-122.120736471666

Rights               : {VIEW,OBJMODEL}
Successful           : False
IsHiddenInfo         : False
```

No hay ninguna búsqueda por ObjectID. Sin embargo, no está limitado por el parámetro `-UserEmail` y no es necesario que la dirección de correo electrónico que especifique forme parte de su inquilino. Si la dirección de correo electrónico proporcionada se almacena en cualquier lugar de los registros de seguimiento de documentos, la entrada del seguimiento de documentos se devuelve en la salida del cmdlet.

### <a name="usage-logs-for-the-azure-information-protection-client-and-rms-client"></a>Registros de uso para los clientes Azure Information Protection y RMS

Cuando se aplican etiquetas y protección a documentos y correos electrónicos, las direcciones de correo electrónico y las direcciones IP pueden almacenarse en archivos de registro en el equipo del usuario en las siguientes ubicaciones:

- Para el cliente de Azure Information Protection: %localappdata%\Microsoft\MSIP\Logs

- Para el cliente de RMS: %localappdata%\Microsoft\MSIPC\msip\Logs

Además, el cliente de Azure Information Protection registra estos datos personales en el registro de eventos local de Windows **Aplicaciones y servicios** > **Azure Information Protection**.

Cuando el cliente de Azure Information Protection ejecuta el analizador, los datos personales se guardan en %localappdata%\Microsoft\MSIP\Scanner\Reports en el equipo de Windows Server que ejecuta el analizador.

[!INCLUDE [GDPR-related guidance](./includes/gdpr-hybrid-note.md)]

## <a name="securing-and-controlling-access-to-personal-information"></a>Protección y control del acceso a la información personal
Los datos personales que ve y especifica en Azure Portal solo están accesibles para los usuarios a los que se ha asignado uno de los siguientes [roles de administrador de Azure Active Directory](/azure/active-directory/active-directory-assign-admin-roles-azure-portal):
    
- **Administrador de Information Protection**

- **Administrador de seguridad**

- **Administrador global/Administrador de empresa**

Los datos personales que vea y especifique por medio del módulo de AADRM solo están accesibles para los usuarios a los que se haya asignado el rol de **administrador de Information Protection** o de **administrador global/administrador de la compañía** en Azure Active Directory, o el rol de administrador global para el servicio Azure Rights Management.  

## <a name="updating-personal-data"></a>Actualizar datos personales

Puede actualizar las direcciones de correo electrónico para las directivas con ámbito y la configuración de protección de la directiva de Azure Information Protection. Para obtener más información, vea [Configuración de la directiva de Azure Information Protection para usuarios específicos mediante directivas de ámbito](configure-policy-scope.md) y [Configuración de una etiqueta para la protección de Rights Management](configure-policy-protection.md). 

En cuanto a la configuración de la protección, puede actualizar la misma información mediante el uso de cmdlets de PowerShell desde el [módulo de AADRM](/powershell/module/aadrm).

No puede actualizar las direcciones de correo electrónico para los superusuarios y administradores delegados. Para ello, lo que puede hacer es quitar la cuenta de usuario especificada y agregar la cuenta de usuario con la dirección de correo electrónico actualizada. 

### <a name="protection-templates"></a>Plantillas de protección

Ejecute el cmdlet [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty) para actualizar la plantilla de protección. Dado que los datos personales están dentro de la propiedad `RightsDefinitions`, también debe usar el cmdlet [New-AadrmRightsDefinition](/powershell/module/aadrm/new-aadrmrightsdefinition) para crear un objeto RightsDefinitions con la información actualizada, y usar el objeto RightsDefinitions con el cmdlet `Set-AadrmTemplateProperty`.

### <a name="super-users-and-delegated-administrators-for-the-azure-rights-management-service"></a>Superusuarios y administradores delegados para el servicio Azure Rights Management

Cuando tenga que actualizar la dirección de correo electrónico de un superusuario:

1. Use [Remove-AadrmSuperUser](/powershell/module/aadrm/Remove-AadrmSuperUser) para quitar el usuario y la dirección de correo electrónico antiguos.

2. Use [Add-AadrmSuperUser](/powershell/module/aadrm/Add-AadrmSuperUser) para agregar el usuario y la dirección de correo electrónico nuevos.

Cuando tenga que actualizar la dirección de correo electrónico de un administrador delegado:

1. Use [Remove-AadrmRoleBasedAdministrator](/powershell/module/aadrm/Remove-AadrmRoleBasedAdministrator) para quitar el usuario y la dirección de correo electrónico antiguos.

2. Use [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/Add-AadrmRoleBasedAdministrator) para agregar el usuario y la dirección de correo electrónico nuevos.

## <a name="deleting-personal-data"></a>Eliminar datos personales
Puede eliminar las direcciones de correo electrónico para las directivas con ámbito y la configuración de protección de la directiva de Azure Information Protection. Para obtener más información, vea [Configuración de la directiva de Azure Information Protection para usuarios específicos mediante directivas de ámbito](configure-policy-scope.md) y [Configuración de una etiqueta para la protección de Rights Management](configure-policy-protection.md). 

En cuanto a la configuración de protección, puede eliminar la misma información mediante el uso de cmdlets de PowerShell desde el [módulo de AADRM](/powershell/module/aadrm).

Para eliminar las direcciones de correo de los superusuarios y administradores delegados, quite estos usuarios mediante los cmdlet [Remove-AadrmSuperUser](/powershell/module/aadrm/Remove-AadrmSuperUser) y [Remove-AadrmRoleBasedAdministrator](/powershell/module/aadrm/Remove-AadrmRoleBasedAdministrator). 

Para eliminar datos personales en los registros de seguimiento de documentos, los registros de administración o los registros de uso del servicio Azure Rights Management, consulte la siguiente sección para ver cómo generar una solicitud al Soporte técnico de Microsoft.

Para eliminar datos personales en los archivos de registro de cliente y los registros de analizador que se almacenan en los equipos, use cualquier herramienta estándar de Windows para quitar los archivos o los datos personales de los archivos. 

### <a name="to-delete-personal-data-with-microsoft-support"></a>Para eliminar datos personales con el Soporte técnico de Microsoft

Siga estos tres pasos para solicitar que Microsoft elimine los datos personales en los registros de seguimiento de documentos, los registros de administración o los registros de uso del servicio Azure Rights Management. 

**Paso 1: Iniciar la solicitud de eliminación**
[Póngase en contacto con el Soporte técnico de Microsoft](information-support.md#to-contact-microsoft-support) para abrir una incidencia de soporte técnico de Azure Information Protection en la que solicite la eliminación de datos de su inquilino. Necesita demostrar que es un administrador del inquilino de Azure Information Protection y entender que este proceso tarda varios días en confirmarse. Al enviar la solicitud, debe proporcionar información adicional, dependiendo de los datos que deban eliminarse.

- Para eliminar el registro de administración, proporcione la **fecha de finalización**. Se eliminarán todos los registros de administración hasta esa fecha de finalización.
- Para eliminar los registros de uso, proporcione la **fecha de finalización**. Se eliminarán todos los registros de uso hasta esa fecha de finalización.
- Para eliminar los registros de seguimiento de documentos, proporcione el valor **UserEmail**. Se eliminará toda la información de seguimiento de documentos relativa a UserEmail.

La eliminación de los datos es una acción permanente. No hay manera de recuperar los datos una vez que se haya procesado una solicitud de eliminación. Se recomienda que los administradores exporten los datos necesarios antes de enviar una solicitud de eliminación.

**Paso 2: Esperar la comprobación** Microsoft comprobará que la solicitud para eliminar uno o más registros es legítima. Este proceso puede tardar hasta cinco días laborables.

**Paso 3: Obtener la confirmación de la eliminación** Los Servicios de soporte técnico de Microsoft (CSS) le enviarán un correo electrónico para confirmar que se han eliminado los datos. 

## <a name="exporting-personal-data"></a>Exportar datos personales
Al usar los cmdlets de PowerShell de AADRM, los datos personales estarán disponibles para la búsqueda y exportación como un objeto de PowerShell. El objeto de PowerShell se puede convertir a JSON y guardarlo usando el cmdlet `ConvertTo-Json`.

## <a name="restricting-the-use-of-personal-data-for-profiling-or-marketing-without-consent"></a>Restricción del uso de datos personales para la generación de perfiles o actividades de marketing sin consentimiento
Azure Information Protection sigue los [términos de privacidad](https://privacy.microsoft.com/privacystatement) de Microsoft para la generación de perfiles o las actividades de marketing que se basan en datos personales.

## <a name="auditing-and-reporting"></a>Auditoría e informes
Solo los usuarios a los que se les hayan asignado [permisos de administrador](#securing-and-controlling-access-to-personal-information) pueden usar el módulo de AADRM para la búsqueda y exportación de datos personales. Estas operaciones quedan registradas en el registro de administración que se puede descargar.

Para las acciones de eliminación, la solicitud de soporte técnico actúa como trazo de auditoría y notificación de las acciones realizadas por Microsoft. Una vez completado el proceso, los datos eliminados no estarán disponibles para la búsqueda y exportación; el administrador puede comprobarlo con los cmdlets Get desde el módulo de AADRM.

