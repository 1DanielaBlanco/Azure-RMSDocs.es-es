# <a name="class-mipprotectionprofileobserver"></a>clase mip::ProtectionProfile::Observer 
Interfaz que recibe las notificaciones relacionadas con [ProtectionProfile](class_mip_protectionprofile.md).
Esta interfaz la deben implementar las aplicaciones que utilizan el SDK de protección
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess(const std::shared_ptr<ProtectionProfile>& profile, const std::shared_ptr<void>& context)  |  Se llama cuando se cargó correctamente el perfil.
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama al cargar un perfil que ha causado un error.
public virtual void OnListEnginesSuccess(const std::vector<std::string>& engineIds, const std::shared_ptr<void>& context)  |  Se llama cuando la lista de motores se generó correctamente.
public virtual void OnListEnginesError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando los motores enumerados dieron lugar a un error.
public virtual void OnAddEngineSuccess(const std::shared_ptr<ProtectionEngine>& engine, const std::shared_ptr<void>& context)  |  Se llama cuando un nuevo motor se agregó correctamente.
public virtual void OnAddEngineError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando la agregación de un nuevo motor originó un error.
public virtual void OnDeleteEngineSuccess(const std::shared_ptr<void>& context)  |  Se llama cuando el motor se ha eliminado correctamente.
public virtual void OnDeleteEngineError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando la eliminación de un motor originó un error.
  
## <a name="members"></a>Miembros
  
### <a name="onloadsuccess"></a>OnLoadSuccess
Se llama cuando se cargó correctamente el perfil.

Parámetros:  
* **profile**: una referencia a la clase [ProtectionProfile](class_mip_protectionprofile.md) recién creada


* **context**: el mismo contexto que se pasó a ProtectionProfile::LoadAsync


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function, etc.) a ProtectionProfile::LoadAsync y ese mismo contexto se reenviará tal cual a [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) o [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure)
  
### <a name="onloadfailure"></a>OnLoadFailure
Se llama al cargar un perfil que ha causado un error.

Parámetros:  
* **error**: [error](class_mip_error.md) que se produjo al cargar 


* **context**: el mismo contexto que se pasó a ProtectionProfile::LoadAsync


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function, etc.) a ProtectionProfile::LoadAsync y ese mismo contexto se reenviará tal cual a [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) o [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure)
  
### <a name="onlistenginessuccess"></a>OnListEnginesSuccess
Se llama cuando la lista de motores se generó correctamente.

Parámetros:  
* **engineIds**: una lista de identificadores de motor que están disponibles. 


* **context**: contexto que se pasa a la operación.


  
### <a name="onlistengineserror"></a>OnListEnginesError
Se llama cuando los motores enumerados dieron lugar a un error.

Parámetros:  
* **error**: el error que hace que la operación de listado del motor produzca un error. 


* **context**: contexto que se pasa a la operación.


  
### <a name="onaddenginesuccess"></a>OnAddEngineSuccess
Se llama cuando un nuevo motor se agregó correctamente.
  
### <a name="onaddengineerror"></a>OnAddEngineError
Se llama cuando la agregación de un nuevo motor originó un error.

Parámetros:  
* **error**: el error que hace que la operación de adición del motor produzca un error. 


* **context**: contexto que se pasa a la operación.


  
### <a name="ondeleteenginesuccess"></a>OnDeleteEngineSuccess
Se llama cuando el motor se ha eliminado correctamente.

Parámetros:  
* **context**: contexto que se pasa a la operación.


  
### <a name="ondeleteengineerror"></a>OnDeleteEngineError
Se llama cuando la eliminación de un motor originó un error.

Parámetros:  
* **error**: el error que hace que la operación de eliminación del motor produzca un error. 


* **context**: contexto que se pasa a la operación.

