---
title: clase mip::ProtectionProfile::Settings
description: 'Documenta la clase MIP:: protectionprofile de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 1998d693de33d2bc37043f750d85296f7282add4
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56254822"
---
# <a name="class-mipprotectionprofilesettings"></a>clase mip::ProtectionProfile::Settings 
[Configuración](class_mip_protectionprofile_settings.md) utilizada por [ProtectionProfile](class_mip_protectionprofile.md) durante su creación y a lo largo de su vigencia.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
Configuración pública (const std:: String & ruta de acceso, bool useInMemoryStorage, const std:: shared_ptr\<AuthDelegate\>& authDelegate, const std:: shared_ptr\<ConsentDelegate\>& consentDelegate const std:: shared_ptr\<protectionprofile:: Observer\>& observer, const ApplicationInfo & applicationInfo)  |  Constructor [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) que especifica un observador que se usará para operaciones asincrónicas.
Configuración pública (const std:: String & ruta de acceso, bool useInMemoryStorage, const std:: shared_ptr\<AuthDelegate\>& authDelegate, const std:: shared_ptr\<ConsentDelegate\>& consentDelegate const ApplicationInfo & applicationInfo)  |  Constructor [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) usado para operaciones sincrónicas.
public const std::string& GetPath() const  |  Obtiene la ruta de acceso bajo la cual se almacena el registro, la telemetría y otras garantías de protección.
public bool GetUseInMemoryStorage() const  |  Obtiene si las memorias caché se almacenan solo en la memoria (en contraposición a en disco).
Public std:: shared_ptr\<AuthDelegate\> GetAuthDelegate() const  |  Obtiene el delegado de autenticación utilizado para la adquisición de tokens de autenticación.
Public std:: shared_ptr\<ConsentDelegate\> GetConsentDelegate() const  |  Obtiene el delegado de consentimiento utilizado para conectarse a servicios.
public std::shared_ptr\<ProtectionProfile::Observer\> GetObserver() const  |  Obtiene el observador que recibe notificaciones de eventos relacionados con [ProtectionProfile](class_mip_protectionprofile.md).
public const ApplicationInfo& GetApplicationInfo() const  |  Obtiene información sobre la aplicación que usa el SDK de protección.
public void OptOutTelemetry()  |  No participa en la recopilación de toda la telemetría.
public bool IsTelemetryOptedOut() const  |  Obtiene si se tiene que deshabilitar o no la recopilación de telemetría.
Public std:: shared_ptr\<LoggerDelegate\> GetLoggerDelegate() const  |  Obtiene el delegado del registrador (si existe) proporcionado por la aplicación.
pública SetLoggerDelegate void (const std:: shared_ptr\<LoggerDelegate\>& loggerDelegate)  |  Invalida el registrador predeterminado.
Public std:: shared_ptr\<HttpDelegate\> GetHttpDelegate() const  |  Obtiene el delegado HTTP (si existe) proporcionado por la aplicación.
pública SetHttpDelegate void (const std:: shared_ptr\<HttpDelegate\>& httpDelegate)  |  Reemplaza la pila HTTP predeterminada por la del cliente.
public bool GetSkipTelemetryInit() const  |  Obtiene si se tiene omitir o no la inicialización de telemetría.
public void SetSkipTelemetryInit()  |  Deshabilita la inicialización de telemetría.
public void SetNewFeaturesDisabled()  |  Deshabilita nuevas características.
public bool AreNewFeaturesDisabled() const  |  Obtiene si las nuevas características están deshabilitadas o no.
public void SetSessionId(const std::string& sessionId)  |  Establece el identificador de sesión.
public const std::string& GetSessionId() const  |  Obtiene el identificador de sesión.
public void SetMinimumLogLevel(LogLevel logLevel)  |  Establece el nivel de registro mínimo que desencadenará un evento de registro.
public LogLevel GetMinimumLogLevel() const  |  Obtiene el objeto de nivel de registro mínimo.
  
## <a name="members"></a>Miembros
  
### <a name="settings-function"></a>Función de configuración
Constructor [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) que especifica un observador que se usará para operaciones asincrónicas.

Parámetros:  
* **Ruta de acceso**: Ruta de acceso de archivo en el registro, telemetría y otras garantías de protección se almacenan 


* **useInMemoryStorage**: Store cualquier estado almacenado en caché en memoria en lugar de en disco 


* **authDelegate**: Objeto de devolución de llamada que se usará para la autenticación, implementada por la aplicación cliente 


* **observer**: [Observador](class_mip_protectionprofile_observer.md) relacionados con la instancia que quiera recibir notificaciones de eventos [ProtectionProfile](class_mip_protectionprofile.md)


* **applicationInfo**: Información acerca de la aplicación que consume el SDK de protección


  
### <a name="settings-function"></a>Función de configuración
Constructor [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) usado para operaciones sincrónicas.

