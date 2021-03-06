---
title: clase mip::ServiceDisabledError
description: Documenta la clase mip::servicedisablederror de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: adcdb252fc6988f7047c2d940ddaa19fe8381405
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56256454"
---
# <a name="class-mipservicedisablederror"></a>clase mip::ServiceDisabledError 
El usuario no pudo obtener acceso al contenido debido a un servicio que se va a deshabilitar.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
GetExtent() de extensión pública const  |  Obtiene la extensión para el que el servicio está deshabilitado.
public char const* what() const  |  Obtiene el mensaje de error.
Public std:: shared_ptr\<Error\> Clone() const  |  Clona el error.
public virtual ErrorType GetErrorType() const  |  Obtiene el tipo de error.
public virtual const std::string& GetErrorName() const  |  Obtiene el nombre del error.
public virtual const std::string& GetMessage() const  |  Obtiene el mensaje de error.
public virtual void SetMessage(const std::string& msg)  |  Establece el mensaje de error.
Extensión de enum  |  Describe la extensión para el que el servicio está deshabilitado.
  
## <a name="members"></a>Miembros
  
### <a name="getextent-function"></a>Función GetExtent
Obtiene la extensión para el que el servicio está deshabilitado.

  
**Devuelve**: Extensión para el que el servicio está deshabilitado
  
### <a name="what-function"></a>¿Qué función
Obtiene el mensaje de error.

  
**Devuelve**: El mensaje de error
  
### <a name="clone-function"></a>Clone (función)
Clona el error.

  
**Devuelve**: Un clon del error.
  
### <a name="geterrortype-function"></a>Función GetErrorType
Obtiene el tipo de error.

  
**Devuelve**: El tipo de error.
  
### <a name="geterrorname-function"></a>Función GetErrorName
Obtiene el nombre del error.

  
**Devuelve**: El nombre del error.
  
### <a name="getmessage-function"></a>Función GetMessage
Obtiene el mensaje de error.

  
**Devuelve**: El mensaje de error.
  
### <a name="setmessage-function"></a>Función SetMessage
Establece el mensaje de error.

Parámetros:  
* **msg**: el mensaje de error.


  
### <a name="extent-enum"></a>Enumeración Extent
 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
Usuario            | Servicio está deshabilitado para el usuario.
Dispositivo            | Servicio está deshabilitado para el dispositivo.
Plataforma            | Servicio está deshabilitado para la plataforma.
Inquilino            | Servicio está deshabilitado para el inquilino.
Describe la extensión para el que el servicio está deshabilitado.
