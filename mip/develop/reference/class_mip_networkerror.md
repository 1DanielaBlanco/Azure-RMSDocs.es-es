---
title: clase mip NetworkError
description: Referencia de la clase mip NetworkError
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 9033a1a2c2eac34e49a4e4c9d745c34a686da230
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446233"
---
# <a name="class-mipnetworkerror"></a>clase mip::NetworkError 
Error de red. Se produjo por un comportamiento inesperado al realizar llamadas de red a los puntos de conexión de servicio.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public char const* what() const  |  Obtiene el mensaje de error.
public std::shared_ptr<Error> Clone() const  |  Clona el error.
 public virtual ErrorType GetErrorType() const  |  Obtiene el tipo de error.
 public virtual const std::string& GetErrorName() const  |  Obtiene el nombre del error.
 public virtual const std::string& GetMessage() const  |  Obtiene el mensaje de error.
 public virtual void SetMessage(const std::string& msg)  |  Establece el mensaje de error.
  
## <a name="members"></a>Miembros
  
### <a name="what"></a>what
Obtiene el mensaje de error.

  
**Devuelve**: el mensaje de error.
  
### <a name="error"></a>Error
Clona el error.

  
**Devuelve**: un clon del error.
  
### <a name="errortype"></a>ErrorType
Obtiene el tipo de error.

  
**Devuelve**: el tipo de error.
  
### <a name="geterrorname"></a>GetErrorName
Obtiene el nombre del error.

  
**Devuelve**: el nombre del error.
  
### <a name="getmessage"></a>GetMessage
Obtiene el mensaje de error.

  
**Devuelve**: el mensaje de error.
  
### <a name="setmessage"></a>SetMessage
Establece el mensaje de error.

Parámetros:  
* **msg**: el mensaje de error.

