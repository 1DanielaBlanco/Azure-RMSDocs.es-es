# <a name="class-mipconsentcallback"></a>clase mip::ConsentCallback 
Interfaz para las notificaciones de solicitud de consentimiento.
Esta devolución de llamada la implementa una aplicación cliente para saber cuándo debe mostrarse al usuario una notificación de consentimiento.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public ConsentList Consents(ConsentList& consents)  |  Se llama cuando el SDK requiere el consentimiento del usuario para una operación.
  
## <a name="members"></a>Miembros
  
### <a name="consentlist"></a>ConsentList
Se llama cuando el SDK requiere el consentimiento del usuario para una operación.

Parámetros:  
* **consents**: la lista de consentimientos solicitados por el SDK



  
**Devuelve**: resultados de [Consent](class_mip_consent.md). Cuando el SDK solicita el consentimiento, la aplicación cliente debe obtener el consentimiento del usuario, los resultados de cada consentimiento deben almacenarse en [Consent::Result(const ConsentResult&)](class_mip_consent.md#result), y debe devolverse una lista de los consentimientos resueltos.