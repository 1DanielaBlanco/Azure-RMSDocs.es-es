# <a name="class-mipprotectionhandler"></a>clase mip::ProtectionHandler 
Realiza acciones relacionadas con la protección para una configuración de protección específica (es decir, usuarios, derechos, roles, etc.)
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public std::shared_ptr<Stream> CreateProtectedStream(const std::shared_ptr<Stream>& backingStream, uint64_t contentStartPosition, uint64_t contentSize)  |  Cree una secuencia protegida que permita el cifrado y descifrado de contenido.
 public int64_t EncryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Cifre un búfer.
 public int64_t DecryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Descifre un búfer.
 public uint64_t GetProtectedContentLength(uint64_t size)  |  Calcule el tamaño (en bytes) de contenido si fuera a cifrarse con este [ProtectionHandler](class_mip_protectionhandler.md).
 public uint64_t GetBlockSize()  |  Obtiene el tamaño de bloque (en bytes) para el modo de cifrado utilizado por este [ProtectionHandler](class_mip_protectionhandler.md).
 public bool AccessCheck(const std::string& right) const  |  Comprueba si el controlador de protección otorga al usuario acceso al derecho especificado.
 public const std::string GetIssuedTo()  |  Obtiene el usuario asociado al controlador de protección.
 public const std::string GetOwner()  |  Obtiene la dirección de correo electrónico del propietario del contenido.
 public bool IsIssuedToOwner()  |  Determina si el usuario actual es o no el propietario del contenido.
public std::shared_ptr<ProtectionDescriptor> GetProtectionDescriptor()  |  Obtiene los detalles de la protección.
 public const std::string GetContentId()  |  Obtiene el identificador único para el documento o contenido.
 public bool DoesUseDeprecatedAlgorithms()  |  Determina si el controlador de protección utiliza o no algoritmos criptográficos en desuso para la compatibilidad con versiones anteriores.
 public bool IsAuditedExtractAllowed()  |  Determina si el controlador de protección otorga o no al usuario el derecho "extracto auditado".
public const std::vector<uint8_t> GetSerializedPublishingLicense()  |  Serialice [ProtectionHandler](class_mip_protectionhandler.md) en una licencia de publicación (PL).
  
## <a name="members"></a>Miembros
  
### <a name="stream"></a>Transmitir
Cree una secuencia protegida que permita el cifrado y descifrado de contenido.

Parámetros:  
* **backingStream**: flujo base desde el que se lee/escribe 


* **contentStartPosition**: posición inicial (en bytes) dentro del flujo base donde comienza el contenido protegido 


* **contentSize**: tamaño (en bytes) del contenido protegido dentro del flujo base



  
**Devuelve**: flujo protegido
  
### <a name="encryptbuffer"></a>EncryptBuffer
Cifre un búfer.

Parámetros:  
* **offsetFromStart**: posición relativa de inputBuffer desde el principio del contenido de texto no cifrado 


* **inputBuffer**: búfer de contenido de texto no cifrado que se va a cifrar 


* **inputBufferSize**: tamaño (en bytes) del búfer de entrada 


* **outputBuffer**: búfer en el que se copiará el contenido cifrado 


* **outputBufferSize**: tamaño (en bytes) del búfer de salida 


* **isFinal**: si el búfer de entrada contiene o no los bytes finales de texto no cifrado



  
**Devuelve**: tamaño real (en bytes) de contenido cifrado
  
### <a name="decryptbuffer"></a>DecryptBuffer
Descifre un búfer.

Parámetros:  
* **offsetFromStart**: posición relativa de inputBuffer desde el principio del contenido cifrado 


* **inputBuffer**: búfer de contenido cifrado que se va a descifrar 


* **inputBufferSize**: tamaño (en bytes) del búfer de entrada 


* **outputBuffer**: búfer en el que se copiará el contenido descifrado 


* **outputBufferSize**: tamaño (en bytes) del búfer de salida 


* **isFinal**: si el búfer de entrada contiene o no los bytes finales cifrados



  
**Devuelve**: tamaño real (en bytes) de contenido descifrado
  
### <a name="getprotectedcontentlength"></a>GetProtectedContentLength
Calcule el tamaño (en bytes) de contenido si fuera a cifrarse con este [ProtectionHandler](class_mip_protectionhandler.md).

Parámetros:  
* **contentLength**: tamaño (en bytes) del contenido no protegido



  
**Devuelve**: tamaño (en bytes) del contenido protegido
  
### <a name="getblocksize"></a>GetBlockSize
Obtiene el tamaño de bloque (en bytes) para el modo de cifrado utilizado por este [ProtectionHandler](class_mip_protectionhandler.md).

  
**Devuelve**: tamaño (en bytes) del bloque
  
### <a name="accesscheck"></a>AccessCheck
Comprueba si el controlador de protección otorga al usuario acceso al derecho especificado.

Parámetros:  
* **right**: derecho para comprobar



  
**Devuelve**: si el controlador de protección otorga o no al usuario acceso al derecho especificado
  
### <a name="getissuedto"></a>GetIssuedTo
Obtiene el usuario asociado al controlador de protección.

  
**Devuelve**: usuario asociado al controlador de protección
  
### <a name="getowner"></a>GetOwner
Obtiene la dirección de correo electrónico del propietario del contenido.

  
**Devuelve**: dirección de correo electrónico del propietario del contenido
  
### <a name="isissuedtoowner"></a>IsIssuedToOwner
Determina si el usuario actual es o no el propietario del contenido.

  
**Devuelve**: determina si el usuario actual es o no el propietario del contenido
  
### <a name="protectiondescriptor"></a>ProtectionDescriptor
Obtiene los detalles de la protección.

  
**Devuelve**: detalles de protección
  
### <a name="getcontentid"></a>GetContentId
Obtiene el identificador único para el documento o contenido.

  
**Devuelve**: identificador de contenido único
  
### <a name="doesusedeprecatedalgorithms"></a>DoesUseDeprecatedAlgorithms
Determina si el controlador de protección utiliza o no algoritmos criptográficos en desuso para la compatibilidad con versiones anteriores.

  
**Devuelve**: si el controlador de protección utiliza o no algoritmos criptográficos en desuso
  
### <a name="isauditedextractallowed"></a>IsAuditedExtractAllowed
Determina si el controlador de protección otorga o no al usuario el derecho "extracto auditado".

  
**Devuelve**: si el controlador de protección otorga o no al usuario el derecho "extracto auditado".
  
### <a name="getserializedpublishinglicense"></a>GetSerializedPublishingLicense
Serialice [ProtectionHandler](class_mip_protectionhandler.md) en una licencia de publicación (PL).

  
**Devuelve**: licencia de publicación serializada