# <a name="class-mipprotectionenginesettings"></a>clase mip::ProtectionEngine::Settings 
[Configuración](class_mip_protectionengine_settings.md) utilizada por [ProtectionEngine](class_mip_protectionengine.md) durante su creación y a lo largo de su vigencia.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  Constructor [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) para crear un nuevo motor.
 public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  Constructor [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) para cargar un motor existente.
 public const std::string& GetEngineId() const  |  Obtiene el identificador del motor.
 public void SetEngineId(const std::string& engineId)  |  Establece el identificador del motor.
 public const Identity& GetIdentity() const  |  Obtiene la identidad de usuario asociada al motor.
 public void SetIdentity(const Identity& identity)  |  Establece la identidad de usuario asociada al motor.
 public const std::string& GetClientData() const  |  Obtiene los datos personalizados especificados por el cliente.
 public const std::string& GetLocale() const  |  Obtiene la configuración regional en la que se escribirán los datos del motor.
public void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& value)  |  Establece pares de nombre/valor que se usan para pruebas y experimentación.
public const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const  |  Obtiene pares de nombre/valor que se usan para pruebas y experimentación.
 public void SetSessionId(const std::string& sessionId)  |  Establece el identificador de sesión del motor, utilizado para la correlación de telemetría y registro.
 public const std::string& GetSessionId() const  |  Obtiene el identificador de sesión del motor.
 public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  Establece la dirección URL base del punto de conexión en la nube, que se usa para especificar los límites de la nube.
 public const std::string& GetCloudEndpointBaseUrl() const  |  Obtiene el valor de cloudEndpointBaseUrl.
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Constructor [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) para crear un nuevo motor.

Parámetros:  
* **identity**: identidad que se asociará con [ProtectionEngine](class_mip_protectionengine.md)


* **clientData**: datos de cliente personalizables que pueden almacenarse con el motor durante la descarga y pueden recuperarse de un motor cargado. 


* **locale**: la salida del motor se proporcionará en esta configuración regional; el valor predeterminado es "en-US".


  
### <a name="settings"></a>Configuración
Constructor [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) para cargar un motor existente.

Parámetros:  
* **engineId**: identificador único del motor que se va a cargar 


* **clientData**: datos de cliente personalizables que pueden almacenarse con el motor durante la descarga y pueden recuperarse de un motor cargado. 


* **locale**: la salida del motor se proporcionará en esta configuración regional; el valor predeterminado es "en-US".


  
### <a name="getengineid"></a>GetEngineId
Obtiene el identificador del motor.

  
**Devuelve**: identificador de motor
  
### <a name="setengineid"></a>SetEngineId
Establece el identificador del motor.

Parámetros:  
* **engineId**: identificador del motor.


  
### <a name="getidentity"></a>GetIdentity
Obtiene la identidad de usuario asociada al motor.

  
**Devuelve**: identidad de usuario asociada al motor
  
### <a name="setidentity"></a>SetIdentity
Establece la identidad de usuario asociada al motor.

Parámetros:  
* **identity**: identidad de usuario asociada al motor


  
### <a name="getclientdata"></a>GetClientData
Obtiene los datos personalizados especificados por el cliente.

  
**Devuelve**: datos personalizados especificados por el cliente
  
### <a name="getlocale"></a>GetLocale
Obtiene la configuración regional en la que se escribirán los datos del motor.

  
**Devuelve**: la configuración regional en la que se escribirán los datos del motor
  
### <a name="setcustomsettings"></a>SetCustomSettings
Establece pares de nombre/valor que se usan para pruebas y experimentación.

Parámetros:  
* **customSettings**: pares de nombre/valor que se usan para pruebas y experimentación.


  
### <a name="getcustomsettings"></a>GetCustomSettings
Obtiene pares de nombre/valor que se usan para pruebas y experimentación.

  
**Devuelve**: pares de nombre/valor que se usan para pruebas y experimentación.
  
### <a name="setsessionid"></a>SetSessionId
Establece el identificador de sesión del motor, utilizado para la correlación de telemetría y registro.

Parámetros:  
* **sessionId**: identificador de sesión del motor, utilizado para la correlación de telemetría/registro


  
### <a name="getsessionid"></a>GetSessionId
Obtiene el identificador de sesión del motor.

  
**Devuelve**: identificador de sesión del motor
  
### <a name="setcloudendpointbaseurl"></a>SetCloudEndpointBaseUrl
Establece la dirección URL base del punto de conexión en la nube, que se usa para especificar los límites de la nube.

Parámetros:  
* **cloudEndpointBaseUrl**: dirección URL base asociada a los puntos de conexión de la protección


  
### <a name="getcloudendpointbaseurl"></a>GetCloudEndpointBaseUrl
Obtiene el valor de cloudEndpointBaseUrl.

  
**Devuelve**: dirección URL base asociada a los puntos de conexión de la protección