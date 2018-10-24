---
title: clase mip PolicyEngine
description: Referencia de la clase mip PolicyEngine
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 57dd325e9c00a3cb2a4056f7ef0b522efef5d0c4
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446046"
---
# <a name="class-mippolicyengine"></a>clase mip::PolicyEngine 
Esta clase proporciona una interfaz para todas las funciones de motor.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Obtiene la [configuración](class_mip_policyengine_settings.md) del motor de directivas.
public const std::vector<std::shared_ptr<Label>>& ListSensitivityLabels()  |  Muestra las etiquetas de confidencialidad asociadas con el motor de directivas.
 public const std::string& GetMoreInfoUrl() const  |  Proporciona una URL para buscar más información sobre la directiva o las etiquetas.
 public bool IsLabelingRequired() const  |  Comprueba si la directiva indica que un documento tiene que etiquetarse o no.
public std::shared_ptr<Label> GetDefaultSensitivityLabel()  |  Obtiene la etiqueta de confidencialidad predeterminada.
public std::shared_ptr<PolicyHandler> CreatePolicyHandler(const std::string& contentIdentifier)  |  Crea un controlador de directiva para ejecutar funciones relacionadas con directivas en el estado de ejecución de un archivo.
 public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  Registra un evento específico de aplicación en la canalización de auditoría.
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Obtiene la [configuración](class_mip_policyengine_settings.md) del motor de directivas.

  
**Devuelve**: configuración del motor de directivas. 
  
**Consulte también**: [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md)
  
### <a name="label"></a>Etiqueta
Muestra las etiquetas de confidencialidad asociadas con el motor de directivas.

  
**Devuelve**: una lista de etiquetas de confidencialidad.
  
### <a name="getmoreinfourl"></a>GetMoreInfoUrl
Proporciona una URL para buscar más información sobre la directiva o las etiquetas.

  
**Devuelve**: una URL con formato de cadena.
  
### <a name="islabelingrequired"></a>IsLabelingRequired
Comprueba si la directiva indica que un documento tiene que etiquetarse o no.

  
**Devuelve**: “true” si el etiquetado es obligatorio; de lo contrario, devuelve “false”.
  
### <a name="label"></a>Etiqueta
Obtiene la etiqueta de confidencialidad predeterminada.

  
**Devuelve**: la etiqueta de confidencialidad predeterminada (si existe); nullptr si no hay ningún conjunto de etiquetas predeterminado.
  
### <a name="policyhandler"></a>PolicyHandler
Crea un controlador de directiva para ejecutar funciones relacionadas con directivas en el estado de ejecución de un archivo.

Parámetros:  
* **contentIdentifier**: un identificador en lenguaje natural del contenido. ejemplo de un archivo: "C:\mip-sdk-for-cpp\files\audit.docx" [ruta] ejemplo de un correo electrónico: "RE: Auditar design:user1@contoso.com" [Asunto:Remitente]



  
**Devuelve**: controlador de directiva.
  
### <a name="sendapplicationauditevent"></a>SendApplicationAuditEvent
Registra un evento específico de aplicación en la canalización de auditoría.

Parámetros:  
* **description**: descripción del nivel de registro (información, error o advertencia). 


* **eventType**: descripción del tipo de evento. 


* **eventData**: datos asociados al evento.

