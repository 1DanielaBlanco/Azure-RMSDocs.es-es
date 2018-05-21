# <a name="class-mipprotectionprofilesettings"></a>clase mip::ProtectionProfile::Settings 
[Configuración](class_mip_protectionprofile_settings.md) utilizada por [ProtectionProfile](class_mip_protectionprofile.md) durante su creación y a lo largo de su vigencia.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, const std::shared_ptr<ProtectionProfile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  Constructor [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md).
 public const std::string& GetPath() const  |  Obtiene la ruta de acceso bajo la cual se almacena el registro, la telemetría y otras garantías de protección.
public const std::shared_ptr<ProtectionProfile::Observer>& GetObserver() const  |  Obtiene el observador que recibe notificaciones de eventos relacionados con [ProtectionProfile](class_mip_protectionprofile.md).
 public const ApplicationInfo& GetApplicationInfo() const  |  Obtiene información relacionada con la aplicación que consume el SDK de protección.
 public bool GetSkipTelemetryInit() const  |  Determina si se debe omitir la inicialización de telemetría.
 public void SetSkipTelemetryInit()  |  Deshabilita la inicialización de telemetría.
 public void SetSessionId(const std::string& sessionId)  |  Establece el identificador de sesión.
 public const std::string& GetSessionId() const  |  Obtiene el identificador de sesión.
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Constructor [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md).

Parámetros:  
* **path**: ruta de acceso al archivo bajo la cual se almacena el registro, la telemetría y otras garantías de protección 


* **observer**: instancia de [Observer](class_mip_protectionprofile_observer.md) que recibirá notificaciones de eventos relacionados con [ProtectionProfile](class_mip_protectionprofile.md)


* **applicationInfo**: información con respecto a la aplicación que consume el SDK de protección


  
### <a name="getpath"></a>GetPath
Obtiene la ruta de acceso bajo la cual se almacena el registro, la telemetría y otras garantías de protección.

  
**Devuelve**: ruta de acceso bajo la cual se almacena el registro, la telemetría y otras garantías de protección
  
### <a name="protectionprofileobserver"></a>ProtectionProfile::Observer
Obtiene el observador que recibe notificaciones de eventos relacionados con [ProtectionProfile](class_mip_protectionprofile.md).

  
**Devuelve**: [Observer](class_mip_protectionprofile_observer.md) que recibe notificaciones de eventos relacionados con [ProtectionProfile](class_mip_protectionprofile.md)
  
### <a name="applicationinfo"></a>ApplicationInfo
Obtiene información relacionada con la aplicación que consume el SDK de protección.

  
**Devuelve**: información relacionada con la aplicación que consume el SDK de protección
  
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