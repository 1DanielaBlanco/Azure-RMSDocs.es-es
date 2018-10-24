---
title: Clase mip ProtectionEngine
description: Referencia de la clase mip ProtectionEngine
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: ddc8cfd58acb2a80d024978084b625f3d3728c87
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446743"
---
# <a name="class-mipprotectionengine"></a>clase mip::ProtectionEngine 
Administra acciones relacionadas con la protección según una identidad específica.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Obtiene la configuración del motor.
public void GetTemplatesAsync(const std::shared_ptr<ProtectionEngine::Observer>& observer, const std::shared_ptr<void>& context)  |  Obtiene la colección de plantillas disponibles para un usuario.
public std::vector<std::string> GetTemplates(const std::shared_ptr<void>& context)  |  Obtiene la colección de plantillas disponibles para un usuario.
public void GetRightsForLabelIdAsync(const std::string& documentId, const std::string& labelId, const std::string& ownerEmail, const std::shared_ptr<ProtectionEngine::Observer>& observer, const std::shared_ptr<void>& context)  |  Obtiene la colección de derechos disponibles para un usuario con un identificador de etiqueta.
public std::vector<std::string> GetRightsForLabelId(const std::string& documentId, const std::string& labelId, const std::string& ownerEmail, const std::shared_ptr<void>& context)  |  Obtiene la colección de derechos disponibles para un usuario según un elemento labelId.
public void GetGrantingLabelIdsAsync(const std::shared_ptr<ProtectionEngine::Observer>& observer, const std::shared_ptr<void>& context)  |  Obtiene una colección de identificadores de etiqueta disponibles para un usuario.
public std::vector<std::string> GetGrantingLabelIds(const std::shared_ptr<void>& context)  |  Obtiene una colección de identificadores de etiqueta disponibles para un usuario.
public void CreateProtectionHandlerFromDescriptorAsync(const std::shared_ptr<ProtectionDescriptor>& descriptor, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  Crea un controlador de protección, donde se asignan derechos y roles a usuarios específicos.
public std::shared_ptr<ProtectionHandler> CreateProtectionHandlerFromDescriptor(const std::shared_ptr<ProtectionDescriptor>& descriptor, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<void>& context)  |  Crea un controlador de protección, donde se asignan derechos y roles a usuarios específicos.
public void CreateProtectionHandlerFromPublishingLicenseAsync(const std::vector<uint8_t>& serializedPublishingLicense, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  Crea un controlador de protección a partir de una licencia de publicación serializada.
public std::shared_ptr<ProtectionHandler> CreateProtectionHandlerFromPublishingLicense(const std::vector<uint8_t>& serializedPublishingLicense, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<void>& context)  |  Crea un controlador de protección a partir de una licencia de publicación serializada.
public void CreateProtectionHandlerFromPublishingLicenseContextAsync(const PublishingLicenseContext& publishingLicenseContext, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  Crea un controlador de protección a partir de un contexto de licencia de publicación.
public std::shared_ptr<ProtectionHandler> CreateProtectionHandlerFromPublishingLicenseContext(const PublishingLicenseContext& publishingLicenseContext, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<void>& context)  |  Crea un controlador de protección a partir de un contexto de licencia de publicación.
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Obtiene la configuración del motor.

  
**Devuelve**: configuración del motor
  
### <a name="gettemplatesasync"></a>GetTemplatesAsync
Obtiene la colección de plantillas disponibles para un usuario.

Parámetros:  
* **observer**: una clase que implementa la interfaz [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) 


* **context**: contexto de cliente que se pasará de forma opaca a los observadores y al elemento [HttpDelegate](class_mip_httpdelegate.md) opcional.


  
### <a name="gettemplates"></a>GetTemplates
Obtiene la colección de plantillas disponibles para un usuario.

Parámetros:  
* **context**: contexto de cliente que se pasará de forma opaca al elemento [HttpDelegate](class_mip_httpdelegate.md) opcional.



  
**Devuelve**: lista de identificadores de plantilla.
  
### <a name="getrightsforlabelidasync"></a>GetRightsForLabelIdAsync
Obtiene la colección de derechos disponibles para un usuario con un identificador de etiqueta.

Parámetros:  
* **documentId**: identificador de documento asociado a los metadatos del documento. 


* **labelId**: identificador de [etiqueta](class_mip_label.md) asociado a los metadatos del documento con los que se ha creado el documento. 


* **ownerEmail**: propietario del documento. 


* **observer**: una clase que implementa la interfaz [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) 


* **context**: este mismo contexto se reenviará a [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess) o [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure).


  
### <a name="getrightsforlabelid"></a>GetRightsForLabelId
Obtiene la colección de derechos disponibles para un usuario según un elemento labelId.

Parámetros:  
* **documentId**: identificador de documento asociado a los metadatos del documento. 


* **labelId**: identificador de [etiqueta](class_mip_label.md) asociado a los metadatos del documento con los que se ha creado el documento. 


* **ownerEmail**: propietario del documento. 


* **context**: este mismo contexto se reenviará al elemento [HttpDelegate](class_mip_httpdelegate.md) opcional.



  
**Devuelve**: lista de derechos.
  
### <a name="getgrantinglabelidsasync"></a>GetGrantingLabelIdsAsync
Obtiene una colección de identificadores de etiqueta disponibles para un usuario.

Parámetros:  
* **observer**: una clase que implementa la interfaz [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) 


* **context**: este mismo contexto se reenviará a [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess) o ProtectionEngine::Observer::OnGrantingLabelIdsFailure.


  
### <a name="getgrantinglabelids"></a>GetGrantingLabelIds
Obtiene una colección de identificadores de etiqueta disponibles para un usuario.

Parámetros:  
* **context**: este mismo contexto se reenviará al elemento [HttpDelegate](class_mip_httpdelegate.md) opcional.



  
**Devuelve**: lista de identificadores de etiquetas.
  
### <a name="createprotectionhandlerfromdescriptorasync"></a>CreateProtectionHandlerFromDescriptorAsync
Crea un controlador de protección, donde se asignan derechos y roles a usuarios específicos.

Parámetros:  
* **descriptor**: un [ProtectionDescriptor](class_mip_protectiondescriptor.md) que describe la configuración de la protección 


* **options**: opciones de creación 


* **observer**: una clase que implementa la interfaz [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md). 


* **context**: contexto de cliente que se pasará de forma opaca a los observadores y al elemento [HttpDelegate](class_mip_httpdelegate.md) opcional.


  
### <a name="protectionhandler"></a>ProtectionHandler
Crea un controlador de protección, donde se asignan derechos y roles a usuarios específicos.

Parámetros:  
* **descriptor**: un [ProtectionDescriptor](class_mip_protectiondescriptor.md) que describe la configuración de la protección 


* **options**: opciones de creación 


* **context**: contexto de cliente que se pasará de forma opaca al elemento [HttpDelegate](class_mip_httpdelegate.md) opcional.



  
**Devuelve**: [ProtectionHandler](class_mip_protectionhandler.md).
  
### <a name="createprotectionhandlerfrompublishinglicenseasync"></a>CreateProtectionHandlerFromPublishingLicenseAsync
Crea un controlador de protección a partir de una licencia de publicación serializada.

Parámetros:  
* **serializedPublishingLicense**: una licencia de publicación en serie 


* **options**: opciones de creación 


* **observer**: una clase que implementa la interfaz [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md). 


* **context**: contexto de cliente que se pasará de forma opaca a los observadores y al elemento [HttpDelegate](class_mip_httpdelegate.md) opcional.


  
### <a name="protectionhandler"></a>ProtectionHandler
Crea un controlador de protección a partir de una licencia de publicación serializada.

Parámetros:  
* **serializedPublishingLicense**: una licencia de publicación en serie 


* **options**: opciones de creación 


* **observer**: una clase que implementa la interfaz [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md). 


* **context**: contexto de cliente que se pasará de forma opaca al elemento [HttpDelegate](class_mip_httpdelegate.md) opcional.



  
**Devuelve**: [ProtectionHandler](class_mip_protectionhandler.md).
  
### <a name="createprotectionhandlerfrompublishinglicensecontextasync"></a>CreateProtectionHandlerFromPublishingLicenseContextAsync
Crea un controlador de protección a partir de un contexto de licencia de publicación.

Parámetros:  
* **publishingLicenseContext**: formulario preprocesado de la licencia de publicación serializada. 


* **options**: opciones de creación 


* **observer**: una clase que implementa la interfaz [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md). 


* **context**: contexto de cliente que se pasará de forma opaca a los observadores y al elemento [HttpDelegate](class_mip_httpdelegate.md) opcional.


  
### <a name="protectionhandler"></a>ProtectionHandler
Crea un controlador de protección a partir de un contexto de licencia de publicación.

Parámetros:  
* **publishingLicenseContext**: formulario preprocesado de la licencia de publicación serializada. 


* **options**: opciones de creación 


* **observer**: una clase que implementa la interfaz [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md). 


* **context**: contexto de cliente que se pasará de forma opaca al elemento [HttpDelegate](class_mip_httpdelegate.md) opcional.



  
**Devuelve**: [ProtectionHandler](class_mip_protectionhandler.md).