---
title: Clase mip RecommendLabelAction
description: Referencia de la clase mip RecommendLabelAction
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: b8e56daed967523b7580087d7bb934c1b2164320
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446012"
---
# <a name="class-miprecommendlabelaction"></a>clase mip::RecommendLabelAction 
Las acciones de recomendación de etiquetas están pensadas para sugerir una etiqueta a los usuarios. La supresión de esta llamada después de que un usuario ignore la etiqueta recomendada debe realizarse a través de las acciones admitidas en el estado de ejecución.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public const std::string& GetLabelId() const  |  Obtiene el identificador de etiqueta sugerido.
 public ActionType GetType() const  |  Obtiene el tipo de [Acción](class_mip_action.md).
  
## <a name="members"></a>Miembros
  
### <a name="getlabelid"></a>GetLabelId
Obtiene el identificador de etiqueta sugerido.

  
**Devuelve**: el identificador de la etiqueta.
  
### <a name="actiontype"></a>ActionType
Obtiene el tipo de [Acción](class_mip_action.md).

  
**Devuelve**: ActionType. El tipo de acción derivada a la que puede convertirse esta clase base.