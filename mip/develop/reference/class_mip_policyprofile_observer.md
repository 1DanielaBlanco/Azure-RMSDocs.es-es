---
title: Clase mip PolicyProfile Observer
description: Referencia de la clase mip PolicyProfile Observer
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 5de2156f4906c14e4ebc1418df8acb092c089d7d
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446902"
---
# <a name="class-mippolicyprofileobserver"></a>Clase mip::PolicyProfile::Observer 
Interfaz de [Observer](class_mip_policyprofile_observer.md) para que los clientes obtengan notificaciones de eventos relacionados con el perfil.
Todos los errores que se heredan de [mip::Error](class_mip_error.md). El cliente no debe volver a llamar al motor en el subproceso que llama al observador.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess(const std::shared_ptr<PolicyProfile>& profile, const std::shared_ptr<void>& context)  |  Se llama cuando se cargó correctamente el perfil.
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama al cargar un perfil que ha causado un error.
public virtual void OnListEnginesSuccess(const std::vector<std::string>& engineIds, const std::shared_ptr<void>& context)  |  Se llama cuando la lista de motores se generó correctamente.
public virtual void OnListEnginesFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando los motores enumerados causan un error.
public virtual void OnUnloadEngineSuccess(const std::shared_ptr<void>& context)  |  Se llama cuando el motor se ha descargado correctamente.
public virtual void OnUnloadEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama al descargar un motor que ha causado un error.
public virtual void OnAddEngineSuccess(const std::shared_ptr<PolicyEngine>& engine, const std::shared_ptr<void>& context)  |  Se llama cuando un nuevo motor se agregó correctamente.
public virtual void OnAddEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando se produce un error al agregar un nuevo motor.
public virtual void OnDeleteEngineSuccess(const std::shared_ptr<void>& context)  |  Se llama cuando el motor se ha eliminado correctamente.
public virtual void OnDeleteEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama al eliminar un motor que ha causado un error.
 public virtual void OnPolicyChanged(const std::string& engineId)  |  Se llama cuando la directiva ha cambiado para el motor con el identificador especificado.
  
## <a name="members"></a>Miembros
  
### <a name="onloadsuccess"></a>OnLoadSuccess
Se llama cuando se cargó correctamente el perfil.

Parámetros:  
* **profile**: el perfil actual usado para iniciar la operación. 


* **context**: contexto que se pasa a la operación.


  
### <a name="onloadfailure"></a>OnLoadFailure
Se llama al cargar un perfil que ha causado un error.

Parámetros:  
* **error**: el error que hace que la operación de carga produzca un error. 


* **context**: contexto que se pasa a la operación.


  
### <a name="onlistenginessuccess"></a>OnListEnginesSuccess
Se llama cuando la lista de motores se generó correctamente.

Parámetros:  
* **engineIds**: una lista de identificadores de motor que están disponibles. 


* **context**: contexto que se pasa a la operación.


  
### <a name="onlistenginesfailure"></a>OnListEnginesFailure
Se llama cuando los motores enumerados causan un error.

Parámetros:  
* **error**: el error que hace que la operación de listado del motor produzca un error. 


* **context**: contexto que se pasa a la operación.


  
### <a name="onunloadenginesuccess"></a>OnUnloadEngineSuccess
Se llama cuando el motor se ha descargado correctamente.

Parámetros:  
* **context**: contexto que se pasa a la operación.


  
### <a name="onunloadenginefailure"></a>OnUnloadEngineFailure
Se llama al descargar un motor que ha causado un error.

Parámetros:  
* **error**: el error que hace que la operación de descarga del motor produzca un error. 


* **context**: contexto que se pasa a la operación.


  
### <a name="onaddenginesuccess"></a>OnAddEngineSuccess
Se llama cuando un nuevo motor se agregó correctamente.
  
### <a name="onaddenginefailure"></a>OnAddEngineFailure
Se llama cuando se produce un error al agregar un nuevo motor.

Parámetros:  
* **error**: el error que hace que la operación de adición del motor produzca un error. 


* **context**: contexto que se pasa a la operación.


  
### <a name="ondeleteenginesuccess"></a>OnDeleteEngineSuccess
Se llama cuando el motor se ha eliminado correctamente.

Parámetros:  
* **context**: contexto que se pasa a la operación.


  
### <a name="ondeleteenginefailure"></a>OnDeleteEngineFailure
Se llama al eliminar un motor que ha causado un error.

Parámetros:  
* **error**: el error que hace que la operación de eliminación del motor produzca un error. 


* **context**: contexto que se pasa a la operación.


  
### <a name="onpolicychanged"></a>OnPolicyChanged
Se llama cuando la directiva ha cambiado para el motor con el identificador especificado.

Parámetros:  
* **engineId**: el motor 


Para cargar la nueva directiva es necesario volver a llamar a AddEngineAsync con el identificador del motor especificado.