---
title: Clase mip UserRoles
description: Referencia de la clase mip UserRoles
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 1cc1da6f443fa22095f216bb2ec2f0e51e75bf78
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445264"
---
# <a name="class-mipuserroles"></a>clase mip::UserRoles 
Un grupo de usuarios y los roles asociados con ellos.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public UserRoles(const std::vector<std::string>& users, const std::vector<std::string>& roles)  |  Constructor [UserRoles](class_mip_userroles.md).
public const std::vector<std::string>& Users() const  |  Obtiene los usuarios asociados a un conjunto de roles.
public const std::vector<std::string>& Roles() const  |  Obtiene los roles asociados a un grupo de usuarios.
  
## <a name="members"></a>Miembros
  
### <a name="userroles"></a>UserRoles
Constructor [UserRoles](class_mip_userroles.md).

Parámetros:  
* **users**: grupo de usuarios que comparten los mismos roles 


* **roles**: roles compartidos por un grupo de usuarios


  
### <a name="users"></a>Usuarios
Obtiene los usuarios asociados a un conjunto de roles.

  
**Devuelve**: usuarios asociados a un conjunto de roles
  
### <a name="roles"></a>Roles
Obtiene los roles asociados a un grupo de usuarios.

  
**Devuelve**: roles asociados a un grupo de usuarios