---
title: clase mip::PolicyEngine::Settings
description: 'Documenta la clase MIP:: policyengine de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 6ad384768ef876109a6a43237765474345a666bc
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56257542"
---
# <a name="class-mippolicyenginesettings"></a>clase mip::PolicyEngine::Settings 
Define la configuración asociada a un elemento [PolicyEngine](class_mip_policyengine.md).
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
Configuración pública (const std:: String & engineId, const std:: String & clientData, const std:: String & configuración regional, bool loadSensitivityTypes)  |  Constructor [PolicyEngine::Settings](class_mip_policyengine_settings.md) para cargar un motor existente.
Configuración pública (const Identity & identidad, const std:: String & clientData, const std:: String & configuración regional, bool loadSensitivityTypes)  |  Constructor [PolicyEngine::Settings](class_mip_policyengine_settings.md) para crear un motor.
public const std::string& GetEngineId() const  |  Obtiene el identificador del motor.
public void SetEngineId(const std::string& id)  |  Establece el identificador del motor.
public const Identity& GetIdentity() const  |  Obtener el [identidad](class_mip_identity.md) objeto.
public void SetIdentity(const Identity& identity)  |  Establecer el [identidad](class_mip_identity.md) objeto.
public const std::string& GetClientData() const  |  Obtiene los datos de cliente establecidos en la configuración.
public void SetClientData(const std::string& clientData)  |  Establece la cadena de datos de cliente.
public const std::string& GetLocale() const  |  Obtiene la configuración regional establecida en la configuración.
pública SetCustomSettings void (const std:: vector\<std:: Pair\<std:: String, std:: String\>\>& customSettings)  |  Establece la configuración personalizada, que se utiliza para el acceso y las pruebas de características.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  Obtiene la configuración personalizada, que se utiliza para el acceso y las pruebas de características.
public void SetSessionId(const std::string& sessionId)  |  Establece el identificador de sesión utilizado para la telemetría definida por el cliente.
public const std::string& GetSessionId() const  |  Obtiene el identificador de sesión, un identificador único.
public bool IsLoadSensitivityTypesEnabled() const  |  Obtener la marca que indica si está habilitada la carga de las etiquetas de confidencialidad.
  
## <a name="members"></a>Miembros
  
### <a name="settings-function"></a>Función de configuración
Constructor [PolicyEngine::Settings](class_mip_policyengine_settings.md) para cargar un motor existente.

Parámetros:  
* **engineId**: Establézcala en el identificador exclusivo del motor generado por AddEngineAsync o uno generado automáticamente. Cuando se carga un motor existente, se reutiliza el identificador; de lo contrario, se creará un nuevo motor. 


* **clientData**: datos de cliente personalizables que pueden almacenarse con el motor durante la descarga, pueden recuperarse de un motor cargado. 


* **locale**: la salida localizable del motor se proporcionará en esta configuración regional. 


* **Opcional**: marca que indica cuando se carga el motor debe cargar también los tipos de sensibilidad personalizada, si se invocará el observador de OnPolicyChange true en el perfil en las actualizaciones de los tipos de sensibilidad personalizada, así como los cambios de directiva. Si llama ListSensitivityTypes falsas siempre devolverá una lista vacía.


  
### <a name="settings-function"></a>Función de configuración
Constructor [PolicyEngine::Settings](class_mip_policyengine_settings.md) para crear un motor.

Parámetros:  
* **identity**: [Identidad](class_mip_identity.md) información del usuario asociado con el nuevo motor. 


* **clientData**: datos de cliente personalizables que pueden almacenarse con el motor durante la descarga, pueden recuperarse de un motor cargado. 


* **locale**: la salida localizable del motor se proporcionará en esta configuración regional. 


* **Opcional**: marca que indica cuando se carga el motor debe cargar también los tipos de sensibilidad personalizada, si se invocará el observador de OnPolicyChange true en el perfil en las actualizaciones de los tipos de sensibilidad personalizada, así como los cambios de directiva. Si llama ListSensitivityTypes falsas siempre devolverá una lista vacía.


  
### <a name="getengineid-function"></a>Función GetEngineId
Obtiene el identificador del motor.

  
**Devuelve**: Una cadena única que identifica al motor.
  
### <a name="setengineid-function"></a>Función SetEngineId
Establece el identificador del motor.

Parámetros:  
* **id**: identificador del motor.


  
### <a name="getidentity-function"></a>Función GetIdentity
Obtener el [identidad](class_mip_identity.md) objeto.

  
**Devuelve**: Una referencia a la identidad en el objeto de configuración. 
  
**Vea también**: [MIP:: Identity](class_mip_identity.md)
  
### <a name="setidentity-function"></a>Función SetIdentity
Establecer el [identidad](class_mip_identity.md) objeto.

Parámetros:  
* **identity**: la identidad única de un usuario. 


  
**Vea también**: [MIP:: Identity](class_mip_identity.md)
  
### <a name="getclientdata-function"></a>Función amp; GetClientData
Obtiene los datos de cliente establecidos en la configuración.

  
**Devuelve**: Una cadena de datos especificados por el cliente.
  
### <a name="setclientdata-function"></a>Función SetClientData
Establece la cadena de datos de cliente.

Parámetros:  
* **clientData**: datos especificados por el usuario.


  
### <a name="getlocale-function"></a>Función GetLocale
Obtiene la configuración regional establecida en la configuración.

  
**Devuelve**: La configuración regional.
  
### <a name="setcustomsettings-function"></a>Función SetCustomSettings
Establece la configuración personalizada, que se utiliza para el acceso y las pruebas de características.

Parámetros:  
* **customSettings**: Lista de pares nombre-valor.


  
### <a name="getcustomsettings-function"></a>Función GetCustomSettings
Obtiene la configuración personalizada, que se utiliza para el acceso y las pruebas de características.

  
**Devuelve**: Lista de pares nombre-valor.
  
### <a name="setsessionid-function"></a>Función SetSessionId
Establece el identificador de sesión utilizado para la telemetría definida por el cliente.

Parámetros:  
* **sessionId**: una cadena única que se conecta a eventos de telemetría.


  
### <a name="getsessionid-function"></a>Función GetSessionId
Obtiene el identificador de sesión, un identificador único.

  
**Devuelve**: El identificador de sesión.
  
### <a name="isloadsensitivitytypesenabled-function"></a>Función IsLoadSensitivityTypesEnabled
Obtener la marca que indica si está habilitada la carga de las etiquetas de confidencialidad.

  
**Devuelve**: True si se habilita false else.
