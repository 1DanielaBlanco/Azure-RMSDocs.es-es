# <a name="class-mipprotectionprofileobserver"></a>clase mip::ProtectionProfile::Observer 
Interfaz que recibe las notificaciones relacionadas con [ProtectionProfile](#classmip_1_1_protection_profile).
Esta interfaz la deben implementar las aplicaciones que utilizan el SDK de protección
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public inline virtual void OnLoadSuccessProtectionProfile > & profile,const std::shared_ptr< void > & context) | Se llama cuando se cargó correctamente el perfil.
public inline virtual void OnLoadFailure | Se llama al cargar un perfil que ha causado un error.
## <a name="members"></a>Miembros
### <a name="onloadsuccess"></a>OnLoadSuccess
Se llama cuando se cargó correctamente el perfil.
#### <a name="parameters"></a>Parámetros
* profile Una referencia a la clase [ProtectionProfile](#classmip_1_1_protection_profile) recién creada
* context El mismo contexto que se pasa a [ProtectionProfile::LoadAsync](#classmip_1_1_protection_profile_1aeb141706dc10935931841fdb82d11031) Una aplicación puede pasar cualquier tipo de contexto (por, ejemplo, std::promise, std::function, etc.) a [ProtectionProfile::LoadAsync](#classmip_1_1_protection_profile_1aeb141706dc10935931841fdb82d11031) y ese mismo contexto se reenviará tal cual a [ProtectionProfile::Observer::OnLoadSuccess](#classmip_1_1_protection_profile_1_1_observer_1a31e73965ffb0bd152b3954b013faa773) o a [ProtectionProfile::Observer::OnLoadFailure](#classmip_1_1_protection_profile_1_1_observer_1acdad73bb6a2dcc93295e0e16e422f291)
### <a name="onloadfailure"></a>OnLoadFailure
Se llama al cargar un perfil que ha causado un error.
#### <a name="parameters"></a>Parámetros
* error [Error](#classmip_1_1_error) que se ha producido al cargar 
* context El mismo contexto que se pasa a [ProtectionProfile::LoadAsync](#classmip_1_1_protection_profile_1aeb141706dc10935931841fdb82d11031) Una aplicación puede pasar cualquier tipo de contexto (por, ejemplo, std::promise, std::function, etc.) a [ProtectionProfile::LoadAsync](#classmip_1_1_protection_profile_1aeb141706dc10935931841fdb82d11031) y ese mismo contexto se reenviará tal cual a [ProtectionProfile::Observer::OnLoadSuccess](#classmip_1_1_protection_profile_1_1_observer_1a31e73965ffb0bd152b3954b013faa773) o a [ProtectionProfile::Observer::OnLoadFailure](#classmip_1_1_protection_profile_1_1_observer_1acdad73bb6a2dcc93295e0e16e422f291)