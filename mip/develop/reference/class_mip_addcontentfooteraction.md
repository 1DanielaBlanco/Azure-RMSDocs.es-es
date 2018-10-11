---
title: Clase mip AddContentFooterAction
description: Referencia de la clase mip AddContentFooterAction
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 73f641d965c3cf0236919557128af2ed07705672
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445842"
---
# <a name="class-mipaddcontentfooteraction"></a>clase mip::AddContentFooterAction 
Una clase de acción que especifica agregar un pie de página de contenido al documento.
  
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
  
### <a name="getuielementname"></a>GetUIElementName
Una API que se utiliza para marcar el elemento del pie de página de contenido.

  
**Devuelve**: el nombre que debe utilizarse para el elemento de la interfaz de usuario que contiene el pie de página de contenido. El mismo nombre se devolverá en [RemoveContentFooterAction](class_mip_removecontentfooteraction.md) en caso de que sea necesario quitar el pie de página de contenido.
  
### <a name="gettext"></a>GetText
Obtiene el texto que está pensado para ir en el pie de página de contenido.

  
**Devuelve**: texto de pie de página de contenido.
  
### <a name="getfontname"></a>GetFontName
Obtiene el nombre de la fuente utilizada para mostrar el pie de página de contenido.

  
**Devuelve**: nombre de la fuente. El valor predeterminado es Calibri si la directiva no establece nada.
  
### <a name="getfontsize"></a>GetFontSize
Obtiene el tamaño de la fuente utilizada para mostrar el pie de página de contenido.

  
**Devuelve**: tamaño de fuente como un entero.
  
### <a name="getfontcolor"></a>GetFontColor
Obtiene el color de la fuente utilizada para mostrar el pie de página de contenido.

  
**Devuelve**: color de fuente como una cadena (por ejemplo, "#000000").
  
### <a name="getalignment"></a>GetAlignment
Obtiene la alineación del pie de página.

  
**Devuelve**: el enumerador ContentMarkAlignment: LEFT|RIGHT|CENTER. 
  
**Consulte también**: ContentMarkAlignment
  
### <a name="getmargin"></a>GetMargin
Obtiene el margen del pie de página de la parte inferior.

  
**Devuelve**: un número entero que representa los márgenes desde la parte inferior del documento (por ejemplo, 10 mm).
  
### <a name="actiontype"></a>ActionType
Obtiene el tipo de [Acción](class_mip_action.md).

  
**Devuelve**: ActionType. El tipo de acción derivada a la que puede convertirse esta clase base.