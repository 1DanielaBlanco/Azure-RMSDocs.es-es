---
title: clase mip::NoPermissionsError
description: Documenta la clase mip::nopermissionserror de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 28068c80bc7d6e7fea5dc1bbeed3f64001fc47cc
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55652071"
---
# <a name="class-mipnopermissionserror"></a>clase mip::NoPermissionsError 
El usuario no pudo obtener acceso al contenido. Por ejemplo, no hay permisos, se ha revocado el contenido, etc.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public std::string GetReferrer() const  |  Obtiene el contacto en el caso de los derechos que faltan en el documento.
public std::string GetOwner() const  | _No se ha documentado todavía._
public char const* what() const  |  Obtiene el mensaje de error.
Public std:: shared_ptr\<Error\> Clone() const  |  Clona el error.
public virtual ErrorType GetErrorType() const  |  Obtiene el tipo de error.
public virtual const std::string& GetErrorName() const  |  Obtiene el nombre del error.
public virtual const std::string& GetMessage() const  |  Obtiene el mensaje de error.
public virtual void SetMessage(const std::string& msg)  |  Establece el mensaje de error.
  
## <a name="members"></a>Miembros
  
### <a name="getreferrer-function"></a>Función GetReferrer
Obtiene el contacto en el caso de los derechos que faltan en el documento.

  
**Devuelve**: El contacto en el caso de los derechos que faltan en el documento.
  
### <a name="getowner-function"></a>GetOwner (función)
_No se ha documentado todavía._

  
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

