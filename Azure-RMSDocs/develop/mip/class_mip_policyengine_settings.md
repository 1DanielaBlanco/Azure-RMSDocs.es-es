# <a name="class-mippolicyenginesettings"></a>clase mip::PolicyEngine::Settings 
Se debe proporcionar una instancia de esta clase con los parámetros apropiados para iniciar un motor.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
`public inline Settings(const std::string& id, const std::string& clientData, const std::string& locale)`  |  Construir una instancia con los parámetros especificados. Utilícelo para crear una [configuración](#classmip_1_1_policy_engine_1_1_settings) para llamar a LoadEngineAsync y cargar un nuevo motor.
`public inline Settings(const Identity& identity, const std::string& clientData, const std::string& locale)`  |  Utilícelo para crear una [configuración](#classmip_1_1_policy_engine_1_1_settings) para llamar a AddEngineAsync y agregar un nuevo motor.
`public inline const std::string& GetId() const`  |  Obtiene el identificador del motor.
`public inline void SetId(const std::string& id)`  |  Establece el identificador del motor.
`public inline const Identity& GetIdentity() const`  |  Obtiene el objeto Identity.
`public inline void SetIdentity(const Identity& identity)`  |  Establece el objeto Identity.
`public inline const std::string& GetClientData() const`  |  Obtiene los datos de cliente establecidos en la configuración.
`public inline void SetClientData(const std::string& clientData)`  |  Establece la cadena de datos de cliente.
`public inline const std::string& GetLocale() const`  |  Obtiene la configuración regional establecida en la configuración.
`public inline void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& customSettings)`  |  Establece la configuración personalizada, que se utiliza para el acceso y las pruebas de características.
`public inline const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const`  |  Establece la configuración personalizada, que se utiliza para el acceso y las pruebas de características.
`public inline void SetSessionId(const std::string& sessionId)`  |  Establece el identificador de sesión que se usa para la telemetría definida por el cliente.
`public inline const std::string& GetSessionId() const`  |  Obtiene el identificador de sesión, un identificador único.
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Construir una instancia con los parámetros especificados. Utilícelo para crear una [configuración](#classmip_1_1_policy_engine_1_1_settings) para llamar a LoadEngineAsync y cargar un nuevo motor.
  
#### <a name="parameters"></a>Parámetros
* id Establézcalo en la identificación única del motor generada por AddEngineAsync o en una autogenerada. Cuando se carga un motor existente, se reutiliza el identificador; de lo contrario, se creará un nuevo motor. 
* clientData Datos de cliente personalizables que pueden almacenarse con el motor durante la descarga, puede recuperarse de un motor cargado. 
* locale La salida localizable del motor se proporcionará en esta configuración regional, el valor predeterminado es "en-US".
  
### <a name="settings"></a>Configuración
Utilícelo para crear una [configuración](#classmip_1_1_policy_engine_1_1_settings) para llamar a AddEngineAsync y agregar un nuevo motor.
  
#### <a name="parameters"></a>Parámetros
* identity Identificador único del usuario para el que debe agregarse el motor. 
* clientData Datos de cliente personalizables que pueden almacenarse con el motor durante la descarga, puede recuperarse de un motor cargado. 
* La salida localizable del motor se proporciona en esta configuración regional, y el valor predeterminado es `en-US`.
  
### <a name="getid"></a>GetId
Obtiene el identificador del motor.
  
#### <a name="returns"></a>Devuelve
Una cadena única que identifica al motor.
  
### <a name="setid"></a>SetId
Establece el identificador del motor.
  
#### <a name="parameters"></a>Parámetros
* Identificador del motor.
  
### <a name="getidentity"></a>GetIdentity
Obtiene el objeto Identity.
  
#### <a name="returns"></a>Devuelve
Referencia a la identidad en el objeto de configuración. 
**Consulte también**: mip::Identity
  
### <a name="setidentity"></a>SetIdentity
Establece el objeto Identity.
  
#### <a name="parameters"></a>Parámetros
* identity La identidad única de un usuario. 
**Consulte también**: mip::Identity
  
### <a name="getclientdata"></a>GetClientData
Obtiene los datos de cliente establecidos en la configuración.
  
#### <a name="returns"></a>Devuelve
Una cadena de datos especificada por el cliente.
  
### <a name="setclientdata"></a>SetClientData
Establece la cadena de datos de cliente.
  
#### <a name="parameters"></a>Parámetros
* clientData Datos especificados por el usuario.
  
### <a name="getlocale"></a>GetLocale
Obtiene la configuración regional establecida en la configuración.
  
#### <a name="returns"></a>Devuelve
La configuración regional
  
### <a name="setcustomsettings"></a>SetCustomSettings
Establece la configuración personalizada, que se utiliza para el acceso y las pruebas de características.
  
#### <a name="parameters"></a>Parámetros
* customSettings Lista de pares nombre/valor.
  
### <a name="getcustomsettings"></a>GetCustomSettings
Establece la configuración personalizada, que se utiliza para el acceso y las pruebas de características.
  
#### <a name="parameters"></a>Parámetros
* Lista de pares nombre-valor.
  
### <a name="setsessionid"></a>SetSessionId
Establece el identificador de sesión que se usa para la telemetría definida por el cliente.
  
#### <a name="parameters"></a>Parámetros
* sessionId Una cadena única que se conecta a eventos de telemetría.
  
### <a name="getsessionid"></a>GetSessionId
Obtiene el identificador de sesión, un identificador único.
  
#### <a name="returns"></a>Devuelve
Identificador de sesión.