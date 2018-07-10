# <a name="class-consentdelegate"></a>clase ConsentDelegate 
Delegado para operaciones relacionadas con el consentimiento.
Este delegado implementa una aplicación cliente para saber cuándo debe mostrarse al usuario una notificación de solicitud de consentimiento.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public Consent GetUserConsent(const std::string& url)  |  Se llama cuando el SDK requiere consentimiento del usuario para conectarse a un punto de conexión de servicio.
  
## <a name="members"></a>Miembros
  
### <a name="consent"></a>Consentimiento
Se llama cuando el SDK requiere consentimiento del usuario para conectarse a un punto de conexión de servicio.

Parámetros:  
* **url**: la dirección URL para el que el SDK requiere el consentimiento del usuario



  
**Devuelve**: enumeración de consentimiento con la decisión del usuario.
Cuando el SDK solicita el consentimiento del usuario con este método, la aplicación cliente debe presentar la dirección URL al usuario. Las aplicaciones cliente deben proporcionar algún medio de obtener el consentimiento del usuario y devolver la enumeración de consentimiento adecuada que corresponda a la decisión del usuario.