---
title: Add-AadrmKey
description: Ayuda para Add-AadrmKey desde el módulo AADRM.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/18/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: A1C99424-D986-4A5A-B2E1-6D18EEF11B21
ms.reviewer: aashishr
ms.suite: ems
ms.openlocfilehash: 98ac49ffac2dcf4baadb961247e3e3447e2d128c
ms.sourcegitcommit: 26a2c1becdf3e3145dc1168f5ea8492f2e1ff2f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2018
ms.locfileid: "44147294"
---
# <a name="add-aadrmkey"></a>Add-AadrmKey

Este cmdlet ahora se quita de la versión más reciente del módulo de Azure Rights Management, porque el servicio Azure Rights Management utiliza el Azure Key Vault para las claves administradas por el cliente.

En su lugar, utilice [Use-AadrmKeyVaultKey](/powershell/module/aadrm/use-aadrmkeyvaultkey). Para más información, vea [Planeamiento e implementación de su clave de inquilino de Azure Information Protection](plan-implement-tenant-key.md).

Además, actualice su versión del módulo para que sea **2.9.0.0** o una versión posterior. Para obtener instrucciones, vea [Instalación del módulo de PowerShell para AADRM](install-powershell.md).

