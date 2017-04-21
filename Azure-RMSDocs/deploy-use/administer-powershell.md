---
title: "Administración de Azure Rights Management con PowerShell - AIP"
description: "Obtenga información sobre cómo usar el módulo de PowerShell del servicio Azure Rights Management (AADRM) para Azure Information Protection con el fin de administrar este servicio para la organización."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/18/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 38c515e482a9d80e10ae691af1d074a78c3771ab
ms.sourcegitcommit: 9c033b7f5a6cbb20275aeecd48ff5071964eb587
translationtype: HT
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
|Migrar de Rights Management local (AD RMS o Windows RMS) a Azure Information Protection.|[Import-AadrmTpd](/powershell/aadrm/vlatest/import-aadrmtpd)<br /><br />[Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties)|
|Conéctate o desconéctate desde el servicio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para tu organización.|[Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice)<br /><br />[Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice)|
|Genera y administra tu propia clave de inquilino; el escenario Aportar tu propia clave (BYOK).|[Use-AadrmKeyVaultKey](/powershell/aadrm/vlatest/use-aadrmkeyvaultkey)<br /><br />[Get-AadrmKeys](/powershell/aadrm/vlatest/get-aadrmkeys)|
|Activa o desactiva el servicio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para tu organización.<br /><br />También puede realizar estas acciones en los portales de administración. Para más información, vea [Activar Azure Rights Management](activate-service.md).|[Enable-Aadrm](/powershell/aadrm/vlatest/enable-aadrm)<br /><br />[Disable-Aadrm](/powershell/aadrm/vlatest/disable-aadrm)|
|Deshabilitar o habilitar el sitio de seguimiento de documentos de Azure Information Protection.|[Disable-AadrmDocumentTrackingFeature](/powershell/aadrm/vlatest/disable-aadrmdocumenttrackingfeature)<br /><br />[Enable-AadrmDocumentTrackingFeature](/powershell/aadrm/vlatest/enable-aadrmdocumenttrackingfeature)<br /><br />[Get-AadrmDocumentTrackingFeature](/powershell/aadrm/vlatest/get-aadrmdocumenttrackingfeature)|
|Configurar los controles de incorporación para una implementación por fases del servicio Azure Rights Management.|[Get-AadrmOnboardingControlPolicy](/powershell/aadrm/vlatest/get-aadrmonboardingcontrolpolicy)<br /><br />[Set-AadrmOnboardingControlPolicy](/powershell/aadrm/vlatest/set-aadrmonboardingcontrolpolicy)|
|Crear y administrar plantillas de Rights Management para la organización.<br /><br />También puede realizar la mayoría de estas acciones en el Portal de Azure clásico, aunque PowerShell ofrece un control más minucioso. Para más información, vea [Configuración de plantillas personalizadas para el servicio Azure Rights Management](configure-custom-templates.md).|[Add-AadrmTemplate](/powershell/aadrm/vlatest/add-aadrmtemplate)<br /><br />[Export-AadrmTemplate](/powershell/aadrm/vlatest/export-aadrmtemplate)<br /><br />[Get-AadrmTemplate](/powershell/aadrm/vlatest/get-aadrmtemplate)<br /><br />[Get-AadrmTemplateProperty](/powershell/aadrm/vlatest/get-aadrmtemplateproperty)<br /><br />[Import-AadrmTemplate](/powershell/aadrm/vlatest/import-aadrmtemplate)<br /><br />[New-AadrmRightsDefinition](/powershell/aadrm/vlatest/new-aadrmrightsdefinition)<br /><br />[Remove-AadrmTemplate](/powershell/aadrm/vlatest/remove-aadrmtemplate)<br /><br />[Set-AadrmTemplateProperty](/powershell/aadrm/vlatest/set-aadrmtemplateproperty)|
|Configurar el número máximo de días que se puede acceder al contenido que protege su organización sin una conexión a Internet (el período de validez de la licencia de uso).|[Get-AadrmMaxUseLicenseValidityTime](/powershell/aadrm/vlatest/get-aadrmmaxuselicensevaliditytime)<br /><br />[Set-AadrmMaxUseLicenseValidityTime](/powershell/aadrm/vlatest/set-aadrmmaxuselicensevaliditytime)|
|Administra la función del superusario de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para tu organización.|[Enable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/enable-aadrmsuperuserfeature)<br /><br />[Disable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/disable-aadrmsuperuserfeature)<br /><br />[Add-AadrmSuperUser](/powershell/aadrm/vlatest/add-aadrmsuperuser)<br /><br />[Get-AadrmSuperUser](/powershell/aadrm/vlatest/get-aadrmsuperuser)<br /><br />[Remove-AadrmSuperUser](/powershell/aadrm/vlatest/remove-aadrmsuperuser)<br /><br />[Set-AadrmSuperUserGroup](/powershell/aadrm/vlatest/set-aadrmsuperusergroup)<br /><br />[Get-AadrmSuperUserGroup](/powershell/aadrm/vlatest/get-aadrmsuperusergroup)<br /><br />[Clear-AadrmSuperUserGroup](/powershell/aadrm/vlatest/clear-aadrmsuperusergroup)|
|Administra usuarios y grupos que estén autorizados a administrar el servicio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para tu organización.|[Add-AadrmRoleBasedAdministrator](/powershell/aadrm/vlatest/add-aadrmrolebasedadministrator)<br /><br />[Get-AadrmRoleBasedAdministrator](/powershell/aadrm/vlatest/get-aadrmrolebasedadministrator)<br /><br />[Remove-AadrmRoleBasedAdministrator](/powershell/aadrm/vlatest/remove-aadrmrolebasedadministrator)|
|Obtén un registro de las tareas administrativas de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para tu organización.|[Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx)|
|Registra y analiza el registro de uso para [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].|[Get-AadrmUserLog](/powershell/aadrm/vlatest/get-aadrmuserlog)|
|Muestra la configuración actual del servicio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para tu organización.|[Get-AadrmConfiguration](/powershell/aadrm/vlatest/get-aadrmconfiguration)|
|Migrar su organización de Azure Information Protection a una implementación de AD RMS local.|[Set-AadrmMigrationUrl](/powershell/aadrm/vlatest/set-aadrmmigrationurl)<br /><br />[Get–AadrmMigrationUrl](/powershell/aadrm/vlatest/get-aadrmmigrationurl)|

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
