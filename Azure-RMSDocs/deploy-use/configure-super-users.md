---
title: Configuración de superusuarios para Azure Rights Management - AIP
description: Obtenga información sobre la característica de superusuario del servicio Azure Rights Management de Azure Information Protection e impleméntela para que los usuarios y servicios autorizados siempre puedan leer e inspeccionar los datos que Azure Rights Management protege para la organización. Esta capacidad se denomina a menudo "razonamiento encima de los datos" y es un elemento crucial en el mantenimiento del control de los datos de su organización.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/31/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 7d52bd4547b24acad3e9b2db8c8ade8b632d517d
ms.sourcegitcommit: 6cbd03b28873b192dc730556c6dd5a7da6e705df
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39411349"
---
# <a name="configuring-super-users-for-azure-rights-management-and-discovery-services-or-data-recovery"></a>Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

La característica de superusuario del servicio Azure Rights Management de Azure Information Protection garantiza que los usuarios y servicios autorizados siempre puedan leer e inspeccionar los datos que Azure Rights Management protege para la organización. Y, si es necesario, quitar la protección o cambiar la protección que se aplicó anteriormente. 

Un superusuario siempre tiene el [derecho de uso](configure-usage-rights.md) de control total de Rights Management para documentos y correos electrónicos que se han protegido mediante el inquilino de Azure Information Protection de su organización. Esta capacidad se denomina a menudo "razonamiento encima de los datos" y es un elemento crucial en el mantenimiento del control de los datos de su organización. Por ejemplo, podría usar esta característica en cualquiera de las siguientes situaciones:

- Un empleado deja la organización y usted necesita leer los archivos que dicho empleado protegió.

- Un administrador de TI necesita quitar la directiva de protección actual que se configuró para los archivos y aplicar una nueva.

- Exchange Server necesita indexar los buzones para las operaciones de búsqueda.

- Tiene servicios de TI existentes para soluciones de prevención de pérdida de datos (DLP), puertas de enlace de cifrado de contenido (CEG) y productos antimalware que deben inspeccionar los archivos que ya están protegidos.

- Tiene que descifrar archivos de forma masiva con fines de auditoría, legales y otros motivos de cumplimiento.

## <a name="configuration-for-the-super-user-feature"></a>Configuración de la característica de superusuario

De forma predeterminada, la característica de superusuario no está habilitada, y no hay ningún usuario asignado a este rol. Se habilita automáticamente si configura el conector de Rights Management para Exchange, y no es necesaria para los servicios estándar que ejecutan Exchange Online, SharePoint Online o SharePoint Server.

Si necesita habilitar manualmente la característica de superusuario, use el cmdlet de PowerShell [Enable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/enable-aadrmsuperuserfeature) y, luego, asigne los usuarios (o cuentas de servicio), según sea necesario, mediante el cmdlet [Add-AadrmSuperUser](/powershell/aadrm/vlatest/add-aadrmsuperuser) o el cmdlet [Set-AadrmSuperUserGroup](/powershell/aadrm/vlatest/set-aadrmsuperusergroup) y agregue usuarios (u otros grupos), según sea necesario para este grupo. 

