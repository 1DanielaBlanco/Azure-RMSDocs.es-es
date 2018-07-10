# <a name="class-mipprotectiondescriptorbuilder"></a>clase mip::ProtectionDescriptorBuilder 
Representa una directiva ad-hoc asociada al contenido protegido.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public MIP_API std::shared_ptr<ProtectionDescriptor> Build()  |  Crea un [ProtectionDescriptor](class_mip_protectiondescriptor.md) cuyos permisos de acceso se definen por esta instancia de [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md).
 public void SetName(const std::string& value)  |  Establece el nombre de la directiva de protección.
 public void SetDescription(const std::string& value)  |  Establece la descripción de la directiva de protección.
public void SetContentValidUntil(const std::chrono::time_point<std::chrono::system_clock>& value)  |  Establece la hora de expiración de la directiva de protección.
 public void SetAllowOfflineAccess(bool value)  |  Establece si la directiva de protección permite o no el acceso a contenido sin conexión.
 public void SetReferrer(const std::string& uri)  |  Establece la dirección del sitio de referencia de la directiva de protección.
public void SetEncryptedAppData(const std::map<std::string, std::string>& value)  |  Establece los datos específicos de la aplicación que fueron cifrados.
public void SetSignedAppData(const std::map<std::string, std::string>& value)  |  Establece los datos específicos de la aplicación que deben firmarse.
 public virtual ~ProtectionDescriptorBuilder()  | _No se ha documentado todavía._
  
## <a name="members"></a>Miembros
  
### <a name="protectiondescriptor"></a>ProtectionDescriptor
Crea un [ProtectionDescriptor](class_mip_protectiondescriptor.md) cuyos permisos de acceso se definen por esta instancia de [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md).

  
**Devuelve**: nueva instancia de [ProtectionDescriptor](class_mip_protectiondescriptor.md)
  
### <a name="setname"></a>SetName
Establece el nombre de la directiva de protección.

Parámetros:  
* **value**: nombre de la directiva de protección


  
### <a name="setdescription"></a>SetDescription
Establece la descripción de la directiva de protección.

Parámetros:  
* **value**: descripción de la directiva


  
### <a name="setcontentvaliduntil"></a>SetContentValidUntil
Establece la hora de expiración de la directiva de protección.

Parámetros:  
* **value**: hora de expiración de la directiva


  
### <a name="setallowofflineaccess"></a>SetAllowOfflineAccess
Establece si la directiva de protección permite o no el acceso a contenido sin conexión.

Parámetros:  
* **value**: si la directiva permite o no el acceso a contenido sin conexión


  
### <a name="setreferrer"></a>SetReferrer
Establece la dirección del sitio de referencia de la directiva de protección.

Parámetros:  
* **uri**: dirección del sitio de referencia de directiva


El sitio de referencia es un identificador URI que puede mostrarse al usuario cuando la adquisición de la directiva de protección ha producido un error y que contiene información sobre cómo el usuario puede obtener permiso para tener acceso al contenido.
  
### <a name="setencryptedappdata"></a>SetEncryptedAppData
Establece los datos específicos de la aplicación que fueron cifrados.

Parámetros:  
* **value**: datos específicos de la aplicación


Una aplicación puede especificar un diccionario de datos específicos de la aplicación cifrados por el servicio de protección. Estos datos cifrados son independientes del conjunto de datos firmado por SetSignedAppData.
  
### <a name="setsignedappdata"></a>SetSignedAppData
Establece los datos específicos de la aplicación que deben firmarse.

Parámetros:  
* **value**: datos específicos de la aplicación


Una aplicación puede especificar un diccionario de datos específicos de la aplicación que se firmarán por el servicio de protección. Estos datos firmados son independientes del conjunto de datos cifrados por SetEncryptedAppData.
  
### <a name="protectiondescriptorbuilder"></a>~ProtectionDescriptorBuilder
_No se ha documentado todavía._
