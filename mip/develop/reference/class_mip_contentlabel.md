---
title: clase mip::ContentLabel
description: 'Documenta la clase MIP:: contentlabel de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 6ef95a20be13123eec6ad17a9eef26f321e36cf8
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56254669"
---
# <a name="class-mipcontentlabel"></a>clase mip::ContentLabel 
Abstracción para una etiqueta de Microsoft Information Protection que se aplica a un fragmento de contenido, normalmente un documento.
También contiene propiedades de una instancia de etiqueta aplicada específica.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const std::string& GetCreationTime() const  |  Obtiene la hora de creación de la solicitud.
public AssignmentMethod GetAssignmentMethod() const  |  Obtiene el método de asignación de la etiqueta.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetExtendedProperties() const  |  Obtiene propiedades extendidas.
public bool IsProtectionAppliedFromLabel() const  |  Obtiene si la etiqueta ha aplicado protección o no.
Public std:: shared_ptr\<etiqueta\> GetLabel() const  |  Obtiene el objeto de la etiqueta real que se aplica en el contenido.
  
## <a name="members"></a>Miembros
  
### <a name="getcreationtime-function"></a>GetCreationTime (función)
Obtiene la hora de creación de la solicitud.

  
**Devuelve**: Hora de creación como una cadena GMT.
  
### <a name="getassignmentmethod-function"></a>Función GetAssignmentMethod
Obtiene el método de asignación de la etiqueta.

  
**Devuelve**: AssignmentMethod STANDARD | PRIVILEGED | AUTO. 
  
**Vea también**: [MIP:: assignmentmethod](mip-enums-and-structs.md#assignmentmethod-enum)
  
### <a name="getextendedproperties-function"></a>Función GetExtendedProperties
Obtiene propiedades extendidas.

  
**Devuelve**: Propiedades extendidas.
  
### <a name="isprotectionappliedfromlabel-function"></a>Función IsProtectionAppliedFromLabel
Obtiene si la etiqueta ha aplicado protección o no.

  
**Devuelve**: True si hay protección de la plantilla y estaba por esta etiqueta, de lo contrario, false.
  
### <a name="getlabel-function"></a>GetLabel (función)
Obtiene el objeto de la etiqueta real que se aplica en el contenido.

  
**Devuelve**: El objeto de etiqueta que se aplica en el contenido. 
  
**Consulte también**: [mip::Label](class_mip_label.md)
