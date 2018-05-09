# <a name="class-mipuserpolicy"></a>clase mip::UserPolicy 
Representa una directiva asociada al contenido protegido.
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public bool AccessCheck | Comprueba si la directiva concede acceso de usuario al derecho especificado.
public UserPolicyType GetType | Obtiene el tipo de directiva.
public std::string GetName | Obtiene el nombre de directiva.
public std::string GetDescription | Obtiene la descripción de la directiva.
public std::shared_ptr< TemplateDescriptor > GetTemplateDescriptor public std::shared_ptr< PolicyDescriptor > GetPolicyDescriptor public std::string GetOwner | Obtiene la dirección de correo electrónico del propietario del contenido.
public std::string GetIssuedTo | Obtiene el usuario asociado a la directiva de protección.
public bool IsIssuedToOwner | Determina si el usuario actual es o no el propietario del contenido.
public std:: String GetContentId | Obtiene el identificador único para el documento o contenido.
public const mip::AppDataHashMap GetEncryptedAppData | Obtiene datos específicos de la aplicación que se cifraron.
public const mip::AppDataHashMap GetSignedAppData | Obtiene datos específicos de la aplicación que se firmaron.
public std::chrono::time_point< std::chrono::system_clock > GetContentValidUntil | Obtiene la hora de expiración de la directiva.
public bool DoesUseDeprecatedAlgorithms | Determina si la directiva utiliza o no algoritmos criptográficos en desuso (ECB) por compatibilidad con versiones anteriores.
public bool IsAuditedExtractAllowed | Determina si la directiva otorga o no al usuario el derecho "extracto auditado".
public const std::vector< unsigned char > GetSerializedPolicy public std::shared_ptr< rmscore::core::ProtectionPolicy > GetImpl
## <a name="members"></a>Miembros
### <a name="accesscheck"></a>AccessCheck
Comprueba si la directiva concede acceso de usuario al derecho especificado.
#### <a name="parameters"></a>Parámetros
* right Derecho para comprobar
#### <a name="returns"></a>Devuelve
Si la directiva concede acceso de usuario o no al derecho especificado.
### <a name="userpolicytype"></a>UserPolicyType
Obtiene el tipo de directiva.
#### <a name="returns"></a>Devuelve
Tipo de directiva
### <a name="getname"></a>GetName
Obtiene el nombre de directiva.
#### <a name="returns"></a>Devuelve
Nombre de la directiva
### <a name="getdescription"></a>GetDescription
Obtiene la descripción de la directiva.
#### <a name="returns"></a>Devuelve
Descripción de la directiva
### <a name="templatedescriptor"></a>TemplateDescriptor
Obtiene [TemplateDescriptor](#classmip_1_1_template_descriptor) para una clase [UserPolicy](#classmip_1_1_user_policy) basada en plantilla.
#### <a name="returns"></a>Devuelve
[TemplateDescriptor](#classmip_1_1_template_descriptor) si [UserPolicy](#classmip_1_1_user_policy) está basado en plantilla; en caso contrario, nullptr
### <a name="policydescriptor"></a>PolicyDescriptor
Obtiene [PolicyDescriptor](#classmip_1_1_policy_descriptor) para una clase [UserPolicy](#classmip_1_1_user_policy) ad hoc.
#### <a name="returns"></a>Devuelve
[PolicyDescriptor](#classmip_1_1_policy_descriptor) si [UserPolicy](#classmip_1_1_user_policy) es ad hoc; de lo contrario, nullptr
### <a name="getowner"></a>GetOwner
Obtiene la dirección de correo electrónico del propietario del contenido.
#### <a name="returns"></a>Devuelve
Dirección de correo electrónico del propietario del contenido
### <a name="getissuedto"></a>GetIssuedTo
Obtiene el usuario asociado a la directiva de protección.
#### <a name="returns"></a>Devuelve
Usuario asociado a la directiva de protección
### <a name="isissuedtoowner"></a>IsIssuedToOwner
Determina si el usuario actual es o no el propietario del contenido.
#### <a name="returns"></a>Devuelve
Si el usuario actual es o no el propietario del contenido
### <a name="getcontentid"></a>GetContentId
Obtiene el identificador único para el documento o contenido.
#### <a name="returns"></a>Devuelve
Tipo de identificador de contenido
### <a name="mipappdatahashmap"></a>mip::AppDataHashMap
Obtiene datos específicos de la aplicación que se cifraron.
[UserPolicy ](#classmip_1_1_user_policy) puede contener un diccionario de datos específicos de la aplicación cifrados por el servicio RMS. Estos datos cifrados son independientes de los datos firmados accesibles mediante [UserPolicy::GetSignedAppData](#classmip_1_1_user_policy_1a1c8a284d50adcac1a0a09316afa1d43e)
### <a name="mipappdatahashmap"></a>mip::AppDataHashMap
Obtiene datos específicos de la aplicación que se firmaron.
[UserPolicy ](#classmip_1_1_user_policy) puede contener un diccionario de datos específicos de la aplicación firmados por el servicio RMS. Estos datos firmados son independientes de los datos cifrados accesibles mediante [UserPolicy::GetEncryptedAppData](#classmip_1_1_user_policy_1a610fbc799284ab0ce4354c0611ece0e8)
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
Obtiene la hora de expiración de la directiva.
#### <a name="returns"></a>Devuelve
Hora de expiración de la directiva
### <a name="doesusedeprecatedalgorithms"></a>DoesUseDeprecatedAlgorithms
Determina si la directiva utiliza o no algoritmos criptográficos en desuso (ECB) por compatibilidad con versiones anteriores.
#### <a name="returns"></a>Devuelve
Si la directiva utiliza o no algoritmos criptográficos en desuso
### <a name="isauditedextractallowed"></a>IsAuditedExtractAllowed
Determina si la directiva otorga o no al usuario el derecho "extracto auditado".
#### <a name="returns"></a>Devuelve
Si la directiva otorga o no al usuario el derecho "extracto auditado"
### <a name="getserializedpolicy"></a>GetSerializedPolicy
Serializa [UserPolicy](#classmip_1_1_user_policy) en una licencia de publicación (PL)
#### <a name="returns"></a>Devuelve
Serializa [UserPolicy](#classmip_1_1_user_policy)
### <a name="getimpl"></a>GetImpl
Obtiene la implementación de clase derivada interna de [UserPolicy](#classmip_1_1_user_policy).
#### <a name="returns"></a>Devuelve
Implementación de clase derivada de [UserPolicy](#classmip_1_1_user_policy) Solo para uso interno