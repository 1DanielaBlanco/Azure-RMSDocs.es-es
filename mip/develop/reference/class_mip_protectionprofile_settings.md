---
title: clase mip ProtectionProfile Settings
description: Referencia de la clase mip ProtectionProfile Settings
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: fe2413b2265cf4994dce0e57a7c472d59336902a
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446675"
---
# <a name="class-mipprotectionprofilesettings"></a>clase mip::ProtectionProfile::Settings 
[Configuración](class_mip_protectionprofile_settings.md) utilizada por [ProtectionProfile](class_mip_protectionprofile.md) durante su creación y a lo largo de su vigencia.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<ConsentDelegate>& consentDelegate, const std::shared_ptr<ProtectionProfile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  Constructor [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) que especifica un observador que se usará para operaciones asincrónicas.
public Settings(const std::string& path, bool useInMemoryStorage, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<ConsentDelegate>& consentDelegate, const ApplicationInfo& applicationInfo)  |  Constructor [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) usado para operaciones sincrónicas.
 public const std::string& GetPath() const  |  Obtiene la ruta de acceso bajo la cual se almacena el registro, la telemetría y otras garantías de protección.
 public bool GetUseInMemoryStorage() const  |  Obtiene si las memorias caché se almacenan solo en la memoria (en contraposición a en disco).
public std::shared_ptr<AuthDelegate> GetAuthDelegate() const  |  Obtiene el delegado de autenticación utilizado para la adquisición de tokens de autenticación.
public std::shared_ptr<ConsentDelegate> GetConsentDelegate() const  |  Obtiene el delegado de consentimiento utilizado para conectarse a servicios.
public std::shared_ptr<ProtectionProfile::Observer> GetObserver() const  |  Obtiene el observador que recibe notificaciones de eventos relacionados con [ProtectionProfile](class_mip_protectionprofile.md).
 public const ApplicationInfo& GetApplicationInfo() const  |  Obtiene información sobre la aplicación que usa el SDK de protección.
 public void OptOutTelemetry()  |  No participa en la recopilación de toda la telemetría.
 public bool IsTelemetryOptedOut() const  |  Obtiene si se tiene que deshabilitar o no la recopilación de telemetría.
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  Obtiene el delegado del registrador (si existe) proporcionado por la aplicación.
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  Invalida el registrador predeterminado.
public std::shared_ptr<HttpDelegate> GetHttpDelegate() const  |  Obtiene el delegado HTTP (si existe) proporcionado por la aplicación.
public void SetHttpDelegate(const std::shared_ptr<HttpDelegate>& httpDelegate)  |  Reemplaza la pila HTTP predeterminada por la del cliente.
 public bool GetSkipTelemetryInit() const  |  Obtiene si se tiene omitir o no la inicialización de telemetría.
 public void SetSkipTelemetryInit()  |  Deshabilita la inicialización de telemetría.
 public void SetNewFeaturesDisabled()  |  Deshabilita nuevas características.
 public bool AreNewFeaturesDisabled() const  |  Obtiene si las nuevas características están deshabilitadas o no.
 public void SetSessionId(const std::string& sessionId)  |  Establece el identificador de sesión.
 public const std::string& GetSessionId() const  |  Obtiene el identificador de sesión.
 public void SetMinimumLogLevel(LogLevel logLevel)  |  Establece el nivel de registro mínimo que desencadenará un evento de registro.
 public LogLevel GetMinimumLogLevel() const  |  Obtiene el objeto de nivel de registro mínimo.
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Constructor [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) que especifica un observador que se usará para operaciones asincrónicas.

Parámetros:  
* **path**: ruta de acceso al archivo bajo la cual se almacena el registro, la telemetría y otras garantías de protección 


* **useInMemoryStorage**: almacene cualquier estado almacenado en caché en memoria en lugar de en disco 


* **authDelegate**: objeto de devolución de llamada que se usará para la autenticación, implementado por la aplicación cliente 


* **observer**: instancia de [Observer](class_mip_protectionprofile_observer.md) que recibirá notificaciones de eventos relacionados con [ProtectionProfile](class_mip_protectionprofile.md)


* **applicationInfo**: información sobre la aplicación que usa el SDK de protección.


  
### <a name="settings"></a>Configuración
Constructor [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) usado para operaciones sincrónicas.

Parámetros:  
* **path**: ruta de acceso al archivo bajo la cual se almacena el registro, la telemetría y otras garantías de protección 


* **useInMemoryStorage**: almacene cualquier estado almacenado en caché en memoria en lugar de en disco 


* **authDelegate**: objeto de devolución de llamada que se usará para la autenticación, implementado por la aplicación cliente 


* **applicationInfo**: información relacionada con la aplicación que usa el SDK de protección.


  
### <a name="getpath"></a>GetPath
Obtiene la ruta de acceso bajo la cual se almacena el registro, la telemetría y otras garantías de protección.

  
**Devuelve**: ruta de acceso bajo la cual se almacena el registro, la telemetría y otras garantías de protección
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
Obtiene si las memorias caché se almacenan solo en la memoria (en contraposición a en disco).

  
**Devuelve**: true si las memorias caché se almacenan en memoria solo
  
### <a name="getauthdelegate"></a>GetAuthDelegate
Obtiene el delegado de autenticación utilizado para la adquisición de tokens de autenticación.

  
**Devuelve**: el delegado de autenticación utilizado para la adquisición de tokens de autenticación
  
### <a name="consentdelegate"></a>ConsentDelegate
Obtiene el delegado de consentimiento utilizado para conectarse a servicios.

  
**Devuelve**: el delegado de consentimiento utilizado para conectarse a servicios
  
### <a name="protectionprofileobserver"></a>ProtectionProfile::Observer
Obtiene el observador que recibe notificaciones de eventos relacionados con [ProtectionProfile](class_mip_protectionprofile.md).

  
**Devuelve**: [observador](class_mip_protectionprofile_observer.md) que recibe notificaciones de eventos relacionados con [ProtectionProfile](class_mip_protectionprofile.md).
  
### <a name="applicationinfo"></a>ApplicationInfo
Obtiene información sobre la aplicación que usa el SDK de protección.

  
**Devuelve**: información sobre la aplicación que usa el SDK de protección.
  
### <a name="optouttelemetry"></a>OptOutTelemetry
No participa en la recopilación de toda la telemetría.
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
Obtiene si se tiene que deshabilitar o no la recopilación de telemetría.

  
**Devuelve**: si se tiene que deshabilitar o no la recopilación de telemetría.
  
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



  
**Devuelve**: valor True
  
### <a name="loglevel"></a>LogLevel
Obtiene el objeto de nivel de registro mínimo.

  
**Devuelve**: nivel de registro mínimo que desencadenará un evento de registro.