# <a name="class-mipfileenginesettings"></a>clase mip::FileEngine::Settings 
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public inline  Settings | Crea una instancia con los parámetros especificados.
public inline  Settings | Crea una instancia con los parámetros especificados.
public inline const std::string & GetId | Devuelve el identificador del motor.
public inline const Identity & GetIdentity | Devuelve la identidad del motor.
public inline void SetIdentity | Establece la identidad del motor.
public inline const std::string & GetClientData | Devuelve los datos de cliente de motor.
public inline const std::string & GetLocale | Devuelve la configuración regional del motor.
public inline void SetCustomSettings | Establece una lista de pares de nombre/valor que se usa para pruebas y experimentación.
public inline const std::vector< std::pair< std::string, std::string > > & GetCustomSettings | Obtiene una lista de pares de nombre/valor que se usa para pruebas y experimentación.
public inline void SetSessionId | Establece el identificador de sesión del motor.
public inline const std::string & GetSessionId | Devuelve el identificador de sesión del motor.
## <a name="members"></a>Miembros
### <a name="settings"></a>Configuración
Crea una instancia con los parámetros especificados.
Utilícelo para crear una [configuración](#classmip_1_1_file_engine_1_1_settings) para llamar a LoadEngineAsync y cargar un motor existente (agregado previamente mediante AddEngineAsync).
#### <a name="parameters"></a>Parámetros
* id Establézcalo en la identificación única del motor generada por AddEngineAsync.
### <a name="settings"></a>Configuración
Crea una instancia con los parámetros especificados.
Utilícelo para crear una [configuración](#classmip_1_1_file_engine_1_1_settings) para llamar a AddEngineAsync y agregar un nuevo motor.
#### <a name="parameters"></a>Parámetros
* identity Información de identidad del usuario para el que se necesita agregar el motor.
### <a name="getid"></a>GetId
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