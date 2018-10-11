---
title: clase ConsentDelegate
description: Referencia de la clase ConsentDelegate
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 841049b1e6b369eb2f6a34d9701ed34eca028af6
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446369"
---
# <a name="class-consentdelegate"></a>clase ConsentDelegate 
Delegado para operaciones relacionadas con el consentimiento.
Este delegado implementa una aplicación cliente para saber cuándo debe mostrarse al usuario una notificación de solicitud de consentimiento.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public Consent GetUserConsent(const std::string& url)  |  Se llama cuando el SDK requiere consentimiento del usuario para conectarse a un punto de conexión de servicio.
  
## <a name="members"></a>Miembros
  
### <a name="consent"></a>Consentimiento
Se llama cuando el SDK requiere consentimiento del usuario para conectarse a un punto de conexión de servicio.

Parámetros:  
* **url**: la dirección URL para el que el SDK requiere el consentimiento del usuario



  
**Devuelve**: enumeración de consentimiento con la decisión del usuario.
Cuando el SDK solicita el consentimiento del usuario con este método, la aplicación cliente debe presentar la dirección URL al usuario. Las aplicaciones cliente deben proporcionar algún medio de obtener el consentimiento del usuario y devolver la enumeración de consentimiento adecuada que corresponda a la decisión del usuario.