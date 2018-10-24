---
title: Clase mip ProtectionDescriptor
description: Referencia de la clase mip ProtectionDescriptor
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: e723041af1eec7be7a839bf36f6d3db67b32447f
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446556"
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
public std::vector<UserRights> GetUserRights() const  |  Obtiene una colección de asignaciones de usuarios a derechos.
public std::vector<UserRoles> GetUserRoles() const  |  Obtiene una colección de asignaciones de usuarios a roles
public std::chrono::time_point<std::chrono::system_clock> GetContentValidUntil() const  |  Obtiene la hora de expiración de la protección.
 public bool DoesAllowOfflineAccess() const  |  Obtiene si la directiva de protección permite o no el acceso a contenido sin conexión.
 public std::string GetReferrer() const  |  Obtiene la dirección del origen de referencia de protección.
public std::map<std::string, std::string> GetEncryptedAppData() const  |  Obtiene datos específicos de la aplicación que se cifraron.
public std::map<std::string, std::string> GetSignedAppData() const  |  Obtiene datos específicos de la aplicación que se firmaron.
  
## <a name="members"></a>Miembros
  
### <a name="protectiontype"></a>ProtectionType
Obtiene el tipo de protección, independientemente de que se haya creado a partir de la plantilla del SDK de protección o no.

  
**Devuelve**: tipo de protección
  
### <a name="getowner"></a>GetOwner
Obtiene el propietario de la protección.

  
**Devuelve**: propietario de la protección.
  
### <a name="getname"></a>GetName
Obtiene el nombre de la protección.

  
**Devuelve**: nombre de la protección.
  
### <a name="getdescription"></a>GetDescription
Obtiene la descripción de la protección.

  
**Devuelve**: descripción de la protección.
  
### <a name="gettemplateid"></a>GetTemplateId
Obtiene el identificador de la plantilla de protección, si corresponde.

  
**Devuelve**: identificador de plantilla.
  
### <a name="getlabelid"></a>GetLabelId
Obtiene el identificador de etiqueta, si corresponde.

  
**Devuelve**: identificador de [etiqueta](class_mip_label.md). Esta propiedad solo se rellenará en ProtectionDescriptors para contenido protegido preexistente. Es un campo rellenado por el servidor en el momento en que se usa el contenido protegido.
  
### <a name="userrights"></a>UserRights
Obtiene una colección de asignaciones de usuarios a derechos.

  
**Devuelve**: colección de asignaciones de usuarios a derechos. El valor de la propiedad [UserRights](class_mip_userrights.md) estará vacío si el usuario actual no tiene acceso a la información de derechos del usuario (es decir, no es el propietario y no tiene el derecho VIEWRIGHTSDATA).
  
### <a name="userroles"></a>UserRoles
Obtiene una colección de asignaciones de usuarios a roles

  
**Devuelve**: colección de asignaciones de usuarios a roles
  
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
Obtiene la hora de expiración de la protección.

  
**Devuelve**: hora de expiración de la protección.
  
### <a name="doesallowofflineaccess"></a>DoesAllowOfflineAccess
Obtiene si la directiva de protección permite o no el acceso a contenido sin conexión.

  
**Devuelve**: si la protección permite que el contenido sin conexión tenga acceso o no (valor predeterminado = true).
  
### <a name="getreferrer"></a>GetReferrer
Obtiene la dirección del origen de referencia de protección.

  
**Devuelve**: dirección del origen de referencia de protección. El origen de referencia es un URI que puede mostrarse al usuario si este no puede desproteger el contenido. Contiene información sobre cómo el usuario puede obtener el permiso para acceder al contenido.
  
### <a name="getencryptedappdata"></a>GetEncryptedAppData
Obtiene datos específicos de la aplicación que se cifraron.

  
**Devuelve**: datos específicos de la aplicación. Un [ProtectionHandler](class_mip_protectionhandler.md) puede contener un diccionario de datos específicos de la aplicación cifrados por el servicio de protección. Estos datos cifrados son independientes de los datos firmados accesibles mediante [ProtectionDescriptor::GetSignedAppData](class_mip_protectiondescriptor.md#getsignedappdata).
  
### <a name="getsignedappdata"></a>GetSignedAppData
Obtiene datos específicos de la aplicación que se firmaron.

  
**Devuelve**: datos específicos de la aplicación. Un [ProtectionHandler](class_mip_protectionhandler.md) puede contener un diccionario de datos específicos de la aplicación firmados por el servicio de protección. Estos datos firmados son independientes de los datos cifrados accesibles mediante [ProtectionDescriptor::GetEncryptedAppData](class_mip_protectiondescriptor.md#getencryptedappdata)