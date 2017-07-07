---
title: "Preparación de usuarios y grupos para Azure Information Protection"
description: "Compruebe que tiene las cuentas de usuario y grupo que necesita para empezar a clasificar, etiquetar y proteger los documentos y correos electrónicos de su organización."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/03/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 362c5108238a0561c35d72faa556417f0f0f8566
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2017
---
# <a name="preparing-users-and-groups-for-azure-information-protection"></a>Preparación de usuarios y grupos para Azure Information Protection

>*Se aplica a: Azure Information Protection, Office 365*

Antes de implementar Azure Information Protection para su organización, asegúrese de que tiene cuentas de usuarios y grupos en Azure AD para el inquilino de su organización.

Hay diferentes maneras de crear estas cuentas para usuarios y grupos, que incluyen:

- Puede crear los usuarios en el centro de administración de Office 365 y los grupos en el centro de administración de Exchange Online.

- Puede crear los usuarios y grupos en Azure Portal.

- Puede crear los usuarios y grupos mediante cmdlets de PowerShell de Azure AD y Exchange Online.

- Puede crear los usuarios y grupos en Active Directory local y sincronizarlos con Azure AD.

- Puede crear los usuarios y grupos en otro directorio y sincronizarlos con Azure AD.

Al crear usuarios y grupos mediante uno de los tres métodos de esta lista, se crean automáticamente en Azure AD y Azure Information Protection puede usar estas cuentas directamente. Sin embargo, muchas redes de empresa usan un directorio local para crear y administrar usuarios y grupos. Azure Information Protection no puede utilizar estas cuentas directamente; hay que sincronizarlas con Azure AD.

## <a name="how-users-and-groups-are-used-by-azure-information-protection"></a>Utilización de usuarios y grupos por Azure Information Protection

Hay tres escenarios para utilizar usuarios y grupos con Azure Information Protection:

**Para asignar etiquetas a los usuarios** al configurar la directiva de Azure Information Protection para que las etiquetas se puedan aplicar a los documentos y correos electrónicos. Solo los administradores pueden seleccionar estos usuarios y grupos:

- La directiva de Azure Information Protection se asigna automáticamente a todos los usuarios de Azure AD del inquilino. Sin embargo, también puede asignar etiquetas adicionales a usuarios o grupos específicos mediante directivas de ámbito.     

**Para asignar derechos de uso y controles de acceso** cuando se usa el servicio Azure Rights Management para proteger documentos y correos electrónicos. Los administradores y usuarios pueden seleccionar estos usuarios y grupos:

- Los derechos de uso determinan si un usuario puede abrir un documento o correo electrónico y cómo puede utilizarlo. Por ejemplo, si solo puede leerlo, o leerlo e imprimirlo, o leerlo y editarlo. 

- Los controles de acceso incluyen una fecha de expiración y si es necesaria una conexión a Internet para acceder. 

**Para configurar el servicio Azure Rights Management** para admitir escenarios específicos y, por tanto, solo los administradores pueden seleccionar estos grupos. Entre los ejemplos se incluye la configuración de lo siguiente:

- Super usuarios, para que los servicios o personas designados puedan abrir contenido cifrado si es necesario para la recuperación de datos o la exhibición de documentos electrónicos.

- Administración delegada del servicio Azure Rights Management.

- Controles de incorporación para admitir una implementación por fases.

## <a name="azure-information-protection-requirements-for-user-accounts"></a>Requisitos de Azure Information Protection para cuentas de usuario

Para asignar etiquetas:

- Todas las cuentas de usuario en Azure AD pueden utilizarse para configurar directivas de ámbito que asignan etiquetas adicionales a los usuarios.

Para asignar derechos de uso y controles de acceso, y configurar el servicio Azure Rights Management:

- Para autorizar usuarios, se utilizan dos atributos en Azure AD: **proxyAddresses** y **userPrincipalName**.

