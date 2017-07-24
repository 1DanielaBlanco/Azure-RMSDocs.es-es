---
title: Add-AadrmKey
description: "Ayuda para Add-AadrmKey desde el módulo AADRM."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/18/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: A1C99424-D986-4A5A-B2E1-6D18EEF11B21
ms.reviewer: aashishr
ms.suite: ems
ms.openlocfilehash: 833cd9ea62b33c780eb40288784880962585cb38
ms.sourcegitcommit: 0fd2e63822280ec96ab957e22868c63de9ef3d47
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2017
---
# <a name="add-aadrmkey"></a>Add-AadrmKey

Este cmdlet ahora se quita de la versión más reciente del módulo de Azure Rights Management, porque el servicio Azure Rights Management utiliza el Azure Key Vault para las claves administradas por el cliente.

En su lugar, utilice [Use-AadrmKeyVaultKey](/powershell/module/aadrm/use-aadrmkeyvaultkey). Para más información, vea [Planeamiento e implementación de su clave de inquilino de Azure Information Protection](../plan-design/plan-implement-tenant-key.md).

Además, actualice su versión del módulo para que sea **2.9.0.0** o una versión posterior. Para obtener instrucciones, vea [Instalación de Windows PowerShell para Azure Rights Management](install-powershell.md).

