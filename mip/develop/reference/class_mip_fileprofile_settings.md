---
title: Clase mip FileProfile Settings
description: Referencia de la clase mip FileProfile Settings
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 4b79d8eb75a54a56f1b3e48645bdd5eec0afaa19
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446386"
---
# <a name="class-mipfileprofilesettings"></a>clase mip::FileProfile::Settings 
[Configuración](class_mip_fileprofile_settings.md) utilizada por [FileProfile](class_mip_fileprofile.md) durante su creación y a lo largo de su vigencia.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, std::shared_ptr<AuthDelegate> authDelegate, std::shared_ptr<ConsentDelegate> consentDelegate, std::shared_ptr<Observer> observer, const ApplicationInfo& applicationInfo)  |  Constructor [FileProfile::Settings](class_mip_fileprofile_settings.md).
 public const std::string& GetPath() const  |  Obtiene la ruta de acceso bajo la cual se almacena el registro, la telemetría y otro estado persistente.
 public bool GetUseInMemoryStorage() const  |  Obtiene si todos los estados se tienen que almacenar o no en memoria (en lugar de almacenarlos en el disco).
public std::shared_ptr<AuthDelegate> GetAuthDelegate() const  |  Obtiene el delegado de autenticación utilizado para la adquisición de tokens de autenticación.
public std::shared_ptr<ConsentDelegate> GetConsentDelegate() const  |  Obtiene el delegado de consentimiento utilizado para solicitar el consentimiento del usuario al conectarse a los servicios.
public std::shared_ptr<Observer> GetObserver() const  |  Obtiene el observador que recibe notificaciones de eventos relacionados con [FileProfile](class_mip_fileprofile.md).
 public const ApplicationInfo GetApplicationInfo() const  |  Obtiene información sobre la aplicación que usa el SDK.
 public bool GetSkipTelemetryInit() const  |  Obtiene si se tiene omitir o no la inicialización de telemetría.
 public void SetSkipTelemetryInit()  |  Deshabilita la inicialización de telemetría.
 public void SetNewFeaturesDisabled()  |  Deshabilita nuevas características.
 public bool AreNewFeaturesDisabled() const  |  Obtiene si las nuevas características están deshabilitadas o no.
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  Obtiene el delegado del registrador (si existe) proporcionado por la aplicación.
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  Invalida el registrador predeterminado.
public std::shared_ptr<HttpDelegate> GetHttpDelegate() const  |  Obtiene el delegado HTTP (si existe) proporcionado por la aplicación.
public void SetHttpDelegate(const std::shared_ptr<HttpDelegate>& httpDelegate)  |  Invalida la pila HTTP predeterminada con la del cliente.
 public void OptOutTelemetry()  |  No participa en la recopilación de toda la telemetría.
 public bool IsTelemetryOptedOut() const  |  Obtiene si se tiene que deshabilitar o no la recopilación de telemetría.
 public void SetSessionId(const std::string& sessionId)  |  Establece el identificador de sesión.
 public const std::string& GetSessionId() const  |  Obtiene el identificador de sesión.
 public void SetMinimumLogLevel(LogLevel logLevel)  |  Establece el nivel de registro mínimo que desencadenará un evento de registro.
 public LogLevel GetMinimumLogLevel() const  |  Obtiene el nivel de registro mínimo que desencadenará un evento de registro.
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Constructor [FileProfile::Settings](class_mip_fileprofile_settings.md).

Parámetros:  
* **path**: ruta de acceso de archivo bajo la cual se almacena el registro, la telemetría y otro estado persistente 


* **useInMemoryStorage**: “true” si todos los estados tienen que almacenarse en memoria; “false” si el estado se puede almacenar en caché en el disco. 


* **authDelegate**: delegado de autenticación utilizado para la adquisición de tokens de autenticación 


* **observer**: instancia de [Observer](class_mip_fileprofile_observer.md) que recibirá notificaciones de eventos relacionados con [FileProfile](class_mip_fileprofile.md)


* **applicationInfo**: información sobre la aplicación que usa el SDK.


  
### <a name="getpath"></a>GetPath
Obtiene la ruta de acceso bajo la cual se almacena el registro, la telemetría y otro estado persistente.

  
**Devuelve**: ruta de acceso bajo la cual se almacena el registro, la telemetría y otro estado persistente
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
Obtiene si todos los estados se tienen que almacenar o no en memoria (en lugar de almacenarlos en el disco).

  
**Devuelve**: si todos los estados se tienen que almacenar o no en memoria (en lugar de almacenarlos en el disco).
  
