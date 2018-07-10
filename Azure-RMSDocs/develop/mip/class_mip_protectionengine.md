# <a name="class-mipprotectionengine"></a>clase mip::ProtectionEngine 
Realiza acciones relacionadas con la protección respecto de una identidad específica.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Obtiene la configuración del motor.
public void GetTemplatesAsync(const std::shared_ptr<ProtectionEngine::Observer>& observer, const std::shared_ptr<void>& context)  |  Obtiene la colección de plantillas disponibles para un usuario.
public void CreateProtectionHandlerFromDescriptorAsync(const std::shared_ptr<ProtectionDescriptor>& descriptor, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  Crea un controlador de protección, donde se asignan derechos y roles a usuarios específicos.
public void CreateProtectionHandlerFromPublishingLicenseAsync(const std::vector<uint8_t>& serializedPublishingLicense, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  Crea un controlador de protección a partir de su formato en serie.
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Obtiene la configuración del motor.

  
**Devuelve**: configuración del motor
  
### <a name="gettemplatesasync"></a>GetTemplatesAsync
Obtiene la colección de plantillas disponibles para un usuario.

Parámetros:  
* **observer**: una clase que implementa la interfaz [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) 


* **context**: este mismo contexto se reenviará a [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) o [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure)


  
### <a name="createprotectionhandlerfromdescriptorasync"></a>CreateProtectionHandlerFromDescriptorAsync
Crea un controlador de protección, donde se asignan derechos y roles a usuarios específicos.

Parámetros:  
* **descriptor**: un [ProtectionDescriptor](class_mip_protectiondescriptor.md) que describe la configuración de la protección 


* **options**: opciones de creación 


* **observer**: una clase que implementa la interfaz [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md). 


* **context**: este mismo contexto se reenviará a [ProtectionHandler::Observer::OnCreateProtectionHandlerSuccess](class_mip_protectionhandler_observer.md#oncreateprotectionhandlersuccess) o ProtectionHandler::Observer::OnCreateProtectionHandlerFailure


  
### <a name="createprotectionhandlerfrompublishinglicenseasync"></a>CreateProtectionHandlerFromPublishingLicenseAsync
Crea un controlador de protección a partir de su formato en serie.

Parámetros:  
* **serializedPublishingLicense**: una licencia de publicación en serie 


* **options**: opciones de creación 


* **observer**: una clase que implementa la interfaz [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md). 


* **context**: este mismo contexto se reenviará a [ProtectionHandler::Observer::OnCreateProtectionHandlerSuccess](class_mip_protectionhandler_observer.md#oncreateprotectionhandlersuccess) o ProtectionHandler::Observer::OnCreateProtectionHandlerFailure

