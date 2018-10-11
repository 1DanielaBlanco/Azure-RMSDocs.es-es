---
title: Clase mip AddWatermarkAction
description: Referencia de la clase mip AddWatermarkAction
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: f49bd7aa16ae12aef240d05fff6acf507ddc341d
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446097"
---
# <a name="class-mipaddwatermarkaction"></a>clase mip::AddWatermarkAction 
Una clase de acción que especifica agregar una marca de agua.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public const std::string& GetUIElementName()  |  Una API que se utiliza para marcar el elemento de marca de agua.
 public WatermarkLayout GetLayout() const  |  Una API que se utiliza para obtener el diseño de la marca de agua.
 public const std::string& GetText() const  |  Obtiene el texto que está pensado para ir en la marca de agua.
 public const std::string& GetFontName() const  |  Obtiene el nombre de la fuente utilizada para mostrar la marca de agua.
 public int GetFontSize() const  |  Obtiene el tamaño de la fuente utilizada para mostrar la marca de agua.
 public const std::string& GetFontColor() const  |  Obtiene el color de la fuente utilizada para mostrar la marca de agua.
 public ActionType GetType() const  |  Obtiene el tipo de [Acción](class_mip_action.md).
  
## <a name="members"></a>Miembros
  
### <a name="getuielementname"></a>GetUIElementName
Una API que se utiliza para marcar el elemento de marca de agua.

  
**Devuelve**: el nombre que debe utilizarse para el elemento de la interfaz de usuario que contiene la marca de agua. El mismo nombre se devolverá en RemoveWatermarkingAction en caso de que sea necesario quitar la marca de agua.
  
### <a name="getlayout"></a>GetLayout
Una API que se utiliza para obtener el diseño de la marca de agua.

  
**Devuelve**: WatermarkLayout. El diseño de la marca de agua en forma de enumeración HORIZONTAL|DIAGONAL. ,
  
### <a name="gettext"></a>GetText
Obtiene el texto que está pensado para ir en la marca de agua.

  
**Devuelve**: texto de encabezado de contenido.
  
### <a name="getfontname"></a>GetFontName
Obtiene el nombre de la fuente utilizada para mostrar la marca de agua.

  
**Devuelve**: nombre de la fuente. El valor predeterminado es Calibri si la directiva no establece nada.
  
### <a name="getfontsize"></a>GetFontSize
Obtiene el tamaño de la fuente utilizada para mostrar la marca de agua.

  
**Devuelve**: tamaño de fuente como un entero.
  
### <a name="getfontcolor"></a>GetFontColor
Obtiene el color de la fuente utilizada para mostrar la marca de agua.

  
**Devuelve**: color de fuente como una cadena (por ejemplo, "#000000").
  
### <a name="actiontype"></a>ActionType
Obtiene el tipo de [Acción](class_mip_action.md).

  
**Devuelve**: ActionType. El tipo de acción derivada a la que puede convertirse esta clase base.