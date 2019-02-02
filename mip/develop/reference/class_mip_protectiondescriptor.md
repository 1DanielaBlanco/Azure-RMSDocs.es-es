---
title: clase mip::ProtectionDescriptor
description: Documenta la clase mip::protectiondescriptor de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: f3bf856982f3e5b4c060a83fe1e822866fb1808b
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651724"
---
# <a name="class-mipprotectiondescriptor"></a>clase mip::ProtectionDescriptor 
Descripción de la protección asociada a un contenido.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public ProtectionType GetProtectionType() const  |  Obtiene el tipo de protección, independientemente de que se haya creado a partir de la plantilla del SDK de protección o no.
public std::string GetOwner() const  |  Obtiene el propietario de la protección.
public std::string GetName() const  |  Obtiene el nombre de la protección.
public std::string GetDescription()  |  Obtiene la descripción de la protección.
public std::string GetTemplateId() const  |  Obtiene el identificador de la plantilla de protección, si corresponde.
public std::string GetLabelId() const  |  Obtiene el identificador de etiqueta, si corresponde.
public std::vector\<UserRights\> GetUserRights() const  |  Obtiene una colección de asignaciones de usuarios a derechos.
public std::vector\<UserRoles\> GetUserRoles() const  |  Obtiene una colección de asignaciones de usuarios a roles
public bool DoesContentExpire() const  |  Comprueba si el contenido tiene un tiempo de expiración o no.
public std::chrono::time_point\<std::chrono::system_clock\> GetContentValidUntil() const  |  Obtiene la hora de expiración de la protección.
public bool DoesAllowOfflineAccess() const  |  Obtiene si la directiva de protección permite o no el acceso a contenido sin conexión.
public std::string GetReferrer() const  |  Obtiene la dirección del origen de referencia de protección.
Public std:: Map\<std:: String, std:: String\> GetEncryptedAppData() const  |  Obtiene datos específicos de la aplicación que se cifraron.
Public std:: Map\<std:: String, std:: String\> GetSignedAppData() const  |  Obtiene datos específicos de la aplicación que se firmaron.
  
## <a name="members"></a>Miembros
  
### <a name="getprotectiontype-function"></a>Función GetProtectionType
Obtiene el tipo de protección, independientemente de que se haya creado a partir de la plantilla del SDK de protección o no.

  
**Devuelve**: Tipo de protección
  
### <a name="getowner-function"></a>GetOwner (función)
Obtiene el propietario de la protección.

  
**Devuelve**: Propietario de protección
  
### <a name="getname-function"></a>Función GetName
Obtiene el nombre de la protección.

  
**Devuelve**: Nombre de la protección
  
### <a name="getdescription-function"></a>GetDescription (función)
Obtiene la descripción de la protección.

  
**Devuelve**: Descripción de la protección
  
### <a name="gettemplateid-function"></a>Función GetTemplateId
Obtiene el identificador de la plantilla de protección, si corresponde.

  
**Devuelve**: Id. de plantilla
  
### <a name="getlabelid-function"></a>Función GetLabelId
Obtiene el identificador de etiqueta, si corresponde.

  
**Devuelve**: [Etiqueta](class_mip_label.md) Id. de esta propiedad solo se rellenarán en ProtectionDescriptors para preexistente contenido protegido. Es un campo rellenado por el servidor en el momento en que se usa el contenido protegido.
  
### <a name="getuserrights-function"></a>Función GetUserRights
Obtiene una colección de asignaciones de usuarios a derechos.

  
**Devuelve**: Colección de asignaciones de usuarios a derechos el valor de la [UserRights](class_mip_userrights.md) propiedad estará vacía si el usuario actual no tiene acceso a esta información (es decir, si el usuario no es el propietario y no tiene el derecho VIEWRIGHTSDATA).
  
### <a name="getuserroles-function"></a>Función GetUserRoles
Obtiene una colección de asignaciones de usuarios a roles

  
**Devuelve**: Colección de asignaciones de usuarios a roles
  
### <a name="doescontentexpire-function"></a>Función DoesContentExpire
Comprueba si el contenido tiene un tiempo de expiración o no.

  
**Devuelve**: True si el contenido puede expirar, otro false
  
### <a name="getcontentvaliduntil-function"></a>Función GetContentValidUntil
Obtiene la hora de expiración de la protección.

  
**Devuelve**: Hora de expiración de protección
  
### <a name="doesallowofflineaccess-function"></a>Función DoesAllowOfflineAccess
Obtiene si la directiva de protección permite o no el acceso a contenido sin conexión.

  
**Devuelve**: Si la protección permite el acceso de contenido sin conexión o no (valor predeterminado = true)
  
### <a name="getreferrer-function"></a>Función GetReferrer
Obtiene la dirección del origen de referencia de protección.

  
**Devuelve**: Dirección de origen de referencia de protección del origen de referencia es un URI que es el que se puede mostrar al usuario si no pueden desproteger el contenido. Contiene información sobre cómo el usuario puede obtener el permiso para acceder al contenido.
  
### <a name="getencryptedappdata-function"></a>Función GetEncryptedAppData
Obtiene datos específicos de la aplicación que se cifraron.

  
**Devuelve**: Datos específicos de la aplicación A [ProtectionHandler](class_mip_protectionhandler.md) puede contener un diccionario de datos específicos de la aplicación que se cifraron con el servicio de protección. Estos datos cifrados son independientes de los datos firmados accesibles mediante [ProtectionDescriptor::GetSignedAppData](class_mip_protectiondescriptor.md#getappsigneddata-function).
  
### <a name="getsignedappdata-function"></a>Función GetSignedAppData
Obtiene datos específicos de la aplicación que se firmaron.

  
**Devuelve**: Datos específicos de la aplicación A [ProtectionHandler](class_mip_protectionhandler.md) puede contener un diccionario de datos específicos de la aplicación que se ha firmado el servicio de protección. Estos datos firmados son independientes de los datos cifrados accesibles mediante [ProtectionDescriptor::GetEncryptedAppData](class_mip_protectiondescriptor.md#getencryptedappdata-function)