---
title: clase mip::ProtectionDescriptorBuilder
description: Documenta la clase mip::protectiondescriptorbuilder de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: b6ac49c7cb4d6f7592abac041365191d90951b7a
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651299"
---
# <a name="class-mipprotectiondescriptorbuilder"></a>clase mip::ProtectionDescriptorBuilder 
Crea un elemento [ProtectionDescriptor](class_mip_protectiondescriptor.md) que describe la protección asociada a un elemento de contenido.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
Public std:: shared_ptr MIP_API\<ProtectionDescriptor\> Build()  |  Crea un [ProtectionDescriptor](class_mip_protectiondescriptor.md) cuyos permisos de acceso se definen por esta instancia de [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md).
public void SetName(const std::string& value)  |  Establece el nombre de la directiva de protección.
public void SetDescription(const std::string& value)  |  Establece la descripción de la directiva de protección.
public void SetContentValidUntil(const std::chrono::time_point\<std::chrono::system_clock\>& value)  |  Establece la hora de expiración de la directiva de protección.
public void SetAllowOfflineAccess(bool value)  |  Establece si la directiva de protección permite o no el acceso a contenido sin conexión.
public void SetReferrer(const std::string& uri)  |  Establece la dirección del sitio de referencia de la directiva de protección.
pública SetEncryptedAppData void (const std:: Map\<std:: String, std:: String\>& valor)  |  Establece los datos específicos de la aplicación que fueron cifrados.
pública SetSignedAppData void (const std:: Map\<std:: String, std:: String\>& valor)  |  Establece los datos específicos de la aplicación que deben firmarse.
public virtual ~ProtectionDescriptorBuilder()  | _No se ha documentado todavía._
  
## <a name="members"></a>Miembros
  
### <a name="build-function"></a>Crear función
Crea un [ProtectionDescriptor](class_mip_protectiondescriptor.md) cuyos permisos de acceso se definen por esta instancia de [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md).

  
**Devuelve**: Nuevo [ProtectionDescriptor](class_mip_protectiondescriptor.md) instancia
  
### <a name="setname-function"></a>Función SetName
Establece el nombre de la directiva de protección.

Parámetros:  
* **value**: Nombre de la directiva de protección


  
### <a name="setdescription-function"></a>Función SetDescription
Establece la descripción de la directiva de protección.

Parámetros:  
* **value**: Descripción de la directiva


  
### <a name="setcontentvaliduntil-function"></a>Función SetContentValidUntil
Establece la hora de expiración de la directiva de protección.

Parámetros:  
* **value**: Hora de expiración de la directiva


  
### <a name="setallowofflineaccess-function"></a>Función SetAllowOfflineAccess
Establece si la directiva de protección permite o no el acceso a contenido sin conexión.

Parámetros:  
* **value**: Si la directiva permite el acceso de contenido sin conexión o no


  
### <a name="setreferrer-function"></a>Función SetReferrer
Establece la dirección del sitio de referencia de la directiva de protección.

Parámetros:  
* **uri**: Dirección de origen de referencia de directiva


El sitio de referencia es un identificador URI que puede mostrarse al usuario cuando la adquisición de la directiva de protección ha producido un error y que contiene información sobre cómo el usuario puede obtener permiso para tener acceso al contenido.
  
### <a name="setencryptedappdata-function"></a>Función SetEncryptedAppData
Establece los datos específicos de la aplicación que fueron cifrados.

Parámetros:  
* **value**: Datos específicos de la aplicación


Una aplicación puede especificar un diccionario de datos específicos de la aplicación cifrados por el servicio de protección. Estos datos cifrados son independientes del conjunto de datos firmado por SetSignedAppData.
  
### <a name="setsignedappdata-function"></a>Función SetSignedAppData
Establece los datos específicos de la aplicación que deben firmarse.

Parámetros:  
* **value**: Datos específicos de la aplicación


Una aplicación puede especificar un diccionario de datos específicos de la aplicación que se firmarán por el servicio de protección. Estos datos firmados son independientes del conjunto de datos cifrados por SetEncryptedAppData.
  
### <a name="protectiondescriptorbuilder-function"></a>~ ProtectionDescriptorBuilder (función)
_No se ha documentado todavía._
