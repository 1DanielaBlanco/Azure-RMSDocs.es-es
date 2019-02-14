---
title: clase mip::MetadataAction
description: 'Documenta la clase MIP:: metadataaction de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 190bccc23ecb5c03faa0ab6748caf8fc206e265f
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56256998"
---
# <a name="class-mipmetadataaction"></a>clase mip::MetadataAction 
Una [acción](class_mip_action.md) que agrega información de metadatos al contenido.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const std::vector\<std::string\>& GetMetadataToRemove() const  |  Obtiene la lista de nombres de metadatos que tienen que quitarse del contenido.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetMetadataToAdd() const  |  Obtiene los pares de nombre y valor de metadatos que tendrán que agregarse al contenido.
public ActionType GetType() const  |  Obtiene el tipo de [Acción](class_mip_action.md).
  
## <a name="members"></a>Miembros
  
### <a name="getmetadatatoremove-function"></a>Función GetMetadataToRemove
Obtiene la lista de nombres de metadatos que tienen que quitarse del contenido.

  
**Devuelve**: Un vector de cadenas para quitar. La eliminación de metadatos tiene que realizarse antes de agregar los metadatos.
  
### <a name="getmetadatatoadd-function"></a>Función GetMetadataToAdd
Obtiene los pares de nombre y valor de metadatos que tendrán que agregarse al contenido.

  
**Devuelve**: Const std:: vector < std:: Pair < std:: String, std:: String >> & quitar metadatos deben realizarse antes de agregar los metadatos.
  
### <a name="gettype-function"></a>Función GetType
Obtiene el tipo de [Acción](class_mip_action.md).

  
**Devuelve**: ActionType El tipo de acción derivada a la que puede convertirse esta clase base.
