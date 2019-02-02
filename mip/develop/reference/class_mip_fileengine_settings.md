---
title: clase mip::FileEngine::Settings
description: 'Documenta la clase MIP:: fileengine de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: db189020c13340409d2aca2f0bdc054dfc961b09
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650772"
---
# <a name="class-mipfileenginesettings"></a>clase mip::FileEngine::Settings 
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
Configuración pública (const std:: String & engineId, const std:: String & clientData, const std:: String & configuración regional, bool loadSensitivityTypes)  |  Constructor [FileEngine::Settings](class_mip_fileengine_settings.md) para cargar un motor existente.
Configuración pública (const Identity & identidad, const std:: String & clientData, const std:: String & configuración regional, bool loadSensitivityTypes)  |  Constructor [FileProfile::Settings](class_mip_fileprofile_settings.md) para crear un nuevo motor.
public const std::string& GetEngineId() const  |  Devuelve el identificador del motor.
public void SetEngineId(const std::string& id)  |  Establece el identificador del motor.
public const Identity& GetIdentity() const  |  Devuelve el motor [identidad](class_mip_identity.md).
public void SetIdentity(const Identity& identity)  |  Establece la identidad del motor.
public const std::string& GetClientData() const  |  Devuelve los datos de cliente de motor.
public const std::string& GetLocale() const  |  Devuelve la configuración regional del motor.
pública SetCustomSettings void (const std:: vector\<std:: Pair\<std:: String, std:: String\>\>& valor)  |  Establece una lista de pares de nombre/valor que se usa para pruebas y experimentación.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  Obtiene una lista de pares de nombre/valor que se usa para pruebas y experimentación.
public void SetSessionId(const std::string& sessionId)  |  Establece el identificador de sesión del motor.
public const std::string& GetSessionId() const  |  Devuelve el identificador de sesión del motor.
public void SetProtectionCloudEndpointBaseUrl(const std::string& protectionCloudEndpointBaseUrl)  |  Establece la dirección URL base del punto de conexión en la nube de protección, que se usa para especificar los límites de la nube.
public const std::string& GetProtectionCloudEndpointBaseUrl() const  |  Obtiene el valor de cloudEndpointBaseUrl.
public void SetProtectionOnlyEngine(const bool protectionOnly)  |  Establece el indicador de motor solo de protección: sin directiva/etiqueta
public const bool IsProtectionOnlyEngine() const  |  Devuelve el indicador de motor solo de protección: sin directiva/etiqueta
public bool IsLoadSensitivityTypesEnabled() const  |  Obtener la marca que indica si está habilitada la carga de las etiquetas de confidencialidad.
  
## <a name="members"></a>Miembros
  
### <a name="settings-function"></a>Función de configuración
Constructor [FileEngine::Settings](class_mip_fileengine_settings.md) para cargar un motor existente.

Parámetros:  
* **engineId**: Establézcala en el identificador exclusivo del motor generado por AddEngineAsync. 


* **clientData**: datos de cliente personalizables que pueden almacenarse con el motor durante la descarga, pueden recuperarse de un motor cargado. 


* **locale**: la salida localizable del motor se proporcionará en esta configuración regional. 


* **loadSensitivityTypes**: Marca opcional que indica cuando se carga el motor debe cargar también tipos de sensibilidad personalizada, si se invocará el observador de OnPolicyChange true en el perfil en las actualizaciones de los tipos de sensibilidad personalizada, así como los cambios de directiva. Si llama ListSensitivityTypes falsas siempre devolverá una lista vacía.


  
### <a name="settings-function"></a>Función de configuración
Constructor [FileProfile::Settings](class_mip_fileprofile_settings.md) para crear un nuevo motor.

Parámetros:  
* **identity**: [Identidad](class_mip_identity.md) información del usuario asociado con el nuevo motor. 


* **clientData**: datos de cliente personalizables que pueden almacenarse con el motor durante la descarga, pueden recuperarse de un motor cargado. 


* **locale**: la salida localizable del motor se proporcionará en esta configuración regional. 


* **loadSensitivityTypes**: Marca opcional que indica cuando se carga el motor debe cargar también tipos de sensibilidad personalizada, si se invocará el observador de OnPolicyChange true en el perfil en las actualizaciones de los tipos de sensibilidad personalizada, así como los cambios de directiva. Si llama ListSensitivityTypes falsas siempre devolverá una lista vacía.


  
### <a name="getengineid-function"></a>Función GetEngineId
Devuelve el identificador del motor.
  
### <a name="setengineid-function"></a>Función SetEngineId
Establece el identificador del motor.

Parámetros:  
* **id**: identificador del motor.


  
### <a name="getidentity-function"></a>Función GetIdentity
Devuelve el motor [identidad](class_mip_identity.md).
  
### <a name="setidentity-function"></a>Función SetIdentity
Establece la identidad del motor.
  
### <a name="getclientdata-function"></a>Función amp; GetClientData
Devuelve los datos de cliente de motor.
  
### <a name="getlocale-function"></a>Función GetLocale
Devuelve la configuración regional del motor.
  
### <a name="setcustomsettings-function"></a>Función SetCustomSettings
Establece una lista de pares de nombre/valor que se usa para pruebas y experimentación.
  
### <a name="getcustomsettings-function"></a>Función GetCustomSettings
Obtiene una lista de pares de nombre/valor que se usa para pruebas y experimentación.
  
### <a name="setsessionid-function"></a>Función SetSessionId
Establece el identificador de sesión del motor.
  
### <a name="getsessionid-function"></a>Función GetSessionId
Devuelve el identificador de sesión del motor.
  
### <a name="setprotectioncloudendpointbaseurl-function"></a>Función SetProtectionCloudEndpointBaseUrl
Establece la dirección URL base del punto de conexión en la nube de protección, que se usa para especificar los límites de la nube.

Parámetros:  
* **protectionCloudEndpointBaseUrl**: Dirección url base asociada con los puntos de conexión de protección


  
### <a name="getprotectioncloudendpointbaseurl-function"></a>Función GetProtectionCloudEndpointBaseUrl
Obtiene el valor de cloudEndpointBaseUrl.

  
**Devuelve**: Dirección url base asociada con los puntos de conexión de protección
  
### <a name="setprotectiononlyengine-function"></a>Función SetProtectionOnlyEngine
Establece el indicador de motor solo de protección: sin directiva/etiqueta
  
### <a name="isprotectiononlyengine-function"></a>Función IsProtectionOnlyEngine
Devuelve el indicador de motor solo de protección: sin directiva/etiqueta
  
### <a name="isloadsensitivitytypesenabled-function"></a>Función IsLoadSensitivityTypesEnabled
Obtener la marca que indica si está habilitada la carga de las etiquetas de confidencialidad.

  
**Devuelve**: True si se habilita false else.