Aunque el uso de un grupo para los superusuarios es más fácil de administrar, tenga en cuenta que, por motivos de rendimiento, Azure Rights Management [almacena en caché la pertenencia al grupo](../plan-design/prepare.md#group-membership-caching-by-azure-information-protection). Por tanto, si necesita asignar un nuevo usuario como superusuario para descifrar contenido inmediatamente, agregue ese usuario mediante Add-AadrmSuperUser, en lugar de agregar el usuario a un grupo existente que ha configurado mediante Set-AadrmSuperUserGroup.

> [!NOTE]
> Si aún no ha instalado el módulo de Windows PowerShell para Azure Rights Management, vea [Installing the AADRM PowerShell module](install-powershell.md) (Instalación del módulo de PowerShell para AADRM).

No importa cuándo se habilita la característica de superusuario o cuándo se agregan usuarios como superusuarios. Por ejemplo, si habilita la característica un jueves y el viernes agrega un usuario, ese usuario puede abrir de inmediato el contenido que estaba protegido al principio de la semana.

## <a name="security-best-practices-for-the-super-user-feature"></a>Procedimientos de seguridad recomendados para la característica de superusuario

- Use el cmdlet [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator) para restringir y supervisar los administradores que tienen asignado el rol Administrador global para el inquilino de Office 365 o Azure Information Protection, o bien para conocer los usuarios que tienen asignado el rol Administrador global. Estos usuarios pueden habilitar la característica de superusuario y asignar usuarios (y a ellos mismos) como superusuarios y posiblemente descifrar todos los archivos que protege su organización.

- Para ver qué usuarios y cuentas de servicio están asignados individualmente como superusuarios, use el cmdlet [Get-AadrmSuperUser](/powershell/module/aadrm/get-aadrmsuperuser). Para ver si se ha configurado un grupo de superusuarios, use el cmdlet [Get-AadrmSuperUserGroup](/powershell/module/aadrm/get-aadrmsuperusergroup) y sus herramientas de administración de usuarios estándar para comprobar qué usuarios forman parte de este grupo. Al igual que todas las acciones de administración, habilitar o deshabilitar la característica de superusuarios y agregar o quitar superusuarios se registran y se pueden auditar mediante el comando [Get-AadrmAdminLog](/powershell/module/aadrm/get-aadrmadminlog) . Vea la sección siguiente para obtener un ejemplo. Cuando los superusuarios descifrar archivos, esta acción se registra y se puede auditar con el [registro de uso](log-analyze-usage.md).

- Si no necesita la característica de superusuario para los servicios diarios, habilítela solo cuando lo necesite y deshabilítela de nuevo con el cmdlet [Disable-AadrmSuperUserFeature](/powershell/module/aadrm/disable-aadrmsuperuserfeature) .

### <a name="example-auditing-for-the-super-user-feature"></a>Ejemplo de auditoría de la característica de superusuario

El siguiente extracto del registro muestra algunas entradas de ejemplo de uso del cmdlet [Get-AadrmAdminLog](/powershell/module/aadrm/get-aadrmadminlog). 

En este ejemplo, el administrador de Contoso Ltd confirma que la característica de superusuario está deshabilitada, agrega a Richard Simone como un superusuario, comprueba que Richard es el único superusuario configurado para el servicio Azure Rights Management y, después, habilita la característica de superusuario para que Richard pueda descifrar archivos que había protegido un empleado que ahora ha dejado la compañía.

`2015-08-01T18:58:20    admin@contoso.com   GetSuperUserFeatureState    Passed  Disabled`

`2015-08-01T18:59:44    admin@contoso.com   AddSuperUser -id rsimone@contoso.com    Passed  True`

`2015-08-01T19:00:51    admin@contoso.com   GetSuperUser    Passed  rsimone@contoso.com`

`2015-08-01T19:01:45    admin@contoso.com   SetSuperUserFeatureState -state Enabled Passed  True`

## <a name="scripting-options-for-super-users"></a>Opciones de script para superusuarios
Con frecuencia, alguien a quien se le asigne un superusuario para Azure Rights Management deberá quitar la protección de varios archivos, en varias ubicaciones. Aunque es posible hacerlo manualmente, resulta más eficaz (y a menudo más fiable) mediante scripts. Para ello, use el cmdlet [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) y el cmdlet [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile), según sea necesario. 

Si usa la clasificación y la protección, también puede utilizar [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) para aplicar una etiqueta nueva que no aplica protección, o quitar la etiqueta que ha aplicado la protección. 

Para más información sobre estos cmdlets, vea [Uso de PowerShell con el cliente de Azure Information Protection ](../rms-client/client-admin-guide-powershell.md) en la guía para administradores del cliente de Azure Information Protection.

> [!NOTE]
> El módulo AzureInformationProtection reemplaza al módulo de PowerShell RMS Protection que se instala con la herramienta de protección de RMS. Ambos módulos son diferentes entre sí y complementan el [módulo de PowerShell para Azure Rights Management](administer-powershell.md). El módulo AzureInformationProtection es compatible con Azure Information Protection, el servicio Azure Rights Management (Azure RMS) para Azure Information Protection y Active Directory Rights Management Services (AD RMS).


