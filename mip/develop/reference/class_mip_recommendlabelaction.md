---
title: clase mip::RecommendLabelAction
description: Documenta la clase mip::recommendlabelaction de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: ec1f82ab5951a5b7813fff2ebd5be6650a80203b
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651350"
---
# <a name="class-miprecommendlabelaction"></a>clase mip::RecommendLabelAction 
Las acciones de recomendación de etiquetas están pensadas para sugerir una etiqueta a los usuarios. La supresión de esta llamada después de que un usuario ignore la etiqueta recomendada debe realizarse a través de las acciones admitidas en el estado de ejecución.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const std::string& GetLabelId() const  |  Obtiene el identificador de etiqueta sugerido.
public const std::vector\<std::string\>& GetClassificationIds() const  |  Obtener los identificadores de clasificación que coincide y que produjo esta etiqueta que aparecerá.
public ActionType GetType() const  |  Obtiene el tipo de [Acción](class_mip_action.md).
  
## <a name="members"></a>Miembros
  
### <a name="getlabelid-function"></a>Función GetLabelId
Obtiene el identificador de etiqueta sugerido.

  
**Devuelve**: El identificador de etiqueta.
  
### <a name="getclassificationids-function"></a>Función GetClassificationIds
Obtener los identificadores de clasificación que coincide y que produjo esta etiqueta que aparecerá.

  
**Devuelve**: Const std:: vector < std:: String > y una lista de clasificación de los identificadores que produjo esta etiqueta que aparecerá.
  
### <a name="gettype-function"></a>Función GetType
Obtiene el tipo de [Acción](class_mip_action.md).

  
**Devuelve**: ActionType El tipo de acción derivada a la que puede convertirse esta clase base.