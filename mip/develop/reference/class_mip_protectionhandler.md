---
title: clase mip::ProtectionHandler
description: Documenta la clase mip::protectionhandler de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 37358a2160c190978a21c491249dab42598d49b6
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651333"
---
# <a name="class-mipprotectionhandler"></a>clase mip::ProtectionHandler 
Administrar las acciones relacionadas con la protección para una configuración de protección específica.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public std::shared_ptr\<Stream\> CreateProtectedStream(const std::shared_ptr\<Stream\>& backingStream, int64_t contentStartPosition, int64_t contentSize)  |  Cree una secuencia protegida que permita el cifrado y descifrado de contenido.
public int64_t EncryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Cifre un búfer.
public int64_t DecryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Descifre un búfer.
public int64_t GetProtectedContentLength(int64_t unprotectedLength, bool includesFinalBlock)  |  Calcule el tamaño (en bytes) de contenido si fuera a cifrarse con este [ProtectionHandler](class_mip_protectionhandler.md).
public int64_t GetBlockSize()  |  Obtiene el tamaño de bloque (en bytes) para el modo de cifrado utilizado por este [ProtectionHandler](class_mip_protectionhandler.md).
public std::vector\<std::string\> GetRights() const  |  Obtiene los derechos concedidos a la identidad o usuario asociados a este elemento [ProtectionHandler](class_mip_protectionhandler.md).
public bool AccessCheck(const std::string& right) const  |  Comprueba si el controlador de protección otorga al usuario acceso al derecho especificado.
public const std::string GetIssuedTo()  |  Obtiene el usuario asociado al controlador de protección.
public const std::string GetOwner()  |  Obtiene la dirección de correo electrónico del propietario del contenido.
public bool IsIssuedToOwner()  |  Obtiene si el usuario actual es o no el propietario del contenido.
Public std:: shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor()  |  Obtiene los detalles de la protección.
public const std::string GetContentId()  |  Obtiene el identificador único para el documento o contenido.
public bool DoesUseDeprecatedAlgorithms()  |  Obtiene si el controlador de protección usa o no algoritmos criptográficos en desuso (ECB) para la compatibilidad con versiones anteriores.
public bool IsAuditedExtractAllowed()  |  Obtiene si el controlador de protección concede o no al usuario el derecho “extracción auditada”.
public const std::vector\<uint8_t\> GetSerializedPublishingLicense()  |  Serialice [ProtectionHandler](class_mip_protectionhandler.md) en una licencia de publicación (PL).
public const std::vector\<uint8_t\> GetSerializedProtectionInfo()  |  Obtiene la información de protección.
  
## <a name="members"></a>Miembros
  
### <a name="createprotectedstream-function"></a>Función CreateProtectedStream
Cree una secuencia protegida que permita el cifrado y descifrado de contenido.

Parámetros:  
* **backingStream**: Flujo base desde la que se va a lectura/escritura 


* **contentStartPosition**: Posición inicial (en bytes) dentro de la secuencia de copia de seguridad donde comienza el contenido protegido 


* **contentSize**: Tamaño (en bytes) del contenido protegido dentro de la secuencia de seguridad



  
**Devuelve**: Secuencia protegida
  
### <a name="encryptbuffer-function"></a>Función EncryptBuffer
Cifre un búfer.

Parámetros:  
* **offsetFromStart**: Posición relativa de inputBuffer desde el principio del contenido de texto no cifrado 


* **inputBuffer**: Búfer de contenido de texto no cifrado que se cifrarán 


* **inputBufferSize**: Tamaño (en bytes) del búfer de entrada 


* **outputBuffer**: Búfer en el que se copiará el contenido cifrado 


* **outputBufferSize**: Tamaño (en bytes) del búfer de salida 


* **isFinal**: Si el búfer de entrada contiene los bytes finales texto no cifrado o no



  
**Devuelve**: Tamaño real (en bytes) de contenido cifrado
  
### <a name="decryptbuffer-function"></a>Función DecryptBuffer
Descifre un búfer.

Parámetros:  
* **offsetFromStart**: Posición relativa de inputBuffer desde el principio del contenido cifrado 


