# <a name="class-mipgetuserpolicyresult"></a>clase mip::GetUserPolicyResult 
Describe los resultados de una solicitud de adquisición de directiva de usuario.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public GetUserPolicyResultStatus GetResultStatus()  |  Obtiene el estado de la solicitud de adquisición de directiva.
public std::shared_ptr<std::string> GetReferrer()  |  Obtiene la dirección del sitio de referencia de la directiva.
public std::shared_ptr<UserPolicy> GetPolicy()  |  Obtiene una instancia [UserPolicy](class_mip_userpolicy.md).
  
## <a name="members"></a>Miembros
  
### <a name="getuserpolicyresultstatus"></a>GetUserPolicyResultStatus
Obtiene el estado de la solicitud de adquisición de directiva.

  
**Devuelve**: estado de la solicitud de adquisición de directiva
  
### <a name="getreferrer"></a>GetReferrer
Obtiene la dirección del sitio de referencia de la directiva.

  
**Devuelve**: dirección del sitio de referencia de la directiva. El sitio de referencia es una URI que puede mostrarse al usuario cuando la adquisición de la directiva ha producido un error y que contiene información sobre cómo el usuario puede obtener permiso para obtener acceso al contenido.
  
### <a name="userpolicy"></a>UserPolicy
Obtiene una instancia [UserPolicy](class_mip_userpolicy.md).

  
**Devuelve**: instancia de [UserPolicy](class_mip_userpolicy.md) si la adquisición se realizó correctamente; de lo contrario, nullptr