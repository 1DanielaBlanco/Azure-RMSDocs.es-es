# <a name="class-mipprofile"></a>clase mip::Profile 
La clase [Profile](#classmip_1_1_profile) es la clase raíz para el uso de las operaciones de Microsoft Information Protection. Una aplicación típica solo necesitará un [perfil ](#classmip_1_1_profile) pero puede crear varios perfiles si es necesario.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Obtiene la configuración establecida en el perfil.
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  Inicia la operación de los motores de la lista.
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  Inicia la descarga el motor de directivas con el identificador especificado.
public void AddEngineAsync(const PolicyEngine::Settings& settings, const std::shared_ptr<void>& context)  |  Comienza a agregar un nuevo motor de directivas al perfil.
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  Inicia la eliminación del motor de directivas con el identificador especificado. Todos los datos para el perfil dado se eliminarán completamente.
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Obtiene la configuración establecida en el perfil.
  
#### <a name="returns"></a>Devuelve
Configuración establecida en el perfil.
  
### <a name="listenginesasync"></a>ListEnginesAsync
Inicia la operación de los motores de la lista.
  
#### <a name="parameters"></a>Parámetros
* context Un parámetro que se pasará en las funciones de observador. 
Se llamará a [Profile::Observer](#classmip_1_1_profile_1_1_observer) después de la realización correcta o de un error.
  
### <a name="unloadengineasync"></a>UnloadEngineAsync
Inicia la descarga el motor de directivas con el identificador especificado.
  
#### <a name="parameters"></a>Parámetros
* id El identificador único del motor. 
* context Un parámetro que se pasará en las funciones de observador. 
Se llamará a [Profile::Observer](#classmip_1_1_profile_1_1_observer) después de la realización correcta o de un error.
  
### <a name="addengineasync"></a>AddEngineAsync
Comienza a agregar un nuevo motor de directivas al perfil.
  
#### <a name="parameters"></a>Parámetros
* settings El objeto [mip::PolicyEngine::Settings](#classmip_1_1_policy_engine_1_1_settings) que especifica los parámetros del motor. 
* context Un parámetro que se pasará en las funciones de observador. 
Se llamará a [Profile::Observer](#classmip_1_1_profile_1_1_observer) después de la realización correcta o de un error.
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
Inicia la eliminación del motor de directivas con el identificador especificado. Todos los datos para el perfil dado se eliminarán completamente.
  
#### <a name="parameters"></a>Parámetros
* id El identificador único del motor. 
* context Un parámetro que se pasará en las funciones de observador. 
Se llamará a [Profile::Observer](#classmip_1_1_profile_1_1_observer) después de la realización correcta o de un error.