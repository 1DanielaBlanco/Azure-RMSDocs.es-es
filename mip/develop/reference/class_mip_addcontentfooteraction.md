---
title: clase mip::AddContentFooterAction
description: 'Documenta la clase MIP:: addcontentfooteraction de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 28f9deb9460c88174f10c9a26c60f51407457b90
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56254040"
---
# <a name="class-mipaddcontentfooteraction"></a>clase mip::AddContentFooterAction 
Clase de acción que especifica que se agregue un pie de página de contenido al documento.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  Una API que se utiliza para marcar el elemento del pie de página de contenido.
public const std::string& GetText() const  |  Obtiene el texto que está pensado para ir en el pie de página de contenido.
public const std::string& GetFontName() const  |  Obtiene el nombre de la fuente utilizada para mostrar el pie de página de contenido.
public int GetFontSize() const  |  Obtiene el tamaño de la fuente utilizada para mostrar el pie de página de contenido.
public const std::string& GetFontColor() const  |  Obtiene el color de la fuente utilizada para mostrar el pie de página de contenido.
public ContentMarkAlignment GetAlignment() const  |  Obtiene la alineación del pie de página.
public int GetMargin() const  |  Obtiene el margen del pie de página de la parte inferior.
public ActionType GetType() const  |  Obtiene el tipo de [Acción](class_mip_action.md).
  
## <a name="members"></a>Miembros
  
### <a name="getuielementname-function"></a>Función GetUIElementName
Una API que se utiliza para marcar el elemento del pie de página de contenido.

  
**Devuelve**: El nombre que se debe usar para el elemento de interfaz de usuario que contiene el pie de página de contenido. El mismo nombre se devolverá en [RemoveContentFooterAction](class_mip_removecontentfooteraction.md) en caso de que sea necesario quitar el pie de página de contenido.
  
### <a name="gettext-function"></a>GetText (función)
Obtiene el texto que está pensado para ir en el pie de página de contenido.

  
**Devuelve**: Texto de pie de página de contenido.
  
### <a name="getfontname-function"></a>Función GetFontName
Obtiene el nombre de la fuente utilizada para mostrar el pie de página de contenido.

  
**Devuelve**: Nombre de la fuente. El valor predeterminado es Calibri si la directiva no establece nada.
  
### <a name="getfontsize-function"></a>Función GetFontSize
Obtiene el tamaño de la fuente utilizada para mostrar el pie de página de contenido.

  
**Devuelve**: Tamaño de fuente como un entero.
  
### <a name="getfontcolor-function"></a>Función GetFontColor
Obtiene el color de la fuente utilizada para mostrar el pie de página de contenido.

  
**Devuelve**: Color de fuente como una cadena (por ejemplo, "#000000").
  
### <a name="getalignment-function"></a>Función GetAlignment
Obtiene la alineación del pie de página.

  
**Devuelve**: El enumerador ContentMarkAlignment: IZQUIERDA | DERECHA | CENTRO. 
  
**Vea también**: [ContentMarkAlignment](mip-enums-and-structs.md#contentmarkalignment-enum)
  
### <a name="getmargin-function"></a>Función GetMargin
Obtiene el margen del pie de página de la parte inferior.

  
**Devuelve**: Los márgenes de la parte inferior del documento (por ejemplo, 10 mm).
  
### <a name="gettype-function"></a>Función GetType
Obtiene el tipo de [Acción](class_mip_action.md).

  
**Devuelve**: ActionType El tipo de acción derivada a la que puede convertirse esta clase base.
