---
title: clase mip::FileEngine
description: 'Documenta la clase MIP:: fileengine de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: e397ad68fa39b318d6e4c08e36c450a474c3e5a9
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56255179"
---
# <a name="class-mipfileengine"></a>clase mip::FileEngine 
Esta clase proporciona una interfaz para todas las funciones de motor.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Devuelve la configuración del motor.
public const std::vector\<std::shared_ptr\<SensitivityTypesRulePackage\>\>& ListSensitivityTypes() const  |  Enumera los tipos de confidencialidad asociados con el motor de directiva.
public const std::vector\<std::shared_ptr\<Label\>\>& ListSensitivityLabels()  |  Devuelve una lista de etiquetas de confidencialidad.
public const std::string& GetMoreInfoUrl() const  |  Proporciona una URL para buscar más información sobre la directiva o las etiquetas.
public bool IsLabelingRequired() const  |  Comprueba si la directiva impone que un documento debe estar etiquetado.
pública CreateFileHandlerAsync void (const std:: String & inputFilePath, isAuditDiscoveryEnabled de bool const std:: String & contentIdentifier, contentState ContentState const, const std:: shared_ptr\<filehandler::Observer\>& fileHandlerObserver, const std:: shared_ptr\<void\>& contexto, const std:: shared_ptr\<FileExecutionState\>& fileExecutionState)  |  Empieza a crear un controlador de archivos para una ruta de acceso de archivo determinada.
pública CreateFileHandlerAsync void (const std:: shared_ptr\<Stream\>& inputStream, const std:: String & inputFilePath, const std:: String & contentIdentifier, const contentState mip::ContentState, bool isAuditDiscoveryEnabled, const std:: shared_ptr\<filehandler:: Observer\>& fileHandlerObserver, const std:: shared_ptr\<void\>& contexto, const std:: shared_ptr\< FileExecutionState\>& fileExecutionState)  |  Empieza a crear un controlador de archivos para una secuencia de archivos determinada.
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  Registra un evento específico de aplicación en la canalización de auditoría.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  Obtiene una lista de configuración personalizada.
  
## <a name="members"></a>Miembros
  
### <a name="getsettings-function"></a>Función GetSettings
Devuelve la configuración del motor.
  
### <a name="listsensitivitytypes-function"></a>Función ListSensitivityTypes
Enumera los tipos de confidencialidad asociados con el motor de directiva.

  
**Devuelve**: Una lista de etiquetas de confidencialidad. vacío si LoadSensitivityTypesEnabled era false)
  
**Vea también**: [FileEngine::Settings](class_mip_fileengine_settings.md)).
  
### <a name="listsensitivitylabels-function"></a>Función ListSensitivityLabels
Devuelve una lista de etiquetas de confidencialidad.
  
### <a name="getmoreinfourl-function"></a>Función GetMoreInfoUrl
Proporciona una URL para buscar más información sobre la directiva o las etiquetas.

  
**Devuelve**: Una dirección url en formato de cadena.
  
### <a name="islabelingrequired-function"></a>Función IsLabelingRequired
Comprueba si la directiva impone que un documento debe estar etiquetado.

  
**Devuelve**: True si el etiquetado es obligatoria, de lo contrario, false.
  
### <a name="createfilehandlerasync-function"></a>Función CreateFileHandlerAsync
Empieza a crear un controlador de archivos para una ruta de acceso de archivo determinada.

Parámetros:  
* **inputFilePath**: El archivo que se va a abrir. La ruta de acceso debe incluir el nombre de archivo y, si existe, la extensión de nombre de archivo. 


* **contentIdentifier**: un identificador legible para el contenido. ejemplo de un archivo: Ejemplo de "C:\mip-sdk-for-cpp\files\audit.docx" [ruta\nombre_archivo] para un correo electrónico: "RE: Auditoría design:user1@contoso.com"[Asunto: remitente] 


* **contentState**: El estado del contenido mientras la aplicación está interactuando con ella. 


* **isAuditDiscoveryEnabled**: que representa si la detección de auditoría está habilitada o no. 


* **fileHandlerObserver**: Una clase que implementa la interfaz [FileHandler::Observer](class_mip_filehandler_observer.md). 


* **context**: Contexto de cliente que se pasará de manera opaca hacia el observador.


  
### <a name="createfilehandlerasync-function"></a>Función CreateFileHandlerAsync
Empieza a crear un controlador de archivos para una secuencia de archivos determinada.

Parámetros:  
* **inputStream**: Una secuencia que contiene los datos del archivo. 


* **inputFilePath**: La ruta de acceso al archivo. La ruta de acceso debe incluir el nombre de archivo y, si existe, la extensión de nombre de archivo. 


* **contentIdentifier**: un identificador legible para el contenido. ejemplo de un archivo: Ejemplo de "C:\mip-sdk-for-cpp\files\audit.docx" [ruta\nombre_archivo] para un correo electrónico: "RE: Auditoría design:user1@contoso.com"[Asunto: remitente] 


* **contentState**: El estado del contenido mientras la aplicación está interactuando con ella. 


* **isAuditDiscoveryEnabled**: que representa si la detección de auditoría está habilitada o no. 


* **fileHandlerObserver**: Una clase que implementa la interfaz [FileHandler::Observer](class_mip_filehandler_observer.md). 


* **context**: Contexto de cliente que se pasará de manera opaca hacia el observador.


  
### <a name="sendapplicationauditevent-function"></a>Función SendApplicationAuditEvent
Registra un evento específico de aplicación en la canalización de auditoría.

Parámetros:  
* **nivel**: una descripción del nivel de registro: Información de Error/advertencia/información 


* **eventType**: descripción del tipo de evento. 


* **eventData**: datos asociados al evento.


  
### <a name="getcustomsettings-function"></a>Función GetCustomSettings
Obtiene una lista de configuración personalizada.

  
**Devuelve**: Un vector de configuración personalizada
