# <a name="class-mipfileprofilesettings"></a>clase mip::FileProfile::Settings 
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public inline  SettingsObserver > observer,const ApplicationInfo & applicationInfo) | Interfaz para configurar el perfil.
public inline  ~Settings | 
public inline const std::string & GetPath | 
public inline bool GetUseInMemoryStorage | 
public inline std::shared_ptr< AuthDelegate > GetAuthDelegate | 
public inline std::shared_ptr< Observer > GetObserver | 
public inline const ApplicationInfo GetApplicationInfo | 
public inline bool GetSkipTelemetryInit | 
public inline void SetSkipTelemetryInit | 
public inline void SetSessionId | Establece el identificador de sesión del perfil.
public inline const std::string & GetSessionId | Devuelve el identificador de sesión del perfil.
## <a name="members"></a>Miembros
### <a name="settings"></a>Configuración
Interfaz para configurar el perfil.
#### <a name="parameters"></a>Parámetros
* observer Una clase que implementa la interfaz [FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer). Puede se nullptr.
### <a name="settings"></a>~Settings
### <a name="getpath"></a>GetPath
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
### <a name="getauthdelegate"></a>GetAuthDelegate
### <a name="observer"></a>Observador
### <a name="applicationinfo"></a>ApplicationInfo
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
### <a name="setsessionid"></a>SetSessionId
Establece el identificador de sesión del perfil.
### <a name="getsessionid"></a>GetSessionId
Devuelve el identificador de sesión del perfil.