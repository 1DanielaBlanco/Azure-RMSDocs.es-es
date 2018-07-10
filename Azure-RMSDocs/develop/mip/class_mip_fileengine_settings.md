# <a name="class-mipfileenginesettings"></a>clase mip::FileEngine::Settings 
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  Crea una instancia con los parámetros especificados.
 public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  Crea una instancia con los parámetros especificados.
 public const std::string& GetEngineId() const  |  Devuelve el identificador del motor.
 public const Identity& GetIdentity() const  |  Devuelve la identidad del motor.
 public void SetIdentity(const Identity& identity)  |  Establece la identidad del motor.
 public const std::string& GetClientData() const  |  Devuelve los datos de cliente de motor.
 public const std::string& GetLocale() const  |  Devuelve la configuración regional del motor.
public void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& value)  |  Establece una lista de pares de nombre/valor que se usa para pruebas y experimentación.
public const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const  |  Obtiene una lista de pares de nombre/valor que se usa para pruebas y experimentación.
 public void SetSessionId(const std::string& sessionId)  |  Establece el identificador de sesión del motor.
 public const std::string& GetSessionId() const  |  Devuelve el identificador de sesión del motor.
 public void SetProtectionCloudEndpointBaseUrl(const std::string& protectionCloudEndpointBaseUrl)  |  Establece la dirección URL base del punto de conexión en la nube de protección, que se usa para especificar los límites de la nube.
 public const std::string& GetProtectionCloudEndpointBaseUrl() const  |  Obtiene el valor de cloudEndpointBaseUrl.
 public void SetProtectionOnlyEngine(const bool protectionOnly)  |  Establece el indicador de motor solo de protección: sin directiva/etiqueta
 public const bool IsProtectionOnlyEngine() const  |  Devuelve el indicador de motor solo de protección: sin directiva/etiqueta
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Crea una instancia con los parámetros especificados.
Utilícelo para crear una [configuración](class_mip_fileengine_settings.md) para llamar a LoadEngineAsync y cargar un motor existente (agregado previamente mediante AddEngineAsync).

Parámetros:  
* **engineId**: establézcalo en la identificación única del motor generada por AddEngineAsync.


  
### <a name="settings"></a>Configuración
Crea una instancia con los parámetros especificados.
Utilícelo para crear una [configuración](class_mip_fileengine_settings.md) para llamar a AddEngineAsync y agregar un nuevo motor.

Parámetros:  
* **identity**: información de identidad del usuario para el que se necesita agregar el motor.


  
### <a name="getengineid"></a>GetEngineId
Devuelve el identificador del motor.
  
### <a name="getidentity"></a>GetIdentity
Devuelve la identidad del motor.
  
### <a name="setidentity"></a>SetIdentity
Establece la identidad del motor.
  
### <a name="getclientdata"></a>GetClientData
Devuelve los datos de cliente de motor.
  
### <a name="getlocale"></a>GetLocale
Devuelve la configuración regional del motor.
  
### <a name="setcustomsettings"></a>SetCustomSettings
Establece una lista de pares de nombre/valor que se usa para pruebas y experimentación.
  
### <a name="getcustomsettings"></a>GetCustomSettings
Obtiene una lista de pares de nombre/valor que se usa para pruebas y experimentación.
  
### <a name="setsessionid"></a>SetSessionId
Establece el identificador de sesión del motor.
  
### <a name="getsessionid"></a>GetSessionId
Devuelve el identificador de sesión del motor.
  
### <a name="setprotectioncloudendpointbaseurl"></a>SetProtectionCloudEndpointBaseUrl
Establece la dirección URL base del punto de conexión en la nube de protección, que se usa para especificar los límites de la nube.

Parámetros:  
* **protectionCloudEndpointBaseUrl**: dirección URL base asociada a los puntos de conexión de protección.


  
### <a name="getprotectioncloudendpointbaseurl"></a>GetProtectionCloudEndpointBaseUrl
Obtiene el valor de cloudEndpointBaseUrl.

  
**Devuelve**: dirección URL base asociada a los puntos de conexión de la protección
  
### <a name="setprotectiononlyengine"></a>SetProtectionOnlyEngine
Establece el indicador de motor solo de protección: sin directiva/etiqueta
  
### <a name="isprotectiononlyengine"></a>IsProtectionOnlyEngine
Devuelve el indicador de motor solo de protección: sin directiva/etiqueta