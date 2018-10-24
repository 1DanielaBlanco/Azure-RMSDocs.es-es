---
title: clase mip MetadataAction
description: Referencia de la clase mip MetadataAction
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 8f7480775a0226c7161c9ad770184e54427a5084
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47444626"
---
# <a name="class-mipmetadataaction"></a>clase mip::MetadataAction 
Una [acción](class_mip_action.md) que agrega información de metadatos al contenido.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const std::vector<std::string>& GetMetadataToRemove() const  |  Obtiene la lista de nombres de metadatos que tienen que quitarse del contenido.
public const std::vector<std::pair<std::string, std::string>>& GetMetadataToAdd() const  |  Obtiene los pares de nombre y valor de metadatos que tendrán que agregarse al contenido.
 public ActionType GetType() const  |  Obtiene el tipo de [Acción](class_mip_action.md).
  
## <a name="members"></a>Miembros
  
### <a name="getmetadatatoremove"></a>GetMetadataToRemove
Obtiene la lista de nombres de metadatos que tienen que quitarse del contenido.

  
**Devuelve**: un vector de cadenas para quitar. La eliminación de metadatos tiene que realizarse antes de agregar los metadatos.
  
### <a name="getmetadatatoadd"></a>GetMetadataToAdd
Obtiene los pares de nombre y valor de metadatos que tendrán que agregarse al contenido.

  
**Devuelve**: Const std::vector<std::pair<std::string, std::string>>& es necesario quitar metadatos antes de agregar metadatos.
  
### <a name="actiontype"></a>ActionType
Obtiene el tipo de [Acción](class_mip_action.md).

  
**Devuelve**: ActionType. El tipo de acción derivada a la que puede convertirse esta clase base.