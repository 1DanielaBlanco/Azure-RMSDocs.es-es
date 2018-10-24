---
title: clase mip FileEngine
description: Referencia de la clase mip FileEngine
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a7342edf27b19f43881b2e8d378fa243d26f7056
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446080"
---
# <a name="class-mipfileengine"></a>clase mip::FileEngine 
Esta clase proporciona una interfaz para todas las funciones de motor.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Devuelve la configuración del motor.
public const std::vector<std::shared_ptr<Label>>& ListSensitivityLabels()  |  Devuelve una lista de etiquetas de confidencialidad.
 public const std::string& GetMoreInfoUrl() const  |  Proporciona una URL para buscar más información sobre la directiva o las etiquetas.
 public bool IsLabelingRequired() const  |  Comprueba si la directiva impone que un documento debe estar etiquetado.
public void CreateFileHandlerAsync(const std::string& inputFilePath, const ContentState contentState, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver, const std::shared_ptr<void>& context)  |  Empieza a crear un controlador de archivos para una ruta de acceso de archivo determinada.
public void CreateFileHandlerAsync(const std::shared_ptr<Stream>& inputStream, const std::string& inputFilePath, const mip::ContentState contentState, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver, const std::shared_ptr<void>& context)  |  Empieza a crear un controlador de archivos para una secuencia de archivos determinada.
 public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  Registra un evento específico de aplicación en la canalización de auditoría.
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Devuelve la configuración del motor.
  
### <a name="label"></a>Etiqueta
Devuelve una lista de etiquetas de confidencialidad.
  
### <a name="getmoreinfourl"></a>GetMoreInfoUrl
Proporciona una URL para buscar más información sobre la directiva o las etiquetas.

  
**Devuelve**: una URL con formato de cadena.
  
### <a name="islabelingrequired"></a>IsLabelingRequired
Comprueba si la directiva impone que un documento debe estar etiquetado.

  
**Devuelve**: “true” si el etiquetado es obligatorio; de lo contrario, devuelve “false”.
  
### <a name="createfilehandlerasync"></a>CreateFileHandlerAsync
Empieza a crear un controlador de archivos para una ruta de acceso de archivo determinada.

Parámetros:  
* **The**: archivo que se va a abrir. La ruta de acceso debe incluir el nombre de archivo y, si existe, la extensión de nombre de archivo. 


* **contentState**: estado del contenido mientras la aplicación interactúa con él. 


* **A**: clase que implementa la interfaz [FileHandler::Observer](class_mip_filehandler_observer.md). 


* **context**: contexto de cliente que se pasará de manera opaca hacia el observador.


  
### <a name="createfilehandlerasync"></a>CreateFileHandlerAsync
Empieza a crear un controlador de archivos para una secuencia de archivos determinada.

Parámetros:  
* **inputStream**: una secuencia que contiene los datos del archivo. 


* **inputFilePath**: ruta de acceso al archivo. La ruta de acceso debe incluir el nombre de archivo y, si existe, la extensión de nombre de archivo. 


* **contentState**: estado del contenido mientras la aplicación interactúa con él. 


* **fileHandlerObserver**: una clase que implementa la interfaz [FileHandler::Observer](class_mip_filehandler_observer.md). 


* **context**: contexto de cliente que se pasará de manera opaca hacia el observador.


  
### <a name="sendapplicationauditevent"></a>SendApplicationAuditEvent
Registra un evento específico de aplicación en la canalización de auditoría.

Parámetros:  
* **level**: una descripción del nivel de registro (información, error o advertencia) 


* **eventType**: descripción del tipo de evento. 


* **eventData**: datos asociados al evento.

