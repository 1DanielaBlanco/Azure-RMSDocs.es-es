---
title: "Configuración de superusuarios para Azure Rights Management - AIP"
description: "Obtenga información sobre la característica de superusuario del servicio Azure Rights Management de Azure Information Protection e impleméntela para que los usuarios y servicios autorizados siempre puedan leer e inspeccionar los datos que Azure Rights Management protege para la organización. Esta capacidad se denomina a menudo &quot;razonamiento encima de los datos&quot; y es un elemento crucial en el mantenimiento del control de los datos de su organización."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/24/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: b11367b726a7740d42719b184b6a522e067e205b
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="configuring-super-users-for-azure-rights-management-and-discovery-services-or-data-recovery"></a>Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos

>*Se aplica a: Azure Information Protection, Office 365*

La característica de superusuario del servicio Azure Rights Management de Azure Information Protection garantiza que los usuarios y servicios autorizados siempre puedan leer e inspeccionar los datos que Azure Rights Management protege para la organización. Y, si es necesario, quitar la protección o cambiar la protección que se aplicó anteriormente. Un superusuario siempre tiene derechos completos de propietario para todas las licencias de uso que le ha concedido el inquilino de Azure Information Protection de la organización. Esta capacidad se denomina a menudo “razonamiento encima de los datos” y es un elemento crucial en el mantenimiento del control de los datos de su organización. Por ejemplo, podría usar esta característica en cualquiera de las siguientes situaciones:

-   Un empleado deja la organización y usted necesita leer los archivos que dicho empleado protegió.

-   Un administrador de TI necesita quitar la directiva de protección actual que se configuró para los archivos y aplicar una nueva.

-   Exchange Server necesita indexar los buzones para las operaciones de búsqueda.

-   Tiene servicios de TI existentes para soluciones de prevención de pérdida de datos (DLP), puertas de enlace de cifrado de contenido (CEG) y productos antimalware que deben inspeccionar los archivos que ya están protegidos.

-   Tiene que descifrar archivos de forma masiva con fines de auditoría, legales y otros motivos de cumplimiento.

De forma predeterminada, la característica de superusuario no está habilitada, y no hay ningún usuario asignado a este rol. Se habilita automáticamente si configura el conector de Rights Management para Exchange, y no es necesaria para los servicios estándar que ejecutan Exchange Online, SharePoint Online o SharePoint Server.

Si necesita habilitar manualmente la característica de superusuario, use el cmdlet de PowerShell [Enable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/enable-aadrmsuperuserfeature) y, luego, asigne los usuarios (o cuentas de servicio), según sea necesario, mediante el cmdlet [Add-AadrmSuperUser](/powershell/aadrm/vlatest/add-aadrmsuperuser) o el cmdlet [Set-AadrmSuperUserGroup](/powershell/aadrm/vlatest/set-aadrmsuperusergroup) y agregue usuarios (u otros grupos), según sea necesario para este grupo. 

Aunque el uso de un grupo para los superusuarios es más fácil de administrar, tenga en cuenta que, por motivos de rendimiento, Azure Rights Management [almacena en caché la pertenencia al grupo](../plan-design/prepare.md#group-membership-caching). Por tanto, si necesita asignar un nuevo usuario como superusuario para descifrar contenido inmediatamente, agregue ese usuario mediante Add-AadrmSuperUser, en lugar de agregar el usuario a un grupo existente que ha configurado mediante Set-AadrmSuperUserGroup.

> [!NOTE]
> Si aún no ha instalado el módulo de Windows PowerShell para [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], consulte [Instalación de Windows PowerShell para Azure Rights Management](install-powershell.md).

Prácticas de seguridad recomendadas para la característica de superusuario:

-   Use el cmdlet [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629417.aspx) para restringir y supervisar los administradores que tienen asignado el rol Administrador global para el inquilino de Office 365 o Azure Information Protection, o bien para conocer los usuarios que tienen asignado el rol Administrador global. Estos usuarios pueden habilitar la característica de superusuario y asignar usuarios (y a ellos mismos) como superusuarios y posiblemente descifrar todos los archivos que protege su organización.

-   Para ver qué usuarios y cuentas de servicio están asignados individualmente como superusuarios, use el cmdlet [Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629408.aspx). Para ver si se ha configurado un grupo de superusuarios, use el cmdlet [Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/mt653942.aspx) y sus herramientas de administración de usuarios estándar para comprobar qué usuarios forman parte de este grupo. Al igual que todas las acciones de administración, habilitar o deshabilitar la característica de superusuarios y agregar o quitar superusuarios se registran y se pueden auditar mediante el comando [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) . Cuando los superusuarios descifrar archivos, esta acción se registra y se puede auditar con el [registro de uso](log-analyze-usage.md).

-   Si no necesita la característica de superusuario para los servicios diarios, habilítela solo cuando lo necesite y deshabilítela de nuevo con el cmdlet [Disable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629428.aspx) .

El siguiente extracto del registro muestra algunas entradas de ejemplo de uso del cmdlet Get-AadrmAdminLog. En este ejemplo, el administrador de Contoso Ltd confirma que la característica de superusuario está deshabilitada, agrega a Richard Simone como un superusuario, comprueba que Richard es el único superusuario configurado para el servicio Azure Rights Management y, después, habilita la característica de superusuario para que Richard pueda descifrar archivos que había protegido un empleado que ahora ha dejado la compañía.

`2015-08-01T18:58:20    admin@contoso.com    GetSuperUserFeatureState    Passed    Disabled`

`2015-08-01T18:59:44    admin@contoso.com    AddSuperUser -id rsimone@contoso.com    Passed    True`

`2015-08-01T19:00:51    admin@contoso.com    GetSuperUser    Passed    rsimone@contoso.com`

`2015-08-01T19:01:45    admin@contoso.com    SetSuperUserFeatureState -state Enabled    Passed    True`

## <a name="scripting-options-for-super-users"></a>Opciones de script para superusuarios
Con frecuencia, alguien asignado como superusuario para [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] deberá quitar la protección de varios archivos, en varias ubicaciones. Aunque es posible hacerlo manualmente, resulta más eficaz (y a menudo más fiable) mediante scripts. Para ello, use el cmdlet [Unprotect-RMSFile](/powershell/azureinformationprotection/vlatest/unprotect-rmsfile) y el cmdlet [Protect-RMSFile](/powershell/azureinformationprotection/vlatest/protect-rmsfile), según sea necesario. 

Si usa la clasificación y la protección, también puede utilizar [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel) para aplicar una etiqueta nueva que no aplica protección, o quitar la etiqueta que ha aplicado la protección. 

Para más información sobre estos cmdlets, vea [Uso de PowerShell con el cliente de Azure Information Protection ](../rms-client/client-admin-guide-powershell.md) en la guía para administradores del cliente de Azure Information Protection.

> [!NOTE]
> El módulo AIP reemplaza al módulo de PowerShell RMS Protection que se instala con la herramienta de protección de RMS. Ambos módulos son diferentes entre sí y complementan el [módulo principal de Windows PowerShell para Azure Rights Management](administer-powershell.md). El módulo AIP es compatible con Azure Information Protection, el servicio Azure Rights Management (Azure RMS) para Azure Information Protection y Active Directory Rights Management Services (AD RMS).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

