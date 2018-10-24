---
title: Clase mip HttpRequest
description: Referencia de la clase mip HttpRequest
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: e838eb247bc00d43da72db1de03304e89a1b1da5
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445247"
---
# <a name="class-miphttprequest"></a>Clase mip::HttpRequest 
Interfaz que describe una única solicitud HTTP.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public HttpRequestType GetRequestType() const  |  Obtiene el tipo de solicitud.
 public const std::string& GetUrl() const  |  Obtiene la URL de la solicitud.
 public const std::string& GetBody() const  |  Obtiene el cuerpo de la solicitud.
public const std::map<std::string, std::string, CaseInsensitiveComparator>& GetHeaders() const  |  Obtiene los encabezados de solicitud.
  
## <a name="members"></a>Miembros
  
### <a name="httprequesttype"></a>HttpRequestType
Obtiene el tipo de solicitud.

  
**Devuelve**: tipo de solicitud.
  
### <a name="geturl"></a>GetUrl
Obtiene la URL de la solicitud.

  
**Devuelve**: URL de la solicitud.
  
### <a name="getbody"></a>GetBody
Obtiene el cuerpo de la solicitud.

  
**Devuelve**: cuerpo de la solicitud.
  
### <a name="getheaders"></a>GetHeaders
Obtiene los encabezados de solicitud.

  
**Devuelve**: encabezados de solicitud.