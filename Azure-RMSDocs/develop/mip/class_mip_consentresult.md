# <a name="class-mipconsentresult"></a>clase mip::ConsentResult 
Describe el resultado de la solicitud de consentimiento tras la interacción del usuario.
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public inline  ConsentResult public inline bool Accepted | Obtiene si el usuario ha consentido o no a la acción.
public inline bool ShowAgain | Obtiene si se requiere o no consentimiento explícito para solicitudes futuras.
public inline const std::string & UserId | Obtiene el usuario (dirección de correo electrónico) de quien se ha solicitado el consentimiento.
## <a name="members"></a>Miembros
### <a name="consentresult"></a>ConsentResult
Constructor [ConsentResult](#classmip_1_1_consent_result).
#### <a name="parameters"></a>Parámetros
* accepted Si el usuario ha consentido o no a la acción 
* showAgain Determina si se requiere o no consentimiento explícito para solicitudes de acción futuras 
* userId Usuario (dirección de correo electrónico) de quien se ha solicitado el consentimiento
### <a name="accepted"></a>Accepted
Determina si el usuario ha consentido o no a la acción.
#### <a name="returns"></a>Devuelve
Si el usuario ha consentido o no a la acción
### <a name="showagain"></a>ShowAgain
Determina si se requiere o no consentimiento explícito para solicitudes futuras.
#### <a name="returns"></a>Devuelve
Si se requiere o no consentimiento explícito para solicitudes futuras. Si esto es cierto, el SDK recordará el resultado de este consentimiento y no solicitará el consentimiento del cliente en el futuro.
### <a name="userid"></a>UserId
Obtiene el usuario (dirección de correo electrónico) de quien se ha solicitado el consentimiento.
#### <a name="returns"></a>Devuelve
Usuario de quien se ha solicitado el consentimiento