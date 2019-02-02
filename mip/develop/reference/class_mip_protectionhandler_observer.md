---
title: clase mip::ProtectionHandler::Observer
description: Documenta la clase mip::protectionhandler de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: ebfa1397ede2f6d4215139366d11d2d333effa14
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651010"
---
# <a name="class-mipprotectionhandlerobserver"></a>clase mip::ProtectionHandler::Observer 
Interfaz que recibe las notificaciones relacionadas con [ProtectionHandler](class_mip_protectionhandler.md).
Esta interfaz deben implementarla las aplicaciones que utilizan el SDK de protección
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
OnCreateProtectionHandlerSuccess de void virtual pública (const std:: shared_ptr\<ProtectionHandler\>& protectionHandler, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando [ProtectionHandler](class_mip_protectionhandler.md) se creó correctamente.
OnCreateProtectionHandlerFailure de void virtual pública (std::exception_ptr const & error, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando no se pudo crear [ProtectionHandler](class_mip_protectionhandler.md).
  
## <a name="members"></a>Miembros
  
### <a name="oncreateprotectionhandlersuccess-function"></a>Función OnCreateProtectionHandlerSuccess
Se llama cuando [ProtectionHandler](class_mip_protectionhandler.md) se creó correctamente.

Parámetros:  
* **protectionHandler**: Recién creado [ProtectionHandler](class_mip_protectionhandler.md)


* **context**: El mismo contexto que se pasó a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function)


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function) a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function) y ese mismo contexto se reenviará tal cual a ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess o ProtectionEngine::Observer::OnCreateProtectionHandlerFailure
  
### <a name="oncreateprotectionhandlerfailure-function"></a>Función OnCreateProtectionHandlerFailure
Se llama cuando no se pudo crear [ProtectionHandler](class_mip_protectionhandler.md).

Parámetros:  
* **error**: Errores ocurridos durante la creación 


* **context**: El mismo contexto que se pasó a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function)


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function) a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function) y ese mismo contexto se reenviará tal cual a ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess o ProtectionEngine::Observer::OnCreateProtectionHandlerFailure