---
title: "Configuración de los superusuarios para Azure Rights Management: AIP"
description: "Comprenda e implemente la característica de superusuario de Azure Rights Management Service de Azure Information Protection, de modo que los servicios y las personas autorizados siempre puedan leer e inspeccionar los datos que protege Azure Rights Management para la organización. Esta capacidad se conoce a veces como \"razonamiento sobre datos\" y es un elemento crucial en el mantenimiento del control de los datos de la organización."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: a134d6619f67bfc3d26cb1726fe07e8ffca403cd
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/29/2018
---
# <a name="configuring-super-users-for-azure-rights-management-and-discovery-services-or-data-recovery"></a>Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos

>*Válido para: Azure Information Protection, Office 365*

La característica de superusuario de Azure Rights Management Service de Azure Information Protection garantiza que los servicios y las personas autorizados siempre puedan leer e inspeccionar los datos que protege Azure Rights Management para la organización. Y, si es necesario, quita la protección o cambiar la que se aplicó anteriormente. 

Un superusuario siempre tiene el [derecho de uso](configure-usage-rights.md) Control total de Rights Management para documentos y correos electrónicos que haya protegido el inquilino de Azure Information Protection de la organización. Esta capacidad se conoce a veces como "razonamiento sobre datos" y es un elemento crucial en el mantenimiento del control de los datos de la organización. Por ejemplo, podría usar esta característica en cualquiera de los siguientes escenarios:

- Un empleado deja la organización y usted necesita leer los archivos que ha protegido.

- Un administrador de TI necesita quitar la directiva de protección actual que se configuró para los archivos y aplicar una nueva directiva de protección.

- Exchange Server necesita indexar los buzones para las operaciones de búsqueda.

- Tiene servicios de TI existentes para soluciones de prevención de pérdida de datos (DLP), puertas de enlace de cifrado de contenido (CEG) y productos antimalware que necesitan inspeccionar los archivos que ya están protegidos.

- Debe descifrar archivos en bloque para auditoría, por temas legales y otros motivos de cumplimiento.

De forma predeterminada, la característica de superusuario no está habilitada y ningún usuario está asignado a este rol. Se habilita automáticamente al configurar el conector de Rights Management para Exchange y no es necesaria para los servicios estándar que ejecutan Exchange Online, SharePoint Online o SharePoint Server.

Si tiene que habilitar manualmente la característica de superusuario, use el cmdlet de PowerShell [Enable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/enable-aadrmsuperuserfeature) y asigne los usuarios (o cuentas de servicio) según sea necesario mediante el cmdlet [Add-AadrmSuperUser](/powershell/aadrm/vlatest/add-aadrmsuperuser) o [Set-AadrmSuperUserGroup](/powershell/aadrm/vlatest/set-aadrmsuperusergroup); finalmente, agregue usuarios (u otros grupos) según sea necesario para este grupo. 

Aunque el uso de un grupo para los superusuarios es más fácil de administrar, tenga en cuenta que, por motivos de rendimiento, Azure Rights Management [almacena en caché la pertenencia al grupo](../plan-design/prepare.md#group-membership-caching-by-azure-information-protection). Por lo que si necesita asignar un nuevo usuario como superusuario para descifrar contenido inmediatamente, debe agregarlo mediante Add-AadrmSuperUser, en lugar de agregarlo a un grupo existente configurado mediante Set-AadrmSuperUserGroup.

> [!NOTE]
> Si aún no tiene instalado el módulo de Windows PowerShell para [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], consulte [Instalación de Windows PowerShell para Azure Rights Management](install-powershell.md).

Procedimientos recomendados de seguridad para la característica de superusuario:

- Restrinja y supervise los administradores que se asignan como administrador global para el inquilino de Office 365 o Azure Information Protection, o quién está asignado al rol GlobalAdministrator mediante el cmdlet [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator). Estos usuarios pueden habilitar la característica de superusuario y asignar usuarios (y asignarse ellos mismos) como superusuarios para poder descifrar todos los archivos que protege la organización.

- Para ver qué usuarios y cuentas de servicio se asignan individualmente como superusuarios, use el [cmdlet Get-AadrmSuperUser](/powershell/module/aadrm/get-aadrmsuperuser). Para ver si se ha configurado un grupo de superusuarios, use el cmdlet [Get-AadrmSuperUser](/powershell/module/aadrm/get-aadrmsuperusergroup) y sus herramientas de administración de usuarios estándar para comprobar qué usuarios pertenecen a este grupo. Al igual que todas las acciones de administración, la habilitación o la deshabilitación de la característica de superusuarios y la incorporación o la eliminación de superusuarios se registra y se puede auditar mediante el comando [Get-AadrmAdminLog](/powershell/module/aadrm/get-aadrmadminlog). Cuando los superusuarios descifran archivos, esta acción se registra y se puede auditar con el [registro de uso](log-analyze-usage.md).

- Si no necesita la característica de superusuario para los servicios diarios, habilítela solo cuando lo necesite y deshabilítela de nuevo mediante el cmdlet [Disable-AadrmSuperUserFeature](/powershell/module/aadrm/disable-aadrmsuperuserfeature).

El siguiente extracto del registro muestra algunas entradas de ejemplo de uso del cmdlet Get-AadrmAdminLog. En este ejemplo, el administrador de Contoso Ltd confirma que la característica de superusuario está deshabilitada, agrega a Richard Simone como superusuario, comprueba que Richard es el único superusuario configurado para Azure Rights Management Service y habilita la característica de superusuario para que Richard pueda descifrar archivos que estaban protegidos por un empleado que ha dejado la empresa.

`2015-08-01T18:58:20    admin@contoso.com   GetSuperUserFeatureState    Passed  Disabled`

`2015-08-01T18:59:44    admin@contoso.com   AddSuperUser -id rsimone@contoso.com    Passed  True`

`2015-08-01T19:00:51    admin@contoso.com   GetSuperUser    Passed  rsimone@contoso.com`

`2015-08-01T19:01:45    admin@contoso.com   SetSuperUserFeatureState -state Enabled Passed  True`

## <a name="scripting-options-for-super-users"></a>Opciones de scripting para superusuarios
Con frecuencia, alguien asignado como superusuario para [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] tendrá que quitar la protección de varios archivos, en varias ubicaciones. Aunque es posible hacerlo manualmente, resulta más eficaz (y a menudo más confiable) hacerlo mediante scripts. Para ello, puede usar los cmdlets [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) y [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile), según sea necesario. 

Si utiliza clasificación y protección, también puede usar [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) para aplicar una etiqueta nueva que no aplica protección, o bien quitar la etiqueta que aplica la protección. 

Para más información sobre estos cmdlets, consulte [Uso de PowerShell con el cliente de Azure Information Protection](../rms-client/client-admin-guide-powershell.md) de la guía del administrador del cliente de Azure Information Protection.

> [!NOTE]
> El módulo AzureInformationProtection reemplaza el módulo RMS Protection de PowerShell que se instala con la herramienta de protección de RMS. Estos dos módulos son diferentes del [módulo Windows PowerShell para Azure Rights Management](administer-powershell.md) y lo complementan. El módulo AzureInformationProtection es compatible con Azure Information Protection, Azure Rights Management Service (Azure RMS) de Azure Information Protection y Active Directory Rights Management Services (AD RMS).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

