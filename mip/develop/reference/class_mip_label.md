---
title: clase mip::Label
description: 'Documenta la clase MIP:: Label de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 5a2444ab0abd944418a8d55eae35c5f6023282f7
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56253251"
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
pública std::weak_ptr\<etiqueta\> getParent (constante)  |  Obtiene la etiqueta principal.
Public const std:: vector\<std:: shared_ptr\<etiqueta\>\>& GetChildren() const  |  Obtiene los elementos secundarios de la etiqueta actual.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  Obtener la configuración de una etiqueta personalizada.
  
## <a name="members"></a>Miembros
  
### <a name="getid-function"></a>GetId (función)
Obtiene el identificador de la etiqueta.

  
**Devuelve**: El identificador de etiqueta.
  
### <a name="getname-function"></a>Función GetName
Obtiene el nombre de la etiqueta.

  
**Devuelve**: El nombre de etiqueta.
  
### <a name="getdescription-function"></a>GetDescription (función)
Obtiene la descripción de la etiqueta.

  
**Devuelve**: La descripción de la etiqueta.
  
### <a name="getcolor-function"></a>GetColor (función)
Obtiene el color que debe mostrar la etiqueta.

  
**Devuelve**: El formato de cadena del valor de color. "#RRGGBB" donde cada RR, GG, BB es un valor hexadecimal 0-f.
  
### <a name="getsensitivity-function"></a>Función GetSensitivity
Obtiene la confidencialidad de la etiqueta.

  
**Devuelve**: Un valor numérico. Un valor más alto define una confidencialidad más alta.
  
### <a name="gettooltip-function"></a>Función GetTooltip
Obtiene la descripción de la información sobre herramientas de la etiqueta.

  
**Devuelve**: Una cadena de información sobre herramientas.
  
### <a name="isactive-function"></a>IsActive (función)
Obtiene un valor booleano de señalización si la etiqueta está activa.
Solo se pueden aplicar etiquetas activas. Las etiquetas inactivas no se puede aplicar y se usan solo con fines de visualización. 

  
**Devuelve**: True si la etiqueta está activo, de lo contrario, false.
  
### <a name="getparent-function"></a>GetParent (función)
Obtiene la etiqueta principal.

  
**Devuelve**: Etiqueta de un puntero débil al elemento primario si existe otro puntero vacío.
  
### <a name="getchildren-function"></a>GetChildren (función)
Obtiene los elementos secundarios de la etiqueta actual.

  
**Devuelve**: Un vector de punteros compartidos a las etiquetas.
  
### <a name="getcustomsettings-function"></a>Función GetCustomSettings
Obtener la configuración de una etiqueta personalizada.

  
**Devuelve**: Un vector de pares clave / valor que representa la configuración personalizada.