### <a name="getauthdelegate"></a>GetAuthDelegate
Obtiene el delegado de autenticación utilizado para la adquisición de tokens de autenticación.

  
**Devuelve**: el delegado de autenticación utilizado para la adquisición de tokens de autenticación
  
### <a name="consentdelegate"></a>ConsentDelegate
Obtiene el delegado de consentimiento utilizado para solicitar el consentimiento del usuario al conectarse a los servicios.

  
**Devuelve**: delegado de consentimiento que se usa para solicitar el consentimiento del usuario
  
### <a name="observer"></a>Observador
Obtiene el observador que recibe notificaciones de eventos relacionados con [FileProfile](class_mip_fileprofile.md).

  
**Devuelve**: [Observer](class_mip_fileprofile_observer.md) que recibe notificaciones de eventos relacionados con [FileProfile](class_mip_fileprofile.md)
  
### <a name="applicationinfo"></a>ApplicationInfo
Obtiene información sobre la aplicación que usa el SDK.

  
**Devuelve**: información sobre la aplicación que usa el SDK.
  
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
Obtiene si se tiene omitir o no la inicialización de telemetría.

  
**Devuelve**: si se tiene que omitir o no la inicialización de telemetría.
  
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
Deshabilita la inicialización de telemetría.
Este método no suele recibir llamadas de aplicaciones cliente; en su lugar, lo usa el SDK de archivos para impedir inicializaciones duplicadas.
  
### <a name="setnewfeaturesdisabled"></a>SetNewFeaturesDisabled
Deshabilita nuevas características.
Para aplicaciones que no quieren probar nuevas características.
  
### <a name="arenewfeaturesdisabled"></a>AreNewFeaturesDisabled
Obtiene si las nuevas características están deshabilitadas o no.

  
**Devuelve**: si las nuevas características están deshabilitadas o no.
  
### <a name="loggerdelegate"></a>LoggerDelegate
Obtiene el delegado del registrador (si existe) proporcionado por la aplicación.

  
**Devuelve**: registrador.
  
### <a name="setloggerdelegate"></a>SetLoggerDelegate
Invalida el registrador predeterminado.

Parámetros:  
* **loggerDelegate**: interfaz de devolución de llamada de registro implementada por las aplicaciones cliente


Las aplicaciones cliente deben llamar a este método si desean usar su propia implementación del registrador.
  
### <a name="httpdelegate"></a>HttpDelegate
Obtiene el delegado HTTP (si existe) proporcionado por la aplicación.

  
**Devuelve**: delegado HTTP que se usará para las operaciones HTTP.
  
### <a name="sethttpdelegate"></a>SetHttpDelegate
Reemplaza la pila HTTP predeterminada por la del cliente.

Parámetros:  
* **httpDelegate**: interfaz de devolución de llamadas HTTP implementada por la aplicación cliente.


  
### <a name="optouttelemetry"></a>OptOutTelemetry
No participa en la recopilación de toda la telemetría.
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
Obtiene si se tiene que deshabilitar o no la recopilación de telemetría.

  
**Devuelve**: si se tiene que deshabilitar o no la recopilación de telemetría.
  
### <a name="setsessionid"></a>SetSessionId
Establece el identificador de sesión.

Parámetros:  
* **sessionId**: identificador de sesión que se usará para poner en correlación los registros o la telemetría.


  
### <a name="getsessionid"></a>GetSessionId
Obtiene el identificador de sesión.

  
**Devuelve**: identificador de sesión que se usará para poner en correlación los registros o la telemetría.
  
### <a name="setminimumloglevel"></a>SetMinimumLogLevel
Establece el nivel de registro mínimo que desencadenará un evento de registro.

Parámetros:  
* **logLevel**: nivel de registro mínimo que desencadenará un evento de registro. 



  
**Devuelve**: valor “true”.
  
### <a name="loglevel"></a>LogLevel
Obtiene el nivel de registro mínimo que desencadenará un evento de registro.

  
**Devuelve**: nivel de registro mínimo que desencadenará un evento de registro.