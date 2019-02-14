---
title: clase mip::HttpResponse
description: Documenta la clase mip::httpresponse de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 00a6d7dd3728edbf6fb1dbb4e59c537d7b6cf911
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56253003"
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
