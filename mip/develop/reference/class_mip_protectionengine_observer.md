---
title: clase mip ProtectionEngine Observer
description: Referencia de la clase mip ProtectionEngine Observer
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 5c5b5e807a80c8db3cbdb69ea5d09da1e79aec6e
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446590"
---
# <a name="class-mipprotectionengineobserver"></a>clase mip::ProtectionEngine::Observer 
Interfaz que recibe las notificaciones relacionadas con [ProtectionEngine](class_mip_protectionengine.md).
Esta interfaz deben implementarla las aplicaciones que utilizan el SDK de protección
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess(const std::shared_ptr<std::vector<std::string>>& templateIds, const std::shared_ptr<void>& context)  |  Se llama cuando se recuperan correctamente las plantillas.
public virtual void OnGetTemplatesFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando se ha generado un error al recuperar las plantillas.
public virtual void OnGetRightsForLabelIdSuccess(const std::shared_ptr<std::vector<std::string>>& rights, const std::shared_ptr<void>& context)  |  Se llama cuando se recuperan correctamente los derechos.
public virtual void OnGetRightsForLabelIdFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando se recuperan los derechos para un identificador de etiqueta para el usuario.
public virtual void OnGetGrantingLabelIdsSuccess(const std::shared_ptr<std::vector<std::string>>& lableIds, const std::shared_ptr<void>& context)  |  Se llama cuando se recuperan correctamente los identificadores de etiqueta.
public virtual void OnGetGrantingLabelIdsFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando se recuperan los identificadores de etiqueta para el usuario.
  
## <a name="members"></a>Miembros
  
### <a name="ongettemplatessuccess"></a>OnGetTemplatesSuccess
Se llama cuando se recuperan correctamente las plantillas.

Parámetros:  
* **templateIds**: una referencia a la lista de plantillas recuperadas 


* **context**: el mismo contexto que se pasó a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync)


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function, etc.) a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync) y ese mismo contexto se reenviará tal cual a [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) o [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure)
  
### <a name="ongettemplatesfailure"></a>OnGetTemplatesFailure
Se llama cuando se ha generado un error al recuperar las plantillas.

Parámetros:  
* **error**: [error](class_mip_error.md) que se ha producido al recuperar plantillas 


* **context**: el mismo contexto que se pasó a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync)


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function, etc.) a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync) y ese mismo contexto se reenviará tal cual a [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) o [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure)
  
### <a name="ongetrightsforlabelidsuccess"></a>OnGetRightsForLabelIdSuccess
Se llama cuando se recuperan correctamente los derechos.

Parámetros:  
* **rights**: una referencia a la lista de derechos recuperados 


* **context**: el mismo contexto que se ha pasado a [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync)


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function, etc.) a [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync) y ese mismo contexto se reenviará tal cual a [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess) o [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure)
  
### <a name="ongetrightsforlabelidfailure"></a>OnGetRightsForLabelIdFailure
Se llama cuando se recuperan los derechos para un identificador de etiqueta para el usuario.

Parámetros:  
* **error**: [error](class_mip_error.md) que se ha producido al recuperar derechos 


* **context**: el mismo contexto que se ha pasado a [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync)


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function, etc.) a [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync) y ese mismo contexto se reenviará tal cual a [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess) o [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure)
  
### <a name="ongetgrantinglabelidssuccess"></a>OnGetGrantingLabelIdsSuccess
Se llama cuando se recuperan correctamente los identificadores de etiqueta.

Parámetros:  
* **labelIds**: una referencia a la lista de identificadores de etiqueta recuperados 


* **context**: el mismo contexto que se ha pasado a [ProtectionEngine::GetGrantingLabelIdsAsync](class_mip_protectionengine.md#getgrantinglabelidsasync)


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function, etc.) a [ProtectionEngine::GetGrantingLabelIdsAsync](class_mip_protectionengine.md#getgrantinglabelidsasync) y ese mismo contexto se reenviará tal cual a [ProtectionEngine::Observer::OnGetGrantingLabelIdsSuccess](class_mip_protectionengine_observer.md#ongetgrantinglabelidssuccess) o [ProtectionEngine::Observer::OnGetGrantingLabelIdsFailure](class_mip_protectionengine_observer.md#ongetgrantinglabelidsfailure)
  
### <a name="ongetgrantinglabelidsfailure"></a>OnGetGrantingLabelIdsFailure
Se llama cuando se recuperan los identificadores de etiqueta para el usuario.

Parámetros:  
* **error**: [error](class_mip_error.md) que se ha producido al recuperar los identificadores de etiqueta 


* **context**: el mismo contexto que se ha pasado a [ProtectionEngine::GetGrantingLabelIdsAsync](class_mip_protectionengine.md#getgrantinglabelidsasync)


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function, etc.) a [ProtectionEngine::GetGrantingLabelIdsAsync](class_mip_protectionengine.md#getgrantinglabelidsasync) y ese mismo contexto se reenviará tal cual a [ProtectionEngine::Observer::OnGetGrantingLabelIdsSuccess](class_mip_protectionengine_observer.md#ongetgrantinglabelidssuccess) o [ProtectionEngine::Observer::OnGetGrantingLabelIdsFailure](class_mip_protectionengine_observer.md#ongetgrantinglabelidsfailure)