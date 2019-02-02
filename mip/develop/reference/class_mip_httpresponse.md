---
title: clase mip::HttpResponse
description: Documenta la clase mip::httpresponse de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 9cbd899548be15833456a7c1e1fe34c3b5629717
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650299"
---
# <a name="class-miphttpresponse"></a>clase mip::HttpResponse 
Interfaz que describe una única respuesta HTTP, implementada por la aplicación cliente cuando se reemplaza [HttpDelegate](class_mip_httpdelegate.md).
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public int32_t GetStatusCode() const  |  Obtenga el código de estado de la respuesta.
public const std::string& GetBody() const  |  Obtiene el cuerpo de la solicitud.
std:: Map de const pública\<std:: String, std:: String, CaseInsensitiveComparator\>& GetHeaders() const  |  Obtiene los encabezados de solicitud.
  
## <a name="members"></a>Miembros
  
### <a name="getstatuscode-function"></a>Función GetStatusCode
Obtenga el código de estado de la respuesta.

  
**Devuelve**: Código de estado
  
### <a name="getbody-function"></a>Función GetBody
Obtiene el cuerpo de la solicitud.

  
**Devuelve**: Cuerpo de la solicitud
  
### <a name="getheaders-function"></a>Función GetHeaders
Obtiene los encabezados de solicitud.

  
**Devuelve**: Encabezados de solicitud