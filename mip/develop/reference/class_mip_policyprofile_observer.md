---
title: Clase mip::PolicyProfile::Observer
description: Documenta la clase mip::policyprofile de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 451cc2b9da086644e561d0a1dd1912de5f38c48c
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651180"
---
# <a name="class-mippolicyprofileobserver"></a>Clase mip::PolicyProfile::Observer 
Interfaz de [Observer](class_mip_policyprofile_observer.md) para que los clientes obtengan notificaciones de eventos relacionados con el perfil.
Todos los errores que se heredan de [mip::Error](class_mip_error.md). El cliente no debe volver a llamar al motor en el subproceso que llama al observador.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
OnLoadSuccess de void virtual pública (const std:: shared_ptr\<PolicyProfile\>& perfil, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando se cargó correctamente el perfil.
OnLoadFailure de void virtual pública (std::exception_ptr const & error, const std:: shared_ptr\<void\>& contexto)  |  Se llama al cargar un perfil que ha causado un error.
OnListEnginesSuccess de void virtual pública (const std:: vector\<std:: String\>& engineIds, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando la lista de motores se generó correctamente.
OnListEnginesFailure de void virtual pública (std::exception_ptr const & error, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando los motores enumerados causan un error.
OnUnloadEngineSuccess de void virtual pública (const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando el motor se ha descargado correctamente.
OnUnloadEngineFailure de void virtual pública (std::exception_ptr const & error, const std:: shared_ptr\<void\>& contexto)  |  Se llama al descargar un motor que ha causado un error.
OnAddEngineSuccess de void virtual pública (const std:: shared_ptr\<PolicyEngine\>& motor, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando un nuevo motor se agregó correctamente.
OnAddEngineStarting void virtual pública (bool requiresPolicyFetch)  |  Se llama antes de la creación de un motor para describir si se deben buscar los datos del motor de la directiva desde el servidor o si pueden crearse desde los datos almacenados en caché localmente.
OnAddEngineFailure de void virtual pública (std::exception_ptr const & error, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando se produce un error al agregar un nuevo motor.
OnDeleteEngineSuccess de void virtual pública (const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando el motor se ha eliminado correctamente.
OnDeleteEngineFailure de void virtual pública (std::exception_ptr const & error, const std:: shared_ptr\<void\>& contexto)  |  Se llama al eliminar un motor que ha causado un error.
public virtual void OnPolicyChanged(const std::string& engineId)  |  Se llama cuando ha cambiado la directiva para el motor con el identificador especificado, o cuando han cambiado los tipos de sensibilidad personalizado cargado.
  
## <a name="members"></a>Miembros
  
### <a name="onloadsuccess-function"></a>Función OnLoadSuccess
Se llama cuando se cargó correctamente el perfil.

Parámetros:  
* **profile**: el perfil actual usado para iniciar la operación. 


* **contexto**: el contexto se pasa a la operación LoadAsync.


  
### <a name="onloadfailure-function"></a>Función OnLoadFailure
Se llama al cargar un perfil que ha causado un error.

Parámetros:  
* **error**: el error que hace que la operación de carga produzca un error. 


* **contexto**: el contexto se pasa a la operación LoadAsync.


  
### <a name="onlistenginessuccess-function"></a>Función OnListEnginesSuccess
Se llama cuando la lista de motores se generó correctamente.

Parámetros:  
* **engineIds**: una lista de los identificadores del motor que están disponibles. 


* **contexto**: el contexto se pasa a la operación ListEnginesAsync.


  
### <a name="onlistenginesfailure-function"></a>Función OnListEnginesFailure
Se llama cuando los motores enumerados causan un error.

Parámetros:  
* **error**: el error que hace que la operación de listado del motor produzca un error. 


* **contexto**: el contexto se pasa a la operación ListEnginesAsync.


  
### <a name="onunloadenginesuccess-function"></a>Función OnUnloadEngineSuccess
Se llama cuando el motor se ha descargado correctamente.

Parámetros:  
* **contexto**: el contexto se pasa a la operación UnloadEngineAsync.


  
### <a name="onunloadenginefailure-function"></a>Función OnUnloadEngineFailure
Se llama al descargar un motor que ha causado un error.

Parámetros:  
* **error**: el error que hace que la operación de descarga del motor produzca un error. 


* **contexto**: el contexto se pasa a la operación UnloadEngineAsync.


  
### <a name="onaddenginesuccess-function"></a>Función OnAddEngineSuccess
Se llama cuando un nuevo motor se agregó correctamente.

Parámetros:  
* **motor**: el motor recién agregada 


* **contexto**: el contexto se pasa a la operación AddEngineAsync


  
### <a name="onaddenginestarting-function"></a>Función OnAddEngineStarting
Se llama antes de la creación de un motor para describir si se deben buscar los datos del motor de la directiva desde el servidor o si pueden crearse desde los datos almacenados en caché localmente.

Parámetros:  
* **requiresPolicyFetch**: Describe si se debe recuperar los datos de motor a través de HTTP o si se cargarán desde caché


Esta devolución de llamada opcional puede utilizarse por una aplicación para ser informado si una operación AddEngineAsync requerirá una operación HTTP (con su retraso asociado) para completar.
  
### <a name="onaddenginefailure-function"></a>Función OnAddEngineFailure
Se llama cuando se produce un error al agregar un nuevo motor.

Parámetros:  
* **error**: error que ha provocado que se produjera un error en la operación de agregar un motor. 


* **contexto**: el contexto se pasa a la operación AddEngineAsync.


  
### <a name="ondeleteenginesuccess-function"></a>Función OnDeleteEngineSuccess
Se llama cuando el motor se ha eliminado correctamente.

Parámetros:  
* **contexto**: el contexto se pasa a la operación DeleteEngineAsync.


  
### <a name="ondeleteenginefailure-function"></a>Función OnDeleteEngineFailure
Se llama al eliminar un motor que ha causado un error.

Parámetros:  
* **error**: error que ha provocado que se produjera un error en la operación de eliminar un motor. 


* **contexto**: el contexto se pasa a la operación DeleteEngineAsync.


  
### <a name="onpolicychanged-function"></a>Función OnPolicyChanged
Se llama cuando ha cambiado la directiva para el motor con el identificador especificado, o cuando han cambiado los tipos de sensibilidad personalizado cargado.

Parámetros:  
* **engineId**: el motor 


Para cargar la nueva directiva es necesario volver a llamar a AddEngineAsync con el identificador del motor especificado.