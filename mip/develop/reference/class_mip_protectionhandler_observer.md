# <a name="class-mipprotectionhandlerobserver"></a>clase mip::ProtectionHandler::Observer 
Interfaz que recibe las notificaciones relacionadas con [ProtectionHandler](class_mip_protectionhandler.md).
Esta interfaz la deben implementar las aplicaciones que utilizan el SDK de protección
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public virtual void OnCreateProtectionHandlerSuccess(const std::shared_ptr<ProtectionHandler>& protectionHandler, const std::shared_ptr<void>& context)  |  Se llama cuando [ProtectionHandler](class_mip_protectionhandler.md) se creó correctamente.
public virtual void OnCreateProtectionHandlerError(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando no se pudo crear [ProtectionHandler](class_mip_protectionhandler.md).
  
## <a name="members"></a>Miembros
  
### <a name="oncreateprotectionhandlersuccess"></a>OnCreateProtectionHandlerSuccess
Se llama cuando [ProtectionHandler](class_mip_protectionhandler.md) se creó correctamente.

Parámetros:  
* **protectionHandler**: el [ProtectionHandler](class_mip_protectionhandler.md) recién creado


* **context**: el mismo contexto que se pasó a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync)


Una aplicación puede pasar cualquier tipo de contexto (p. ej. std::promise, std::function, etc.) a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync) y ese mismo contexto se reenviará tal cual a ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess o ProtectionEngine::Observer::OnCreateProtectionHandlerFailure
  
### <a name="oncreateprotectionhandlererror"></a>OnCreateProtectionHandlerError
Se llama cuando no se pudo crear [ProtectionHandler](class_mip_protectionhandler.md).

Parámetros:  
* **error**: [error](class_mip_error.md) que se produjo durante la creación 


* **context**: el mismo contexto que se pasó a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync)


Una aplicación puede pasar cualquier tipo de contexto (p. ej. std::promise, std::function, etc.) a [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) o [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync) y ese mismo contexto se reenviará tal cual a ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess o ProtectionEngine::Observer::OnCreateProtectionHandlerFailure