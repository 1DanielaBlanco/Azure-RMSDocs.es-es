---
title: clase mip ProtectionEngine Settings
description: Referencia de la clase mip ProtectionEngine Settings
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: f61e86a87ecfea21bc9d02f4e55f3fbe663e9b80
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446709"
---
# <a name="class-mipprotectionenginesettings"></a>clase mip::ProtectionEngine::Settings 
[Configuración](class_mip_protectionengine_settings.md) utilizada por [ProtectionEngine](class_mip_protectionengine.md) durante su creación y a lo largo de su vigencia.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  Constructor [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) para crear un nuevo motor.
 public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  Constructor [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) para cargar un motor existente.
 public const std::string& GetEngineId() const  |  Obtiene el id. del motor.
 public void SetEngineId(const std::string& engineId)  |  Establece el id. del motor.
 public const Identity& GetIdentity() const  |  Obtiene la identidad de usuario asociada al motor.
 public void SetIdentity(const Identity& identity)  |  Establece la identidad de usuario asociada al motor.
 public const std::string& GetClientData() const  |  Obtiene los datos personalizados especificados por el cliente.
 public void SetClientData(const std::string& clientData)  |  Obtiene los datos personalizados especificados por el cliente.
 public const std::string& GetLocale() const  |  Obtiene la configuración regional en la que se escribirán los datos del motor.
public void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& value)  |  Establece pares de nombre/valor que se usan para pruebas y experimentación.
public const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const  |  Obtiene pares de nombre/valor que se usan para pruebas y experimentación.
 public void SetSessionId(const std::string& sessionId)  |  Establece el id. de sesión del motor usado para la correlación de telemetría y registro.
 public const std::string& GetSessionId() const  |  Obtiene el id. de sesión del motor.
 public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  De manera opcional, establece la URL base del punto de conexión de la nube.
 public const std::string& GetCloudEndpointBaseUrl() const  |  Obtiene la URL base de la nube usada por todas las solicitudes de servicio (si se especifica).
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Constructor [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) para crear un nuevo motor.

Parámetros:  
* **identity**: identidad que se asociará a [ProtectionEngine](class_mip_protectionengine.md).


* **clientData**: datos de cliente personalizables que pueden almacenarse con el motor durante la descarga y pueden recuperarse de un motor cargado. 


* **locale**: la salida del motor se proporcionará en esta configuración regional.


  
### <a name="settings"></a>Configuración
Constructor [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) para cargar un motor existente.

Parámetros:  
* **engineId**: identificador único del motor que se va a cargar. 


* **clientData**: datos de cliente personalizables que pueden almacenarse con el motor durante la descarga y pueden recuperarse de un motor cargado. 


* **locale**: la salida del motor se proporcionará en esta configuración regional.


  
### <a name="getengineid"></a>GetEngineId
Obtiene el id. del motor.

  
**Devuelve**: id. del motor.
  
### <a name="setengineid"></a>SetEngineId
Establece el id. del motor.

Parámetros:  
* **engineId**: id. del motor.


  
### <a name="getidentity"></a>GetIdentity
Obtiene la identidad de usuario asociada al motor.

  
**Devuelve**: identidad de usuario asociada al motor
  
### <a name="setidentity"></a>SetIdentity
Establece la identidad de usuario asociada al motor.

Parámetros:  
* **identity**: identidad de usuario asociada al motor


  
### <a name="getclientdata"></a>GetClientData
Obtiene los datos personalizados especificados por el cliente.

  
**Devuelve**: datos personalizados especificados por el cliente
  
### <a name="setclientdata"></a>SetClientData
Obtiene los datos personalizados especificados por el cliente.

Parámetros:  
* **Custom**: datos especificados por el cliente.


  
### <a name="getlocale"></a>GetLocale
Obtiene la configuración regional en la que se escribirán los datos del motor.

  
**Devuelve**: la configuración regional en la que se escribirán los datos del motor
  
### <a name="setcustomsettings"></a>SetCustomSettings
Establece pares de nombre/valor que se usan para pruebas y experimentación.

Parámetros:  
* **customSettings**: pares de nombre/valor que se usan para pruebas y experimentación.


  
### <a name="getcustomsettings"></a>GetCustomSettings
Obtiene pares de nombre/valor que se usan para pruebas y experimentación.

  
**Devuelve**: pares de nombre/valor que se usan para pruebas y experimentación.
  
### <a name="setsessionid"></a>SetSessionId
Establece el id. de sesión del motor usado para la correlación de telemetría y registro.

Parámetros:  
* **sessionId**: id. de sesión del motor usado para la correlación de telemetría/registro.


  
### <a name="getsessionid"></a>GetSessionId
Obtiene el id. de sesión del motor.

  
**Devuelve**: id. de sesión del motor.
  
### <a name="setcloudendpointbaseurl"></a>SetCloudEndpointBaseUrl
De manera opcional, establece la URL base del punto de conexión de la nube.

Parámetros:  
* **cloudEndpointBaseUrl**: la URL base usada por todas las solicitudes de servicio (por ejemplo, “https://api.aadrm.com”).


Si no se especifica la URL base, se determinará mediante una búsqueda DNS del dominio de la identidad del motor.
  
### <a name="getcloudendpointbaseurl"></a>GetCloudEndpointBaseUrl
Obtiene la URL base de la nube usada por todas las solicitudes de servicio (si se especifica).

  
**Devuelve**: URL base.