---
title: Clase mip::ProtectionHandler::Observer
description: Referencia de la clase mip::ProtectionHandler::Observer
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 7fed286dec42f16d7dfa8e375ec739264bd365ba
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446202"
---
# <a name="class-mipprotectionhandlerobserver"></a>clase mip::ProtectionHandler::Observer 
Interfaz que recibe las notificaciones relacionadas con [ProtectionHandler](class_mip_protectionhandler.md).
Esta interfaz la deben implementar las aplicaciones que utilizan el SDK de protección
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public virtual void OnCreateProtectionHandlerSuccess(const std::shared_ptr<ProtectionHandler>& protectionHandler, const std::shared_ptr<void>& context)  |  Se llama cuando [ProtectionHandler](class_mip_protectionhandler.md) se creó correctamente.
public virtual void OnCreateProtectionHandlerFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando no se pudo crear [ProtectionHandler](class_mip_protectionhandler.md).
  
## <a name="members"></a>Miembros
  
### <a name="oncreateprotectionhandlersuccess"></a>OnCreateProtectionHandlerSuccess
Se llama cuando [ProtectionHandler](class_mip_protectionhandler.md) se creó correctamente.

Parámetros:  
* **protectionHandler**: el objeto [ProtectionHandler](class_mip_protectionhandler.md) recién creado.


* **context**: el mismo contexto que se pasó a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync)


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function) a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync) y ese mismo contexto se reenviará tal cual a ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess o ProtectionEngine::Observer::OnCreateProtectionHandlerFailure
  
### <a name="oncreateprotectionhandlerfailure"></a>OnCreateProtectionHandlerFailure
Se llama cuando no se pudo crear [ProtectionHandler](class_mip_protectionhandler.md).

Parámetros:  
* **error**: error producido durante la creación. 


* **context**: el mismo contexto que se pasó a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync)


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function) a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync) y ese mismo contexto se reenviará tal cual a ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess o ProtectionEngine::Observer::OnCreateProtectionHandlerFailure