- El atributo **proxyAddresses de Azure AD** almacena todas las direcciones de correo electrónico para una cuenta y se puede rellenar de distintas maneras. Por ejemplo, un usuario de Office 365 que tiene un buzón de Exchange Online tendrá automáticamente una dirección de correo electrónico almacenada en este atributo. Si asigna una dirección de correo electrónico alternativa a un usuario de Office 365, también se guarda en este atributo. También se puede rellenar con las direcciones de correo electrónico que se sincronizan desde cuentas locales. 
    
    Azure Information Protection puede usar cualquier valor de este atributo proxyAddresses de Azure AD si se ha agregado el dominio en el inquilino (un "dominio comprobado"). Para más información sobre la comprobación de dominios:
    
    - Para Azure AD: [Incorporación de su nombre de dominio personalizado a Azure Active Directory](/active-directory/active-directory-add-domain)
    
    - Para Office 365: [Add a domain and users to Office 365](https://go.microsoft.com/fwlinkid/?linkid=847121) (Incorporación de un dominio y usuarios a Office 365)

- El atributo **userPrincipalName de Azure AD** solo se utiliza cuando una cuenta del inquilino no tiene valores en el atributo proxyAddresses de Azure AD. Por ejemplo, puede crear un usuario en Azure Portal, o crear un usuario para Office 365 que no tenga un buzón.

### <a name="assigning-usage-rights-and-access-controls-to-external-users"></a>Asignación de derechos de uso y controles de acceso a usuarios externos

Además de utilizar los atributos proxyAddresses y userPrincipalName de Azure AD para los usuarios de su inquilino, Azure Information Protection también utiliza estos atributos de la misma manera para autorizar usuarios de otro inquilino.

## <a name="azure-information-protection-requirements-for-group-accounts"></a>Requisitos de Azure Information Protection para cuentas de grupo

Para asignar etiquetas:

- Puede utilizar cualquier tipo de grupo en Azure AD para configurar directivas de ámbito que asignen etiquetas adicionales a los miembros del grupo.

Para asignar derechos de uso y controles de acceso a usuarios externos:

- Puede utilizar cualquier tipo de grupo en Azure AD con una dirección de correo electrónico que contenga un dominio comprobado para el inquilino del usuario. Un grupo que tenga una dirección de correo electrónico a menudo se conoce como un grupo habilitado para correo electrónico. 
    
    Por ejemplo, puede usar un grupo de seguridad habilitado para correo electrónico, un grupo de distribución (que puede ser estático o dinámico) y un grupo de Office 365. No puede usar un grupo de seguridad (dinámico o estático) porque este tipo de grupo no tiene una dirección de correo electrónico.

Para configurar el servicio Azure Rights Management:

- Puede utilizar cualquier tipo de grupo en Azure AD con una dirección de correo electrónico de un dominio comprobado en el inquilino, con una excepción. Esta excepción se origina al configurar los controles de incorporación para usar un grupo, que debe ser un grupo de seguridad de Azure AD para el inquilino.
    
- Puede utilizar cualquier tipo de grupo en Azure AD (con o sin dirección de correo electrónico) de un dominio comprobado en el inquilino para la administración delegada del servicio Azure Rights Management.

### <a name="assigning-usage-rights-and-access-controls-to-external-groups"></a>Asignación de derechos de uso y controles de acceso a grupos externos

Además de utilizar el atributo proxyAddresses de Azure AD para los grupos de su inquilino, Azure Information Protection también utiliza ese atributo de la misma manera para autorizar grupos de otro inquilino.

## <a name="using-accounts-from-active-directory-on-premises-for-azure-information-protection"></a>Uso de cuentas de Active Directory local para Azure Information Protection

Si dispone de cuentas que son administradas de forma local y que quiere utilizar con Azure Information Protection, debe sincronizarlas con Azure AD. Para facilitar la implementación, se recomienda que use [Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect). Sin embargo, puede utilizar cualquier método de sincronización de directorios, que consigue el mismo resultado.

Al sincronizar las cuentas, no necesita sincronizar todos los atributos. Para consultar una lista de los atributos que deben sincronizarse, consulte la [sección Azure RMS](/azure/active-directory/connect/active-directory-aadconnectsync-attributes-synchronized#azure-rms) en la documentación de Azure Active Directory. 

En la lista de atributos de Azure Rights Management, verá que los atributos de AD locales de **mail**, **proxyAddresses** y **userPrincipalName** para los usuarios son necesarios para la sincronización. Los valores para **mail** y **proxyAddresses** se sincronizan con el atributo proxyAddresses de Azure AD. Para más información, consulte [Cómo se rellena el atributo proxyAddresses en Azure AD](https://support.microsoft.com/help/3190357/how-the-proxyaddresses-attribute-is-populated-in-azure-ad)

## <a name="confirming-your-users-and-groups-are-prepared-for-azure-information-protection"></a>Confirmación de que los usuarios y grupos están preparados para Azure Information Protection

Puede usar PowerShell de Azure AD para confirmar que los usuarios y grupos pueden utilizarse con Azure Information Protection. También puede usar PowerShell para confirmar los valores que pueden usarse para autorizarlos. 

Por ejemplo, con el módulo de V1 de PowerShell para Azure Active Directory, [MSOnline](/powershell/module/msonline/?view=azureadps-1.0), en una sesión de PowerShell, primero conéctese al servicio y proporcione las credenciales de administrador global:

    Connect-MsolService
    

Nota: Si este comando no funciona, puede ejecutar `Install-Module MSOnline` para instalar el módulo MSOnline.

Después, configure la sesión de PowerShell para que no se trunquen los valores:

    $Formatenumerationlimit =-1

### <a name="confirm-user-accounts-are-ready-for-azure-information-protection"></a>Confirmación de que las cuentas de usuario están preparadas para Azure Information Protection

Para confirmar las cuentas de usuario, ejecute el siguiente comando:

    Get-Msoluser | select DisplayName, UserPrincipalName, ProxyAddresses
        
La primera comprobación es asegurarse de que se muestran los usuarios que desea utilizar con Azure Information Protection. 

A continuación, compruebe si se rellena la columna **ProxyAddresses**. Si es así, los valores de correo electrónico en esta columna se pueden usar para autorizar al usuario para el servicio Azure Rights Management. 

Si la columna **ProxyAddresses** no se rellena, se usará el valor del atributo **UserPrincipalName** para autorizar al usuario para el servicio Azure Rights Management.

Por ejemplo: 
    
|Nombre para mostrar|UserPrincipalName|ProxyAddresses
|-------------------|-----------------|--------------------|
|Jagannath Reddy |jagannathreddy@contoso.com|{}|
|Ankur Roy|ankurroy@contoso.com|{SMTP:ankur.roy@contoso.com, smtp: ankur.roy@onmicrosoft.contoso.com}|

En este ejemplo:

- La cuenta de usuario para Jagannath Reddy la autorizará  **jagannathreddy@contoso.com** .

-  La cuenta de usuario de Ankur Roy se puede autorizar mediante el uso de **ankur.roy@contoso.com** y **ankur.roy@onmicrosoft.contoso.com**, pero no de **ankurroy@contoso.com**.

En la mayoría de los casos, el valor del atributo UserPrincipalName coincidirá con uno de los valores del campo ProxyAddresses. Esta es la configuración recomendada, pero si no se puede cambiar el valor de UPN para que coincida con la dirección de correo electrónico, debe realizar los pasos siguientes:

1. Si el nombre de dominio en el valor de UPN es un dominio comprobado para su inquilino de Azure AD, agregue el valor de UPN otra dirección de correo electrónico de Azure AD para que el valor de UPN ahora se puede utilizar para autorizar la cuenta de usuario para la protección de la información de Azure.
    
    Si el nombre de dominio en el valor de UPN no es un dominio comprobado para su inquilino, no podrá usarse con Azure Information Protection. Sin embargo, el usuario todavía se puede ser autorizado como miembro de un grupo cuando la dirección de correo electrónico del grupo utiliza un nombre de dominio comprobado.

2. Si el valor de UPN no es enrutable (por ejemplo, **ankurroy@contoso.local**), configure un identificador de inicio de sesión alternativo para los usuarios e indíqueles cómo deben iniciar sesión en Office con este inicio de sesión alternativo. También debe establecer una clave del Registro para Office.
    
    Para más información, consulte [Configuración de identificador de inicio de sesión alternativo](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id) y [Las aplicaciones de Office periódicamente piden credenciales a SharePoint Online, OneDrive y Lync Online](https://support.microsoft.com/help/2913639/office-applications-periodically-prompt-for-credentials-to-sharepoint-online,-onedrive,-and-lync-online).

> [!TIP]
> Puede usar el cmdlet Export-Csv para exportar los resultados a una hoja de cálculo con el fin de facilitar la administración, como la búsqueda y edición masiva para la importación. 
> 
> Por ejemplo: `Get-MsolGroup | select DisplayName, ProxyAddresses | Export-Csv -Path UserAccounts.csv`

### <a name="confirm-group-accounts-are-ready-for-azure-information-protection"></a>Confirmación de que las cuentas de grupo están preparadas para Azure Information Protection

Para confirmar las cuentas de grupo, utilice el siguiente comando:
         
    Get-MsolGroup | select DisplayName, ProxyAddresses

Asegúrese de que se muestran los grupos que desea utilizar con Azure Information Protection. En los grupos que se muestran, se pueden utilizar las direcciones de correo electrónico de la **ProxyAddresses** para autorizar a los miembros del grupo del servicio Azure Rights Management.

A continuación, compruebe que los grupos contienen los usuarios (u otros grupos) que desea usar en Azure Information Protection. Puede usar PowerShell para hacerlo (por ejemplo, [Get-MsolGroupMember](/powershell/module/msonline/Get-MsolGroupMember?view=azureadps-1.0)), o usar el portal de administración. 

Para los dos escenarios de la configuración del servicio Azure Rights Management que usan grupos de seguridad, puede utilizar el siguiente comando de PowerShell para buscar el identificador de objeto y el nombre para mostrar que puede usarse para identificar estos grupos. También puede utilizar Azure Portal para buscar estos grupos y copiar los valores para el identificador de objeto y el nombre para mostrar:

    Get-MsolGroup | where {$_.GroupType -eq "Security"}

## <a name="considerations-for-azure-information-protection-if-email-addresses-change"></a>Consideraciones en Azure Information Protection si cambian de direcciones de correo electrónico

Si cambia la dirección de correo electrónico de un usuario o grupo, se recomienda agregar la dirección de correo electrónico anterior como una segunda dirección de correo electrónico (también conocida como dirección de proxy, alias o dirección de correo electrónico alternativa) para el usuario o grupo. De esta forma, se agrega la dirección de correo electrónico anterior al atributo proxyAddresses de Azure AD. Esta administración de cuentas garantiza la continuidad del negocio para los derechos de uso u otras configuraciones que se guardaron allí cuando se usaba la dirección de correo electrónico anterior. 

Si no puede hacerlo, el usuario o grupo con la nueva dirección de correo electrónico se arriesga a que se le deniegue el acceso a los documentos y a correos electrónicos que anteriormente estaban protegidos, y a cualquier otra configuración errónea que usaba el valor anterior. En este caso, debe repetir la configuración para guardar la nueva dirección de correo electrónico. 

Tenga en cuenta que es raro que un grupo cambie su dirección de correo electrónico y si asigna derechos de uso a un grupo en lugar de a usuarios individuales, no importa si cambia la dirección de correo electrónico del usuario. En este escenario, los derechos de uso se asignan a la dirección de correo electrónico del grupo y no a las direcciones de correo electrónico de usuarios individuales. Este es el método más adecuado (y recomendado) para que un administrador configure los derechos de uso que protegen documentos y correos electrónicos. Sin embargo, los usuarios normalmente pueden asignar permisos personalizados a usuarios individuales. Dado que no siempre se puede saber si una cuenta de usuario o grupo se ha utilizado para conceder acceso, resulta más seguro agregar siempre la dirección de correo electrónico anterior como una segunda dirección.

## <a name="group-membership-caching-by-azure-rights-management"></a>Almacenamiento en caché de la pertenencia al grupo de Azure Rights Management

Por motivos de rendimiento, el servicio Azure Rights Management almacena en caché la pertenencia al grupo. Esto significa que cualquier cambio realizado en la pertenencia al grupo en Azure AD puede tardar hasta tres horas en aplicarse cuando estos grupos los utiliza Azure Rights Management y este período está sujeto a cambios. 

No olvide incluir este retraso en los cambios o pruebas que realice cuando use grupos en Azure Rights Management, como la asignación de derechos de uso o la configuración del servicio Azure Rights Management. 


## <a name="next-steps"></a>Pasos siguientes

Cuando haya confirmado que los usuarios y grupos pueden utilizarse con Azure Information Protection y esté listo para empezar a proteger los documentos y correos electrónicos, active el servicio Rights Management para habilitar este servicio de protección de datos. Para más información, consulte [Activación de Azure Rights Management](../deploy-use/activate-service.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


