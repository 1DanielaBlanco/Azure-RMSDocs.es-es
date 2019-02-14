---
title: Clase mip::HttpDelegate
description: Documenta la clase mip::httpdelegate de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 8dd81508766c65d6232c278d56f3720a98aaa9eb
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56256301"
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
