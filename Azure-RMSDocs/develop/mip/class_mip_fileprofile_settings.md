# <a name="class-mipfileprofilesettings"></a>clase mip::FileProfile::Settings 
[Configuración](class_mip_fileprofile_settings.md) utilizada por [FileProfile](class_mip_fileprofile.md) durante su creación y a lo largo de su vigencia.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, bool isLicenseCachingEnabled, std::shared_ptr<AuthDelegate> authDelegate, std::shared_ptr<ConsentDelegate> consentDelegate, std::shared_ptr<Observer> observer, const ApplicationInfo& applicationInfo)  |  Constructor [FileProfile::Settings](class_mip_fileprofile_settings.md).
 public const std::string& GetPath() const  |  Obtiene la ruta de acceso bajo la cual se almacena el registro, la telemetría y otro estado persistente.
 public bool GetUseInMemoryStorage() const  |  Obtiene si todos los estados se deben almacenar o no en memoria (en contraposición a en disco).
 public bool IsLicenseCachingEnabled() const  |  Obtiene si está habilitado el almacenamiento en caché de licencias.
public std::shared_ptr<AuthDelegate> GetAuthDelegate() const  |  Obtiene el delegado de autenticación utilizado para la adquisición de tokens de autenticación.
public std::shared_ptr<ConsentDelegate> GetConsentDelegate() const  |  Obtiene el delegado de consentimiento utilizado para solicitar el consentimiento del usuario al conectarse a los servicios.
public std::shared_ptr<Observer> GetObserver() const  |  Obtiene el observador que recibe notificaciones de eventos relacionados con [FileProfile](class_mip_fileprofile.md).
 public const ApplicationInfo GetApplicationInfo() const  |  Obtiene información relacionada con la aplicación que consume el SDK.
 public bool GetSkipTelemetryInit() const  |  Determina si se debe omitir la inicialización de telemetría.
 public void SetSkipTelemetryInit()  |  Deshabilita la inicialización de telemetría.
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  Obtiene el delegado del registrador (si existe) proporcionado por la aplicación.
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  Use la implementación del registrador externo.
 public void OptOutTelemetry()  |  No participa en la recopilación de toda la telemetría.
 public bool IsTelemetryOptedOut() const  |  Obtiene si se debe deshabilitar o no la recopilación de telemetría.
 public void SetSessionId(const std::string& sessionId)  |  Establece el identificador de sesión.
 public const std::string& GetSessionId() const  |  Obtiene el identificador de sesión.
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Constructor [FileProfile::Settings](class_mip_fileprofile_settings.md).

Parámetros:  
* **path**: ruta de acceso de archivo bajo la cual se almacena el registro, la telemetría y otro estado persistente 


* **useInMemoryStorage**: si todos los estados deben almacenarse o no en memoria (en contraposición a en disco) 


* **isLicenseCachingEnabled**: habilitar o deshabilitar el almacenamiento en caché de licencias de protección 


* **authDelegate**: delegado de autenticación utilizado para la adquisición de tokens de autenticación 


* **observer**: instancia de [Observer](class_mip_fileprofile_observer.md) que recibirá notificaciones de eventos relacionados con [FileProfile](class_mip_fileprofile.md)


* **applicationInfo**: información con respecto a la aplicación que consume el SDK


  
### <a name="getpath"></a>GetPath
Obtiene la ruta de acceso bajo la cual se almacena el registro, la telemetría y otro estado persistente.

  
**Devuelve**: ruta de acceso bajo la cual se almacena el registro, la telemetría y otro estado persistente
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
Obtiene si todos los estados se deben almacenar o no en memoria (en contraposición a en disco).

  
**Devuelve**: si todos los estados se deben almacenar o no en memoria (en contraposición a en disco).
  
### <a name="islicensecachingenabled"></a>IsLicenseCachingEnabled
Obtiene si está habilitado el almacenamiento en caché de licencias.

  
**Devuelve**: true si las memorias caché se almacenan en memoria solo
  
### <a name="getauthdelegate"></a>GetAuthDelegate
Obtiene el delegado de autenticación utilizado para la adquisición de tokens de autenticación.

  
**Devuelve**: el delegado de autenticación utilizado para la adquisición de tokens de autenticación
  
### <a name="consentdelegate"></a>ConsentDelegate
Obtiene el delegado de consentimiento utilizado para solicitar el consentimiento del usuario al conectarse a los servicios.

  
**Devuelve**: delegado de consentimiento que se usa para solicitar el consentimiento del usuario
  
### <a name="observer"></a>Observador
Obtiene el observador que recibe notificaciones de eventos relacionados con [FileProfile](class_mip_fileprofile.md).

  
**Devuelve**: [Observer](class_mip_fileprofile_observer.md) que recibe notificaciones de eventos relacionados con [FileProfile](class_mip_fileprofile.md)
  
### <a name="applicationinfo"></a>ApplicationInfo
Obtiene información relacionada con la aplicación que consume el SDK.

  
**Devuelve**: información relacionada con la aplicación que consume el SDK
  
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
Determina si se debe omitir la inicialización de telemetría.

  
**Devuelve**: determina si se debe omitir la inicialización de telemetría
  
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
Deshabilita la inicialización de telemetría.
Esto normalmente no deberían llamarlo las aplicaciones cliente, sino que debería usarse por el SDK del archivo (que ya inicializa la telemetría) para evitar la duplicación de la inicialización.
  
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
  
### <a name="setsessionid"></a>SetSessionId
Establece el identificador de sesión.

Parámetros:  
* **sessionId**: identificador de sesión que se usará para correlacionar los registros o telemetría


  
### <a name="getsessionid"></a>GetSessionId
Obtiene el identificador de sesión.

  
**Devuelve**: identificador de sesión que se usará para correlacionar los registros o telemetría