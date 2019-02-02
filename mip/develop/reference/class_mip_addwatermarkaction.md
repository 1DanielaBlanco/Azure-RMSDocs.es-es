---
title: clase mip::AddWatermarkAction
description: 'Documenta la clase MIP:: addwatermarkaction de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: d9a2049238e2b45f1c19265ed2f940b3fea079e6
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650840"
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
  
### <a name="getuielementname-function"></a>Función GetUIElementName
Una API que se utiliza para marcar el elemento de marca de agua.

  
**Devuelve**: El nombre que se debe usar para el elemento de interfaz de usuario que contiene la marca de agua. El mismo nombre se devolverá en RemoveWatermarkingAction en caso de que sea necesario quitar la marca de agua.
  
### <a name="getlayout-function"></a>Función GetLayout
Una API que se utiliza para obtener el diseño de la marca de agua.

  
**Devuelve**: WatermarkLayout El diseño de la marca de agua en forma de enumeración HORIZONTAL|DIAGONAL. ,
  
### <a name="gettext-function"></a>GetText (función)
Obtiene el texto que está pensado para ir en la marca de agua.

  
**Devuelve**: Texto de encabezado de contenido.
  
### <a name="getfontname-function"></a>Función GetFontName
Obtiene el nombre de la fuente utilizada para mostrar la marca de agua.

  
**Devuelve**: Nombre de la fuente. El valor predeterminado es Calibri si la directiva no establece nada.
  
### <a name="getfontsize-function"></a>Función GetFontSize
Obtiene el tamaño de la fuente utilizada para mostrar la marca de agua.

  
**Devuelve**: Tamaño de fuente como un entero.
  
### <a name="getfontcolor-function"></a>Función GetFontColor
Obtiene el color de la fuente utilizada para mostrar la marca de agua.

  
**Devuelve**: Color de fuente como una cadena (por ejemplo, "#000000").
  
### <a name="gettype-function"></a>Función GetType
Obtiene el tipo de [Acción](class_mip_action.md).

  
**Devuelve**: ActionType El tipo de acción derivada a la que puede convertirse esta clase base.