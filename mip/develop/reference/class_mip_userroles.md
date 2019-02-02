---
title: clase mip::UserRoles
description: 'Documenta la clase MIP:: UserRoles de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 1a060652ea61ed452867bb67d281c9531f4e1b98
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651520"
---
# <a name="class-mipuserroles"></a>clase mip::UserRoles 
Un grupo de usuarios y los roles asociados a estos.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
roles de usuario público (const std:: vector\<std:: String\>& los usuarios, const std:: vector\<std:: String\>& roles)  |  Constructor [UserRoles](class_mip_userroles.md).
Public const std:: vector\<std:: String\>& Users() const  |  Obtiene los usuarios asociados a un conjunto de roles.
Public const std:: vector\<std:: String\>& Roles() const  |  Obtiene los roles asociados a un grupo de usuarios.
  
## <a name="members"></a>Miembros
  
### <a name="userroles-function"></a>Función UserRoles
Constructor [UserRoles](class_mip_userroles.md).

Parámetros:  
* **los usuarios**: Grupo de usuarios que comparten los mismos roles 


* **roles**: Compartidos por grupo de usuarios de roles


  
### <a name="users-function"></a>Función de los usuarios
Obtiene los usuarios asociados a un conjunto de roles.

  
**Devuelve**: Usuarios asociados a un conjunto de roles
  
### <a name="roles-function"></a>Función de roles
Obtiene los roles asociados a un grupo de usuarios.

  
**Devuelve**: Roles asociados a un grupo de usuarios