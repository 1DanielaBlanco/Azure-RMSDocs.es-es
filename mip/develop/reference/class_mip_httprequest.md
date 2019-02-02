---
title: Clase mip::HttpRequest
description: Documenta la clase mip::httprequest de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 3c23d37836b241a416cbaf5ee5cd22f8c726794d
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650092"
---
# <a name="class-miphttprequest"></a>Clase mip::HttpRequest 
Interfaz que describe una única solicitud HTTP.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public HttpRequestType GetRequestType() const  |  Obtiene el tipo de solicitud.
public const std::string& GetUrl() const  |  Obtiene la URL de la solicitud.
public const std::string& GetBody() const  |  Obtiene el cuerpo de la solicitud.
std:: Map de const pública\<std:: String, std:: String, CaseInsensitiveComparator\>& GetHeaders() const  |  Obtiene los encabezados de solicitud.
  
## <a name="members"></a>Miembros
  
### <a name="getrequesttype-function"></a>Función GetRequestType
Obtiene el tipo de solicitud.

  
**Devuelve**: Tipo de solicitud
  
### <a name="geturl-function"></a>GetUrl (función)
Obtiene la URL de la solicitud.

  
**Devuelve**: Dirección url de solicitud
  
### <a name="getbody-function"></a>Función GetBody
Obtiene el cuerpo de la solicitud.

  
**Devuelve**: Cuerpo de la solicitud
  
### <a name="getheaders-function"></a>Función GetHeaders
Obtiene los encabezados de solicitud.

  
**Devuelve**: Encabezados de solicitud