* **inputBuffer**: Búfer de contenido cifrado que se van a descifrar 


* **inputBufferSize**: Tamaño (en bytes) del búfer de entrada 


* **outputBuffer**: Búfer en el que se copiará el contenido descifrado 


* **outputBufferSize**: Tamaño (en bytes) del búfer de salida 


* **isFinal**: Si el búfer de entrada contiene los bytes finales cifrados o no



  
**Devuelve**: Tamaño real (en bytes) de contenido descifrado
  
### <a name="getprotectedcontentlength-function"></a>Función GetProtectedContentLength
Calcule el tamaño (en bytes) de contenido si fuera a cifrarse con este [ProtectionHandler](class_mip_protectionhandler.md).

Parámetros:  
* **unprotectedLength**: Tamaño (en bytes) del contenido no protegido 


* **includesFinalBlock**: Describe si el contenido no protegido en cuestión incluye el bloque final o no. Por ejemplo, en el modo de cifrado CBC4k, los bloques protegidos que no sean finales tienen el mismo tamaño que los bloques no protegidos, pero los bloques protegidos finales tienen un tamaño superior que sus homólogos no protegidos.



  
**Devuelve**: Tamaño (en bytes) del contenido protegido
  
### <a name="getblocksize-function"></a>Función GetBlockSize
Obtiene el tamaño de bloque (en bytes) para el modo de cifrado utilizado por este [ProtectionHandler](class_mip_protectionhandler.md).

  
**Devuelve**: Tamaño de bloque (en bytes)
  
### <a name="getrights-function"></a>Función GetRights
Obtiene los derechos concedidos a la identidad o usuario asociados a este elemento [ProtectionHandler](class_mip_protectionhandler.md).

  
**Devuelve**: Derechos concedidos al usuario
  
### <a name="accesscheck-function"></a>Función AccessCheck
Comprueba si el controlador de protección otorga al usuario acceso al derecho especificado.

Parámetros:  
* **right**: Derecho a comprobar



  
**Devuelve**: Si el controlador de protección concede acceso de usuario al especificado hacia la derecha o no
  
### <a name="getissuedto-function"></a>Función GetIssuedTo
Obtiene el usuario asociado al controlador de protección.

  
**Devuelve**: Usuario asociado con el controlador de protección
  
### <a name="getowner-function"></a>GetOwner (función)
Obtiene la dirección de correo electrónico del propietario del contenido.

  
**Devuelve**: Dirección de correo electrónico del propietario del contenido
  
### <a name="isissuedtoowner-function"></a>Función IsIssuedToOwner
Obtiene si el usuario actual es o no el propietario del contenido.

  
**Devuelve**: Si el usuario actual es el propietario del contenido o no
  
### <a name="getprotectiondescriptor-function"></a>Función GetProtectionDescriptor
Obtiene los detalles de la protección.

  
**Devuelve**: Detalles de protección
  
### <a name="getcontentid-function"></a>Función GetContentId
Obtiene el identificador único para el documento o contenido.

  
**Devuelve**: Tipo de identificador de contenido
  
### <a name="doesusedeprecatedalgorithms-function"></a>Función DoesUseDeprecatedAlgorithms
Obtiene si el controlador de protección usa o no algoritmos criptográficos en desuso (ECB) para la compatibilidad con versiones anteriores.

  
**Devuelve**: Si el controlador de protección usa algoritmos criptográficos en desuso o no
  
### <a name="isauditedextractallowed-function"></a>Función IsAuditedExtractAllowed
Obtiene si el controlador de protección concede o no al usuario el derecho “extracción auditada”.

  
**Devuelve**: Si el controlador de protección le concede el usuario "extracto auditado" hacia la derecha o no
  
### <a name="getserializedpublishinglicense-function"></a>Función GetSerializedPublishingLicense
Serialice [ProtectionHandler](class_mip_protectionhandler.md) en una licencia de publicación (PL).

  
**Devuelve**: Licencia de publicación serializado
  
### <a name="getserializedprotectioninfo-function"></a>Función GetSerializedProtectionInfo
Obtiene la información de protección.

  
**Devuelve**: Información serializada de protección