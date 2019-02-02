---
title: clase mip::PolicyEngine
description: 'Documenta la clase MIP:: policyengine de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 298d9789fb46c2725401425af51a9de8b3436f53
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650976"
---
# <a name="class-mippolicyengine"></a>clase mip::PolicyEngine 
Esta clase proporciona una interfaz para todas las funciones de motor.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Obtiene la [configuración](class_mip_policyengine_settings.md) del motor de directivas.
public const std::vector\<std::shared_ptr\<Label\>\>& ListSensitivityLabels()  |  Muestra las etiquetas de confidencialidad asociadas con el motor de directivas.
public const std::vector\<std::shared_ptr\<SensitivityTypesRulePackage\>\>& ListSensitivityTypes() const  |  Enumera los tipos de confidencialidad asociados con el motor de directiva.
public const std::string& GetMoreInfoUrl() const  |  Proporciona una URL para buscar más información sobre la directiva o las etiquetas.
public bool IsLabelingRequired() const  |  Comprueba si la directiva indica que un documento tiene que etiquetarse o no.
Public std:: shared_ptr\<etiqueta\> GetDefaultSensitivityLabel()  |  Obtiene la etiqueta de confidencialidad predeterminada.
Public std:: shared_ptr\<PolicyHandler\> CreatePolicyHandler (bool isAuditDiscoveryEnabled)  |  Crea un controlador de directiva para ejecutar funciones relacionadas con directivas en el estado de ejecución de un archivo.
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  Registra un evento específico de aplicación en la canalización de auditoría.
Public const std:: String & GetPolicyDataXml() const  |  Obtiene los datos de la directiva XML que describe la configuración, las etiquetas y reglas asociadas a esta directiva.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  Obtiene una lista de configuración personalizada.
  
## <a name="members"></a>Miembros
  
### <a name="getsettings-function"></a>Función GetSettings
Obtiene la [configuración](class_mip_policyengine_settings.md) del motor de directivas.

  
**Devuelve**: Configuración del motor de directiva. 
  
**Consulte también**: [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md)
  
### <a name="listsensitivitylabels-function"></a>Función ListSensitivityLabels
Muestra las etiquetas de confidencialidad asociadas con el motor de directivas.

  
**Devuelve**: Una lista de etiquetas de confidencialidad.
  
### <a name="listsensitivitytypes-function"></a>Función ListSensitivityTypes
Enumera los tipos de confidencialidad asociados con el motor de directiva.

  
**Devuelve**: Una lista de etiquetas de confidencialidad. vacío si LoadSensitivityTypesEnabled era false)
  
**Vea también**: [PolicyEngine::Settings](class_mip_policyengine_settings.md)).
  
### <a name="getmoreinfourl-function"></a>Función GetMoreInfoUrl
Proporciona una URL para buscar más información sobre la directiva o las etiquetas.

  
**Devuelve**: Una dirección url en formato de cadena.
  
### <a name="islabelingrequired-function"></a>Función IsLabelingRequired
Comprueba si la directiva indica que un documento tiene que etiquetarse o no.

  
**Devuelve**: True si el etiquetado es obligatoria, de lo contrario, false.
  
### <a name="getdefaultsensitivitylabel-function"></a>Función GetDefaultSensitivityLabel
Obtiene la etiqueta de confidencialidad predeterminada.

  
**Devuelve**: Etiqueta de confidencialidad el valor predeterminado si existe, nullptr si no hay ninguna etiqueta predeterminada establecida.
  
### <a name="createpolicyhandler-function"></a>Función CreatePolicyHandler
Crea un controlador de directiva para ejecutar funciones relacionadas con directivas en el estado de ejecución de un archivo.

Parámetros:  
* **Un**: bool que representa si la detección de auditoría está habilitada o no



  
**Devuelve**: Controlador de la directiva.
Aplicación necesita mantener el objeto de controlador de la directiva durante la vigencia del documento
  
### <a name="sendapplicationauditevent-function"></a>Función SendApplicationAuditEvent
Registra un evento específico de aplicación en la canalización de auditoría.

Parámetros:  
* **nivel**: el nivel de registro: Información de Error/advertencia/información 


* **eventType**: descripción del tipo de evento. 


* **eventData**: datos asociados al evento.


  
### <a name="getpolicydataxml-function"></a>Función GetPolicyDataXml
Obtiene los datos de la directiva XML que describe la configuración, las etiquetas y reglas asociadas a esta directiva.

  
**Devuelve**: Datos de la directiva XML
  
### <a name="getcustomsettings-function"></a>Función GetCustomSettings
Obtiene una lista de configuración personalizada.

  
**Devuelve**: Un vector de configuración personalizada