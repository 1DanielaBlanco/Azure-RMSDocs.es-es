---
title: clase mip::AuthDelegate
description: Documenta la clase mip::authdelegate de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: cf6ea43b36518f2eec74b9ed0f8682466aa6b64d
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56258018"
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

