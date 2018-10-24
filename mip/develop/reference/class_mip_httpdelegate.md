---
title: Clase mip HttpDelegate
description: Referencia de la clase mip HttpDelegate
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 3e55f9aff5a9ebd97731ec21e408a33f22905648
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445384"
---
# <a name="class-miphttpdelegate"></a>Clase mip::HttpDelegate 
Interfaz para reemplazar el control de HTTP.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public std::shared_ptr<HttpResponse> Send(const std::shared_ptr<HttpRequest>& request, const std::shared_ptr<void>& context)  |  Envía una solicitud HTTP.
  
## <a name="members"></a>Miembros
  
### <a name="httpresponse"></a>HttpResponse
Envía una solicitud HTTP.

Parámetros:  
* **request**: solicitud HTTP. 


* **context**: el mismo contexto de cliente opaco que se ha pasado a la API que ha producido esta solicitud HTTP.



  
**Devuelve**: respuesta HTTP.