---
title: "PowerShell para plantillas de protección - Azure Information Protection"
description: "Todo lo que puede hacer en Azure Portal para crear y administrar plantillas de protección puede hacerlo desde la línea de comandos mediante PowerShell. Además, puede exportar e importar plantillas, de manera que pueda copiar plantillas entre inquilinos o llevar a cabo ediciones en masa de propiedades complejas en plantillas, como descripciones y nombres multilingües."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 051144562b1c26a22953f6e83a41b4902404fd2f
ms.sourcegitcommit: 85250f5ea80c2ee22197058ff2f65a79503b0f0c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/24/2018
---
# <a name="powershell-reference-for-protection-templates"></a>Referencia de PowerShell para plantillas de protección

>*Se aplica a: Azure Information Protection, Office 365*

La configuración de la protección de Azure Information Protection se guarda en plantillas de protección. Todo lo que puede hacer en Azure Portal para crear y administrar la configuración de protección puede hacerlo desde la línea de comandos mediante PowerShell. 

Además, puede exportar e importar plantillas de protección. Estas dos acciones permiten copiar plantillas de protección entre inquilinos o realizar ediciones en masa de propiedades complejas, como descripciones y nombres multilingües.

También puede utilizar la exportación y la importación para efectuar una copia de seguridad de las plantillas de protección y restaurarlas. Como procedimiento recomendado, realice copias de seguridad de las plantillas con regularidad. Después, si hace algún cambio no deliberado en la configuración de protección, puede revertir fácilmente a una versión anterior.

Para obtener instrucciones de instalación, vea [Instalación del módulo de PowerShell para AADRM](install-powershell.md).

Los cmdlets que admiten la creación y la administración de plantillas de protección:

- [Add-AadrmTemplate](/powershell/module/aadrm/add-aadrmtemplate)

- [Export-AadrmTemplate](/powershell/module/aadrm/export-aadrmtemplate)

- [Get-AadrmTemplate](/powershell/module/aadrm/get-aadrmtemplate)

- [Get-AadrmTemplateProperty](/powershell/module/aadrm/get-aadrmtemplateproperty)

- [Import-AadrmTemplate](/powershell/module/aadrm/import-aadrmtemplate)

- [New-AadrmRightsDefinition](/powershell/module/aadrm/new-aadrmrightsdefinition)

- [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate)

- [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty)



## <a name="see-also"></a>Consulte también
[Configuración y administración de plantillas para Azure Information Protection](configure-policy-templates.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
