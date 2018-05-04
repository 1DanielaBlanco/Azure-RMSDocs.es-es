# <a name="class-mipfileprofile"></a>clase mip::FileProfile 
La clase [FileProfile](#classmip_1_1_file_profile) es la clase raíz para el uso de las operaciones de Microsoft Information Protection.
Una aplicación típica solo necesitará un [perfil ](#classmip_1_1_profile) pero puede crear varios perfiles si es necesario.
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public inline virtual  ~FileProfile | 
public const Settings & GetSettings | Devuelve la configuración del perfil.
public void ListEnginesAsync | Inicia la operación de los motores de la lista.
public void UnloadEngineAsync | Inicia la descarga el motor de archivos con el identificador especificado.
public void AddEngineAsyncFileEngine::Settings & settings,const std::shared_ptr< void > & context) | Comienza a agregar un nuevo motor de archivos al perfil.
public void DeleteEngineAsync | Inicia la eliminación del motor de archivos con el identificador especificado. Todos los datos para el perfil dado se eliminarán completamente.
protected inline  FileProfile | 
## <a name="members"></a>Miembros
### <a name="fileprofile"></a>~FileProfile
### <a name="settings"></a>Configuración
Devuelve la configuración del perfil.
### <a name="listenginesasync"></a>ListEnginesAsync
Inicia la operación de los motores de la lista.
Se llamará a [FileProfile::Observer](#classmip_1_1_file_profile_1_1_observer) después de la realización correcta o de un error.
### <a name="unloadengineasync"></a>UnloadEngineAsync
Inicia la descarga el motor de archivos con el identificador especificado. Se llamará a [FileProfile::Observer](#classmip_1_1_file_profile_1_1_observer) después de la realización correcta o de un error.
### <a name="addengineasync"></a>AddEngineAsync
Comienza a agregar un nuevo motor de archivos al perfil.
Se llamará a [FileProfile::Observer](#classmip_1_1_file_profile_1_1_observer) después de la realización correcta o de un error.
### <a name="deleteengineasync"></a>DeleteEngineAsync
Inicia la eliminación del motor de archivos con el identificador especificado. Todos los datos para el perfil dado se eliminarán completamente.
Se llamará a [FileProfile::Observer](#classmip_1_1_file_profile_1_1_observer) después de la realización correcta o de un error.
### <a name="fileprofile"></a>FileProfile