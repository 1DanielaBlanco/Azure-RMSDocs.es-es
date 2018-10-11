---
title: Clase mip UserRights
description: Referencia de la clase mip UserRights
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: c1ef7aaba00bf595d80f07f318aa5808f3a56409
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445128"
---
# <a name="class-mipuserrights"></a>clase mip::UserRights 
Un grupo de usuarios y los derechos asociados con ellos.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public UserRights(const std::vector<std::string>& users, const std::vector<std::string>& rights)  |  Constructor [UserRights](class_mip_userrights.md).
public const std::vector<std::string>& Users() const  |  Obtiene los usuarios asociados a un conjunto de derechos.
public const std::vector<std::string>& Rights() const  |  Obtiene los derechos asociados a un grupo de usuarios.
  
## <a name="members"></a>Miembros
  
### <a name="userrights"></a>UserRights
Constructor [UserRights](class_mip_userrights.md).

Parámetros:  
* **users**: grupo de usuarios que comparten los mismos derechos 


* **rights**: derechos compartidos por grupo de usuarios


  
### <a name="users"></a>Usuarios
Obtiene los usuarios asociados a un conjunto de derechos.

  
**Devuelve**: usuarios asociados a un conjunto de derechos
  
### <a name="rights"></a>Derechos
Obtiene los derechos asociados a un grupo de usuarios.

  
**Devuelve**: derechos asociados a un grupo de usuarios