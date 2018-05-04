# <a name="class-mipprofileobserver"></a>clase mip::Profile::Observer 
Interfaz de [Observer](#classmip_1_1_profile_1_1_observer) para que los clientes obtengan notificaciones de eventos relacionados con el perfil.
Si *se produce el evento de error, el objeto de error se almacena en la clase [mip::Error](#classmip_1_1_error). El cliente no debe volver a llamar al motor en el subproceso que llama al observador.
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public inline virtual void OnLoadSuccessProfile > & profile,const std::shared_ptr< void > & context) | Se llama cuando se cargó correctamente el perfil.
public inline virtual void OnLoadFailure | Se llama al cargar un perfil que ha causado un error.
public inline virtual void OnListEnginesSuccess | Se llama cuando la lista de motores se generó correctamente.
public inline virtual void OnListEnginesError | Se llama cuando los motores enumerados causan un error.
public inline virtual void OnUnloadEngineSuccess | Se llama cuando el motor se ha descargado correctamente.
public inline virtual void OnUnloadEngineError | Se llama al descargar un motor que ha causado un error.
public inline virtual void OnAddEngineSuccessPolicyEngine > & engine,const std::shared_ptr< void > & context) | Se llama cuando un nuevo motor se agregó correctamente.
public inline virtual void OnAddEngineError | Se llama cuando se produce un error al agregar un nuevo motor.
public inline virtual void OnDeleteEngineSuccess | Se llama cuando el motor se ha eliminado correctamente.
public inline virtual void OnDeleteEngineError | Se llama al eliminar un motor que ha causado un error.
public inline virtual void OnPolicyChanged | Se llama cuando la directiva ha cambiado para el motor con el identificador especificado.
## <a name="members"></a>Miembros
### <a name="onloadsuccess"></a>OnLoadSuccess
Se llama cuando se cargó correctamente el perfil.
#### <a name="parameters"></a>Parámetros
* profile El perfil actual usado para iniciar la operación. 
* context Contexto que se pasa a la operación.
### <a name="onloadfailure"></a>OnLoadFailure
Se llama al cargar un perfil que ha causado un error.
#### <a name="parameters"></a>Parámetros
* error El error que hace que la operación de carga produzca un error. 
* context Contexto que se pasa a la operación.
### <a name="onlistenginessuccess"></a>OnListEnginesSuccess
Se llama cuando la lista de motores se generó correctamente.
#### <a name="parameters"></a>Parámetros
* engineIds Una lista de identificadores de motor que están disponibles. 
* context Contexto que se pasa a la operación.
### <a name="onlistengineserror"></a>OnListEnginesError
Se llama cuando los motores enumerados causan un error.
#### <a name="parameters"></a>Parámetros
* error El error que hace que la operación de listado del motor produzca un error. 
* context Contexto que se pasa a la operación.
### <a name="onunloadenginesuccess"></a>OnUnloadEngineSuccess
Se llama cuando el motor se ha descargado correctamente.
#### <a name="parameters"></a>Parámetros
* context Contexto que se pasa a la operación.
### <a name="onunloadengineerror"></a>OnUnloadEngineError
Se llama al descargar un motor que ha causado un error.
#### <a name="parameters"></a>Parámetros
* error El error que hace que la operación de carga del motor produzca un error. 
* context Contexto que se pasa a la operación.
### <a name="onaddenginesuccess"></a>OnAddEngineSuccess
Se llama cuando un nuevo motor se agregó correctamente.
### <a name="onaddengineerror"></a>OnAddEngineError
Se llama cuando se produce un error al agregar un nuevo motor.
#### <a name="parameters"></a>Parámetros
* error El error que hace que la operación de adición del motor produzca un error. 
* context Contexto que se pasa a la operación.
### <a name="ondeleteenginesuccess"></a>OnDeleteEngineSuccess
Se llama cuando el motor se ha eliminado correctamente.
#### <a name="parameters"></a>Parámetros
* context Contexto que se pasa a la operación.
### <a name="ondeleteengineerror"></a>OnDeleteEngineError
Se llama al eliminar un motor que ha causado un error.
#### <a name="parameters"></a>Parámetros
* error El error que hace que la operación de eliminación del motor produzca un error. 
* context Contexto que se pasa a la operación.
### <a name="onpolicychanged"></a>OnPolicyChanged
Se llama cuando la directiva ha cambiado para el motor con el identificador especificado.
#### <a name="parameters"></a>Parámetros
* engineId El motor para cargar la nueva directiva es necesario para volver a llamar a AddEngineAsync con el identificador del motor especificado.