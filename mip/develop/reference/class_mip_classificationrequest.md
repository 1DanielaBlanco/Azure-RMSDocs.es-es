---
title: clase mip::ClassificationRequest
description: Documenta la clase mip::classificationrequest de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: a7350961af4c2e5d63211840382ee7a0b701f1c4
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55652037"
---
# <a name="class-mipclassificationrequest"></a>clase mip::ClassificationRequest 
Clase que contiene la solicitud de una llamada de clasificación en el estado de ejecución.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
Public std:: String GetClassificationId() const  |  Obtiene el identificador de la directiva de clasificación.
Public std:: String GetRulePackageId() const  |  Obtiene el identificador del paquete de la regla.
  
## <a name="members"></a>Miembros
  
### <a name="getclassificationid-function"></a>Función GetClassificationId
Obtiene el identificador de la directiva de clasificación.

  
**Devuelve**: Id. de la directiva de clasificación.
  
### <a name="getrulepackageid-function"></a>Función GetRulePackageId
Obtiene el identificador del paquete de la regla.

  
**Devuelve**: Id. de paquete de la regla. clasificaciones creados previamente se establecerá en un guid vacío.