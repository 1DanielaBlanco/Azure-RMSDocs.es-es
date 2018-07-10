# <a name="class-mipprotectionprofilesettings"></a>clase mip::ProtectionProfile::Settings 
[Configuración](class_mip_protectionprofile_settings.md) utilizada por [ProtectionProfile](class_mip_protectionprofile.md) durante su creación y a lo largo de su vigencia.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, bool isLicenseCachingEnabled, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<ConsentDelegate>& consentDelegate, const std::shared_ptr<ProtectionProfile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  Constructor [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md).
 public const std::string& GetPath() const  |  Obtiene la ruta de acceso bajo la cual se almacena el registro, la telemetría y otras garantías de protección.
 public bool GetUseInMemoryStorage() const  |  Obtiene si las memorias caché se almacenan solo en la memoria (en contraposición a en disco).
 public bool IsLicenseCachingEnabled() const  |  Obtiene si está habilitado el almacenamiento en caché de licencias.
public std::shared_ptr<AuthDelegate> GetAuthDelegate() const  |  Obtiene el delegado de autenticación utilizado para la adquisición de tokens de autenticación.
public std::shared_ptr<ConsentDelegate> GetConsentDelegate() const  |  Obtiene el delegado de consentimiento utilizado para conectarse a servicios.
public const std::shared_ptr<ProtectionProfile::Observer>& GetObserver() const  |  Obtiene el observador que recibe notificaciones de eventos relacionados con [ProtectionProfile](class_mip_protectionprofile.md).
 public const ApplicationInfo& GetApplicationInfo() const  |  Obtiene información relacionada con la aplicación que consume el SDK de protección.
 public void OptOutTelemetry()  |  No participa en la recopilación de toda la telemetría.
 public bool IsTelemetryOptedOut() const  |  Obtiene si se debe deshabilitar o no la recopilación de telemetría.
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  Obtiene el delegado del registrador (si existe) proporcionado por la aplicación.
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  Use la implementación del registrador externo.
 public bool GetSkipTelemetryInit() const  |  Determina si se debe omitir la inicialización de telemetría.
 public void SetSkipTelemetryInit()  |  Deshabilita la inicialización de telemetría.
 public void SetSessionId(const std::string& sessionId)  |  Establece el identificador de sesión.
 public const std::string& GetSessionId() const  |  Obtiene el identificador de sesión.
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Constructor [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md).

Parámetros:  
* **path**: ruta de acceso al archivo bajo la cual se almacena el registro, la telemetría y otras garantías de protección 


* **useInMemoryStorage**: almacene cualquier estado almacenado en caché en memoria en lugar de en disco 


* **isLicenseCachingEnabled**: habilite o deshabilite el almacenamiento en caché de licencias del SDK de protección 


* **authDelegate**: objeto de devolución de llamada que se usará para la autenticación, implementado por la aplicación cliente 


* **observer**: instancia de [Observer](class_mip_protectionprofile_observer.md) que recibirá notificaciones de eventos relacionados con [ProtectionProfile](class_mip_protectionprofile.md)


* **applicationInfo**: información con respecto a la aplicación que consume el SDK de protección


  
### <a name="getpath"></a>GetPath
Obtiene la ruta de acceso bajo la cual se almacena el registro, la telemetría y otras garantías de protección.

  
**Devuelve**: ruta de acceso bajo la cual se almacena el registro, la telemetría y otras garantías de protección
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
Obtiene si las memorias caché se almacenan solo en la memoria (en contraposición a en disco).

  
**Devuelve**: true si las memorias caché se almacenan en memoria solo
  
### <a name="islicensecachingenabled"></a>IsLicenseCachingEnabled
Obtiene si está habilitado el almacenamiento en caché de licencias.

  
**Devuelve**: true si está habilitado el almacenamiento en caché de licencias del SDK de protección
  
### <a name="getauthdelegate"></a>GetAuthDelegate
Obtiene el delegado de autenticación utilizado para la adquisición de tokens de autenticación.

  
**Devuelve**: el delegado de autenticación utilizado para la adquisición de tokens de autenticación
  
### <a name="consentdelegate"></a>ConsentDelegate
Obtiene el delegado de consentimiento utilizado para conectarse a servicios.

  
**Devuelve**: el delegado de consentimiento utilizado para conectarse a servicios
  
### <a name="protectionprofileobserver"></a>ProtectionProfile::Observer
Obtiene el observador que recibe notificaciones de eventos relacionados con [ProtectionProfile](class_mip_protectionprofile.md).

  
**Devuelve**: [Observer](class_mip_protectionprofile_observer.md) que recibe notificaciones de eventos relacionados con [ProtectionProfile](class_mip_protectionprofile.md)
  
### <a name="applicationinfo"></a>ApplicationInfo
Obtiene información relacionada con la aplicación que consume el SDK de protección.

  
**Devuelve**: información relacionada con la aplicación que consume el SDK de protección
  
### <a name="optouttelemetry"></a>OptOutTelemetry
No participa en la recopilación de toda la telemetría.
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
Obtiene si se debe deshabilitar o no la recopilación de telemetría.

  
**Devuelve**: si se debe deshabilitar o no la recopilación de telemetría
  
### <a name="loggerdelegate"></a>LoggerDelegate
Obtiene el delegado del registrador (si existe) proporcionado por la aplicación.

  
**Devuelve**: delegado del registrador que se usará para el registro
  
### <a name="setloggerdelegate"></a>SetLoggerDelegate
Use la implementación del registrador externo.
Se debe llamar a esto por las aplicaciones cliente si desean usar su propia implementación del registrador
  
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
Determina si se debe omitir la inicialización de telemetría.

  
**Devuelve**: determina si se debe omitir la inicialización de telemetría
  
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
Deshabilita la inicialización de telemetría.
Esto normalmente no deberían llamarlo las aplicaciones cliente, sino que debería usarse por el SDK del archivo (que ya inicializa la telemetría) para evitar la duplicación de la inicialización.
  
### <a name="setsessionid"></a>SetSessionId
Establece el identificador de sesión.

Parámetros:  
* **sessionId**: identificador de sesión que se usará para correlacionar los registros o telemetría


  
### <a name="getsessionid"></a>GetSessionId
Obtiene el identificador de sesión.

  
**Devuelve**: identificador de sesión que se usará para correlacionar los registros o telemetría