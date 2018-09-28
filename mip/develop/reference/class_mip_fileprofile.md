# <a name="class-mipfileprofile"></a>clase mip::FileProfile 
La clase [FileProfile](class_mip_fileprofile.md) es la clase raíz para el uso de las operaciones de Microsoft Information Protection.
Una aplicación típica solo necesitará un [perfil ](class_mip_profile.md) pero puede crear varios perfiles si es necesario.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Devuelve la configuración del perfil.
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  Inicia la operación de los motores de la lista.
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  Inicia la descarga el motor de archivos con el identificador especificado.
public void AddEngineAsync(const FileEngine::Settings& settings, const std::shared_ptr<void>& context)  |  Comienza a agregar un nuevo motor de archivos al perfil.
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  Inicia la eliminación del motor de archivos con el identificador especificado. Todos los datos para el perfil dado se eliminarán completamente.
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Devuelve la configuración del perfil.
  
### <a name="listenginesasync"></a>ListEnginesAsync
Inicia la operación de los motores de la lista.
Se llamará a [FileProfile::Observer](class_mip_fileprofile_observer.md) después de la realización correcta o de un error.
  
### <a name="unloadengineasync"></a>UnloadEngineAsync
Inicia la descarga el motor de archivos con el identificador especificado. Se llamará a [FileProfile::Observer](class_mip_fileprofile_observer.md) después de la realización correcta o de un error.
  
### <a name="addengineasync"></a>AddEngineAsync
Comienza a agregar un nuevo motor de archivos al perfil.
Se llamará a [FileProfile::Observer](class_mip_fileprofile_observer.md) después de la realización correcta o de un error.
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
Inicia la eliminación del motor de archivos con el identificador especificado. Todos los datos para el perfil dado se eliminarán completamente.
Se llamará a [FileProfile::Observer](class_mip_fileprofile_observer.md) después de la realización correcta o de un error.