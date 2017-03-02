---
title: "Administración de Azure Rights Management con PowerShell - AIP"
description: "Obtenga información sobre cómo usar el módulo de PowerShell del servicio Azure Rights Management (AADRM) para Azure Information Protection con el fin de administrar este servicio para la organización."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/14/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 085dc82fcb9632bfdf4fb1b14ca5c632846e81d0
ms.lasthandoff: 02/24/2017


---

# <a name="administering-the-azure-rights-management-service-by-using-windows-powershell"></a>Administración del servicio Azure Rights Management mediante Windows PowerShell

>*Se aplica a: Azure Information Protection, Office 365*

¿Necesita usar PowerShell para administrar el servicio Azure Rights Management para Azure Information Protection? No es necesario si es un administrador global y la única configuración necesaria para este servicio es activarlo (o desactivarlo) y configurar las plantillas de Rights Management.

Sin embargo, sí necesita usar PowerShell para configuraciones más avanzadas y también si no es un administrador global, pero un administrador global le ha concedido permisos para administrar el servicio. También es preferible usar PowerShell para el scripting y un control más eficaz de la línea de comandos.

En la tabla de la siguiente sección se incluyen algunos de los escenarios de configuración avanzada que usan PowerShell. Esta información también se incluye en la tabla aunque la configuración se pueda realizar también sin usar PowerShell.

Para una lista completa de los cmdlets disponibles con más información acerca de cada uno de ellos, consulte [Cmdlets de Azure Rights Management](http://msdn.microsoft.com/library/azure/dn629398.aspx).

> [!NOTE]
> Para instalar este módulo de PowerShell, vea [Instalación de Windows PowerShell para Azure Rights Management](install-powershell.md).

Aparte de este módulo de PowerShell del lado de servicio, el cliente de Azure Information Protection instala un módulo de PowerShell complementario, **AzureInformationProtection**. Este módulo de cliente permite clasificar y proteger varios archivos para que, por ejemplo, pueda proteger en masa todos los archivos de una carpeta. Para más información, vea [Uso de PowerShell con el cliente de Azure Information Protection](../rms-client/client-admin-guide-powershell.md) en la guía del administrador.

## <a name="cmdlets-grouped-by-administration-task"></a>Cmdlets agrupados por tarea de administración

|Si tienes que…|…usar los cmdlets siguientes|
|-------------------|------------------------------|
|Migrar de Rights Management local (AD RMS o Windows RMS) a Azure Information Protection.|[Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx)|
|Conéctate o desconéctate desde el servicio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para tu organización.|[Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx)<br /><br />[Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx)|
|Genera y administra tu propia clave de inquilino; el escenario Aportar tu propia clave (BYOK).|[Use-AadrmKeyVaultKey](https://msdn.microsoft.com/library/azure/mt759829.aspx)<br /><br />[Get-AadrmKeys](http://msdn.microsoft.com/library/azure/dn629420.aspx)|
|Activa o desactiva el servicio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para tu organización.<br /><br />También puede realizar estas acciones en los portales de administración. Para más información, vea [Activar Azure Rights Management](activate-service.md).|[Enable-Aadrm](http://msdn.microsoft.com/library/azure/dn629412.aspx)<br /><br />[Disable-Aadrm](http://msdn.microsoft.com/library/azure/dn629422.aspx)|
|Deshabilitar o habilitar el sitio de seguimiento de documentos de Azure Information Protection.|[Disable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548471.aspx)<br /><br />[Enable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548469.aspx)<br /><br />[Get-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548470.aspx)|
|Configurar los controles de incorporación para una implementación por fases del servicio Azure Rights Management.|[Get-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857522.aspx)<br /><br />[Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx)|
|Crear y administrar plantillas de Rights Management para la organización.<br /><br />También puede realizar la mayoría de estas acciones en el Portal de Azure clásico, aunque PowerShell ofrece un control más minucioso. Para más información, vea [Configuración de plantillas personalizadas para el servicio Azure Rights Management](configure-custom-templates.md).|[Add-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727075.aspx)<br /><br />[Export-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727078.aspx)<br /><br />[Get-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727079.aspx)<br /><br />[Get-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727081.aspx)<br /><br />[Import-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727077.aspx)<br /><br />[New-AadrmRightsDefinition](http://msdn.microsoft.com/library/azure/dn727080.aspx)<br /><br />[Remove-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727082.aspx)<br /><br />[Set-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727076.aspx)|
|Configurar el número máximo de días que se puede acceder al contenido que protege su organización sin una conexión a Internet (el período de validez de la licencia de uso).|[Get-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932062.aspx)<br /><br />[Set-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx)|
|Administra la función del superusario de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para tu organización.|[Enable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629400.aspx)<br /><br />[Disable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629428.aspx)<br /><br />[Add-AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629411.aspx)<br /><br />[Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629408.aspx)<br /><br />[Remove-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629405.aspx)<br /><br />[Set-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653943.aspx)<br /><br />[Get-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653942.aspx)<br /><br />[Clear-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653944.aspx)|
|Administra usuarios y grupos que estén autorizados a administrar el servicio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para tu organización.|[Add-AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629417.aspx)<br /><br />[Get-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629407.aspx)<br /><br />[Remove-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629424.aspx)|
|Obtén un registro de las tareas administrativas de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para tu organización.|[Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx)|
|Registra y analiza el registro de uso para [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].|[Get-AadrmUserLog](https://msdn.microsoft.com/library/azure/mt653941.aspx)|
|Muestra la configuración actual del servicio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para tu organización.|[Get-AadrmConfiguration](http://msdn.microsoft.com/library/azure/dn629410.aspx)|
|Migrar su organización de Azure Information Protection a una implementación de AD RMS local.|[Set-AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx)<br /><br />[Get–AadrmMigrationUrl](http://msdn.microsoft.com/library/azure/dn629403.aspx)|

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



