---
title: Clase mip ProtectionHandler
description: Referencia de la clase mip ProtectionHandler
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 6fbae05030f56d3c9e680e6de9c8177a11b2f1e2
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446760"
---
# <a name="class-mipprotectionhandler"></a>clase mip::ProtectionHandler 
Administrar las acciones relacionadas con la protección para una configuración de protección específica.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public std::shared_ptr<Stream> CreateProtectedStream(const std::shared_ptr<Stream>& backingStream, int64_t contentStartPosition, int64_t contentSize)  |  Cree una secuencia protegida que permita el cifrado y descifrado de contenido.
 public int64_t EncryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Cifre un búfer.
 public int64_t DecryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Descifre un búfer.
 public int64_t GetProtectedContentLength(int64_t unprotectedLength, bool includesFinalBlock)  |  Calcule el tamaño (en bytes) de contenido si fuera a cifrarse con este [ProtectionHandler](class_mip_protectionhandler.md).
 public int64_t GetBlockSize()  |  Obtiene el tamaño de bloque (en bytes) para el modo de cifrado utilizado por este [ProtectionHandler](class_mip_protectionhandler.md).
public std::vector<std::string> GetRights() const  |  Obtiene los derechos concedidos a la identidad o usuario asociados a este elemento [ProtectionHandler](class_mip_protectionhandler.md).
 public bool AccessCheck(const std::string& right) const  |  Comprueba si el controlador de protección otorga al usuario acceso al derecho especificado.
 public const std::string GetIssuedTo()  |  Obtiene el usuario asociado al controlador de protección.
 public const std::string GetOwner()  |  Obtiene la dirección de correo electrónico del propietario del contenido.
 public bool IsIssuedToOwner()  |  Obtiene si el usuario actual es o no el propietario del contenido.
public std::shared_ptr<ProtectionDescriptor> GetProtectionDescriptor()  |  Obtiene los detalles de la protección.
 public const std::string GetContentId()  |  Obtiene el identificador único para el documento o contenido.
 public bool DoesUseDeprecatedAlgorithms()  |  Obtiene si el controlador de protección usa o no algoritmos criptográficos en desuso (ECB) para la compatibilidad con versiones anteriores.
 public bool IsAuditedExtractAllowed()  |  Obtiene si el controlador de protección concede o no al usuario el derecho “extracción auditada”.
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


* **isFinal**: si el búfer de entrada contiene o no los bytes finales de texto no cifrado.



  
**Devuelve**: tamaño real (en bytes) de contenido cifrado
  
### <a name="decryptbuffer"></a>DecryptBuffer
Descifre un búfer.

Parámetros:  
* **offsetFromStart**: posición relativa de inputBuffer desde el principio del contenido cifrado 


* **inputBuffer**: búfer de contenido cifrado que se va a descifrar 


* **inputBufferSize**: tamaño (en bytes) del búfer de entrada 


* **outputBuffer**: búfer en el que se copiará el contenido descifrado 


* **outputBufferSize**: tamaño (en bytes) del búfer de salida 


* **isFinal**: si el búfer de entrada contiene o no los bytes cifrados finales.



  
**Devuelve**: tamaño real (en bytes) de contenido descifrado
  
### <a name="getprotectedcontentlength"></a>GetProtectedContentLength
Calcule el tamaño (en bytes) de contenido si fuera a cifrarse con este [ProtectionHandler](class_mip_protectionhandler.md).

Parámetros:  
* **unprotectedLength**: tamaño (en bytes) del contenido no protegido. 


* **includesFinalBlock**: describe si en el contenido no protegido en cuestión se incluye el bloque final o no. Por ejemplo, en el modo de cifrado CBC4k, los bloques protegidos que no sean finales tienen el mismo tamaño que los bloques no protegidos, pero los bloques protegidos finales tienen un tamaño superior que sus homólogos no protegidos.



  
**Devuelve**: tamaño (en bytes) del contenido protegido
  
### <a name="getblocksize"></a>GetBlockSize
Obtiene el tamaño de bloque (en bytes) para el modo de cifrado utilizado por este [ProtectionHandler](class_mip_protectionhandler.md).

  
**Devuelve**: tamaño (en bytes) del bloque
  
### <a name="getrights"></a>GetRights
Obtiene los derechos concedidos a la identidad o usuario asociados a este elemento [ProtectionHandler](class_mip_protectionhandler.md).

  
**Devuelve**: derechos concedidos al usuario.
  
### <a name="accesscheck"></a>AccessCheck
Comprueba si el controlador de protección otorga al usuario acceso al derecho especificado.

Parámetros:  
* **right**: derecho para comprobar



  
**Devuelve**: si el controlador de protección concede al usuario acceso al derecho especificado.
  
### <a name="getissuedto"></a>GetIssuedTo
Obtiene el usuario asociado al controlador de protección.

  
**Devuelve**: usuario asociado al controlador de protección
  
### <a name="getowner"></a>GetOwner
Obtiene la dirección de correo electrónico del propietario del contenido.

  
**Devuelve**: dirección de correo electrónico del propietario del contenido
  
### <a name="isissuedtoowner"></a>IsIssuedToOwner
Obtiene si el usuario actual es o no el propietario del contenido.

  
**Devuelve**: si el usuario actual es o no el propietario del contenido.
  
### <a name="protectiondescriptor"></a>ProtectionDescriptor
Obtiene los detalles de la protección.

  
**Devuelve**: detalles de protección
  
### <a name="getcontentid"></a>GetContentId
Obtiene el identificador único para el documento o contenido.

  
**Devuelve**: identificador de contenido único
  
### <a name="doesusedeprecatedalgorithms"></a>DoesUseDeprecatedAlgorithms
Obtiene si el controlador de protección usa o no algoritmos criptográficos en desuso (ECB) para la compatibilidad con versiones anteriores.

  
**Devuelve**: si el controlador de protección usa o no algoritmos criptográficos en desuso
  
### <a name="isauditedextractallowed"></a>IsAuditedExtractAllowed
Obtiene si el controlador de protección concede o no al usuario el derecho “extracción auditada”.

  
**Devuelve**: si el controlador de protección concede o no al usuario el derecho “extracción auditada”.
  
### <a name="getserializedpublishinglicense"></a>GetSerializedPublishingLicense
Serialice [ProtectionHandler](class_mip_protectionhandler.md) en una licencia de publicación (PL).

  
**Devuelve**: licencia de publicación serializada