---
title: clase mip::ApplyLabelAction
description: Documenta la clase mip::applylabelaction de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: ce813a544504ce18b382cdb86bd31d89b6626fad
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650500"
---
# <a name="class-mipapplylabelaction"></a>clase mip::ApplyLabelAction 
La aplicación de acciones de la etiqueta requiere que la aplicación que realiza la llamada aplique una etiqueta específica.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const std::string& GetLabelId() const  |  Obtiene el identificador de etiqueta necesario.
public const std::vector\<std::string\>& GetClassificationIds() const  |  Obtener los identificadores de clasificación que coincide y que produjo esta etiqueta que aparecerá.
public ActionType GetType() const  |  Obtiene el tipo de [Acción](class_mip_action.md).
  
## <a name="members"></a>Miembros
  
### <a name="getlabelid-function"></a>Función GetLabelId
Obtiene el identificador de etiqueta necesario.

  
**Devuelve**: El identificador de etiqueta.
  
### <a name="getclassificationids-function"></a>Función GetClassificationIds
Obtener los identificadores de clasificación que coincide y que produjo esta etiqueta que aparecerá.

  
**Devuelve**: Const std:: vector < std:: String > y una lista de clasificación de los identificadores que produjo esta etiqueta que aparecerá.
  
### <a name="gettype-function"></a>Función GetType
Obtiene el tipo de [Acción](class_mip_action.md).

  
**Devuelve**: ActionType El tipo de acción derivada a la que puede convertirse esta clase base.