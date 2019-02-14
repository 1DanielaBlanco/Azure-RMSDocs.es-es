---
title: clase mip::ProtectionEngine
description: Documenta la clase mip::protectionengine de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: d12fbe050ba86dbcef58dada971134c96dc637d1
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56252918"
---
# <a name="class-mipprotectionengine"></a>clase mip::ProtectionEngine 
Administra acciones relacionadas con la protección según una identidad específica.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Obtiene la configuración del motor.
pública GetTemplatesAsync void (const std:: shared_ptr\<ProtectionEngine::Observer\>& observer, const std:: shared_ptr\<void\>& contexto)  |  Obtiene la colección de plantillas disponibles para un usuario.
Public std:: vector\<std:: String\> GetTemplates (const std:: shared_ptr\<void\>& contexto)  |  Obtiene la colección de plantillas disponibles para un usuario.
pública GetRightsForLabelIdAsync void (const std:: String & documentId, const std:: String & labelId, const std:: String & ownerEmail, const std:: shared_ptr\<ProtectionEngine::Observer\>& observer, const std: : shared_ptr\<void\>& contexto)  |  Obtiene la colección de derechos disponibles para un usuario con un identificador de etiqueta.
Public std:: vector\<std:: String\> GetRightsForLabelId (const std:: String & documentId, const std:: String & labelId, const std:: String & ownerEmail, const std:: shared_ptr\<void\> & contexto)  |  Obtiene la colección de derechos disponibles para un usuario según un elemento labelId.
pública CreateProtectionHandlerFromDescriptorAsync void (const std:: shared_ptr\<ProtectionDescriptor\>& descriptor ProtectionHandlerCreationOptions const & opciones, const std:: shared_ptr\< ProtectionHandler::Observer\>& observer, const std:: shared_ptr\<void\>& contexto)  |  Crea un controlador de protección, donde se asignan derechos y roles a usuarios específicos.
Public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerFromDescriptor (const std:: shared_ptr\<ProtectionDescriptor\>& descriptor, ProtectionHandlerCreationOptions const & opciones, const std:: shared_ptr\<void\>& contexto)  |  Crea un controlador de protección, donde se asignan derechos y roles a usuarios específicos.
pública CreateProtectionHandlerFromPublishingLicenseAsync void (const std:: vector\<uint8_t\>& serializedPublishingLicense ProtectionHandlerCreationOptions const & opciones, const std:: shared_ptr\<ProtectionHandler::Observer\>& observer, const std:: shared_ptr\<void\>& contexto)  |  Crea un controlador de protección a partir de una licencia de publicación serializada.
Public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerFromPublishingLicense (const std:: vector\<uint8_t\>& serializedPublishingLicense, const ProtectionHandlerCreationOptions & opciones, const std:: shared_ptr\<void\>& contexto)  |  Crea un controlador de protección a partir de una licencia de publicación serializada.
pública CreateProtectionHandlerFromProtectionInfoAsync void (const std:: vector\<uint8_t\>& serializedPublishingLicense, const std:: vector\<uint8_t\>& serializedProtectionInfo, Const std:: shared_ptr\<ProtectionHandler::Observer\>& observer, const std:: shared_ptr\<void\>& contexto)  |  Crea un controlador de protección de una licencia de publicación serializada y una información serializada de protección.
Public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerFromProtectionInfo (const std:: vector\<uint8_t\>& serializedPublishingLicense, const std:: vector\< uint8_t\>& serializedProtectionInfo, const std:: shared_ptr\<void\>& contexto)  |  Crea un controlador de protección de una licencia de publicación serializada y una información serializada de protección.
pública CreateProtectionHandlerFromPublishingLicenseContextAsync void (const PublishingLicenseContext & publishingLicenseContext ProtectionHandlerCreationOptions const & opciones, const std:: shared_ptr\< ProtectionHandler::Observer\>& observer, const std:: shared_ptr\<void\>& contexto)  |  Crea un controlador de protección a partir de un contexto de licencia de publicación.
Public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerFromPublishingLicenseContext (const PublishingLicenseContext & publishingLicenseContext, ProtectionHandlerCreationOptions const & Opciones, const std:: shared_ptr\<void\>& contexto)  |  Crea un controlador de protección a partir de un contexto de licencia de publicación.
  
## <a name="members"></a>Miembros
  
### <a name="getsettings-function"></a>Función GetSettings
Obtiene la configuración del motor.

  
**Devuelve**: Configuración del motor
  
### <a name="gettemplatesasync-function"></a>Función GetTemplatesAsync
Obtiene la colección de plantillas disponibles para un usuario.

Parámetros:  
* **observer**: Una clase que implementa el [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) interfaz 


* **context**: Contexto de cliente que se forma opaca pasados a los observadores y opcional [HttpDelegate](class_mip_httpdelegate.md)


  
### <a name="gettemplates-function"></a>Función GetTemplates
Obtiene la colección de plantillas disponibles para un usuario.

Parámetros:  
* **context**: Contexto de cliente que se pasará de manera opaca en opcional [HttpDelegate](class_mip_httpdelegate.md)



  
**Devuelve**: Lista de identificadores de plantilla.
  
### <a name="getrightsforlabelidasync-function"></a>Función GetRightsForLabelIdAsync
Obtiene la colección de derechos disponibles para un usuario con un identificador de etiqueta.

