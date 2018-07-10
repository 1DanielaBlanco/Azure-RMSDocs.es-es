# <a name="class-mipprotectiondescriptor"></a>clase mip::ProtectionDescriptor 
Representa una directiva ad-hoc asociada al contenido protegido.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public ProtectionType GetProtectionType() const  |  Obtiene el tipo de protección, con independencia de que se haya creado a partir de la plantilla del SDK de protección o no.
 public const std::string& GetName() const  |  Obtiene el nombre de directiva.
 public const std::string& GetDescription() const  |  Obtiene la descripción de la directiva.
 public const std::string& GetTemplateId() const  |  Obtiene el identificador de la plantilla de protección.
public const std::vector<UserRights>& GetUserRights() const  |  Obtiene una colección de asignaciones de usuarios a derechos.
public const std::vector<UserRoles>& GetUserRoles() const  |  Obtiene una colección de asignaciones de usuarios a roles
public const std::chrono::time_point<std::chrono::system_clock>& GetContentValidUntil() const  |  Obtiene la hora de expiración de la directiva.
 public bool DoesAllowOfflineAccess() const  |  Determina si la directiva permite o no el acceso a contenido sin conexión.
 public const std::string& GetReferrer() const  |  Obtiene la dirección del sitio de referencia de directiva.
public const std::map<std::string, std::string>& GetEncryptedAppData() const  |  Obtiene datos específicos de la aplicación que se cifraron.
public const std::map<std::string, std::string>& GetSignedAppData() const  |  Obtiene datos específicos de la aplicación que se firmaron.
  
## <a name="members"></a>Miembros
  
### <a name="protectiontype"></a>ProtectionType
Obtiene el tipo de protección, con independencia de que se haya creado a partir de la plantilla del SDK de protección o no.

  
**Devuelve**: tipo de protección
  
### <a name="getname"></a>GetName
Obtiene el nombre de directiva.

  
**Devuelve**: nombre de la directiva
  
### <a name="getdescription"></a>GetDescription
Obtiene la descripción de la directiva.

  
**Devuelve**: descripción de la directiva
  
### <a name="gettemplateid"></a>GetTemplateId
Obtiene el identificador de la plantilla de protección.

  
**Devuelve**: identificador de la plantilla
  
### <a name="userrights"></a>UserRights
Obtiene una colección de asignaciones de usuarios a derechos.

  
**Devuelve**: colección de asignaciones de usuarios a derechos. El valor de la propiedad [UserRights](class_mip_userrights.md) estará vacío si el usuario actual no tiene acceso a la información de derechos del usuario (es decir, no es el propietario y no tiene el derecho VIEWRIGHTSDATA).
  
### <a name="userroles"></a>UserRoles
Obtiene una colección de asignaciones de usuarios a roles

  
**Devuelve**: colección de asignaciones de usuarios a roles
  
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
Obtiene la hora de expiración de la directiva.

  
**Devuelve**: hora de expiración de la directiva
  
### <a name="doesallowofflineaccess"></a>DoesAllowOfflineAccess
Determina si la directiva permite o no el acceso a contenido sin conexión.

  
**Devuelve**: si la directiva permite o no el acceso a contenido sin conexión (valor predeterminado = true)
  
### <a name="getreferrer"></a>GetReferrer
Obtiene la dirección del sitio de referencia de directiva.

  
**Devuelve**: dirección del sitio de referencia de la directiva. El sitio de referencia es una URI que puede mostrarse al usuario cuando la adquisición de la directiva ha producido un error y que contiene información sobre cómo el usuario puede obtener permiso para tener acceso al contenido.
  
### <a name="getencryptedappdata"></a>GetEncryptedAppData
Obtiene datos específicos de la aplicación que se cifraron.

  
**Devuelve**: datos específicos de la aplicación Un [ProtectionHandler](class_mip_protectionhandler.md) puede contener un diccionario de datos específicos de la aplicación que se cifraron con el servicio de protección. Estos datos cifrados son independientes de los datos firmados accesibles a través de [ProtectionDescriptor::GetSignedAppData](class_mip_protectiondescriptor.md#getsignedappdata)
  
### <a name="getsignedappdata"></a>GetSignedAppData
Obtiene datos específicos de la aplicación que se firmaron.

  
**Devuelve**: datos específicos de la aplicación Un [ProtectionHandler](class_mip_protectionhandler.md) puede contener un diccionario de datos específicos de la aplicación firmados por el servicio de protección. Estos datos firmados son independientes de los datos cifrados accesibles mediante [ProtectionDescriptor::GetEncryptedAppData](class_mip_protectiondescriptor.md#getencryptedappdata)