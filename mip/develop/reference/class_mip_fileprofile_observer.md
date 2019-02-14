---
title: clase mip::FileProfile::Observer
description: 'Documenta la clase MIP:: fileprofile de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: e1eb3a91b4acb1687563fb10d26e9f7c6b873e94
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56254737"
---
# <a name="class-mipfileprofileobserver"></a>clase mip::FileProfile::Observer 
Interfaz de [Observer](class_mip_fileprofile_observer.md) para que los clientes obtengan notificaciones de eventos relacionados con el perfil.
Todos los errores que se heredan de [mip::Error](class_mip_error.md). El cliente no debe volver a llamar al motor en el subproceso que llama al observador.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public virtual ~Observer()  | _No se ha documentado todavía._
OnLoadSuccess de void virtual pública (const std:: shared_ptr\<MIP:: fileprofile\>& perfil, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando se cargó correctamente el perfil.
OnLoadFailure de void virtual pública (std::exception_ptr const & error, const std:: shared_ptr\<void\>& contexto)  |  Se llama al cargar un perfil que ha causado un error.
OnListEnginesSuccess de void virtual pública (const std:: vector\<std:: String\>& engineIds, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando la lista de motores se generó correctamente.
OnListEnginesFailure de void virtual pública (std::exception_ptr const & error, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando los motores enumerados causan un error.
OnUnloadEngineSuccess de void virtual pública (const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando el motor se ha descargado correctamente.
OnUnloadEngineFailure de void virtual pública (std::exception_ptr const & error, const std:: shared_ptr\<void\>& contexto)  |  Se llama al descargar un motor que ha causado un error.
OnAddEngineSuccess de void virtual pública (const std:: shared_ptr\<MIP:: fileengine\>& motor, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando un nuevo motor se agregó correctamente.
OnAddEngineFailure de void virtual pública (std::exception_ptr const & error, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando se produce un error al agregar un nuevo motor.
OnDeleteEngineSuccess de void virtual pública (const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando el motor se ha eliminado correctamente.
OnDeleteEngineFailure de void virtual pública (std::exception_ptr const & error, const std:: shared_ptr\<void\>& contexto)  |  Se llama al eliminar un motor que ha causado un error.
public virtual void OnPolicyChanged(const std::string& engineId)  |  Se llama cuando la directiva ha cambiado para el motor con el identificador especificado.
OnAddPolicyEngineStarting void virtual pública (bool requiresPolicyFetch)  |  Se llama antes de la creación de un motor para describir si se deben buscar los datos de la directiva del motor de directiva desde el servidor o si pueden crearse desde los datos almacenados en caché localmente.
protected Observer()  | _No se ha documentado todavía._
  
## <a name="members"></a>Miembros
  
### <a name="observer-function"></a>~ Función observador
_No se ha documentado todavía._

  
### <a name="onloadsuccess-function"></a>Función OnLoadSuccess
Se llama cuando se cargó correctamente el perfil.
  
### <a name="onloadfailure-function"></a>Función OnLoadFailure
Se llama al cargar un perfil que ha causado un error.
  
### <a name="onlistenginessuccess-function"></a>Función OnListEnginesSuccess
Se llama cuando la lista de motores se generó correctamente.
  
### <a name="onlistenginesfailure-function"></a>Función OnListEnginesFailure
Se llama cuando los motores enumerados causan un error.
  
### <a name="onunloadenginesuccess-function"></a>Función OnUnloadEngineSuccess
Se llama cuando el motor se ha descargado correctamente.
  
### <a name="onunloadenginefailure-function"></a>Función OnUnloadEngineFailure
Se llama al descargar un motor que ha causado un error.
  
### <a name="onaddenginesuccess-function"></a>Función OnAddEngineSuccess
Se llama cuando un nuevo motor se agregó correctamente.
  
### <a name="onaddenginefailure-function"></a>Función OnAddEngineFailure
Se llama cuando se produce un error al agregar un nuevo motor.
  
### <a name="ondeleteenginesuccess-function"></a>Función OnDeleteEngineSuccess
Se llama cuando el motor se ha eliminado correctamente.
  
### <a name="ondeleteenginefailure-function"></a>Función OnDeleteEngineFailure
Se llama al eliminar un motor que ha causado un error.
  
### <a name="onpolicychanged-function"></a>Función OnPolicyChanged
Se llama cuando la directiva ha cambiado para el motor con el identificador especificado.
  
### <a name="onaddpolicyenginestarting-function"></a>Función OnAddPolicyEngineStarting
Se llama antes de la creación de un motor para describir si se deben buscar los datos de la directiva del motor de directiva desde el servidor o si pueden crearse desde los datos almacenados en caché localmente.

Parámetros:  
* **requiresPolicyFetch**: Describe si se debe recuperar los datos de motor a través de HTTP o si se cargarán desde caché


Esta devolución de llamada opcional puede utilizarse por una aplicación para ser informado si una operación AddEngineAsync requerirá una operación HTTP (con su retraso asociado) para completar.
  
### <a name="observer-function"></a>Función de observador
_No se ha documentado todavía._
