# <a name="class-mipconsent"></a>clase mip::Consent 
Representa la aceptación o rechazo de un usuario para permitir una acción.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public const mip::ConsentResult& Result() const  |  Obtiene el resultado de una solicitud de consentimiento.
 public void Result(const ConsentResult& value)  |  Establece el resultado de una solicitud de consentimiento.
 public mip::ConsentType Type() const  |  Obtiene el tipo de consentimiento.
public const std::vector<std::string> Urls() const  |  Obtiene las direcciones URL implicadas en la solicitud de consentimiento.
 public const std::string User() const  |  Obtiene el usuario (dirección de correo electrónico) al que se solicita el consentimiento.
 public const std::string Domain() const  |  Obtiene el dominio asociado con el usuario desde el que se solicita el consentimiento.
  
## <a name="members"></a>Miembros
  
### <a name="mipconsentresult"></a>mip::ConsentResult
Obtiene el resultado de una solicitud de consentimiento.

  
**Devuelve**: resultado de la solicitud de consentimiento
  
### <a name="result"></a>Result
Establece el resultado de una solicitud de consentimiento.

Parámetros:  
* **value**: resultado de la solicitud de consentimiento


  
### <a name="mipconsenttype"></a>mip::ConsentType
Obtiene el tipo de consentimiento.

  
**Devuelve**: tipo de consentimiento
  
### <a name="urls"></a>Direcciones URL
Obtiene las direcciones URL implicadas en la solicitud de consentimiento.

  
**Devuelve**: direcciones URL implicadas en la solicitud de consentimiento
  
### <a name="user"></a>Usuario
Obtiene el usuario (dirección de correo electrónico) al que se solicita el consentimiento.

  
**Devuelve**: usuario de quien se ha solicitado el consentimiento
  
### <a name="domain"></a>Dominio
Obtiene el dominio asociado con el usuario desde el que se solicita el consentimiento.

  
**Devuelve**: dominio asociado al usuario desde el que se solicita el consentimiento