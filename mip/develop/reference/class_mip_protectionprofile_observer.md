---
title: clase mip::ProtectionProfile::Observer
description: 'Documenta la clase MIP:: protectionprofile de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: ad8aebf1c5c05dfeed1e04a59dd7190406c5603c
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651418"
---
# <a name="class-mipprotectionprofileobserver"></a>clase mip::ProtectionProfile::Observer 
Interfaz que recibe las notificaciones relacionadas con [ProtectionProfile](class_mip_protectionprofile.md).
Esta interfaz deben implementarla las aplicaciones que utilizan el SDK de protección
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
OnLoadSuccess de void virtual pública (const std:: shared_ptr\<ProtectionProfile\>& perfil, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando se cargó correctamente el perfil.
OnLoadFailure de void virtual pública (std::exception_ptr const & error, const std:: shared_ptr\<void\>& contexto)  |  Se llama al cargar un perfil que ha causado un error.
OnListEnginesSuccess de void virtual pública (const std:: vector\<std:: String\>& engineIds, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando la lista de motores se generó correctamente.
OnListEnginesFailure de void virtual pública (std::exception_ptr const & error, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando los motores enumerados dieron lugar a un error.
OnAddEngineSuccess de void virtual pública (const std:: shared_ptr\<ProtectionEngine\>& motor, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando un nuevo motor se agregó correctamente.
OnAddEngineFailure de void virtual pública (std::exception_ptr const & error, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando la agregación de un nuevo motor originó un error.
OnDeleteEngineSuccess de void virtual pública (const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando el motor se ha eliminado correctamente.
OnDeleteEngineFailure de void virtual pública (std::exception_ptr const & error, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando la eliminación de un motor originó un error.
  
## <a name="members"></a>Miembros
  
### <a name="onloadsuccess-function"></a>Función OnLoadSuccess
Se llama cuando se cargó correctamente el perfil.

Parámetros:  
* **profile**: Una referencia a los recién creado [ProtectionProfile](class_mip_protectionprofile.md)


* **context**: El mismo contexto que se pasó a [protectionprofile:: LoadAsync](class_mip_protectionprofile.md#addengineasync-function)


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function) a [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync-function) y ese mismo contexto se reenviará tal cual a [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess-function) o [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure-function)
  
### <a name="onloadfailure-function"></a>Función OnLoadFailure
Se llama al cargar un perfil que ha causado un error.

Parámetros:  
* **error**: [Error](class_mip_error.md) que se ha producido al cargar 


* **context**: El mismo contexto que se pasó a [protectionprofile:: LoadAsync](class_mip_protectionprofile.md#addengineasync-function)


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function) a [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync-function) y ese mismo contexto se reenviará tal cual a [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess-function) o [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure-function)
  
### <a name="onlistenginessuccess-function"></a>Función OnListEnginesSuccess
Se llama cuando la lista de motores se generó correctamente.

Parámetros:  
* **engineIds**: una lista de los identificadores del motor que están disponibles. 


* **context**: El mismo contexto que se pasó a [ProtectionProfile::ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync-function)


  
### <a name="onlistenginesfailure-function"></a>Función OnListEnginesFailure
Se llama cuando los motores enumerados dieron lugar a un error.

Parámetros:  
* **error**: error que ha provocado que se produjera un error en la operación de crear una lista de motores. 


* **context**: El mismo contexto que se pasó a [ProtectionProfile::ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync-function)


  
### <a name="onaddenginesuccess-function"></a>Función OnAddEngineSuccess
Se llama cuando un nuevo motor se agregó correctamente.

Parámetros:  
* **engine**: Recién creado motor 


* **context**: El mismo contexto que se pasó a [ProtectionProfile::AddEngineAsync](class_mip_protectionprofile.md#addengineasync-function)


  
### <a name="onaddenginefailure-function"></a>Función OnAddEngineFailure
Se llama cuando la agregación de un nuevo motor originó un error.

Parámetros:  
* **error**: error que ha provocado que se produjera un error en la operación de agregar un motor. 


* **context**: El mismo contexto que se pasó a [ProtectionProfile::AddEngineAsync](class_mip_protectionprofile.md#addengineasync-function)


  
### <a name="ondeleteenginesuccess-function"></a>Función OnDeleteEngineSuccess
Se llama cuando el motor se ha eliminado correctamente.

Parámetros:  
* **context**: El mismo contexto que se pasó a [ProtectionProfile::DeleteEngineAsync](class_mip_protectionprofile.md#deleteengineasync-function)


  
### <a name="ondeleteenginefailure-function"></a>Función OnDeleteEngineFailure
Se llama cuando la eliminación de un motor originó un error.

Parámetros:  
* **error**: error que ha provocado que se produjera un error en la operación de eliminar un motor. 


* **context**: El mismo contexto que se pasó a [ProtectionProfile::DeleteEngineAsync](class_mip_protectionprofile.md#deleteengineasync-function)

