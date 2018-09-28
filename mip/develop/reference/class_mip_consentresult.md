# <a name="class-mipconsentresult"></a>clase mip::ConsentResult 
Describe el resultado de la solicitud de consentimiento tras la interacción del usuario.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public ConsentResult(bool accepted, bool showAgain, const std::string& userId)  |  Constructor [ConsentResult](class_mip_consentresult.md).
 public bool Accepted() const  |  Determina si el usuario ha consentido o no a la acción.
 public bool ShowAgain() const  |  Determina si se requiere o no consentimiento explícito para solicitudes futuras.
 public const std::string& UserId() const  |  Obtiene el usuario (dirección de correo electrónico) de quien se ha solicitado el consentimiento.
  
## <a name="members"></a>Miembros
  
### <a name="consentresult"></a>ConsentResult
Constructor [ConsentResult](class_mip_consentresult.md).

Parámetros:  
* **accepted**: si el usuario ha consentido o no a la acción 


* **showAgain**: determina si se requiere o no consentimiento explícito para solicitudes de acción futuras 


* **userId**: usuario (dirección de correo electrónico) de quien se ha solicitado el consentimiento


  
### <a name="accepted"></a>Accepted
Determina si el usuario ha consentido o no a la acción.

  
**Devuelve**: si el usuario ha consentido o no a la acción
  
### <a name="showagain"></a>ShowAgain
Determina si se requiere o no consentimiento explícito para solicitudes futuras.

  
**Devuelve**: si se requiere o no consentimiento explícito para solicitudes futuras. Si esto es cierto, el SDK recordará el resultado de este consentimiento y no solicitará el consentimiento del cliente en el futuro.
  
### <a name="userid"></a>UserId
Obtiene el usuario (dirección de correo electrónico) de quien se ha solicitado el consentimiento.

  
**Devuelve**: usuario de quien se ha solicitado el consentimiento