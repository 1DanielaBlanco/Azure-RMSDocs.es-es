---
title: clase mip::UserRights
description: 'Documenta la clase MIP:: userrights de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 3e3abd2045b0e66ee8c2b307d555bf860e489625
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650619"
---
# <a name="class-mipuserrights"></a>clase mip::UserRights 
Un grupo de usuarios y los derechos asociados a estos.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
UserRights públicas (const std:: vector\<std:: String\>& los usuarios, const std:: vector\<std:: String\>& rights)  |  Constructor [UserRights](class_mip_userrights.md).
Public const std:: vector\<std:: String\>& Users() const  |  Obtiene los usuarios asociados a un conjunto de derechos.
Public const std:: vector\<std:: String\>& Rights() const  |  Obtiene los derechos asociados a un grupo de usuarios.
  
## <a name="members"></a>Miembros
  
### <a name="userrights-function"></a>Función UserRights
Constructor [UserRights](class_mip_userrights.md).

Parámetros:  
* **los usuarios**: Grupo de usuarios que comparten los mismos derechos 


* **rights**: Derechos compartidos por grupo de usuarios


  
### <a name="users-function"></a>Función de los usuarios
Obtiene los usuarios asociados a un conjunto de derechos.

  
**Devuelve**: Usuarios asociados a un conjunto de derechos
  
### <a name="rights-function"></a>Función de derechos
Obtiene los derechos asociados a un grupo de usuarios.

  
**Devuelve**: Derechos asociados a un grupo de usuarios