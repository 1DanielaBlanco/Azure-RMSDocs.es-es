# <a name="class-mipprotectionprofile"></a>clase mip::ProtectionProfile 
[ProtectionProfile](#classmip_1_1_protection_profile) es la clase raíz para realizar las operaciones de protección.
Una aplicación debe crear una clase [ProtectionProfile](#classmip_1_1_protection_profile) antes de realizar cualquier operación de protección.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Obtiene la configuración utilizada por [ProtectionProfile](#classmip_1_1_protection_profile) durante su inicialización y a lo largo de su vigencia.
public void ClearCaches()  |  Elimina las cachés (por ejemplo, bases de datos de consentimiento)
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Obtiene la configuración utilizada por [ProtectionProfile](#classmip_1_1_protection_profile) durante su inicialización y a lo largo de su vigencia.
  
#### <a name="returns"></a>Devuelve
La [configuración](#classmip_1_1_protection_profile_1_1_settings) utilizada por [ProtectionProfile](#classmip_1_1_protection_profile) durante su inicialización y a lo largo de su vigencia
  
### <a name="clearcaches"></a>ClearCaches
Elimina las cachés (por ejemplo, bases de datos de consentimiento) Útiles para depuración o pruebas