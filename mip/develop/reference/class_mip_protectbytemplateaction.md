---
title: Clase mip ProtectByTemplateAction
description: Referencia de la clase mip ProtectByTemplateAction
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: cb5f42b25e6f499bc09f3f460ec4a253627b45a5
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445468"
---
# <a name="class-mipprotectbytemplateaction"></a>clase mip::ProtectByTemplateAction 
Una clase de acción que especifica agregar la protección por plantilla al documento.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public const std::string& GetTemplateId() const  |  Obtiene el identificador de plantilla de protección asociado a la acción.
 public ActionType GetType() const  |  Obtiene el tipo de [Acción](class_mip_action.md).
  
## <a name="members"></a>Miembros
  
### <a name="gettemplateid"></a>GetTemplateId
Obtiene el identificador de plantilla de protección asociado a la acción.

  
**Devuelve**: obtiene el identificador de la plantilla de protección.
  
### <a name="actiontype"></a>ActionType
Obtiene el tipo de [Acción](class_mip_action.md).

  
**Devuelve**: ActionType. El tipo de acción derivada a la que puede convertirse esta clase base.