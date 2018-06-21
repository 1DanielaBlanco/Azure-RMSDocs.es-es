# <a name="class-mipprotectionprofile"></a>clase mip::ProtectionProfile 
[ProtectionProfile](class_mip_protectionprofile.md) es la clase raíz para realizar las operaciones de protección.
Una aplicación debe crear una clase [ProtectionProfile](class_mip_protectionprofile.md) antes de realizar cualquier operación de protección.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Obtiene la configuración utilizada por [ProtectionProfile](class_mip_protectionprofile.md) durante su inicialización y a lo largo de su vigencia.
 public void ClearCaches()  |  Elimina las cachés (por ejemplo, bases de datos de consentimiento)
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Obtiene la configuración utilizada por [ProtectionProfile](class_mip_protectionprofile.md) durante su inicialización y a lo largo de su vigencia.

  
**Devuelve**: [configuración](class_mip_protectionprofile_settings.md) utilizada por [ProtectionProfile](class_mip_protectionprofile.md) durante su inicialización y a lo largo de su vigencia
  
### <a name="clearcaches"></a>ClearCaches
Elimina las cachés (por ejemplo, bases de datos de consentimiento) Útiles para depuración o pruebas