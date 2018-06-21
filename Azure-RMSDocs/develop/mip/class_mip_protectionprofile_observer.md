# <a name="class-mipprotectionprofileobserver"></a>clase mip::ProtectionProfile::Observer 
Interfaz que recibe las notificaciones relacionadas con [ProtectionProfile](class_mip_protectionprofile.md).
Esta interfaz la deben implementar las aplicaciones que utilizan el SDK de protección
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess(const std::shared_ptr<ProtectionProfile>& profile, const std::shared_ptr<void>& context)  |  Se llama cuando se cargó correctamente el perfil.
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama al cargar un perfil que ha causado un error.
  
## <a name="members"></a>Miembros
  
### <a name="onloadsuccess"></a>OnLoadSuccess
Se llama cuando se cargó correctamente el perfil.

Parámetros:  
* **profile**: una referencia a la clase [ProtectionProfile](class_mip_protectionprofile.md) recién creada


* **context**: el mismo contexto que se pasó a [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#loadasync)


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function, etc.) a [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#loadasync) y ese mismo contexto se reenviará tal cual a [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) o [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure)
  
### <a name="onloadfailure"></a>OnLoadFailure
Se llama al cargar un perfil que ha causado un error.

Parámetros:  
* **error**: [error](class_mip_error.md) que se ha producido al cargar 


* **context**: el mismo contexto que se pasó a [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#loadasync)


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function, etc.) a [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#loadasync) y ese mismo contexto se reenviará tal cual a [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) o [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure)