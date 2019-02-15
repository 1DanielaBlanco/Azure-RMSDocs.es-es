---
title: Add-AadrmKey
description: Ayuda para Add-AadrmKey desde el módulo AADRM.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/19/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: A1C99424-D986-4A5A-B2E1-6D18EEF11B21
ms.reviewer: aashishr
ms.suite: ems
ms.openlocfilehash: e61bf5fab8aeed01e200b5238d3d4756293a0cea
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56258290"
---
# <a name="add-aadrmkey"></a>Add-AadrmKey

Este cmdlet ahora se quita de la versión más reciente del módulo de Azure Rights Management, porque el servicio Azure Rights Management utiliza el Azure Key Vault para las claves administradas por el cliente.

En su lugar, utilice [Use-AadrmKeyVaultKey](/powershell/module/aadrm/use-aadrmkeyvaultkey). Para más información, vea [Planeamiento e implementación de su clave de inquilino de Azure Information Protection](plan-implement-tenant-key.md).

Además, actualice su versión del módulo para que sea **2.9.0.0** o una versión posterior. Para obtener instrucciones, vea [Instalación del módulo de PowerShell para AADRM](install-powershell.md).

