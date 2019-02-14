---
title: Clase mip::PolicyProfile::Settings
description: Documenta la clase mip::policyprofile de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: a857f8f2dd9b5544fbdff4949c833f048bb78aca
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56253397"
---
# <a name="class-mippolicyprofilesettings"></a>Clase mip::PolicyProfile::Settings 
[Configuración](class_mip_policyprofile_settings.md) que usa [PolicyProfile](class_mip_policyprofile.md) durante su creación y vigencia.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
Configuración pública (const std:: String & ruta de acceso, bool useInMemoryStorage, const std:: shared_ptr\<AuthDelegate\>& authDelegate, const std:: shared_ptr\<PolicyProfile::Observer\>& Observer, const ApplicationInfo & applicationInfo)  |  Interfaz para configurar el perfil.
public const std::string& GetPath() const  |  Obtiene la ruta de acceso al estado almacenado.
public bool GetUseInMemoryStorage() const  |  Obtiene la marca de uso de almacenamiento en memoria.
Public const std:: shared_ptr\<AuthDelegate\>& GetAuthDelegate() const  |  Obtiene el delegado de autenticación.
Public const std:: shared_ptr\<PolicyProfile::Observer\>& GetObserver() const  |  Obtiene el observador de eventos.
public const ApplicationInfo GetApplicationInfo() const  |  Obtiene la información de aplicación.
Public std:: shared_ptr\<LoggerDelegate\> GetLoggerDelegate() const  |  Obtiene el delegado del registrador (si existe) proporcionado por la aplicación.
pública SetLoggerDelegate void (const std:: shared_ptr\<LoggerDelegate\>& loggerDelegate)  |  Invalida el registrador predeterminado.
Public std:: shared_ptr\<HttpDelegate\> GetHttpDelegate() const  |  Obtiene el delegado HTTP (si existe) proporcionado por la aplicación.
pública SetHttpDelegate void (const std:: shared_ptr\<HttpDelegate\>& httpDelegate)  |  Reemplaza la pila HTTP predeterminada por la del cliente.
public void OptOutTelemetry()  |  No participa en la recopilación de toda la telemetría.
public bool IsTelemetryOptedOut() const  |  Obtiene si se tiene que deshabilitar o no la recopilación de telemetría.
public void SetMinimumLogLevel(LogLevel logLevel)  |  Establece el nivel de registro mínimo que desencadenará un evento de registro.
public LogLevel GetMinimumLogLevel() const  |  Obtiene el objeto de nivel de registro mínimo.
  
## <a name="members"></a>Miembros
  
### <a name="settings-function"></a>Función de configuración
Interfaz para configurar el perfil.

Parámetros:  
* **Ruta de acceso**: La ruta de acceso a un directorio en el que el SDK almacenará el estado del perfil. 


* **useInMemoryStorage**: Store cualquier estado almacenado en caché en memoria en lugar de en disco. 


* **authDelegate**: El delegado de autenticación utilizado por el SDK para adquirir tokens de autenticación. 


* **observer**: Una clase que implementa el [PolicyProfile::Observer](class_mip_policyprofile_observer.md) interfaz. Puede se nullptr. 


* **applicationInfo**: Los identificadores de aplicación usados para el acceso al servicio.


  
### <a name="getpath-function"></a>Función GetPath
Obtiene la ruta de acceso al estado almacenado.

  
**Devuelve**: Ruta de acceso al estado almacenado.
  
### <a name="getuseinmemorystorage-function"></a>Función GetUseInMemoryStorage
Obtiene la marca de uso de almacenamiento en memoria.

  
**Devuelve**: True si se establece el uso de memoria lo contrario, false.
  
### <a name="getauthdelegate-function"></a>Función GetAuthDelegate
Obtiene el delegado de autenticación.

  
**Devuelve**: El delegado de autenticación.
  
### <a name="getobserver-function"></a>Función GetObserver
Obtiene el observador de eventos.

  
**Devuelve**: El observador de eventos.
  
### <a name="getapplicationinfo-function"></a>Función GetApplicationInfo
Obtiene la información de aplicación.

  
**Devuelve**: La información de la aplicación.
  
### <a name="getloggerdelegate-function"></a>Función GetLoggerDelegate
Obtiene el delegado del registrador (si existe) proporcionado por la aplicación.

  
**Devuelve**: Registrador
  
### <a name="setloggerdelegate-function"></a>Función SetLoggerDelegate
Invalida el registrador predeterminado.

Parámetros:  
* **loggerDelegate**: Registro de la interfaz de devolución de llamada implementada por las aplicaciones cliente


Las aplicaciones cliente deben llamar a este método si desean usar su propia implementación del registrador.
  
### <a name="gethttpdelegate-function"></a>Función GetHttpDelegate
Obtiene el delegado HTTP (si existe) proporcionado por la aplicación.

  
**Devuelve**: Delegado de HTTP que se usará para las operaciones de HTTP
  
### <a name="sethttpdelegate-function"></a>Función SetHttpDelegate
Reemplaza la pila HTTP predeterminada por la del cliente.

Parámetros:  
* **httpDelegate**: Interfaz de devolución de llamada HTTP implementada por la aplicación cliente


  
### <a name="optouttelemetry-function"></a>Función OptOutTelemetry
No participa en la recopilación de toda la telemetría.
  
### <a name="istelemetryoptedout-function"></a>Función IsTelemetryOptedOut
Obtiene si se tiene que deshabilitar o no la recopilación de telemetría.

  
**Devuelve**: True si se debe deshabilitar la recopilación de telemetría false else
  
### <a name="setminimumloglevel-function"></a>Función SetMinimumLogLevel
Establece el nivel de registro mínimo que desencadenará un evento de registro.

Parámetros:  
* **logLevel**: nivel de registro mínimo que desencadenará un evento de registro. 



  
**Devuelve**: True
  
### <a name="getminimumloglevel-function"></a>Función GetMinimumLogLevel
Obtiene el objeto de nivel de registro mínimo.

  
**Devuelve**: Nivel de registro mínimo que se desencadenará un evento de registro.
