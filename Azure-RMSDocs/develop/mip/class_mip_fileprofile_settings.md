# <a name="class-mipfileprofilesettings"></a>clase mip::FileProfile::Settings 
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, std::shared_ptr<AuthDelegate> authDelegate, std::shared_ptr<Observer> observer, const ApplicationInfo& applicationInfo)  |  Interfaz para configurar el perfil.
 public ~Settings()  | _No se ha documentado todavía._
 public const std::string& GetPath() const  | _No se ha documentado todavía._
 public bool GetUseInMemoryStorage() const  | _No se ha documentado todavía._
public std::shared_ptr<AuthDelegate> GetAuthDelegate() const  | _No se ha documentado todavía._
public std::shared_ptr<Observer> GetObserver() const  | _No se ha documentado todavía._
 public const ApplicationInfo GetApplicationInfo() const  | _No se ha documentado todavía._
 public bool GetSkipTelemetryInit() const  | _No se ha documentado todavía._
 public void SetSkipTelemetryInit()  | _No se ha documentado todavía._
 public void SetSessionId(const std::string& sessionId)  |  Establece el identificador de sesión del perfil.
 public const std::string& GetSessionId() const  |  Devuelve el identificador de sesión del perfil.
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Interfaz para configurar el perfil.

Parámetros:  
* **observer**: una clase que implementa la interfaz [FileHandler::Observer](class_mip_filehandler_observer.md). Puede se nullptr.


  
### <a name="settings"></a>~Settings
_No se ha documentado todavía._

  
### <a name="getpath"></a>GetPath
_No se ha documentado todavía._

  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
_No se ha documentado todavía._

  
### <a name="getauthdelegate"></a>GetAuthDelegate
_No se ha documentado todavía._

  
### <a name="observer"></a>Observador
_No se ha documentado todavía._

  
### <a name="applicationinfo"></a>ApplicationInfo
_No se ha documentado todavía._

  
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
_No se ha documentado todavía._

  
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
_No se ha documentado todavía._

  
### <a name="setsessionid"></a>SetSessionId
Establece el identificador de sesión del perfil.
  
### <a name="getsessionid"></a>GetSessionId
Devuelve el identificador de sesión del perfil.