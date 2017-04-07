---
title: PowerShell para plantillas personalizadas de Azure RMS - AIP
description: "Todo lo que puede hacer en el Portal de Azure clásico para crear y administrar plantillas de administración de derechos también puede hacerlo desde la línea de comandos con PowerShell. Además, puede exportar e importar plantillas, de manera que pueda copiar plantillas entre inquilinos o llevar a cabo ediciones en masa de propiedades complejas en plantillas, como descripciones y nombres multilingües."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 40db2ba3856cab24f0162a1b46960816b85a5089
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="powershell-reference-for-custom-templates"></a>Referencia de PowerShell para plantillas personalizadas

>*Se aplica a: Azure Information Protection, Office 365*

Todo lo que puede hacer en el Portal de Azure clásico para crear y administrar plantillas de administración de derechos también puede hacerlo desde la línea de comandos con PowerShell. Además, puede exportar e importar plantillas, de manera que pueda copiar plantillas entre inquilinos o llevar a cabo ediciones en masa de propiedades complejas en plantillas, como descripciones y nombres multilingües.

También puede utilizar la exportación e importación para restaurar y hacer una copia de seguridad de sus plantillas personalizadas. Como práctica recomendada, haga una copia de seguridad de sus plantillas personalizadas periódicamente, de modo que si realiza un cambio que no pretendía, pueda revertir fácilmente a una versión anterior.

> [!IMPORTANT]
> Para usar Windows PowerShell para crear y administrar plantillas de Azure Rights Management se necesita como mínimo la versión 2.0.0.0 del [módulo de Windows PowerShell para Azure RMS](http://go.microsoft.com/fwlink/?LinkId=257721).
> 
> Si ya ha instalado este módulo de PowerShell, ejecute el comando siguiente en una ventana de PowerShell para comprobar el número de versión: `(Get-Module aadrm -ListAvailable).Version`

Para obtener instrucciones de instalación, consulte [Instalación de Windows PowerShell para Azure Rights Management](install-powershell.md).

Los cmdlets que admite la creación y administración de plantillas:

-   [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx)

-   [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx)

-   [Get-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727079.aspx)

-   [Get-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727081.aspx)

-   [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx)

-   [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx)

-   [Remove-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727082.aspx)

-   [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx)



## <a name="see-also"></a>Véase también
[Configuración de plantillas personalizadas para Azure Rights Management](configure-custom-templates.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]