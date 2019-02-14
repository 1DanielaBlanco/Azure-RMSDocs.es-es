---
title: clase mip::ApplyLabelAction
description: Documenta la clase mip::applylabelaction de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 58dfc0716d4c6f590a9b560f737531740fee071d
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56258120"
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
