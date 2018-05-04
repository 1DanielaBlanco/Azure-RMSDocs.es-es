# <a name="class-mippolicydescriptor"></a>clase mip::PolicyDescriptor 
Representa una directiva ad-hoc asociada al contenido protegido.
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const std::string & GetName | Obtiene el nombre de directiva.
public void SetName | Establece el nombre de la directiva.
public const std::string & GetDescription | Obtiene la descripción de la directiva.
public void SetDescription | Establece la descripción de la directiva.
public const std::vector< UserRights > & GetUserRightsList | Obtiene una colección de asignaciones de usuarios a derechos.
public const std::vector< mip::UserRoles > & GetUserRolesList | Obtiene una colección de asignaciones de usuarios a roles
public const std::chrono::time_point< std::chrono::system_clock > & GetContentValidUntil | Obtiene la hora de expiración de la directiva.
public void SetContentValidUntil | Establece la hora de expiración de la directiva.
public bool DoesAllowOfflineAccess | Determina si la directiva permite o no el acceso a contenido sin conexión.
public void SetAllowOfflineAccess | Establece si la directiva permite o no el acceso a contenido sin conexión.
public const std::string & GetReferrer | Obtiene la dirección del sitio de referencia de directiva.
public void SetReferrer | Establece la dirección del sitio de referencia de directiva.
public const AppDataHashMap & GetEncryptedAppData | Obtiene datos específicos de la aplicación que se cifraron.
public void SetEncryptedAppDataAppDataHashMap & value) | Establece los datos específicos de la aplicación que fueron cifrados.
public const AppDataHashMap & GetSignedAppData | Obtiene datos específicos de la aplicación que se firmaron.
public void SetSignedAppDataAppDataHashMap & value) | Establece los datos específicos de la aplicación que deben firmarse.
## <a name="members"></a>Miembros
### <a name="getname"></a>GetName
Obtiene el nombre de directiva.
#### <a name="returns"></a>Devuelve
Nombre de la directiva
### <a name="setname"></a>SetName
Establece el nombre de la directiva.
#### <a name="parameters"></a>Parámetros
* value Nombre de la directiva
### <a name="getdescription"></a>GetDescription
Obtiene la descripción de la directiva.
#### <a name="returns"></a>Devuelve
Descripción de la directiva
### <a name="setdescription"></a>SetDescription
Establece la descripción de la directiva.
#### <a name="parameters"></a>Parámetros
* value Descripción de la directiva
### <a name="userrights"></a>UserRights
Obtiene una colección de asignaciones de usuarios a derechos.
#### <a name="returns"></a>Devuelve
Colección de asignaciones de usuarios a derechos El valor de la propiedad UserRightsList estará vacía si el usuario actual no tiene acceso a la información de derechos del usuario (es decir, no es el propietario y no tiene el derecho VIEWRIGHTSDATA).
### <a name="mipuserroles"></a>mip::UserRoles
Obtiene una colección de asignaciones de usuarios a roles
#### <a name="returns"></a>Devuelve
Colección de asignaciones de usuarios a roles
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
Obtiene la hora de expiración de la directiva.
#### <a name="returns"></a>Devuelve
Hora de expiración de la directiva
### <a name="setcontentvaliduntil"></a>SetContentValidUntil
Establece la hora de expiración de la directiva.
#### <a name="parameters"></a>Parámetros
* value Hora de expiración de la directiva
### <a name="doesallowofflineaccess"></a>DoesAllowOfflineAccess
Determina si la directiva permite o no el acceso a contenido sin conexión.
#### <a name="returns"></a>Devuelve
Si la directiva permite o no el acceso a contenido sin conexión (valor predeterminado = true)
### <a name="setallowofflineaccess"></a>SetAllowOfflineAccess
Establece si la directiva permite o no el acceso a contenido sin conexión.
#### <a name="parameters"></a>Parámetros
* value Si la directiva permite o no el acceso a contenido sin conexión
### <a name="getreferrer"></a>GetReferrer
Obtiene la dirección del sitio de referencia de directiva.
#### <a name="returns"></a>Devuelve
Dirección del sitio de referencia de la directiva El sitio de referencia es una URI que puede mostrarse al usuario cuando la adquisición de la directiva ha producido un error y que contiene información sobre cómo el usuario puede obtener permiso para acceder al contenido.
### <a name="setreferrer"></a>SetReferrer
Establece la dirección del sitio de referencia de directiva.
#### <a name="parameters"></a>Parámetros
* uri Dirección del sitio de referencia de la directiva El sitio de referencia es una URI que puede mostrarse al usuario cuando la adquisición de la directiva ha producido un error y que contiene información sobre cómo el usuario puede obtener permiso para acceder al contenido.
### <a name="appdatahashmap"></a>AppDataHashMap
Obtiene datos específicos de la aplicación que se cifraron.
#### <a name="returns"></a>Devuelve
Datos específicos de la aplicación. Una clase [UserPolicy ](#classmip_1_1_user_policy) puede contener un diccionario de datos específicos de la aplicación cifrados por el servicio RMS. Estos datos cifrados son independientes de los datos firmados accesibles mediante [PolicyDescriptor::GetSignedAppData](#classmip_1_1_policy_descriptor_1ad523870efc92f9f81c82121a054d74d4)
### <a name="setencryptedappdata"></a>SetEncryptedAppData
Establece los datos específicos de la aplicación que fueron cifrados.
#### <a name="parameters"></a>Parámetros
* value Datos específicos de la aplicación que una aplicación puede especificar un diccionario de datos específicos de la aplicación cifrados por el servicio RMS. Estos datos cifrados son independientes del conjunto de datos firmado por [PolicyDescriptor::SetSignedAppData](#classmip_1_1_policy_descriptor_1a00f35c0b91e48ccdcc6387466a61f362).
### <a name="appdatahashmap"></a>AppDataHashMap
Obtiene datos específicos de la aplicación que se firmaron.
#### <a name="returns"></a>Devuelve
Datos específicos de la aplicación. Una clase [UserPolicy ](#classmip_1_1_user_policy) puede contener un diccionario de datos específicos de la aplicación firmados por el servicio RMS. Estos datos firmados son independientes de los datos cifrados accesibles mediante [PolicyDescriptor::GetEncryptedAppData](#classmip_1_1_policy_descriptor_1a9a5bcf9d1bf7357de549429179197ab6)
### <a name="setsignedappdata"></a>SetSignedAppData
Establece los datos específicos de la aplicación que deben firmarse.
#### <a name="parameters"></a>Parámetros
* value Datos específicos de la aplicación que una aplicación puede especificar un diccionario de datos específicos de la aplicación firmados por el servicio RMS. Estos datos firmados son independientes del conjunto de datos cifrados por [PolicyDescriptor::SetEncryptedAppData](#classmip_1_1_policy_descriptor_1a5275224932dc17319092304497e59eb2).