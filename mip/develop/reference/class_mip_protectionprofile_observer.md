---
title: clase mip ProtectionProfile Observer
description: Referencia de la clase mip ProtectionProfile Observer
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 3678e6c1e1659f28b2f1dcc36f61295a8d29393e
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446437"
---
# <a name="class-mipprotectionprofileobserver"></a>clase mip::ProtectionProfile::Observer 
Interfaz que recibe las notificaciones relacionadas con [ProtectionProfile](class_mip_protectionprofile.md).
Esta interfaz deben implementarla las aplicaciones que utilizan el SDK de protección
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess(const std::shared_ptr<ProtectionProfile>& profile, const std::shared_ptr<void>& context)  |  Se llama cuando se cargó correctamente el perfil.
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama al cargar un perfil que ha causado un error.
public virtual void OnListEnginesSuccess(const std::vector<std::string>& engineIds, const std::shared_ptr<void>& context)  |  Se llama cuando la lista de motores se generó correctamente.
public virtual void OnListEnginesFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando los motores enumerados dieron lugar a un error.
public virtual void OnAddEngineSuccess(const std::shared_ptr<ProtectionEngine>& engine, const std::shared_ptr<void>& context)  |  Se llama cuando un nuevo motor se agregó correctamente.
public virtual void OnAddEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando la agregación de un nuevo motor originó un error.
public virtual void OnDeleteEngineSuccess(const std::shared_ptr<void>& context)  |  Se llama cuando el motor se ha eliminado correctamente.
public virtual void OnDeleteEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando la eliminación de un motor originó un error.
  
## <a name="members"></a>Miembros
  
### <a name="onloadsuccess"></a>OnLoadSuccess
Se llama cuando se cargó correctamente el perfil.

Parámetros:  
* **profile**: una referencia al [ProtectionProfile](class_mip_protectionprofile.md) recién creado


* **context**: el mismo contexto que se pasó a [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync)


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function) a [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync) y ese mismo contexto se reenviará tal cual a [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) o [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure)
  
### <a name="onloadfailure"></a>OnLoadFailure
Se llama al cargar un perfil que ha causado un error.

Parámetros:  
* **error**: [error](class_mip_error.md) que se produjo al cargar 


* **context**: el mismo contexto que se pasó a [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync)


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function) a [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync) y ese mismo contexto se reenviará tal cual a [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) o [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure)
  
### <a name="onlistenginessuccess"></a>OnListEnginesSuccess
Se llama cuando la lista de motores se generó correctamente.

Parámetros:  
* **engineIds**: una lista de los identificadores del motor que están disponibles. 


* **context**: el mismo contexto que se ha pasado a [ProtectionProfile::ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync)


  
### <a name="onlistenginesfailure"></a>OnListEnginesFailure
Se llama cuando los motores enumerados dieron lugar a un error.

Parámetros:  
* **error**: error que ha provocado que se produjera un error en la operación de crear una lista de motores. 


* **context**: el mismo contexto que se ha pasado a [ProtectionProfile::ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync)


  
### <a name="onaddenginesuccess"></a>OnAddEngineSuccess
Se llama cuando un nuevo motor se agregó correctamente.

Parámetros:  
* **motor**: motor recién creado 


* **context**: el mismo contexto que se ha pasado a [ProtectionProfile::AddEngineAsync](class_mip_protectionprofile.md#addengineasync)


  
### <a name="onaddenginefailure"></a>OnAddEngineFailure
Se llama cuando la agregación de un nuevo motor originó un error.

Parámetros:  
* **error**: error que ha provocado que se produjera un error en la operación de agregar un motor. 


* **context**: el mismo contexto que se ha pasado a [ProtectionProfile::AddEngineAsync](class_mip_protectionprofile.md#addengineasync)


  
### <a name="ondeleteenginesuccess"></a>OnDeleteEngineSuccess
Se llama cuando el motor se ha eliminado correctamente.

Parámetros:  
* **context**: el mismo contexto que se ha pasado a [ProtectionProfile::DeleteEngineAsync](class_mip_protectionprofile.md#deleteengineasync)


  
### <a name="ondeleteenginefailure"></a>OnDeleteEngineFailure
Se llama cuando la eliminación de un motor originó un error.

Parámetros:  
* **error**: error que ha provocado que se produjera un error en la operación de eliminar un motor. 


* **context**: el mismo contexto que se ha pasado a [ProtectionProfile::DeleteEngineAsync](class_mip_protectionprofile.md#deleteengineasync)

