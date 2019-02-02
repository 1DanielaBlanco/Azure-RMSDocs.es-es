---
title: clase mip::CustomAction
description: 'Documenta la clase MIP:: CustomAction de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 49840aebf5d49e91671145d0c5dc9e3b6d8e4694
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650653"
---
# <a name="class-mipcustomaction"></a>clase mip::CustomAction 
[CustomAction](class_mip_customaction.md) es una clase de acción genérica que captura todas las subpropiedades de la acción como un contenedor de propiedades. El autor de llamada es responsable de entender el significado de la acción.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  Obtenga el nombre de la acción.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetProperties() const  |  Obtiene la lista de pares de clave-valor de propiedades.
public ActionType GetType() const  |  Obtiene el tipo de [Acción](class_mip_action.md).
  
## <a name="members"></a>Miembros
  
### <a name="getname-function"></a>Función GetName
Obtenga el nombre de la acción.

  
**Devuelve**: Un nombre de acción, si existe otro una cadena vacía.
  
### <a name="getproperties-function"></a>GetProperties (función)
Obtiene la lista de pares de clave-valor de propiedades.

  
**Devuelve**: Una lista de pares clave-valor.
  
### <a name="gettype-function"></a>Función GetType
Obtiene el tipo de [Acción](class_mip_action.md).

  
**Devuelve**: ActionType El tipo de acción derivada a la que puede convertirse esta clase base.