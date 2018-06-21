---
title: Add-AadrmKey
description: Ayuda para Add-AadrmKey desde el módulo AADRM.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/18/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: A1C99424-D986-4A5A-B2E1-6D18EEF11B21
ms.reviewer: aashishr
ms.suite: ems
ms.openlocfilehash: a75b67f72410170500bf9ad3b93bdd6165c5af2d
ms.sourcegitcommit: 31c79d948ec3089a4dc65639f1842c07c7aecba6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/20/2018
ms.locfileid: "29371141"
---
# <a name="add-aadrmkey"></a>Add-AadrmKey

Este cmdlet ahora se quita de la versión más reciente del módulo de Azure Rights Management, porque el servicio Azure Rights Management utiliza el Azure Key Vault para las claves administradas por el cliente.

En su lugar, utilice [Use-AadrmKeyVaultKey](/powershell/module/aadrm/use-aadrmkeyvaultkey). Para más información, vea [Planeamiento e implementación de su clave de inquilino de Azure Information Protection](../plan-design/plan-implement-tenant-key.md).

Además, actualice su versión del módulo para que sea **2.9.0.0** o una versión posterior. Para obtener instrucciones, vea [Instalación del módulo de PowerShell para AADRM](install-powershell.md).

