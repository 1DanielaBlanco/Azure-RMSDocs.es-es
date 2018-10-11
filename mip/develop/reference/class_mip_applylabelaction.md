---
title: Clase mip ApplyLabelAction
description: Referencia de la clase mip ApplyLabelAction
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 06a17ef1e60503cfb7d690bea9bb72316544f16d
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445774"
---
# <a name="class-mipapplylabelaction"></a>clase mip::ApplyLabelAction 
La aplicación de acciones de la etiqueta requiere que la aplicación que realiza la llamada aplique una etiqueta específica.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public const std::string& GetLabelId() const  |  Obtiene el identificador de etiqueta necesario.
 public ActionType GetType() const  |  Obtiene el tipo de [Acción](class_mip_action.md).
  
## <a name="members"></a>Miembros
  
### <a name="getlabelid"></a>GetLabelId
Obtiene el identificador de etiqueta necesario.

  
**Devuelve**: el identificador de la etiqueta.
  
### <a name="actiontype"></a>ActionType
Obtiene el tipo de [Acción](class_mip_action.md).

  
**Devuelve**: ActionType. El tipo de acción derivada a la que puede convertirse esta clase base.