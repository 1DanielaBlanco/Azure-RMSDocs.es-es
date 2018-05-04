# <a name="class-mipprotectionprofilesettings"></a>clase mip::ProtectionProfile::Settings 
[Configuración](#classmip_1_1_protection_profile_1_1_settings) utilizada por [ProtectionProfile](#classmip_1_1_protection_profile) durante su creación y a lo largo de su vigencia.
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public inline  SettingsProtectionProfile::Observer > & observer,const ApplicationInfo & applicationInfo) public inline const std::string & GetPath | Obtiene la ruta de acceso bajo la cual se almacena el registro, la telemetría y otras garantías de protección.
public inline const std::shared_ptr< ProtectionProfile::Observer > & GetObserver public inline const ApplicationInfo & GetApplicationInfo | Obtiene información relacionada con la aplicación que consume el SDK de protección.
public inline bool GetSkipTelemetryInit | Determina si se debe omitir la inicialización de telemetría.
public inline void SetSkipTelemetryInit | Deshabilita la inicialización de telemetría.
public inline void SetSessionId | Establece el identificador de sesión. public inline const std::string & GetSessionId | Obtiene el identificador de sesión.
## <a name="members"></a>Miembros
### <a name="settings"></a>Configuración
Constructor [ProtectionProfile::Settings](#classmip_1_1_protection_profile_1_1_settings).
#### <a name="parameters"></a>Parámetros
* path Ruta de acceso al archivo bajo la cual se almacena el registro, la telemetría y otras garantías de protección 
* observer Instancia de [Observer](#classmip_1_1_protection_profile_1_1_observer) que recibirá notificaciones de eventos relacionadas con [ProtectionProfile](#classmip_1_1_protection_profile)
* applicationInfo Información con respecto a la aplicación que consume el SDK de protección
### <a name="getpath"></a>GetPath
Obtiene la ruta de acceso bajo la cual se almacena el registro, la telemetría y otras garantías de protección.
#### <a name="returns"></a>Devuelve
Ruta de acceso bajo la cual se almacena el registro, la telemetría y otras garantías de protección
### <a name="protectionprofileobserver"></a>ProtectionProfile::Observer
Obtiene el observador que recibe notificaciones de eventos relacionados con [ProtectionProfile](#classmip_1_1_protection_profile).
#### <a name="returns"></a>Devuelve
[Observer](#classmip_1_1_protection_profile_1_1_observer) que recibe notificaciones de eventos relacionados con [ProtectionProfile](#classmip_1_1_protection_profile)
### <a name="applicationinfo"></a>ApplicationInfo
Obtiene información relacionada con la aplicación que consume el SDK de protección.
#### <a name="returns"></a>Devuelve
Información con respecto a la aplicación que consume el SDK de protección
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
Determina si se debe omitir la inicialización de telemetría.
#### <a name="returns"></a>Devuelve
Si se debe omitir la inicialización de telemetría
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
Deshabilita la inicialización de telemetría.
Esto normalmente no deberían llamarlo las aplicaciones cliente, sino que debería usarse por el SDK del archivo (que ya inicializa la telemetría) para evitar la duplicación de la inicialización.
### <a name="setsessionid"></a>SetSessionId
Establece el identificador de sesión.
#### <a name="parameters"></a>Parámetros
* sessionId Identificador de sesión que se usará para correlacionar los registros o telemetría
### <a name="getsessionid"></a>GetSessionId
Obtiene el identificador de sesión.
#### <a name="returns"></a>Devuelve
Identificador de sesión que se usará para correlacionar los registros o telemetría