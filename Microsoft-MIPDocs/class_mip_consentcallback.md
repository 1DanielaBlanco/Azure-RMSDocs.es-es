# <a name="class-mipconsentcallback"></a>clase mip::ConsentCallback 
Interfaz para las notificaciones de solicitud de consentimiento.
Esta devolución de llamada la implementa una aplicación cliente para saber cuándo debe mostrarse al usuario una notificación de consentimiento.
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public ConsentList ConsentsConsentList & consents) | Se llama cuando el SDK requiere el consentimiento del usuario para una operación.
## <a name="members"></a>Miembros
### <a name="consentlist"></a>ConsentList
Se llama cuando el SDK requiere el consentimiento del usuario para una operación.
#### <a name="parameters"></a>Parámetros
* consents La lista de consentimientos solicitados por el SDK
#### <a name="returns"></a>Devuelve
Resultados de [Consent](#classmip_1_1_consent) Cuando el SDK solicita el consentimiento, la aplicación cliente debe obtener el consentimiento del usuario, los resultados de cada consentimiento deben almacenarse en [Consent::Result(const ConsentResult&)](#classmip_1_1_consent_1ad6c17d9af548a40b2fe854fe0d9bca64), y debe devolverse una lista de los consentimientos resueltos.