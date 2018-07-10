# <a name="class-mipprotectionengineobserver"></a>clase mip::ProtectionEngine::Observer 
Interfaz que recibe las notificaciones relacionadas con [ProtectionEngine](class_mip_protectionengine.md).
Esta interfaz la deben implementar las aplicaciones que utilizan el SDK de protección
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess(const std::shared_ptr<std::vector<std::string>>& templateIds, const std::shared_ptr<void>& context)  |  Se llama cuando se recuperan correctamente las plantillas.
public virtual void OnGetTemplatesFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando se ha generado un error al recuperar las plantillas.
  
## <a name="members"></a>Miembros
  
### <a name="ongettemplatessuccess"></a>OnGetTemplatesSuccess
Se llama cuando se recuperan correctamente las plantillas.

Parámetros:  
* **templateIds**: una referencia a la lista de plantillas recuperadas 


* **context**: el mismo contexto que se pasó a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync)


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function, etc.) a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync) y ese mismo contexto se reenviará tal cual a [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) o [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure)
  
### <a name="ongettemplatesfailure"></a>OnGetTemplatesFailure
Se llama cuando se ha generado un error al recuperar las plantillas.

Parámetros:  
* **error**: [error](class_mip_error.md) que se produjo al recuperar las plantillas 


* **context**: el mismo contexto que se pasó a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync)


Una aplicación puede pasar cualquier tipo de contexto (por ejemplo, std::promise, std::function, etc.) a [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync) y ese mismo contexto se reenviará tal cual a [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) o [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure)