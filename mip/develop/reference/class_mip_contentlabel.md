---
title: clase mip ContentLabel
description: Referencia de la clase mip ContentLabel
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: c105f620ed2cd3d6f1427f2543784ea66ce2c4d7
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446029"
---
# <a name="class-mipcontentlabel"></a>clase mip::ContentLabel 
Abstracción para una etiqueta de Microsoft Information Protection que se aplica a un fragmento de contenido, normalmente un documento.
También contiene propiedades de una instancia de etiqueta aplicada específica.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public const std::string& GetCreationTime() const  |  Obtiene la hora de creación de la solicitud.
 public AssignmentMethod GetAssignmentMethod() const  |  Obtiene el método de asignación de la etiqueta.
public const std::vector<std::pair<std::string, std::string>>& GetExtendedProperties() const  |  Obtiene propiedades extendidas.
 public bool IsProtectionAppliedFromLabel() const  |  Obtiene si la etiqueta ha aplicado protección o no.
public std::shared_ptr<Label> GetLabel() const  |  Obtiene el objeto de la etiqueta real que se aplica en el contenido.
  
## <a name="members"></a>Miembros
  
### <a name="getcreationtime"></a>GetCreationTime
Obtiene la hora de creación de la solicitud.

  
**Devuelve**: hora de creación como una cadena GMT.
  
### <a name="getassignmentmethod"></a>GetAssignmentMethod
Obtiene el método de asignación de la etiqueta.

  
**Devuelve**: AssignmentMethod STANDARD | PRIVILEGED | AUTO. 
  
**Consulte también**: mip::AssignmentMethod
  
### <a name="getextendedproperties"></a>GetExtendedProperties
Obtiene propiedades extendidas.

  
**Devuelve**: propiedades extendidas.
  
### <a name="isprotectionappliedfromlabel"></a>IsProtectionAppliedFromLabel
Obtiene si la etiqueta ha aplicado protección o no.

  
**Devuelve**: “true” si hay una protección de plantilla por esta etiqueta; de lo contrario, “false”.
  
### <a name="label"></a>Etiqueta
Obtiene el objeto de la etiqueta real que se aplica en el contenido.

  
**Devuelve**: el objeto de la etiqueta que se aplica en el contenido. 
  
**Consulte también**: [mip::Label](class_mip_label.md)