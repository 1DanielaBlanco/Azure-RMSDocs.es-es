---
title: Clase mip CustomAction
description: Referencia de la clase mip CustomAction
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a94a41c0e7f7848201e2af44187cce2540579b27
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47444734"
---
# <a name="class-mipcustomaction"></a>clase mip::CustomAction 
[CustomAction](class_mip_customaction.md) es una clase de acción genérica que captura todas las subpropiedades de la acción como un contenedor de propiedades. El autor de llamada es responsable de entender el significado de la acción.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public const std::string& GetName() const  |  Obtenga el nombre de la acción.
public const std::vector<std::pair<std::string, std::string>>& GetProperties() const  |  Obtiene la lista de pares de clave-valor de propiedades.
 public ActionType GetType() const  |  Obtiene el tipo de [Acción](class_mip_action.md).
  
## <a name="members"></a>Miembros
  
### <a name="getname"></a>GetName
Obtenga el nombre de la acción.

  
**Devuelve**: un nombre de acción si ya existe uno; de lo contrario, una cadena vacía.
  
### <a name="getproperties"></a>GetProperties
Obtiene la lista de pares de clave-valor de propiedades.

  
**Devuelve**: una lista de pares de clave-valor.
  
### <a name="actiontype"></a>ActionType
Obtiene el tipo de [Acción](class_mip_action.md).

  
**Devuelve**: ActionType. El tipo de acción derivada a la que puede convertirse esta clase base.