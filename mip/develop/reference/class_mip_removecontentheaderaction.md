---
title: clase mip::RemoveContentHeaderAction
description: 'Documenta la clase MIP:: removecontentheaderaction de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 5025b35d9c8edd7e01a6799bd5b08a8703784086
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259253"
---
# <a name="class-mipremovecontentheaderaction"></a>clase mip::RemoveContentHeaderAction 
Clase de acción que especifica que se quite el encabezado de contenido del documento.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const std::vector\<std::string\>& GetUIElementNames()  |  Obtiene una lista de nombres que se debe usar para buscar los elementos de interfaz de usuario que deben quitarse.
public ActionType GetType() const  |  Obtiene el tipo de [Acción](class_mip_action.md).
  
## <a name="members"></a>Miembros
  
### <a name="getuielementnames-function"></a>Función GetUIElementNames
Obtiene una lista de nombres que se debe usar para buscar los elementos de interfaz de usuario que deben quitarse.

  
**Devuelve**: Una lista de nombres de elemento de interfaz de usuario.
  
### <a name="gettype-function"></a>Función GetType
Obtiene el tipo de [Acción](class_mip_action.md).

  
**Devuelve**: ActionType El tipo de acción derivada a la que puede convertirse esta clase base.
