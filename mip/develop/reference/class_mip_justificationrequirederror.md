---
title: Clase mip JustificationRequiredError
description: Referencia de la clase mip JustificationRequiredError
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 059d139fc5222fd5f1865c66834519347e23a5a9
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445995"
---
# <a name="class-mipjustificationrequirederror"></a>clase mip::JustificationRequiredError 
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public virtual std::shared_ptr<Error> Clone() const  |  Clona el error.
 public char const* what() const  |  Obtiene el mensaje de error.
 public virtual ErrorType GetErrorType() const  |  Obtiene el tipo de error.
 public virtual const std::string& GetErrorName() const  |  Obtiene el nombre del error.
 public virtual const std::string& GetMessage() const  |  Obtiene el mensaje de error.
 public virtual void SetMessage(const std::string& msg)  |  Establece el mensaje de error.
  
## <a name="members"></a>Miembros
  
### <a name="error"></a>Error
Clona el error.

  
**Devuelve**: un clon del error.
  
### <a name="what"></a>what
Obtiene el mensaje de error.

  
**Devuelve**: el mensaje de error.
  
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

