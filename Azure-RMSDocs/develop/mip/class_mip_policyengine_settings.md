# <a name="class-mippolicyenginesettings"></a>clase mip::PolicyEngine::Settings 
Se debe proporcionar una instancia de esta clase con los parámetros apropiados para iniciar un motor.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  Construir una instancia con los parámetros especificados. Utilícelo para crear una [configuración](class_mip_policyengine_settings.md) para llamar a LoadEngineAsync y cargar un nuevo motor.
 public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  Utilícelo para crear una [configuración](class_mip_policyengine_settings.md) para llamar a AddEngineAsync y agregar un nuevo motor.
 public const std::string& GetEngineId() const  |  Obtiene el identificador del motor.
 public void SetEngineId(const std::string& id)  |  Establece el identificador del motor.
 public const Identity& GetIdentity() const  |  Obtiene el objeto Identity.
 public void SetIdentity(const Identity& identity)  |  Establece el objeto Identity.
 public const std::string& GetClientData() const  |  Obtiene los datos de cliente establecidos en la configuración.
 public void SetClientData(const std::string& clientData)  |  Establece la cadena de datos de cliente.
 public const std::string& GetLocale() const  |  Obtiene la configuración regional establecida en la configuración.
public void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& customSettings)  |  Establece la configuración personalizada, que se utiliza para el acceso y las pruebas de características.
public const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const  |  Obtiene la configuración personalizada, que se utiliza para el acceso y las pruebas de características.
 public void SetSessionId(const std::string& sessionId)  |  Establece el identificador de sesión que se usa para la telemetría definida por el cliente.
 public const std::string& GetSessionId() const  |  Obtiene el identificador de sesión, un identificador único.
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Construir una instancia con los parámetros especificados. Utilícelo para crear una [configuración](class_mip_policyengine_settings.md) para llamar a LoadEngineAsync y cargar un nuevo motor.

Parámetros:  
* **engineId**: establézcalo en la identificación única del motor generada por AddEngineAsync o en una autogenerada. Cuando se carga un motor existente, se reutiliza el identificador; de lo contrario, se creará un nuevo motor. 


* **clientData**: datos de cliente personalizables que pueden almacenarse con el motor durante la descarga; puede recuperarse de un motor cargado. 


* **locale**: la salida localizable del motor se proporcionará en esta configuración regional; el valor predeterminado es "en-US".


  
### <a name="settings"></a>Configuración
Utilícelo para crear una [configuración](class_mip_policyengine_settings.md) para llamar a AddEngineAsync y agregar un nuevo motor.

Parámetros:  
* **identity**: identificador único del usuario para el que debe agregarse el motor. 


* **clientData**: datos de cliente personalizables que pueden almacenarse con el motor durante la descarga; puede recuperarse de un motor cargado. 


* **locale**: la salida localizable del motor se proporcionará en esta configuración regional; el valor predeterminado es "en-US".


  
### <a name="getengineid"></a>GetEngineId
Obtiene el identificador del motor.

  
**Devuelve**: una cadena única que identifica el motor.
  
### <a name="setengineid"></a>SetEngineId
Establece el identificador del motor.

Parámetros:  
* **id**: identificador del motor.


  
### <a name="getidentity"></a>GetIdentity
Obtiene el objeto Identity.

  
**Devuelve**: una referencia a la identidad en el objeto de configuración. 
  
**Consulte también**: mip::Identity
  
### <a name="setidentity"></a>SetIdentity
Establece el objeto Identity.

Parámetros:  
* **identity**: la identidad única de un usuario. 


  
**Consulte también**: mip::Identity
  
### <a name="getclientdata"></a>GetClientData
Obtiene los datos de cliente establecidos en la configuración.

  
**Devuelve**: una cadena de datos especificada por el cliente.
  
### <a name="setclientdata"></a>SetClientData
Establece la cadena de datos de cliente.

Parámetros:  
* **clientData**: datos especificados por el usuario.


  
### <a name="getlocale"></a>GetLocale
Obtiene la configuración regional establecida en la configuración.

  
**Devuelve**: la configuración regional.
  
### <a name="setcustomsettings"></a>SetCustomSettings
Establece la configuración personalizada, que se utiliza para el acceso y las pruebas de características.

Parámetros:  
* **customSettings**: lista de pares nombre-valor.


  
### <a name="getcustomsettings"></a>GetCustomSettings
Obtiene la configuración personalizada, que se utiliza para el acceso y las pruebas de características.

  
**Devuelve**: lista de pares nombre-valor.
  
### <a name="setsessionid"></a>SetSessionId
Establece el identificador de sesión que se usa para la telemetría definida por el cliente.

Parámetros:  
* **sessionId**: una cadena única que se conecta a eventos de telemetría.


  
### <a name="getsessionid"></a>GetSessionId
Obtiene el identificador de sesión, un identificador único.

  
**Devuelve**: el identificador de sesión.