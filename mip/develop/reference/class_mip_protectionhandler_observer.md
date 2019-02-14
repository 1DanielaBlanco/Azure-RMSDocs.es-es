---
title: clase mip::ProtectionHandler::Observer
description: Documenta la clase mip::protectionhandler de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 4dac87e4fba8cf5bbcf6eef98ff1edda28a9947f
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56255857"
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
