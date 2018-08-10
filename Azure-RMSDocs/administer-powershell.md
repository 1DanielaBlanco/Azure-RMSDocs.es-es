---
title: Administración de Azure Rights Management con PowerShell - AIP
description: Obtenga información sobre cómo usar el módulo de PowerShell del servicio Azure Rights Management (AADRM) para Azure Information Protection con el fin de administrar este servicio para la organización.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/13/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 4b37c178ab98ee826acb958201dd197748d045c0
ms.sourcegitcommit: 5fdf013fe05b65517b56245e1807875d80be6e70
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2018
ms.locfileid: "39490218"
---
# <a name="administering-the-azure-rights-management-service-by-using-windows-powershell"></a>Administración del servicio Azure Rights Management mediante Windows PowerShell

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

¿Necesita usar PowerShell para administrar el servicio Azure Rights Management para Azure Information Protection? Probablemente pueda prescindir de ello si toda su configuración se puede realizar en Azure Portal o en el Portal de Office 365. A pesar de ello, PowerShell es necesario para algunas configuraciones avanzadas y también es preferible usar PowerShell para el scripting y un control más eficaz de la línea de comandos.

En la tabla de la siguiente sección se incluyen algunos de los escenarios de configuración avanzada que usan PowerShell. Esta información también se incluye en la tabla aunque la configuración se pueda realizar también sin usar PowerShell.

