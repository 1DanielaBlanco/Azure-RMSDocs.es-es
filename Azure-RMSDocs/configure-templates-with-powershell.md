---
title: PowerShell para plantillas de protección - Azure Information Protection
description: Todo lo que puede hacer en Azure Portal para crear y administrar plantillas de protección puede hacerlo desde la línea de comandos mediante PowerShell. Además, puede exportar e importar plantillas, de manera que pueda copiar plantillas entre inquilinos o llevar a cabo ediciones en masa de propiedades complejas en plantillas, como descripciones y nombres multilingües.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 12/12/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 3e1915c327daaee35d9f0e8053f944fd1fcdbd7a
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56254618"
---
# <a name="powershell-reference-for-protection-templates"></a>Referencia de PowerShell para plantillas de protección

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

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

