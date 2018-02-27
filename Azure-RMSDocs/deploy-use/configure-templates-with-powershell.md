---
title: PowerShell para plantillas personalizadas de Azure RMS - AIP
description: "Todo lo que puede hacer en Azure Portal para crear y administrar plantillas de administración de derechos puede hacerlo también desde la línea de comandos mediante PowerShell. Además, puede exportar e importar plantillas, de manera que pueda copiar plantillas entre inquilinos o llevar a cabo ediciones en masa de propiedades complejas en plantillas, como descripciones y nombres multilingües."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d8e31eb4f573a149ae39c32c89607775de61bfce
ms.sourcegitcommit: 31c79d948ec3089a4dc65639f1842c07c7aecba6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/20/2018
---
# <a name="powershell-reference-for-custom-templates"></a>Referencia de PowerShell para plantillas personalizadas

>*Se aplica a: Azure Information Protection, Office 365*

Todo lo que puede hacer en Azure Portal para crear y administrar plantillas puede hacerlo desde la línea de comandos mediante PowerShell. Además, puede exportar e importar plantillas, de manera que pueda copiar plantillas entre inquilinos o llevar a cabo ediciones en masa de propiedades complejas en plantillas, como descripciones y nombres multilingües.

También puede utilizar la exportación e importación para restaurar y hacer una copia de seguridad de sus plantillas personalizadas. Como práctica recomendada, haga una copia de seguridad de sus plantillas personalizadas periódicamente, de modo que si realiza un cambio que no pretendía, pueda revertir fácilmente a una versión anterior.

> [!IMPORTANT]
> Para usar PowerShell para crear y administrar plantillas de Azure Rights Management se necesita como mínimo la versión 2.0.0.0 del [módulo de Windows PowerShell para Azure RMS](https://go.microsoft.com/fwlink/?LinkId=257721).
> 
> Si ya ha instalado este módulo de PowerShell, ejecute el comando siguiente en una ventana de PowerShell para comprobar el número de versión: `(Get-Module aadrm -ListAvailable).Version`

Para obtener instrucciones de instalación, vea [Instalación del módulo de PowerShell para AADRM](install-powershell.md).

Los cmdlets que admite la creación y administración de plantillas:

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