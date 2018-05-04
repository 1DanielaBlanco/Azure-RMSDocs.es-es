# <a name="class-mippolicyenginesettings"></a>clase mip::PolicyEngine::Settings 
Se debe proporcionar una instancia de esta clase con los parámetros apropiados para iniciar un motor.
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public inline  Settings public inline  Settings public inline const std::string & GetId | Obtiene el identificador del motor. public inline void SetId | Establece el identificador del motor. public inline const Identity & GetIdentity | Obtiene el objeto Identity.
public inline void SetIdentity | Establece el objeto Identity.
public inline const std::string &amp; GetClientData | Obtiene el conjunto de datos de cliente en la configuración.
public inline void SetClientData | Establece la cadena de datos de cliente.
public inline const std::string & GetLocale | Obtiene el conjunto de configuración regional del cliente en la configuración.
public inline void SetCustomSettings | Establece la configuración personalizada, utilizada para la característica de acceso y pruebas.
public inline const std::vector< std::pair< std::string, std::string > > & GetCustomSettings | Establece la configuración personalizada, utilizada para el acceso y pruebas de la característica.
public inline void SetSessionId | Establece el identificador de sesión que se utiliza para la telemetría definida por el cliente.
public inline const std::string & GetSessionId | Obtiene el identificador de sesión, un identificador único.
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
* locale La salida localizable del motor se proporcionará en esta configuración regional, el valor predeterminado es "en-US".
### <a name="getid"></a>GetId
Obtiene el identificador del motor.
#### <a name="returns"></a>Devuelve
Una cadena única que identifica al motor.
### <a name="setid"></a>SetId
Establece el identificador del motor.
#### <a name="parameters"></a>Parámetros
* id Identificador de motor.
### <a name="getidentity"></a>GetIdentity
Obtiene el objeto Identity.
#### <a name="returns"></a>Devuelve
Una referencia a la identidad en el objeto de configuración. 
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
Establece el identificador de sesión que se utiliza para la telemetría definida por el cliente.
#### <a name="parameters"></a>Parámetros
* sessionId Una cadena única que se conecta a eventos de telemetría.
### <a name="getsessionid"></a>GetSessionId
Obtiene el identificador de sesión, un identificador único.
#### <a name="returns"></a>Devuelve
El identificador de sesión.