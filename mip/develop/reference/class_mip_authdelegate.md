---
title: clase mip::AuthDelegate
description: Documenta la clase mip::authdelegate de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: b6278d605dfbb9a9c4cf0cf1282a159c456c5561
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55652003"
---
# <a name="class-mipauthdelegate"></a>clase mip::AuthDelegate 
Delegado de autenticación relacionadas con las operaciones.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public bool AcquireOAuth2Token (const MIP:: Identity, identidad, OAuth2Challenge const & desafío, OAuth2Token & símbolo (token))  |  Este método se llama cuando un token de autenticación es necesario para el motor de directiva con la identidad dada y el desafío dado. El cliente debe devolver si adquirir el token fue correcto. Si se realiza correctamente, debe inicializar el objeto de token especificado.
  
## <a name="members"></a>Miembros
  
### <a name="acquireoauth2token-function"></a>Función AcquireOAuth2Token
Este método se llama cuando un token de autenticación es necesario para el motor de directiva con la identidad dada y el desafío dado. El cliente debe devolver si adquirir el token fue correcto. Si se realiza correctamente, debe inicializar el objeto de token especificado.

Parámetros:  
* **identity**: 


* **challenge**: 


* **token**:

