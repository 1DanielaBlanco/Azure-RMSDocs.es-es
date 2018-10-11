---
title: Clase mip Label
description: Referencia de la clase mip Label
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 2a80748430df83a16a4d5ee716344d17ce7deee4
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446284"
---
# <a name="class-miplabel"></a>clase mip::Label 
Abstracción para una única etiqueta de Microsoft Information Protection.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public const std::string& GetId() const  |  Obtiene el identificador de la etiqueta.
 public const std::string& GetName() const  |  Obtiene el nombre de la etiqueta.
 public const std::string& GetDescription() const  |  Obtiene la descripción de la etiqueta.
 public const std::string& GetColor() const  |  Obtiene el color que debe mostrar la etiqueta.
 public int GetSensitivity() const  |  Obtiene la confidencialidad de la etiqueta.
 public const std::string& GetTooltip() const  |  Obtiene la descripción de la información sobre herramientas de la etiqueta.
 public bool IsActive() const  |  Obtiene un valor booleano de señalización si la etiqueta está activa.
public std::weak_ptr<Label> GetParent() const  |  Obtiene la etiqueta principal.
public const std::vector<std::shared_ptr<Label>>& GetChildren() const  |  Obtiene los elementos secundarios de la etiqueta actual.
  
## <a name="members"></a>Miembros
  
### <a name="getid"></a>GetId
Obtiene el identificador de la etiqueta.

  
**Devuelve**: el identificador de la etiqueta.
  
### <a name="getname"></a>GetName
Obtiene el nombre de la etiqueta.

  
**Devuelve**: el nombre de la etiqueta.
  
### <a name="getdescription"></a>GetDescription
Obtiene la descripción de la etiqueta.

  
**Devuelve**: la descripción de la etiqueta.
  
### <a name="getcolor"></a>GetColor
Obtiene el color que debe mostrar la etiqueta.

  
**Devuelve**: color value Formato de la cadena. "#RRGGBB" donde cada RR, GG, BB es un valor hexadecimal 0-f.
  
### <a name="getsensitivity"></a>GetSensitivity
Obtiene la confidencialidad de la etiqueta.

  
**Devuelve**: un valor numérico. Un valor más alto define una confidencialidad más alta.
  
### <a name="gettooltip"></a>GetTooltip
Obtiene la descripción de la información sobre herramientas de la etiqueta.

  
**Devuelve**: una cadena de información sobre herramientas.
  
### <a name="isactive"></a>IsActive
Obtiene un valor booleano de señalización si la etiqueta está activa.
Solo se pueden aplicar etiquetas activas. Las etiquetas inactivas no se puede aplicar y se usan solo con fines de visualización. 

  
**Devuelve**: true si la etiqueta está activa; de lo contrario, false.
  
### <a name="label"></a>Etiqueta
Obtiene la etiqueta principal.

  
**Devuelve**: un puntero débil a la etiqueta principal si existe; de lo contrario, un puntero vacío.
  
### <a name="label"></a>Etiqueta
Obtiene los elementos secundarios de la etiqueta actual.

  
**Devuelve**: un vector de punteros compartidos a las etiquetas.