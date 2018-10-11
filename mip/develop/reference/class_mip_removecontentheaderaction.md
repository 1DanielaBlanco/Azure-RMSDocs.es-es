---
title: Clase mip RemoveContentHeaderAction
description: Referencia de la clase mip RemoveContentHeaderAction
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: dc79ebf5d5c7cd35a8fc5ed854315179ed9190f0
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446454"
---
# <a name="class-mipremovecontentheaderaction"></a>clase mip::RemoveContentHeaderAction 
Una clase de acción que especifica quitar el encabezado de contenido del documento.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const std::vector<std::string>& GetUIElementNames()  |  Obtiene una lista de nombres que se debe usar para buscar los elementos de interfaz de usuario que deben quitarse.
 public ActionType GetType() const  |  Obtiene el tipo de [Acción](class_mip_action.md).
  
## <a name="members"></a>Miembros
  
### <a name="getuielementnames"></a>GetUIElementNames
Obtiene una lista de nombres que se debe usar para buscar los elementos de interfaz de usuario que deben quitarse.

  
**Devuelve**: una lista de nombres de elementos de interfaz de usuario.
  
### <a name="actiontype"></a>ActionType
Obtiene el tipo de [Acción](class_mip_action.md).

  
**Devuelve**: ActionType. El tipo de acción derivada a la que puede convertirse esta clase base.