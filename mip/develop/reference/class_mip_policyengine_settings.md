---
title: clase mip PolicyEngine Settings
description: Referencia de la clase mip PolicyEngine Settings
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 6ac94d1e34615a0248dac85f28c55154b127574f
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446352"
---
# <a name="class-mippolicyenginesettings"></a>clase mip::PolicyEngine::Settings 
Define la configuración asociada a un elemento [PolicyEngine](class_mip_policyengine.md).
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  Constructor [PolicyEngine::Settings](class_mip_policyengine_settings.md) para cargar un motor existente.
 public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  Constructor [PolicyEngine::Settings](class_mip_policyengine_settings.md) para crear un motor.
 public const std::string& GetEngineId() const  |  Obtiene el identificador del motor.
 public void SetEngineId(const std::string& id)  |  Establece el identificador del motor.
 public const Identity& GetIdentity() const  |  Obtiene el objeto Identity.
 public void SetIdentity(const Identity& identity)  |  Establece el objeto Identity.
 public const std::string& GetClientData() const  |  Obtiene los datos de cliente establecidos en la configuración.
 public void SetClientData(const std::string& clientData)  |  Establece la cadena de datos de cliente.
 public const std::string& GetLocale() const  |  Obtiene la configuración regional establecida en la configuración.
public void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& customSettings)  |  Establece la configuración personalizada, que se utiliza para el acceso y las pruebas de características.
public const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const  |  Obtiene la configuración personalizada, que se utiliza para el acceso y las pruebas de características.
 public void SetSessionId(const std::string& sessionId)  |  Establece el identificador de sesión utilizado para la telemetría definida por el cliente.
 public const std::string& GetSessionId() const  |  Obtiene el identificador de sesión, un identificador único.
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Constructor [PolicyEngine::Settings](class_mip_policyengine_settings.md) para cargar un motor existente.

Parámetros:  
* **engineId**: establézcalo en el identificador del motor único generado por AddEngineAsync o en uno autogenerado. Cuando se carga un motor existente, se reutiliza el identificador; de lo contrario, se creará un nuevo motor. 


* **clientData**: datos de cliente personalizables que pueden almacenarse con el motor durante la descarga, pueden recuperarse de un motor cargado. 


* **locale**: la salida localizable del motor se proporcionará en esta configuración regional.


  
### <a name="settings"></a>Configuración
Constructor [PolicyEngine::Settings](class_mip_policyengine_settings.md) para crear un motor.

Parámetros:  
* **identity**: información de identidad del usuario asociado con el nuevo motor. 


* **clientData**: datos de cliente personalizables que pueden almacenarse con el motor durante la descarga, pueden recuperarse de un motor cargado. 


* **locale**: la salida localizable del motor se proporcionará en esta configuración regional.


  
### <a name="getengineid"></a>GetEngineId
Obtiene el identificador del motor.

  
**Devuelve**: una cadena única que identifica el motor.
  
### <a name="setengineid"></a>SetEngineId
Establece el identificador del motor.

Parámetros:  
* **id**: identificador del motor.


  
### <a name="getidentity"></a>GetIdentity
Obtiene el objeto Identity.

  
**Devuelve**: una referencia a la identidad en el objeto de configuración. 
  
**Consulte también**: mip::Identity
  
### <a name="setidentity"></a>SetIdentity
Establece el objeto Identity.

Parámetros:  
* **identity**: la identidad única de un usuario. 


  
**Consulte también**: mip::Identity
  
### <a name="getclientdata"></a>GetClientData
Obtiene los datos de cliente establecidos en la configuración.

  
**Devuelve**: una cadena de datos especificada por el cliente.
  
### <a name="setclientdata"></a>SetClientData
Establece la cadena de datos de cliente.

Parámetros:  
* **clientData**: datos especificados por el usuario.


  
### <a name="getlocale"></a>GetLocale
Obtiene la configuración regional establecida en la configuración.

  
**Devuelve**: la configuración regional.
  
### <a name="setcustomsettings"></a>SetCustomSettings
Establece la configuración personalizada, que se utiliza para el acceso y las pruebas de características.

Parámetros:  
* **customSettings**: lista de pares nombre-valor.


  
### <a name="getcustomsettings"></a>GetCustomSettings
Obtiene la configuración personalizada, que se utiliza para el acceso y las pruebas de características.

  
**Devuelve**: lista de pares nombre-valor.
  
### <a name="setsessionid"></a>SetSessionId
Establece el identificador de sesión utilizado para la telemetría definida por el cliente.

Parámetros:  
* **sessionId**: una cadena única que se conecta a eventos de telemetría.


  
### <a name="getsessionid"></a>GetSessionId
Obtiene el identificador de sesión, un identificador único.

  
**Devuelve**: identificador de la sesión.