---
title: clase mip::ProtectByTemplateAction
description: 'Documenta la clase MIP:: protectbytemplateaction de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 9c7114bcceceef537675ca04499cdb1710456b82
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56252374"
---
# <a name="class-mipprotectbytemplateaction"></a>clase mip::ProtectByTemplateAction 
Clase de acción que especifica que se agregue la protección por plantilla al documento.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const std::string& GetTemplateId() const  |  Obtiene el identificador de plantilla de protección asociado a la acción.
public ActionType GetType() const  |  Obtiene el tipo de [Acción](class_mip_action.md).
  
## <a name="members"></a>Miembros
  
### <a name="gettemplateid-function"></a>Función GetTemplateId
Obtiene el identificador de plantilla de protección asociado a la acción.

  
**Devuelve**: El identificador de plantilla de protección.
  
### <a name="gettype-function"></a>Función GetType
Obtiene el tipo de [Acción](class_mip_action.md).

  
**Devuelve**: ActionType El tipo de acción derivada a la que puede convertirse esta clase base.
