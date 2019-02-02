---
title: clase mip::AuthDelegate::OAuth2Token
description: Documenta la clase mip::authdelegate de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 7ce9e336edfeeee07725b30c4d76c3b3c2073bc6
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55652054"
---
# <a name="class-mipauthdelegateoauth2token"></a>clase mip::AuthDelegate::OAuth2Token 
Una clase que define cómo el SDK de MIP espera que el token de oauth2 que se pasarán en el SDK.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public OAuth2Token()  |  Crear un nuevo [OAuth2Token](class_mip_authdelegate_oauth2token.md) objeto.
OAuth2Token públicas (const std:: String & accessToken)  |  Crear un nuevo [OAuth2Token](class_mip_authdelegate_oauth2token.md) objeto desde un accessToken.
Public const std:: String & GetAccessToken() const  |  Obtener la cadena de token de acceso.
pública SetAccessToken void (const std:: String & accessToken)  |  Establecer la cadena de Token de acceso.
  
## <a name="members"></a>Miembros
  
### <a name="oauth2token-function"></a>Función OAuth2Token
Crear un nuevo [OAuth2Token](class_mip_authdelegate_oauth2token.md) objeto.
  
### <a name="oauth2token-function"></a>Función OAuth2Token
Crear un nuevo [OAuth2Token](class_mip_authdelegate_oauth2token.md) objeto desde un accessToken.

Parámetros:  
* **accessToken**: El token de acceso real que se pasa en el SDK de.


  
### <a name="getaccesstoken-function"></a>Función GetAccessToken
Obtener la cadena de token de acceso.

  
**Devuelve**: La cadena de token de acceso.
  
### <a name="setaccesstoken-function"></a>Función SetAccessToken
Establecer la cadena de Token de acceso.

Parámetros:  
* **accessToken**: la cadena de token de acceso.

