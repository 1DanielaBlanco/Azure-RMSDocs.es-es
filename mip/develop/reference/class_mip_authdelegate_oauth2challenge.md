---
title: clase mip::AuthDelegate::OAuth2Challenge
description: Documenta la clase mip::authdelegate de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 86834f0236319613df4a9ef3ab64c1ec7dc9b20e
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55652360"
---
# <a name="class-mipauthdelegateoauth2challenge"></a>clase mip::AuthDelegate::OAuth2Challenge 
una clase que contiene toda la información necesaria de la aplicación que realiza la llamada con el fin de generar un token de oauth2.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
OAuth2Challenge públicas (const std:: String & autoridad, const std:: String & recursos, const std:: String & ámbito)  |  Crear un nuevo [OAuth2Challenge](class_mip_authdelegate_oauth2challenge.md) objeto.
Public const std:: String & GetAuthority() const  |  Obtener la cadena de la entidad.
public const std::string& GetResource() const  |  Obtener la cadena de recurso.
public const std::string& GetScope() const  |  Obtener la cadena de ámbito.
  
## <a name="members"></a>Miembros
  
### <a name="oauth2challenge-function"></a>Función OAuth2Challenge
Crear un nuevo [OAuth2Challenge](class_mip_authdelegate_oauth2challenge.md) objeto.

Parámetros:  
* **autoridad**: la autoridad debe generarse en el token. 


* **recurso**: el recurso en el token se establece en. 


* **ámbito**: el token se establece en el ámbito de aplicación.


  
### <a name="getauthority-function"></a>Función GetAuthority
Obtener la cadena de la entidad.

  
**Devuelve**: La cadena de la entidad.
  
### <a name="getresource-function"></a>Función GetResource
Obtener la cadena de recurso.

  
**Devuelve**: La cadena de recurso.
  
### <a name="getscope-function"></a>GetScope (función)
Obtener la cadena de ámbito.

  
**Devuelve**: La cadena de ámbito.