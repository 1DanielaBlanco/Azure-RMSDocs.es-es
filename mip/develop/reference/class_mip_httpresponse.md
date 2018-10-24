---
title: clase mip HttpResponse
description: Referencia de la clase mip HttpResponse
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a19ea78b048cafe94501d452bb9c7409237f6ffd
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445374"
---
# <a name="class-miphttpresponse"></a>clase mip::HttpResponse 
Interfaz que describe una única respuesta HTTP, implementada por la aplicación cliente cuando se reemplaza [HttpDelegate](class_mip_httpdelegate.md).
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public int32_t GetStatusCode() const  |  Obtenga el código de estado de la respuesta.
 public const std::string& GetBody() const  |  Obtiene el cuerpo de la solicitud.
public const std::map<std::string, std::string, CaseInsensitiveComparator>& GetHeaders() const  |  Obtiene los encabezados de solicitud.
  
## <a name="members"></a>Miembros
  
### <a name="getstatuscode"></a>GetStatusCode
Obtenga el código de estado de la respuesta.

  
**Devuelve**: código de estado
  
### <a name="getbody"></a>GetBody
Obtiene el cuerpo de la solicitud.

  
**Devuelve**: cuerpo de la solicitud.
  
### <a name="getheaders"></a>GetHeaders
Obtiene los encabezados de solicitud.

  
**Devuelve**: encabezados de solicitud.