Parámetros:  
* **documentId**: Id. de documento asociado con los metadatos de documentos 


* **labelId**: [Etiqueta](class_mip_label.md) identificador asociado a los metadatos de documentos con la que se creó el documento 


* **ownerEmail**: propietario del documento. 


* **observer**: Una clase que implementa el [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) interfaz 


* **context**: Este mismo contexto se reenviará a [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function) o [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function)


  
### <a name="getrightsforlabelid-function"></a>Función GetRightsForLabelId
Obtiene la colección de derechos disponibles para un usuario según un elemento labelId.

Parámetros:  
* **documentId**: Id. de documento asociado con los metadatos de documentos 


* **labelId**: [Etiqueta](class_mip_label.md) identificador asociado a los metadatos de documentos con la que se creó el documento 


* **ownerEmail**: Propietario del documento 


* **context**: Este mismo contexto se reenviará a opcional [HttpDelegate](class_mip_httpdelegate.md)



  
**Devuelve**: Lista de derechos
  
### <a name="createprotectionhandlerfromdescriptorasync-function"></a>Función CreateProtectionHandlerFromDescriptorAsync
Crea un controlador de protección, donde se asignan derechos y roles a usuarios específicos.

Parámetros:  
* **descriptor**: Un [ProtectionDescriptor](class_mip_protectiondescriptor.md) que describe la configuración de protección 


* **Opciones de**: Opciones de creación 


* **observer**: Una clase que implementa el [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) interfaz 


* **context**: Contexto de cliente que se forma opaca pasados a los observadores y opcional [HttpDelegate](class_mip_httpdelegate.md)


  
### <a name="createprotectionhandlerfromdescriptor-function"></a>Función CreateProtectionHandlerFromDescriptor
Crea un controlador de protección, donde se asignan derechos y roles a usuarios específicos.

Parámetros:  
* **descriptor**: Un [ProtectionDescriptor](class_mip_protectiondescriptor.md) que describe la configuración de protección 


* **Opciones de**: Opciones de creación 


* **context**: Contexto de cliente que se pasará de manera opaca a opcional [HttpDelegate](class_mip_httpdelegate.md)



  
**Devuelve**: [ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerfrompublishinglicenseasync-function"></a>Función CreateProtectionHandlerFromPublishingLicenseAsync
Crea un controlador de protección a partir de una licencia de publicación serializada.

Parámetros:  
* **serializedPublishingLicense**: Una licencia de publicación serializada 


* **Opciones de**: Opciones de creación 


* **observer**: Una clase que implementa el [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) interfaz 


* **context**: Contexto de cliente que se forma opaca pasados a los observadores y opcional [HttpDelegate](class_mip_httpdelegate.md)


  
### <a name="createprotectionhandlerfrompublishinglicense-function"></a>Función CreateProtectionHandlerFromPublishingLicense
Crea un controlador de protección a partir de una licencia de publicación serializada.

Parámetros:  
* **serializedPublishingLicense**: Una licencia de publicación serializada 


* **Opciones de**: Opciones de creación 


* **observer**: Una clase que implementa el [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) interfaz 


* **context**: Contexto de cliente que se pasará de manera opaca a opcional [HttpDelegate](class_mip_httpdelegate.md)



  
**Devuelve**: [ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerfromprotectioninfoasync-function"></a>Función CreateProtectionHandlerFromProtectionInfoAsync
Crea un controlador de protección de una licencia de publicación serializada y una información serializada de protección.

Parámetros:  
* **serializedPublishingLicense**: Una licencia de publicación serializada 


* **serializedProtectionInfo**: Una información serializada de protección 


* **observer**: Una clase que implementa el [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) interfaz 


* **context**: Contexto de cliente que se pasarán a los observadores de manera opaca


  
### <a name="createprotectionhandlerfromprotectioninfo-function"></a>Función CreateProtectionHandlerFromProtectionInfo
Crea un controlador de protección de una licencia de publicación serializada y una información serializada de protección.

Parámetros:  
* **serializedPublishingLicense**: Una licencia de publicación serializada 


* **serializedProtectionInfo**: Una información serializada de protección 


* **context**: Contexto de cliente que se pasarán a los observadores de manera opaca



  
**Devuelve**: [ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerfrompublishinglicensecontextasync-function"></a>CreateProtectionHandlerFromPublishingLicenseContextAsync function
Crea un controlador de protección a partir de un contexto de licencia de publicación.

Parámetros:  
* **publishingLicenseContext**: Un formulario de la licencia de publicación serializada preprocesado 


* **Opciones de**: Opciones de creación 


* **observer**: Una clase que implementa el [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) interfaz 


* **context**: Contexto de cliente que se forma opaca pasados a los observadores y opcional [HttpDelegate](class_mip_httpdelegate.md)


  
### <a name="createprotectionhandlerfrompublishinglicensecontext-function"></a>CreateProtectionHandlerFromPublishingLicenseContext function
Crea un controlador de protección a partir de un contexto de licencia de publicación.

Parámetros:  
* **publishingLicenseContext**: Un formulario de la licencia de publicación serializada preprocesado 


* **Opciones de**: Opciones de creación 


* **observer**: Una clase que implementa el [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) interfaz 


* **context**: Contexto de cliente que se pasará de manera opaca a opcional [HttpDelegate](class_mip_httpdelegate.md)



  
**Devuelve**: [ProtectionHandler](class_mip_protectionhandler.md)
