---
title: clase mip::ProtectionEngine::Settings
description: Documenta la clase mip::protectionengine de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: d4f4902626dcedb4bcc64a46a1bef2a0c49ca8f6
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56254890"
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
public const Identity& GetIdentity() const  |  Obtiene el usuario [identidad](class_mip_identity.md) asociadas con el motor.
public void SetIdentity(const Identity& identity)  |  Establece el usuario [identidad](class_mip_identity.md) asociadas con el motor.
public const std::string& GetClientData() const  |  Obtiene los datos personalizados especificados por el cliente.
public void SetClientData(const std::string& clientData)  |  Obtiene los datos personalizados especificados por el cliente.
public const std::string& GetLocale() const  |  Obtiene la configuración regional en la que se escribirán los datos del motor.
pública SetCustomSettings void (const std:: vector\<std:: Pair\<std:: String, std:: String\>\>& valor)  |  Establece pares de nombre/valor que se usan para pruebas y experimentación.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  Obtiene pares de nombre/valor que se usan para pruebas y experimentación.
public void SetSessionId(const std::string& sessionId)  |  Establece el id. de sesión del motor usado para la correlación de telemetría y registro.
public const std::string& GetSessionId() const  |  Obtiene el id. de sesión del motor.
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  De manera opcional, establece la URL base del punto de conexión de la nube.
public const std::string& GetCloudEndpointBaseUrl() const  |  Obtiene la URL base de la nube usada por todas las solicitudes de servicio (si se especifica).
  
## <a name="members"></a>Miembros
  
### <a name="settings-function"></a>Función de configuración
Constructor [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) para crear un nuevo motor.

Parámetros:  
* **identity**: [Identidad](class_mip_identity.md) que se asociará con [ProtectionEngine](class_mip_protectionengine.md)


* **clientData**: datos de cliente personalizables que pueden almacenarse con el motor durante la descarga y pueden recuperarse de un motor cargado. 


* **locale**: Salida del motor se proporcionará en esta configuración regional.


  
### <a name="settings-function"></a>Función de configuración
Constructor [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) para cargar un motor existente.

Parámetros:  
* **engineId**: Identificador único del motor de que se van a cargar 


* **clientData**: datos de cliente personalizables que pueden almacenarse con el motor durante la descarga y pueden recuperarse de un motor cargado. 


* **locale**: Salida del motor se proporcionará en esta configuración regional.


  
### <a name="getengineid-function"></a>Función GetEngineId
Obtiene el id. del motor.

  
**Devuelve**: Identificador de motor
  
### <a name="setengineid-function"></a>Función SetEngineId
Establece el id. del motor.

Parámetros:  
* **engineId**: id. del motor.


  
### <a name="getidentity-function"></a>Función GetIdentity
Obtiene el usuario [identidad](class_mip_identity.md) asociadas con el motor.

  
**Devuelve**: Usuario [identidad](class_mip_identity.md) asociadas con el motor
  
### <a name="setidentity-function"></a>Función SetIdentity
Establece el usuario [identidad](class_mip_identity.md) asociadas con el motor.

Parámetros:  
* **identity**: Usuario [identidad](class_mip_identity.md) asociadas con el motor


  
### <a name="getclientdata-function"></a>Función amp; GetClientData
Obtiene los datos personalizados especificados por el cliente.

  
**Devuelve**: Datos personalizados especificados por el cliente
  
### <a name="setclientdata-function"></a>Función SetClientData
Obtiene los datos personalizados especificados por el cliente.

Parámetros:  
* **Custom**: datos especificados por el cliente.


  
### <a name="getlocale-function"></a>Función GetLocale
Obtiene la configuración regional en la que se escribirán los datos del motor.

  
**Devuelve**: En el motor se escribirán los datos de configuración regional
  
### <a name="setcustomsettings-function"></a>Función SetCustomSettings
Establece pares de nombre/valor que se usan para pruebas y experimentación.

Parámetros:  
* **customSettings**: Se usa para pruebas y experimentación de pares nombre/valor


  
### <a name="getcustomsettings-function"></a>Función GetCustomSettings
Obtiene pares de nombre/valor que se usan para pruebas y experimentación.

  
**Devuelve**: Se usa para pruebas y experimentación de pares nombre/valor
  
### <a name="setsessionid-function"></a>Función SetSessionId
Establece el id. de sesión del motor usado para la correlación de telemetría y registro.

Parámetros:  
* **sessionId**: Identificador de sesión del motor, utilizado para la correlación de telemetría/registro


  
### <a name="getsessionid-function"></a>Función GetSessionId
Obtiene el id. de sesión del motor.

  
**Devuelve**: Id. de sesión del motor
  
### <a name="setcloudendpointbaseurl-function"></a>Función SetCloudEndpointBaseUrl
De manera opcional, establece la URL base del punto de conexión de la nube.

Parámetros:  
* **cloudEndpointBaseUrl**: la URL base usada por todas las solicitudes de servicio (por ejemplo, “https://api.aadrm.com”).


Si no se especifica la URL base, se determinará mediante una búsqueda DNS del dominio de la identidad del motor.
  
### <a name="getcloudendpointbaseurl-function"></a>Función GetCloudEndpointBaseUrl
Obtiene la URL base de la nube usada por todas las solicitudes de servicio (si se especifica).

  
**Devuelve**: Dirección URL base
