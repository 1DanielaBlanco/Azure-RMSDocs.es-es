---
# required metadata

title: Referencia de PowerShell para plantillas personalizadas | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---



# Referencia de PowerShell para plantillas personalizadas

*Se aplica a: Azure Rights Management, Office 365*

Todo lo que puede hacer en el Portal de Azure clásico para crear y administrar plantillas puede hacerlo desde la línea de comandos, mediante PowerShell. Además, puede exportar e importar plantillas, de manera que pueda copiar plantillas entre inquilinos o llevar a cabo ediciones en masa de propiedades complejas en plantillas, como descripciones y nombres multilingües.

También puede utilizar la exportación e importación para restaurar y hacer una copia de seguridad de sus plantillas personalizadas. Como práctica recomendada, haga una copia de seguridad de sus plantillas personalizadas periódicamente, de modo que si realiza un cambio que no pretendía, pueda revertir fácilmente a una versión anterior.

> [!IMPORTANT] Para usar Windows PowerShell para crear y administrar plantillas de directiva de permisos de Azure RMS, debe tener al menos la versión 2.0.0.0 del [módulo de Windows PowerShell para Azure RMS](http://go.microsoft.com/fwlink/?LinkId=257721).
> 
> Si ya instaló este módulo de PowerShell, ejecute el comando siguiente en una ventana de PowerShell para comprobar el número de versión: `(Get-Module aadrm -ListAvailable).Version`

Para obtener instrucciones de instalación, consulte [Instalación de Windows PowerShell para Azure Rights Management](install-powershell.md).

Los cmdlets que admite la creación y administración de plantillas:

-   [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx)

-   [Expot-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx)

-   [Get-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727079.aspx)

-   [Get-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727081.aspx)

-   [Impot-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx)

-   [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx)

-   [Remove-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727082.aspx)

-   [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx)



## Véase también
[Configuración de plantillas personalizadas para Azure Rights Management](configure-custom-templates.md)

<!--HONumber=May16_HO3-->


