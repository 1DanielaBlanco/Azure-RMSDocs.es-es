---
title: clase mip::ClassificationResult
description: Documenta la clase mip::classificationresult de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 28b174fe65de5980fb1922cfb4c3e5cee7cab1d8
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650755"
---
# <a name="class-mipclassificationresult"></a>clase mip::ClassificationResult 
Clase que contiene el resultado de una llamada de clasificación en el estado de ejecución.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public std::string GetId() const  |  Obtiene el identificador de la directiva de clasificación.
public int GetCount() const  |  Obtiene el recuento de instancias.
public int GetConfidenceLevel() const  |  Obtiene la confianza en el resultado.
  
## <a name="members"></a>Miembros
  
### <a name="getid-function"></a>GetId (función)
Obtiene el identificador de la directiva de clasificación.

  
**Devuelve**: Id. de la directiva de clasificación.
  
### <a name="getcount-function"></a>GetCount (función)
Obtiene el recuento de instancias.

  
**Devuelve**: El recuento de instancias.
  
### <a name="getconfidencelevel-function"></a>Función GetConfidenceLevel
Obtiene la confianza en el resultado.