---
title: "Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: 0ca9b8d9643f5489c100fa3aa614e89cd396df52


---

# Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos

*Se aplica a: Azure Rights Management, Office 365*

La característica de superusuario de Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) garantiza que personas y servicios autorizados pueden siempre leer e inspeccionar los datos que protege Azure RMS en su organización. Y, si es necesario, quitar la protección o cambiar la protección que se aplicó anteriormente. Un superusuario siempre tiene derechos completos de propietario para todas las licencias de uso que le ha concedido el inquilino de RMS de la organización. Esta capacidad se denomina a menudo “razonamiento encima de los datos” y es un elemento crucial en el mantenimiento del control de los datos de su organización. Por ejemplo, podría usar esta característica en cualquiera de las siguientes situaciones:

-   Un empleado deja la organización y usted necesita leer los archivos que dicho empleado protegió.

-   Un administrador de TI necesita quitar la directiva de protección actual que se configuró para los archivos y aplicar una nueva.

-   Exchange Server necesita indexar los buzones para las operaciones de búsqueda.

-   Tiene servicios de TI existentes para soluciones de prevención de pérdida de datos (DLP), puertas de enlace de cifrado de contenido (CEG) y productos antimalware que deben inspeccionar los archivos que ya están protegidos.

-   Tiene que descifrar archivos de forma masiva con fines de auditoría, legales y otros motivos de cumplimiento.

De forma predeterminada, la característica de superusuario no está habilitada, y no hay ningún usuario asignado a este rol. Se habilita automáticamente si configura el conector de Rights Management para Exchange, y no es necesaria para los servicios estándar que ejecutan Exchange Online, SharePoint Online o SharePoint Server.

Si necesita habilitar manualmente la característica de superusuario, use el cmdlet de Windows PowerShell [Enable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629400.aspx) y, luego, asigne los usuarios (o cuentas de servicio), según sea necesario, mediante el cmdlet [Add-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629411.aspx) o el cmdlet [Set-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653943.aspx) y agregue usuarios (u otros grupos), según sea necesario para este grupo. 

> [!NOTE]
> Si aún no ha instalado el módulo de Windows PowerShell para [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], consulte [Instalación de Windows PowerShell para Azure Rights Management](install-powershell.md).

Prácticas de seguridad recomendadas para la característica de superusuario:

-   Restrinja y supervise qué administradores se asignan como administrador global para el inquilino de Office 365 o Azure RMS, o quién está asignado al rol GlobalAdministrator mediante el cmdlet [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629417.aspx) . Estos usuarios pueden habilitar la característica de superusuario y asignar usuarios (y a ellos mismos) como superusuarios y posiblemente descifrar todos los archivos que protege su organización.

-   Para ver qué usuarios y cuentas de servicio están asignados individualmente como superusuarios, use el cmdlet [Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629408.aspx). Para ver si se ha configurado un grupo de superusuarios, use el cmdlet [Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/mt653942.aspx) y sus herramientas de administración de usuarios estándar para comprobar qué usuarios forman parte de este grupo. Al igual que todas las acciones de administración, habilitar o deshabilitar la característica de superusuarios y agregar o quitar superusuarios se registran y se pueden auditar mediante el comando [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) . Cuando los superusuarios descifrar archivos, esta acción se registra y se puede auditar con el [registro de uso](log-analyze-usage.md).

-   Si no necesita la característica de superusuario para los servicios diarios, habilítela solo cuando lo necesite y deshabilítela de nuevo con el cmdlet [Disable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629428.aspx) .

El siguiente extracto del registro muestra algunas entradas de ejemplo de uso del cmdlet Get-AadrmAdminLog. En este ejemplo, el administrador de Contoso Ltd confirma que la característica de superusuario está deshabilitada, agrega a Richard Simone como un superusuario, comprueba que Richard es el único superusuario configurado para Azure RMS y, luego, habilita la característica de superusuario para que Richard pueda descifrar algunos archivos que protegió un empleado que ahora ha dejado la empresa.

`2015-08-01T18:58:20    admin@contoso.com   GetSuperUserFeatureState    Passed  Disabled`

`2015-08-01T18:59:44    admin@contoso.com   AddSuperUser -id rsimone@contoso.com    Passed  True`

`2015-08-01T19:00:51    admin@contoso.com   GetSuperUser    Passed  rsimone@contoso.com`

`2015-08-01T19:01:45    admin@contoso.com   SetSuperUserFeatureState -state Enabled Passed  True`

## Opciones de script para superusuarios
Con frecuencia, alguien asignado como superusuario para [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] deberá quitar la protección de varios archivos, en varias ubicaciones. Aunque es posible hacerlo manualmente, resulta más eficaz (y a menudo más fiable) mediante scripts. Para ello, [descargue la herramienta de protección de RMS](http://www.microsoft.com/en-us/download/details.aspx?id=47256). Luego, use el cmdlet  [Unprotect-RMSFile](https://msdn.microsoft.com/library/azure/mt433200.aspx) y el cmdlet [Protect-RMSFile](https://msdn.microsoft.com/library/azure/mt433201.aspx) , según sea necesario.

Para obtener más información sobre estos cmdlets, consulte [Cmdlets de protección de RMS](https://msdn.microsoft.com/library/azure/mt433195.aspx).

> [!NOTE]
> El módulo de protección de RMS de PowerShell que se suministra con la herramienta de protección de RMS es diferente del [módulo de Windows PowerShell para Azure Rights Management](administer-powershell.md)y lo complementa. El módulo de protección de RMS admite Azure RMS y AD RMS.





<!--HONumber=Jun16_HO4-->


