---
title: Configuración de superusuarios para Azure Rights Management - AIP
description: Obtenga información sobre la característica de superusuario del servicio Azure Rights Management de Azure Information Protection e impleméntela para que los usuarios y servicios autorizados siempre puedan leer e inspeccionar los datos que Azure Rights Management protege para la organización. Esta capacidad se denomina a menudo "razonamiento encima de los datos" y es un elemento crucial en el mantenimiento del control de los datos de su organización.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/12/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: c4b4df01be10ce033dd7369e71420e949750e667
ms.sourcegitcommit: 1e6394044d646278ae582c7713cac8ffb9bf4c1e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2018
ms.locfileid: "49169914"
---
# <a name="configuring-super-users-for-azure-rights-management-and-discovery-services-or-data-recovery"></a>Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

La característica de superusuario del servicio Azure Rights Management de Azure Information Protection garantiza que los usuarios y servicios autorizados siempre puedan leer e inspeccionar los datos que Azure Rights Management protege para la organización. Si es necesario, la protección se puede quitar o modificar.

Un superusuario siempre tiene el [derecho de uso](configure-usage-rights.md) de control total de Rights Management para documentos y correos electrónicos que se han protegido mediante el inquilino de Azure Information Protection de su organización. Esta capacidad se denomina a menudo "razonamiento encima de los datos" y es un elemento crucial en el mantenimiento del control de los datos de su organización. Por ejemplo, podría usar esta característica en cualquiera de las siguientes situaciones:

- Un empleado deja la organización y usted necesita leer los archivos que dicho empleado protegió.

- Un administrador de TI necesita quitar la directiva de protección actual que se configuró para los archivos y aplicar una nueva.

- Exchange Server necesita indexar los buzones para las operaciones de búsqueda.

- Tiene servicios de TI existentes para soluciones de prevención de pérdida de datos (DLP), puertas de enlace de cifrado de contenido (CEG) y productos antimalware que deben inspeccionar los archivos que ya están protegidos.

- Tiene que descifrar archivos de forma masiva con fines de auditoría, legales y otros motivos de cumplimiento.

## <a name="configuration-for-the-super-user-feature"></a>Configuración de la característica de superusuario

De forma predeterminada, la característica de superusuario no está habilitada, y no hay ningún usuario asignado a este rol. Se habilita automáticamente si configura el conector de Rights Management para Exchange, y no es necesaria para los servicios estándar que ejecutan Exchange Online, SharePoint Online o SharePoint Server.

Si necesita habilitar manualmente la característica de superusuario, use el cmdlet de PowerShell [Enable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/enable-aadrmsuperuserfeature) y, luego, asigne los usuarios (o cuentas de servicio), según sea necesario, mediante el cmdlet [Add-AadrmSuperUser](/powershell/aadrm/vlatest/add-aadrmsuperuser) o el cmdlet [Set-AadrmSuperUserGroup](/powershell/aadrm/vlatest/set-aadrmsuperusergroup) y agregue usuarios (u otros grupos), según sea necesario para este grupo. 

Aunque el uso de un grupo para los superusuarios es más fácil de administrar, tenga en cuenta que, por motivos de rendimiento, Azure Rights Management [almacena en caché la pertenencia al grupo](prepare.md#group-membership-caching-by-azure-information-protection). Por tanto, si necesita asignar un nuevo usuario como superusuario para descifrar contenido inmediatamente, agregue ese usuario mediante Add-AadrmSuperUser, en lugar de agregar el usuario a un grupo existente que ha configurado mediante Set-AadrmSuperUserGroup.

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

Para más información sobre estos cmdlets, vea [Uso de PowerShell con el cliente de Azure Information Protection ](./rms-client/client-admin-guide-powershell.md) en la guía para administradores del cliente de Azure Information Protection.

> [!NOTE]
> El módulo AzureInformationProtection es diferente y complementa al [módulo AADRM PowerShell](administer-powershell.md) que administra el servicio Azure Rights Management para Azure Information Protection.

### <a name="guidance-for-using-unprotect-rmsfile-for-ediscovery"></a>Instrucciones de uso de Unprotect-RMSFile para eDiscovery

Aunque el cmdlet Unprotect-RMSFile se pueda usar para descifrar contenido protegido en archivos PST, úselo de forma estratégica como parte del proceso de eDiscovery. La ejecución de Unprotect-RMSFile en archivos de gran tamaño en un equipo usa una gran cantidad de recursos (memoria y espacio en disco) y el tamaño de archivo máximo que se admite para este cmdlet es de 5 GB.

Lo ideal es usar [eDiscovery de Office 365](/office365/securitycompliance/ediscovery) para buscar y extraer correos electrónicos protegidos y datos adjuntos protegidos en los mensajes de correo electrónico. La capacidad de superusuario se integra de forma automática en Exchange Online para que eDiscovery en el Centro de seguridad y cumplimiento de Office 365 pueda buscar elementos cifrados antes de la exportación, o bien descifrar el correo electrónico cifrado durante la exportación.

Si no puede usar eDiscovery de Office 365, es posible que tenga otra solución de eDiscovery que se integre con el servicio Azure Rights Management para analizar los datos de forma similar. O bien, si su solución de eDiscovery no puede leer y descifrar de forma automática el contenido cifrado, aún puede usar esta solución en un proceso de varios pasos que le permite ejecutar Unprotect-RMSFile con mayor eficacia:

1. Exporte el correo electrónico a un archivo PST desde Exchange Online o Exchange Server, o bien desde la estación de trabajo en la que lo haya almacenado el usuario.

2. Importe el archivo PST a su herramienta de eDiscovery. Como la herramienta no puede leer el contenido protegido, se espera que estos elementos generen errores.

3. A partir de todos los elementos que la herramienta no ha podido abrir, genere un archivo PST nuevo que, en esta ocasión, contenga solo los elementos protegidos. Probablemente este segundo archivo PST será mucho más pequeño que el original.

4. Ejecute Unprotect-RMSFile en este segundo archivo PST para descifrar el contenido de este archivo mucho más pequeño. Desde la salida, importe el archivo PST descifrado a la herramienta de detección.

Para obtener más información e instrucciones para ejecutar eDiscovery en buzones y archivos PST, vea la entrada de blog siguiente: [Azure Information Protection and eDiscovery Processes](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-and-eDiscovery-Processes/ba-p/270216) (Procesos de Azure Information Protection y eDiscovery).

