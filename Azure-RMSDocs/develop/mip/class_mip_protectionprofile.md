# <a name="class-mipprotectionprofile"></a>clase mip::ProtectionProfile 
[ProtectionProfile](class_mip_protectionprofile.md) es la clase raíz para realizar las operaciones de protección.
Una aplicación debe crear una clase [ProtectionProfile](class_mip_protectionprofile.md) antes de realizar cualquier operación de protección.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Obtiene la configuración utilizada por [ProtectionProfile](class_mip_protectionprofile.md) durante su inicialización y a lo largo de su vigencia.
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  Inicia la operación de los motores de la lista.
public void AddEngineAsync(const ProtectionEngine::Settings& settings, const std::shared_ptr<void>& context)  |  Comienza a agregar un nuevo motor de protección al perfil.
public void DeleteEngineAsync(const std::string& engineId, const std::shared_ptr<void>& context)  |  Inicia la eliminación del motor de protección con el identificador especificado. Todos los datos para el motor dado se eliminarán completamente.
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Obtiene la configuración utilizada por [ProtectionProfile](class_mip_protectionprofile.md) durante su inicialización y a lo largo de su vigencia.

  
**Devuelve**: [configuración](class_mip_protectionprofile_settings.md) utilizada por [ProtectionProfile](class_mip_protectionprofile.md) durante su inicialización y a lo largo de su vigencia
  
### <a name="listenginesasync"></a>ListEnginesAsync
Inicia la operación de los motores de la lista.

Parámetros:  
* **context**: un parámetro que se pasará en las funciones de observador. 


Se llamará a [Profile::Observer](class_mip_protectionprofile_observer.md) una vez que la operación se complete correctamente o genere un error.
  
### <a name="addengineasync"></a>AddEngineAsync
Comienza a agregar un nuevo motor de protección al perfil.

Parámetros:  
* **settings**: el objeto [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) que especifica los parámetros del motor. 


* **context**: un parámetro que se pasará en las funciones de observador. 


Se llamará a [Profile::Observer](class_mip_protectionprofile_observer.md) una vez que la operación se complete correctamente o genere un error.
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
Inicia la eliminación del motor de protección con el identificador especificado. Todos los datos para el motor dado se eliminarán completamente.

Parámetros:  
* **id**: el identificador único del motor. 


* **context**: un parámetro que se pasará en las funciones de observador. 


Se llamará a [Profile::Observer](class_mip_protectionprofile_observer.md) una vez que la operación se complete correctamente o genere un error.