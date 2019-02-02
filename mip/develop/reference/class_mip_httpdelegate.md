---
title: Clase mip::HttpDelegate
description: Documenta la clase mip::httpdelegate de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 68d26b23c1e3ea2e29c22316f80e18937ab78d5c
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651028"
---
# <a name="class-miphttpdelegate"></a>Clase mip::HttpDelegate 
Interfaz para reemplazar el control de HTTP.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
Public std:: shared_ptr\<HttpResponse\> enviar (const std:: shared_ptr\<HttpRequest\>& solicitud, const std:: shared_ptr\<void\>& contexto)  |  Envía una solicitud HTTP.
SendAsync void público (const std:: shared_ptr\<HttpRequest\>& solicitud, const std:: shared_ptr\<void\>& contexto, const std:: Function\<void(std::shared_ptr\<HttpResponse\>)\>& fnCallback)  | _No se ha documentado todavía._
  
## <a name="members"></a>Miembros
  
### <a name="send-function"></a>Send (función)
Envía una solicitud HTTP.

Parámetros:  
* **request**: Solicitud HTTP 


* **context**: El mismo contexto de cliente opaco que se pasó a la API que dieron lugar a esta solicitud HTTP



  
**Devuelve**: Respuesta HTTP
  
### <a name="sendasync-function"></a>SendAsync (función)
_No se ha documentado todavía._
