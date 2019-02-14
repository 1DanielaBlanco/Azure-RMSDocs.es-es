---
title: clase mip::FileIOError
description: 'Documenta la clase MIP:: fileioerror de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 28e67ec1f267ac134fff2cec18a638c9eb1c1eff
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56252969"
---
# <a name="class-mipfileioerror"></a>clase mip::FileIOError 
Error de E/S de archivo.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public char const* what() const  |  Obtiene el mensaje de error.
Public std:: shared_ptr\<Error\> Clone() const  |  Clona el error.
public virtual ErrorType GetErrorType() const  |  Obtiene el tipo de error.
public virtual const std::string& GetErrorName() const  |  Obtiene el nombre del error.
public virtual const std::string& GetMessage() const  |  Obtiene el mensaje de error.
public virtual void SetMessage(const std::string& msg)  |  Establece el mensaje de error.
  
## <a name="members"></a>Miembros
  
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

