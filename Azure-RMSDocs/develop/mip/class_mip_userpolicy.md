# <a name="class-mipuserpolicy"></a>clase mip::UserPolicy 
Representa una directiva asociada al contenido protegido.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public bool AccessCheck(const std::string& right) const  |  Comprueba si la directiva concede acceso de usuario al derecho especificado.
 public UserPolicyType GetType()  |  Obtiene el tipo de directiva.
 public std::string GetName()  |  Obtiene el nombre de directiva.
 public std::string GetDescription()  |  Obtiene la descripción de la directiva.
public std::shared_ptr<TemplateDescriptor> GetTemplateDescriptor()  |  Obtiene [TemplateDescriptor](class_mip_templatedescriptor.md) para una clase [UserPolicy](class_mip_userpolicy.md) basada en plantilla.
public std::shared_ptr<PolicyDescriptor> GetPolicyDescriptor()  |  Obtiene [PolicyDescriptor](class_mip_policydescriptor.md) para una clase [UserPolicy](class_mip_userpolicy.md) ad hoc.
 public std::string GetOwner()  |  Obtiene la dirección de correo electrónico del propietario del contenido.
 public std::string GetIssuedTo()  |  Obtiene el usuario asociado a la directiva de protección.
 public bool IsIssuedToOwner()  |  Determina si el usuario actual es o no el propietario del contenido.
 public std::string GetContentId()  |  Obtiene el identificador único para el documento o contenido.
 public const mip::AppDataHashMap GetEncryptedAppData()  |  Obtiene datos específicos de la aplicación que se cifraron.
 public const mip::AppDataHashMap GetSignedAppData()  |  Obtiene datos específicos de la aplicación que se firmaron.
public std::chrono::time_point<std::chrono::system_clock> GetContentValidUntil()  |  Obtiene la hora de expiración de la directiva.
 public bool DoesUseDeprecatedAlgorithms()  |  Determina si la directiva utiliza o no algoritmos criptográficos en desuso (ECB) por compatibilidad con versiones anteriores.
 public bool IsAuditedExtractAllowed()  |  Determina si la directiva otorga o no al usuario el derecho "extracto auditado".
public const std::vector<unsigned char> GetSerializedPolicy()  |  Serializa [UserPolicy](class_mip_userpolicy.md) en una licencia de publicación (PL)
public std::shared_ptr<rmscore::core::ProtectionPolicy> GetImpl()  |  Obtiene la implementación de clase derivada interna de [UserPolicy](class_mip_userpolicy.md).
  
## <a name="members"></a>Miembros
  
### <a name="accesscheck"></a>AccessCheck
Comprueba si la directiva concede acceso de usuario al derecho especificado.

Parámetros:  
* **right**: derecho para comprobar



  
**Devuelve**: si la directiva concede acceso de usuario o no al derecho especificado
  
### <a name="userpolicytype"></a>UserPolicyType
Obtiene el tipo de directiva.

  
**Devuelve**: tipo de directiva
  
### <a name="getname"></a>GetName
Obtiene el nombre de directiva.

  
**Devuelve**: nombre de la directiva
  
### <a name="getdescription"></a>GetDescription
Obtiene la descripción de la directiva.

  
**Devuelve**: descripción de la directiva
  
### <a name="templatedescriptor"></a>TemplateDescriptor
Obtiene [TemplateDescriptor](class_mip_templatedescriptor.md) para una clase [UserPolicy](class_mip_userpolicy.md) basada en plantilla.

  
**Devuelve**: [TemplateDescriptor](class_mip_templatedescriptor.md) si [UserPolicy](class_mip_userpolicy.md) está basado en plantilla; en caso contrario, nullptr
  
### <a name="policydescriptor"></a>PolicyDescriptor
Obtiene [PolicyDescriptor](class_mip_policydescriptor.md) para una clase [UserPolicy](class_mip_userpolicy.md) ad hoc.

  
**Devuelve**: [PolicyDescriptor](class_mip_policydescriptor.md) si [UserPolicy](class_mip_userpolicy.md) es ad hoc; de lo contrario, nullptr
  
### <a name="getowner"></a>GetOwner
Obtiene la dirección de correo electrónico del propietario del contenido.

  
**Devuelve**: dirección de correo electrónico del propietario del contenido
  
### <a name="getissuedto"></a>GetIssuedTo
Obtiene el usuario asociado a la directiva de protección.

  
**Devuelve**: usuario asociado a la directiva de protección
  
### <a name="isissuedtoowner"></a>IsIssuedToOwner
Determina si el usuario actual es o no el propietario del contenido.

  
**Devuelve**: determina si el usuario actual es o no el propietario del contenido
  
### <a name="getcontentid"></a>GetContentId
Obtiene el identificador único para el documento o contenido.

  
**Devuelve**: identificador de contenido único
  
### <a name="mipappdatahashmap"></a>mip::AppDataHashMap
Obtiene datos específicos de la aplicación que se cifraron.
[UserPolicy ](class_mip_userpolicy.md) puede contener un diccionario de datos específicos de la aplicación cifrados por el servicio RMS. Estos datos cifrados son independientes de los datos firmados accesibles mediante [UserPolicy::GetSignedAppData](class_mip_userpolicy.md#getsignedappdata)
  
### <a name="mipappdatahashmap"></a>mip::AppDataHashMap
Obtiene datos específicos de la aplicación que se firmaron.
[UserPolicy ](class_mip_userpolicy.md) puede contener un diccionario de datos específicos de la aplicación firmados por el servicio RMS. Estos datos firmados son independientes de los datos cifrados accesibles mediante [UserPolicy::GetEncryptedAppData](class_mip_userpolicy.md#getencryptedappdata)
  
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
Obtiene la hora de expiración de la directiva.

  
**Devuelve**: hora de expiración de la directiva
  
### <a name="doesusedeprecatedalgorithms"></a>DoesUseDeprecatedAlgorithms
Determina si la directiva utiliza o no algoritmos criptográficos en desuso (ECB) por compatibilidad con versiones anteriores.

  
**Devuelve**: si la directiva utiliza o no algoritmos criptográficos en desuso
  
### <a name="isauditedextractallowed"></a>IsAuditedExtractAllowed
Determina si la directiva otorga o no al usuario el derecho "extracto auditado".

  
**Devuelve**: si la directiva otorga o no al usuario el derecho "extracto auditado"
  
### <a name="getserializedpolicy"></a>GetSerializedPolicy
Serializa [UserPolicy](class_mip_userpolicy.md) en una licencia de publicación (PL)

  
**Devuelve**: [UserPolicy](class_mip_userpolicy.md) en serie
  
### <a name="getimpl"></a>GetImpl
Obtiene la implementación de clase derivada interna de [UserPolicy](class_mip_userpolicy.md).

  
**Devuelve**: implementación de clase derivada de [UserPolicy](class_mip_userpolicy.md). Solo para uso interno