Parámetros:  
* **Ruta de acceso**: Ruta de acceso de archivo en el registro, telemetría y otras garantías de protección se almacenan 


* **useInMemoryStorage**: Store cualquier estado almacenado en caché en memoria en lugar de en disco 


* **authDelegate**: Objeto de devolución de llamada que se usará para la autenticación, implementada por la aplicación cliente 


* **applicationInfo**: Información acerca de la aplicación que consume el SDK de protección


  
### <a name="getpath-function"></a>Función GetPath
Obtiene la ruta de acceso bajo la cual se almacena el registro, la telemetría y otras garantías de protección.

  
**Devuelve**: Ruta de acceso bajo la cual se almacena el registro, la telemetría y otras garantías de protección
  
### <a name="getuseinmemorystorage-function"></a>Función GetUseInMemoryStorage
Obtiene si las memorias caché se almacenan solo en la memoria (en contraposición a en disco).

  
**Devuelve**: True si las memorias caché se almacenan en memoria solo
  
### <a name="getauthdelegate-function"></a>Función GetAuthDelegate
Obtiene el delegado de autenticación utilizado para la adquisición de tokens de autenticación.

  
**Devuelve**: Delegado de autenticación utilizado para la adquisición de tokens de autenticación
  
### <a name="getconsentdelegate-function"></a>Función GetConsentDelegate
Obtiene el delegado de consentimiento utilizado para conectarse a servicios.

  
**Devuelve**: Delegado que se usa para conectarse a servicios de consentimiento
  
### <a name="getobserver-function"></a>Función GetObserver
Obtiene el observador que recibe notificaciones de eventos relacionados con [ProtectionProfile](class_mip_protectionprofile.md).

  
**Devuelve**: [Observador](class_mip_protectionprofile_observer.md) que recibe notificaciones de eventos relacionados con [ProtectionProfile](class_mip_protectionprofile.md)
  
### <a name="getapplicationinfo-function"></a>Función GetApplicationInfo
Obtiene información sobre la aplicación que usa el SDK de protección.

  
**Devuelve**: Información acerca de la aplicación que consume el SDK de protección
  
### <a name="optouttelemetry-function"></a>Función OptOutTelemetry
No participa en la recopilación de toda la telemetría.
  
### <a name="istelemetryoptedout-function"></a>Función IsTelemetryOptedOut
Obtiene si se tiene que deshabilitar o no la recopilación de telemetría.

  
**Devuelve**: Si se debe deshabilitar la recopilación de telemetría o no
  
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

  
**Devuelve**: Delegado HTTP que se usará para las operaciones de HTTP
  
### <a name="sethttpdelegate-function"></a>Función SetHttpDelegate
Reemplaza la pila HTTP predeterminada por la del cliente.

Parámetros:  
* **httpDelegate**: Interfaz de devolución de llamada HTTP implementada por la aplicación cliente


  
### <a name="getskiptelemetryinit-function"></a>Función GetSkipTelemetryInit
Obtiene si se tiene omitir o no la inicialización de telemetría.

  
**Devuelve**: Si se debe omitir la inicialización de telemetría o no
  
### <a name="setskiptelemetryinit-function"></a>Función SetSkipTelemetryInit
Deshabilita la inicialización de telemetría.
Este método no suele recibir llamadas de aplicaciones cliente; en su lugar, lo usa el SDK de archivos para impedir inicializaciones duplicadas.
  
### <a name="setnewfeaturesdisabled-function"></a>Función SetNewFeaturesDisabled
Deshabilita nuevas características.
Para aplicaciones que no quieren probar nuevas características.
  
### <a name="arenewfeaturesdisabled-function"></a>Función AreNewFeaturesDisabled
Obtiene si las nuevas características están deshabilitadas o no.

  
**Devuelve**: Si se deshabilitan las nuevas características o no
  
### <a name="setsessionid-function"></a>Función SetSessionId
Establece el identificador de sesión.

Parámetros:  
* **sessionId**: Id. de sesión que se usará para correlacionar los registros o telemetría


  
### <a name="getsessionid-function"></a>Función GetSessionId
Obtiene el identificador de sesión.

  
**Devuelve**: Id. de sesión que se usará para correlacionar los registros o telemetría
  
### <a name="setminimumloglevel-function"></a>Función SetMinimumLogLevel
Establece el nivel de registro mínimo que desencadenará un evento de registro.

Parámetros:  
* **logLevel**: nivel de registro mínimo que desencadenará un evento de registro. 



  
**Devuelve**: True
  
### <a name="getminimumloglevel-function"></a>Función GetMinimumLogLevel
Obtiene el objeto de nivel de registro mínimo.

  
**Devuelve**: Nivel de registro mínimo que se desencadenará un evento de registro.
