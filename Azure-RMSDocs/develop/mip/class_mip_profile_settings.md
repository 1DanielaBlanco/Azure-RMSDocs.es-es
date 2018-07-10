# <a name="class-mipprofilesettings"></a>clase mip::Profile::Settings 
[Configuración](class_mip_profile_settings.md) utilizada por [Profile](class_mip_profile.md) durante su creación y a lo largo de su vigencia.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<Profile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  Interfaz para configurar el perfil.
 public const std::string& GetPath() const  |  Obtiene la ruta de acceso al estado almacenado.
 public bool GetUseInMemoryStorage() const  |  Obtiene la marca de uso de almacenamiento en memoria.
public const std::shared_ptr<AuthDelegate>& GetAuthDelegate() const  |  Obtiene el delegado de autenticación.
public const std::shared_ptr<Profile::Observer>& GetObserver() const  |  Obtiene el observador de eventos.
 public const ApplicationInfo GetApplicationInfo() const  |  Obtiene la información de aplicación.
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  Obtiene el delegado del registrador (si existe) proporcionado por la aplicación.
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  Use la implementación del registrador externo.
 public void OptOutTelemetry()  |  No participa en la recopilación de toda la telemetría.
 public bool IsTelemetryOptedOut() const  |  Obtiene si se debe deshabilitar o no la recopilación de telemetría.
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Interfaz para configurar el perfil.

Parámetros:  
* **path**: la ruta de acceso a un directorio en el que el sdk almacenará el estado del perfil. 


* **useInMemoryStorage**: marca que indica si se debe almacenar o no el estado en disco. 


* **authDelegate**: el delegado de autenticación utilizado por el SDK para adquirir tokens de autenticación. 


* **observer**: una clase que implementa la interfaz [Profile::Observer](class_mip_profile_observer.md). Puede se nullptr. 


* **applicationInfo**: los identificadores de aplicación que se usan para el acceso al servicio.


  
### <a name="getpath"></a>GetPath
Obtiene la ruta de acceso al estado almacenado.

  
**Devuelve**: ruta de acceso al estado almacenado.
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
Obtiene la marca de uso de almacenamiento en memoria.

  
**Devuelve**: true si se establece el uso en memoria; de lo contrario, false.
  
### <a name="getauthdelegate"></a>GetAuthDelegate
Obtiene el delegado de autenticación.

  
**Devuelve**: el delegado de autenticación.
  
### <a name="profileobserver"></a>Profile::Observer
Obtiene el observador de eventos.

  
**Devuelve**: el observador de eventos.
  
### <a name="applicationinfo"></a>ApplicationInfo
Obtiene la información de aplicación.

  
**Devuelve**: la información de aplicación.
  
### <a name="loggerdelegate"></a>LoggerDelegate
Obtiene el delegado del registrador (si existe) proporcionado por la aplicación.

  
**Devuelve**: delegado del registrador que se usará para el registro
  
### <a name="setloggerdelegate"></a>SetLoggerDelegate
Use la implementación del registrador externo.
Se debe llamar a esto por las aplicaciones cliente si desean usar su propia implementación del registrador
  
### <a name="optouttelemetry"></a>OptOutTelemetry
No participa en la recopilación de toda la telemetría.
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
Obtiene si se debe deshabilitar o no la recopilación de telemetría.

  
**Devuelve**: si se debe deshabilitar o no la recopilación de telemetría