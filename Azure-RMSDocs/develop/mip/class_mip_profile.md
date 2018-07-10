# <a name="class-mipprofile"></a>clase mip::Profile 
La clase [Profile](class_mip_profile.md) es la clase raíz para el uso de las operaciones de Microsoft Information Protection. Una aplicación típica solo necesitará un [perfil ](class_mip_profile.md) pero puede crear varios perfiles si es necesario.
  
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

  
**Devuelve**: configuración establecida en el perfil.
  
### <a name="listenginesasync"></a>ListEnginesAsync
Inicia la operación de los motores de la lista.

Parámetros:  
* **context**: un parámetro que se pasará en las funciones de observador. 


Se llamará a [Profile::Observer](class_mip_profile_observer.md) después de la realización correcta o de un error.
  
### <a name="unloadengineasync"></a>UnloadEngineAsync
Inicia la descarga el motor de directivas con el identificador especificado.

Parámetros:  
* **id**: el identificador único del motor. 


* **context**: un parámetro que se pasará en las funciones de observador. 


Se llamará a [Profile::Observer](class_mip_profile_observer.md) después de la realización correcta o de un error.
  
### <a name="addengineasync"></a>AddEngineAsync
Comienza a agregar un nuevo motor de directivas al perfil.

Parámetros:  
* **settings**: el objeto [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md) que especifica los parámetros del motor. 


* **context**: un parámetro que se pasará en las funciones de observador. 


Se llamará a [Profile::Observer](class_mip_profile_observer.md) después de la realización correcta o de un error.
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
Inicia la eliminación del motor de directivas con el identificador especificado. Todos los datos para el perfil dado se eliminarán completamente.

Parámetros:  
* **id**: el identificador único del motor. 


* **context**: un parámetro que se pasará en las funciones de observador. 


Se llamará a [Profile::Observer](class_mip_profile_observer.md) después de la realización correcta o de un error.