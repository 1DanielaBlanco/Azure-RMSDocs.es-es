---
title: clase mip TransientNetworkError
description: Referencia de la clase mip TransientNetworkError
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 33b0bdd6c04e506bb7852d9925c943558da52b5e
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445379"
---
# <a name="class-miptransientnetworkerror"></a>clase mip::TransientNetworkError 
Error de red temporal. Se produjo por un comportamiento inesperado al realizar llamadas de red a los puntos de conexión de servicio. Se puede reintentar la operación porque este error es temporal.
  
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

