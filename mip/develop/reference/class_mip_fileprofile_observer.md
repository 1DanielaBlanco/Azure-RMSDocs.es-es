# <a name="class-mipfileprofileobserver"></a>clase mip::FileProfile::Observer 
Interfaz de [Observer](class_mip_fileprofile_observer.md) para que los clientes obtengan notificaciones de eventos relacionados con el perfil.
Si *se produce el evento de error, el objeto de error se almacena en la clase [mip::Error](class_mip_error.md). El cliente no debe volver a llamar al motor en el subproceso que llama al observador.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public virtual ~Observer()  | _No se ha documentado todavía._
public virtual void OnLoadSuccess(const std::shared_ptr<mip::FileProfile>& profile, const std::shared_ptr<void>& context)  |  Se llama cuando se cargó correctamente el perfil.
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama al cargar un perfil que ha causado un error.
public virtual void OnListEnginesSuccess(const std::vector<std::string>& engineIds, const std::shared_ptr<void>& context)  |  Se llama cuando la lista de motores se generó correctamente.
public virtual void OnListEnginesError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando los motores enumerados causan un error.
public virtual void OnUnloadEngineSuccess(const std::shared_ptr<void>& context)  |  Se llama cuando el motor se ha descargado correctamente.
public virtual void OnUnloadEngineError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama al descargar un motor que ha causado un error.
public virtual void OnAddEngineSuccess(const std::shared_ptr<mip::FileEngine>& engine, const std::shared_ptr<void>& context)  |  Se llama cuando un nuevo motor se agregó correctamente.
public virtual void OnAddEngineError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando se produce un error al agregar un nuevo motor.
public virtual void OnDeleteEngineSuccess(const std::shared_ptr<void>& context)  |  Se llama cuando el motor se ha eliminado correctamente.
public virtual void OnDeleteEngineError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama al eliminar un motor que ha causado un error.
 public virtual void OnPolicyChanged(const std::string& engineId)  |  Se llama cuando la directiva ha cambiado para el motor con el identificador especificado.
 protected Observer()  | _No se ha documentado todavía._
  
## <a name="members"></a>Miembros
  
### <a name="observer"></a>~Observer
_No se ha documentado todavía._

  
### <a name="onloadsuccess"></a>OnLoadSuccess
Se llama cuando se cargó correctamente el perfil.
  
### <a name="onloadfailure"></a>OnLoadFailure
Se llama al cargar un perfil que ha causado un error.
  
### <a name="onlistenginessuccess"></a>OnListEnginesSuccess
Se llama cuando la lista de motores se generó correctamente.
  
### <a name="onlistengineserror"></a>OnListEnginesError
Se llama cuando los motores enumerados causan un error.
  
### <a name="onunloadenginesuccess"></a>OnUnloadEngineSuccess
Se llama cuando el motor se ha descargado correctamente.
  
### <a name="onunloadengineerror"></a>OnUnloadEngineError
Se llama al descargar un motor que ha causado un error.
  
### <a name="onaddenginesuccess"></a>OnAddEngineSuccess
Se llama cuando un nuevo motor se agregó correctamente.
  
### <a name="onaddengineerror"></a>OnAddEngineError
Se llama cuando se produce un error al agregar un nuevo motor.
  
### <a name="ondeleteenginesuccess"></a>OnDeleteEngineSuccess
Se llama cuando el motor se ha eliminado correctamente.
  
### <a name="ondeleteengineerror"></a>OnDeleteEngineError
Se llama al eliminar un motor que ha causado un error.
  
### <a name="onpolicychanged"></a>OnPolicyChanged
Se llama cuando la directiva ha cambiado para el motor con el identificador especificado.
  
### <a name="observer"></a>Observador
_No se ha documentado todavía._
