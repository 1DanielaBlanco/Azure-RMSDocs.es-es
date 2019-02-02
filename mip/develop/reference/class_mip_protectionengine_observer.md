---
title: clase mip::ProtectionEngine::Observer
description: Documenta la clase mip::protectionengine de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 48dc726b8f541d8163cceb16e330f160b6d6bafb
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651639"
---
# <a name="class-mipprotectionengineobserver"></a>clase mip::ProtectionEngine::Observer 
Interfaz que recibe las notificaciones relacionadas con [ProtectionEngine](class_mip_protectionengine.md).
Esta interfaz deben implementarla las aplicaciones que utilizan el SDK de protección
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess(const std::shared_ptr\<std::vector\<std::string\>\>& templateIds, const std::shared_ptr\<void\>& context)  |  Se llama cuando se recuperan correctamente las plantillas.
OnGetTemplatesFailure de void virtual pública (std::exception_ptr const & error, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando se ha generado un error al recuperar las plantillas.
OnGetRightsForLabelIdSuccess de void virtual pública (const std:: shared_ptr\<std:: vector\<std:: String\>\>& derechos, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando se recuperan correctamente los derechos.
OnGetRightsForLabelIdFailure de void virtual pública (std::exception_ptr const & error, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando se recuperan los derechos para un identificador de etiqueta para el usuario.
  
## <a name="members"></a>Miembros
  
### <a name="ongettemplatessuccess-function"></a>Función OnGetTemplatesSuccess
Se llama cuando se recuperan correctamente las plantillas.

Parámetros:  
* **templateIds**: Recupera una referencia a la lista de plantillas 


* **context**: El mismo contexto que se pasó a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function)


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function, etc.) a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function) y ese mismo contexto se reenviará tal cual a [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess-function) o [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure-function)
  
### <a name="ongettemplatesfailure-function"></a>Función OnGetTemplatesFailure
Se llama cuando se ha generado un error al recuperar las plantillas.

Parámetros:  
* **error**: [Error](class_mip_error.md) que se produjo al recuperar las plantillas 


* **context**: El mismo contexto que se pasó a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function)


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function, etc.) a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function) y ese mismo contexto se reenviará tal cual a [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess-function) o [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure-function)
  
### <a name="ongetrightsforlabelidsuccess-function"></a>Función OnGetRightsForLabelIdSuccess
Se llama cuando se recuperan correctamente los derechos.

Parámetros:  
* **rights**: Recupera una referencia a la lista de derechos 


* **context**: El mismo contexto que se pasó a [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync-function)


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function, etc.) a [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync-function) y ese mismo contexto se reenviará tal cual a [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function) o [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function)
  
### <a name="ongetrightsforlabelidfailure-function"></a>Función OnGetRightsForLabelIdFailure
Se llama cuando se recuperan los derechos para un identificador de etiqueta para el usuario.

Parámetros:  
* **error**: [Error](class_mip_error.md) que se produjo al recuperar los derechos 


* **context**: El mismo contexto que se pasó a [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync-function)


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function, etc.) a [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync-function) y ese mismo contexto se reenviará tal cual a [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function) o [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function)