Para una lista completa de los cmdlets disponibles para este módulo con más información sobre cada uno de ellos, consulte [AADRM](/powershell/module/aadrm/?view=azureipps#aadrm).

> [!NOTE]
> Para instalar este módulo de PowerShell, vea [Instalación del módulo de PowerShell para AADRM](install-powershell.md).

Aparte de este módulo de PowerShell del lado de servicio, el cliente de Azure Information Protection instala un módulo de PowerShell complementario, **AzureInformationProtection**. Este módulo de cliente permite clasificar y proteger varios archivos para que, por ejemplo, pueda proteger en masa todos los archivos de una carpeta. Para más información, vea [Uso de PowerShell con el cliente de Azure Information Protection](./rms-client/client-admin-guide-powershell.md) en la guía del administrador.

## <a name="cmdlets-grouped-by-administration-task"></a>Cmdlets agrupados por tarea de administración

|Si tienes que…|…usar los cmdlets siguientes|
|-------------------|------------------------------|
|Migrar de Rights Management local (AD RMS o Windows RMS) a Azure Information Protection.|[Import-AadrmTpd](/powershell/aadrm/vlatest/import-aadrmtpd)<br /><br />[Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties)|
|Conectarse o desconectarse desde el servicio Rights Management de la organización.|[Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice)<br /><br />[Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice)|
|Genera y administra tu propia clave de inquilino; el escenario Aportar tu propia clave (BYOK).|[Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties)<br /><br />[Use-AadrmKeyVaultKey](/powershell/aadrm/vlatest/use-aadrmkeyvaultkey)<br /><br />[Get-AadrmKeys](/powershell/aadrm/vlatest/get-aadrmkeys)|
|Activar o desactivar el servicio Rights Management de la organización.<br /><br />También puede realizar estas acciones en los portales de administración. Para más información, vea [Activar Azure Rights Management](activate-service.md).|[Enable-Aadrm](/powershell/aadrm/vlatest/enable-aadrm)<br /><br />[Disable-Aadrm](/powershell/aadrm/vlatest/disable-aadrm)|
|Administre el sitio de seguimiento de documentos para Azure Information Protection.|[Disable-AadrmDocumentTrackingFeature](/powershell/aadrm/vlatest/disable-aadrmdocumenttrackingfeature)<br /><br />[Enable-AadrmDocumentTrackingFeature](/powershell/aadrm/vlatest/enable-aadrmdocumenttrackingfeature)<br /><br />[Get-AadrmDocumentTrackingFeature](/powershell/aadrm/vlatest/get-aadrmdocumenttrackingfeature)<br /><br />[Set-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/set-aadrmdonottrackusergroup)<br /><br />[Clear-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/Clear-AadrmDoNotTrackUserGroup)<br /><br />[Get-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/get-AadrmDoNotTrackUserGroup)<br /><br />[Get-AadrmTrackingLog](/powershell/module/aadrm/Get-AadrmTrackingLog)<br /><br />[Get-AadrmDocumentLog](/powershell/module/aadrm/Get-AadrmDocumentLog)|
|Configurar los controles de incorporación para una implementación por fases del servicio Azure Rights Management.|[Get-AadrmOnboardingControlPolicy](/powershell/aadrm/vlatest/get-aadrmonboardingcontrolpolicy)<br /><br />[Set-AadrmOnboardingControlPolicy](/powershell/aadrm/vlatest/set-aadrmonboardingcontrolpolicy)|
|Crear y administrar plantillas de Rights Management para la organización.<br /><br />También puede realizar la mayoría de estas acciones en Azure Portal, aunque PowerShell ofrece un control más minucioso. Para obtener más información, vea [Configuración y administración de plantillas para Azure Information Protection](configure-policy-templates.md).|[Add-AadrmTemplate](/powershell/aadrm/vlatest/add-aadrmtemplate)<br /><br />[Export-AadrmTemplate](/powershell/aadrm/vlatest/export-aadrmtemplate)<br /><br />[Get-AadrmTemplate](/powershell/aadrm/vlatest/get-aadrmtemplate)<br /><br />[Get-AadrmTemplateProperty](/powershell/aadrm/vlatest/get-aadrmtemplateproperty)<br /><br />[Import-AadrmTemplate](/powershell/aadrm/vlatest/import-aadrmtemplate)<br /><br />[New-AadrmRightsDefinition](/powershell/aadrm/vlatest/new-aadrmrightsdefinition)<br /><br />[Remove-AadrmTemplate](/powershell/aadrm/vlatest/remove-aadrmtemplate)<br /><br />[Set-AadrmTemplateProperty](/powershell/aadrm/vlatest/set-aadrmtemplateproperty)|
|Configurar el número máximo de días que se puede acceder al contenido que protege su organización sin una conexión a Internet (el período de validez de la licencia de uso).|[Get-AadrmMaxUseLicenseValidityTime](/powershell/aadrm/vlatest/get-aadrmmaxuselicensevaliditytime)<br /><br />[Set-AadrmMaxUseLicenseValidityTime](/powershell/aadrm/vlatest/set-aadrmmaxuselicensevaliditytime)|
|Administrar la función de superusario de Rights Management de la organización.|[Enable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/enable-aadrmsuperuserfeature)<br /><br />[Disable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/disable-aadrmsuperuserfeature)<br /><br />[Add-AadrmSuperUser](/powershell/aadrm/vlatest/add-aadrmsuperuser)<br /><br />[Get-AadrmSuperUser](/powershell/aadrm/vlatest/get-aadrmsuperuser)<br /><br />[Remove-AadrmSuperUser](/powershell/aadrm/vlatest/remove-aadrmsuperuser)<br /><br />[Set-AadrmSuperUserGroup](/powershell/aadrm/vlatest/set-aadrmsuperusergroup)<br /><br />[Get-AadrmSuperUserGroup](/powershell/aadrm/vlatest/get-aadrmsuperusergroup)<br /><br />[Clear-AadrmSuperUserGroup](/powershell/aadrm/vlatest/clear-aadrmsuperusergroup)|
|Administrar usuarios y grupos que estén autorizados a administrar el servicio Rights Management de la organización.|[Add-AadrmRoleBasedAdministrator](/powershell/aadrm/vlatest/add-aadrmrolebasedadministrator)<br /><br />[Get-AadrmRoleBasedAdministrator](/powershell/aadrm/vlatest/get-aadrmrolebasedadministrator)<br /><br />[Remove-AadrmRoleBasedAdministrator](/powershell/aadrm/vlatest/remove-aadrmrolebasedadministrator)|
|Obtener un registro de las tareas administrativas de Rights Management de la organización.|[Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx)|
|Registrar y analizar el registro de uso de Rights Management.|[Get-AadrmUserLog](/powershell/aadrm/vlatest/get-aadrmuserlog)|
|Mostrar la configuración actual del servicio Rights Management de la organización.|[Get-AadrmConfiguration](/powershell/aadrm/vlatest/get-aadrmconfiguration)|
|Migrar su organización de Azure Information Protection a una implementación de AD RMS local.|[Set-AadrmMigrationUrl](/powershell/aadrm/vlatest/set-aadrmmigrationurl)<br /><br />[Get–AadrmMigrationUrl](/powershell/aadrm/vlatest/get-aadrmmigrationurl)|

