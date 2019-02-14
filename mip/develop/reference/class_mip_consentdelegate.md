---
title: clase mip::ConsentDelegate
description: Documenta la clase mip::consentdelegate de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 6b4ec544e0390f9fd17d39dc146cfd538cfb927c
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56254873"
---
# <a name="class-mipconsentdelegate"></a>clase mip::ConsentDelegate 
Delegado para operaciones relacionadas con el consentimiento.
Este delegado implementa una aplicación cliente para saber cuándo debe mostrarse al usuario una notificación de solicitud de consentimiento.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public Consent GetUserConsent(const std::string& url)  |  Se llama cuando el SDK requiere consentimiento del usuario para conectarse a un punto de conexión de servicio.
  
## <a name="members"></a>Miembros
  
### <a name="getuserconsent-function"></a>Función GetUserConsent
Se llama cuando el SDK requiere consentimiento del usuario para conectarse a un punto de conexión de servicio.

Parámetros:  
* **url**: La dirección URL para el que el SDK requiere el consentimiento del usuario



  
**Devuelve**: Una enumeración de consentimiento con la Decisión del usuario.
Cuando el SDK solicita el consentimiento del usuario con este método, la aplicación cliente debe presentar la dirección URL al usuario. Las aplicaciones cliente deben proporcionar algún medio de obtener el consentimiento del usuario y devolver la enumeración de consentimiento adecuada que corresponda a la decisión del usuario.
