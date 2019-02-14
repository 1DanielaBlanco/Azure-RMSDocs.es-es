---
title: clase mip::AddContentHeaderAction
description: 'Documenta la clase MIP:: addcontentheaderaction de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: ab4ce12c9a11c0e2319bcf2b337b6a6f0f7f9f0e
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56256777"
---
# <a name="class-mipaddcontentheaderaction"></a>clase mip::AddContentHeaderAction 
Una clase de acción que especifica agregar un encabezado de contenido.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  Una API que se utiliza para marcar el elemento del encabezado de contenido.
public const std::string& GetText() const  |  Obtiene el texto que está pensado para ir en el encabezado de contenido.
public const std::string& GetFontName() const  |  Obtiene el nombre de la fuente utilizada para mostrar el encabezado de contenido.
public int GetFontSize() const  |  Obtiene el tamaño de la fuente utilizada para mostrar el encabezado de contenido.
public const std::string& GetFontColor() const  |  Obtiene el color de la fuente utilizada para mostrar el encabezado de contenido.
public ContentMarkAlignment GetAlignment() const  |  Obtiene la alineación del encabezado.
public int GetMargin() const  |  Obtiene el margen del encabezado de la parte inferior.
public ActionType GetType() const  |  Obtiene el tipo de [Acción](class_mip_action.md).
  
## <a name="members"></a>Miembros
  
### <a name="getuielementname-function"></a>Función GetUIElementName
Una API que se utiliza para marcar el elemento del encabezado de contenido.

  
**Devuelve**: El nombre que se debe usar para el elemento de interfaz de usuario que contiene el encabezado de contenido. El mismo nombre se devolverá en [RemoveContentHeaderAction](class_mip_removecontentheaderaction.md) en caso de que sea necesario quitar el encabezado de contenido.
  
### <a name="gettext-function"></a>GetText (función)
Obtiene el texto que está pensado para ir en el encabezado de contenido.

  
**Devuelve**: Texto de encabezado de contenido.
  
### <a name="getfontname-function"></a>Función GetFontName
Obtiene el nombre de la fuente utilizada para mostrar el encabezado de contenido.

  
**Devuelve**: Nombre de la fuente. El valor predeterminado es Calibri si la directiva no establece nada.
  
### <a name="getfontsize-function"></a>Función GetFontSize
Obtiene el tamaño de la fuente utilizada para mostrar el encabezado de contenido.

  
**Devuelve**: Tamaño de fuente como un entero.
  
### <a name="getfontcolor-function"></a>Función GetFontColor
Obtiene el color de la fuente utilizada para mostrar el encabezado de contenido.

  
**Devuelve**: Color de fuente como una cadena (por ejemplo, #000000 ").
  
### <a name="getalignment-function"></a>Función GetAlignment
Obtiene la alineación del encabezado.

  
**Devuelve**: El enumerador ContentMarkAlignment: IZQUIERDA | DERECHA | CENTRO. 
  
**Vea también**: [ContentMarkAlignment](mip-enums-and-structs.md#contentmarkalignment-enum)
  
### <a name="getmargin-function"></a>Función GetMargin
Obtiene el margen del encabezado de la parte inferior.

  
**Devuelve**: Los márgenes de la parte inferior del documento (por ejemplo, 10 mm).
  
### <a name="gettype-function"></a>Función GetType
Obtiene el tipo de [Acción](class_mip_action.md).

  
**Devuelve**: ActionType El tipo de acción derivada a la que puede convertirse esta clase base.
