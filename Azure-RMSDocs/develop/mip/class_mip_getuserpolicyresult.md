# <a name="class-mipgetuserpolicyresult"></a>clase mip::GetUserPolicyResult 
Describe los resultados de una solicitud de adquisición de directiva de usuario.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public GetUserPolicyResultStatus GetResultStatus()  |  Obtiene el estado de la solicitud de adquisición de directiva.
public std::shared_ptr<std::string> GetReferrer()  |  Obtiene la dirección del sitio de referencia de la directiva.
public std::shared_ptr<UserPolicy> GetPolicy()  |  Obtiene una instancia [UserPolicy](#classmip_1_1_user_policy).
  
## <a name="members"></a>Miembros
  
### <a name="getuserpolicyresultstatus"></a>GetUserPolicyResultStatus
Obtiene el estado de la solicitud de adquisición de directiva.
  
#### <a name="returns"></a>Devuelve
Estado de la solicitud de adquisición de directiva
  
### <a name="getreferrer"></a>GetReferrer
Obtiene la dirección del sitio de referencia de la directiva.
  
#### <a name="returns"></a>Devuelve
Dirección del sitio de referencia de la directiva El sitio de referencia es un URI que puede mostrarse al usuario cuando la adquisición de la directiva ha producido un error y que contiene información sobre cómo el usuario puede obtener permiso para acceder al contenido.
  
### <a name="userpolicy"></a>UserPolicy
Obtiene una instancia [UserPolicy](#classmip_1_1_user_policy).
  
#### <a name="returns"></a>Devuelve
Instancia de [UserPolicy](#classmip_1_1_user_policy) si la adquisición se ha realizado correctamente; de lo contrario, `nullptr`.