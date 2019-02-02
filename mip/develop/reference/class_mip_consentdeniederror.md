---
title: clase mip::ConsentDeniedError
description: Documenta la clase mip::consentdeniederror de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: c85e5d14fa02c42b322a240f6266efcf97c92c85
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650568"
---
# <a name="class-mipconsentdeniederror"></a>clase mip::ConsentDeniedError 
Una operación que necesitaba el consentimiento del usuario, pero que no lo ha recibido.
  
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

