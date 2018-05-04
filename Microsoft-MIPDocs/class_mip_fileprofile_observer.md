# <a name="class-mipfileprofileobserver"></a>clase mip::FileProfile::Observer 
Interfaz de [Observer](#classmip_1_1_file_profile_1_1_observer) para que los clientes obtengan notificaciones de eventos relacionados con el perfil.
Si *se produce el evento de error, el objeto de error se almacena en la clase [mip::Error](#classmip_1_1_error). El cliente no debe volver a llamar al motor en el subproceso que llama al observador.
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public inline virtual  ~Observer | 
public inline virtual void OnLoadSuccessmip::FileProfile > & profile,const std::shared_ptr< void > & context) | Se llama cuando se cargó correctamente el perfil.
public inline virtual void OnLoadFailure | Se llama al cargar un perfil que ha causado un error.
public inline virtual void OnListEnginesSuccess | Se llama cuando la lista de motores se generó correctamente.
public inline virtual void OnListEnginesError | Se llama cuando los motores enumerados causan un error.
public inline virtual void OnUnloadEngineSuccess | Se llama cuando el motor se ha descargado correctamente.
public inline virtual void OnUnloadEngineError | Se llama al descargar un motor que ha causado un error.
public inline virtual void OnAddEngineSuccessmip::FileEngine > & engine,const std::shared_ptr< void > & context) | Se llama cuando un nuevo motor se agregó correctamente.
public inline virtual void OnAddEngineError | Se llama cuando se produce un error al agregar un nuevo motor.
public inline virtual void OnDeleteEngineSuccess | Se llama cuando el motor se ha eliminado correctamente.
public inline virtual void OnDeleteEngineError | Se llama al eliminar un motor que ha causado un error.
public inline virtual void OnPolicyChanged | Se llama cuando la directiva ha cambiado para el motor con el identificador especificado.
protected inline  Observer | 
## <a name="members"></a>Miembros
### <a name="observer"></a>~Observer
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