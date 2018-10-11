---
title: Configuración de la clase mip::PolicyProfile::Settings
description: Referencia de la configuración de la clase mip::PolicyProfile::Settings
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 07cbcbc022c02a43f751e1cf55b5b0efdfb816d1
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446910"
---
# <a name="class-mippolicyprofilesettings"></a>Clase mip::PolicyProfile::Settings 
La [configuración](class_mip_policyprofile_settings.md) que utiliza [PolicyProfile](class_mip_policyprofile.md) durante su creación y a lo largo de su vigencia.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<PolicyProfile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  Interfaz para configurar el perfil.
 public const std::string& GetPath() const  |  Obtiene la ruta de acceso al estado almacenado.
 public bool GetUseInMemoryStorage() const  |  Obtiene la marca de uso de almacenamiento en memoria.
public const std::shared_ptr<AuthDelegate>& GetAuthDelegate() const  |  Obtiene el delegado de autenticación.
public const std::shared_ptr<PolicyProfile::Observer>& GetObserver() const  |  Obtiene el observador de eventos.
 public const ApplicationInfo GetApplicationInfo() const  |  Obtiene la información de aplicación.
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  Obtiene el delegado del registrador (si existe) proporcionado por la aplicación.
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  Invalida el registrador predeterminado.
public std::shared_ptr<HttpDelegate> GetHttpDelegate() const  |  Obtiene el delegado HTTP (si existe) proporcionado por la aplicación.
public void SetHttpDelegate(const std::shared_ptr<HttpDelegate>& httpDelegate)  |  Invalida la pila HTTP predeterminada con la del cliente.
 public void OptOutTelemetry()  |  No participa en la recopilación de toda la telemetría.
 public bool IsTelemetryOptedOut() const  |  Obtiene si se debe deshabilitar o no la recopilación de telemetría.
 public void SetMinimumLogLevel(LogLevel logLevel)  |  Establece el nivel de registro mínimo que desencadenará un evento de registro.
 public LogLevel GetMinimumLogLevel() const  |  Obtiene el objeto de nivel de registro mínimo.
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Interfaz para configurar el perfil.

Parámetros:  
* **path**: la ruta de acceso a un directorio en el que el SDK almacenará el estado del perfil. 


* **useInMemoryStorage**: almacene cualquier estado almacenado en caché en memoria en lugar de en disco. 


* **authDelegate**: el delegado de autenticación utilizado por el SDK para adquirir tokens de autenticación. 


* **observer**: una clase que implementa la interfaz [PolicyProfile::Observer](class_mip_policyprofile_observer.md). Puede se nullptr. 


* **applicationInfo**: los identificadores de aplicación que se usan para el acceso al servicio.


  
### <a name="getpath"></a>GetPath
Obtiene la ruta de acceso al estado almacenado.

  
**Devuelve**: ruta de acceso al estado almacenado.
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
Obtiene la marca de uso de almacenamiento en memoria.

  
**Devuelve**: true si se establece el uso en memoria; de lo contrario, false.
  
### <a name="getauthdelegate"></a>GetAuthDelegate
Obtiene el delegado de autenticación.

  
**Devuelve**: el delegado de autenticación.
  
### <a name="policyprofileobserver"></a>PolicyProfile::Observer
Obtiene el observador de eventos.

  
**Devuelve**: el observador de eventos.
  
### <a name="applicationinfo"></a>ApplicationInfo
Obtiene la información de aplicación.

  
**Devuelve**: la información de aplicación.
  
### <a name="loggerdelegate"></a>LoggerDelegate
Obtiene el delegado del registrador (si existe) proporcionado por la aplicación.

  
**Devuelve**: registrador
  
### <a name="setloggerdelegate"></a>SetLoggerDelegate
Invalida el registrador predeterminado.

Parámetros:  
* **loggerDelegate**: interfaz de devolución de llamada de registro implementada por las aplicaciones cliente


Las aplicaciones cliente deben llamar a este método si desean usar su propia implementación del registrador.
  
### <a name="httpdelegate"></a>HttpDelegate
Obtiene el delegado HTTP (si existe) proporcionado por la aplicación.

  
**Devuelve**: delegado HTTP que se usará para las operaciones HTTP.
  
### <a name="sethttpdelegate"></a>SetHttpDelegate
Invalida la pila HTTP predeterminada con la del cliente.

Parámetros:  
* **httpDelegate**: interfaz de devolución de llamada HTTP implementada por la aplicación cliente.


  
### <a name="optouttelemetry"></a>OptOutTelemetry
No participa en la recopilación de toda la telemetría.
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
Obtiene si se debe deshabilitar o no la recopilación de telemetría.

  
**Devuelve**: si se debe deshabilitar o no la recopilación de telemetría.
  
### <a name="setminimumloglevel"></a>SetMinimumLogLevel
Establece el nivel de registro mínimo que desencadenará un evento de registro.

Parámetros:  
* **logLevel**: nivel de registro mínimo que desencadenará un evento de registro. 



  
**Devuelve**: valor True
  
### <a name="loglevel"></a>LogLevel
Obtiene el objeto de nivel de registro mínimo.

  
**Devuelve**: nivel de registro mínimo que desencadenará un evento de registro.