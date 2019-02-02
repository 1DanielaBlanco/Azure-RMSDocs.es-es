---
title: class mip::FileExecutionState
description: Documenta la clase mip::fileexecutionstate de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 08a9064645f0ffb3ffbaa72f00db26c5b29d3643
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55652343"
---
# <a name="class-mipfileexecutionstate"></a>class mip::FileExecutionState 
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
std:: Map virtual pública\<std:: String, std:: shared_ptr\<ClassificationResult\> \> GetClassificationResults (const std:: shared_ptr\<FileHandler\> &, const std :: vector\<std:: shared_ptr\<ClassificationRequest\> \> &) const  |  Devuelve un mapa de los resultados de la clasificación.
public virtual std::vector\<uint8_t\> GetSerializedProtectionInfo() const  |  Devuelve un búfer con el plan serializado
  
## <a name="members"></a>Miembros
  
### <a name="getclassificationresults-function"></a>Función GetClassificationResults
Devuelve un mapa de los resultados de la clasificación.

Parámetros:  
* **fileHandler**:-el controlador de archivo del archivo usado 


* **classificationIds**: una lista de identificadores de clasificación. 



  
**Devuelve**: Una lista de resultados de clasificación.
  
### <a name="getserializedprotectioninfo-function"></a>Función GetSerializedProtectionInfo
Devuelve un búfer con el plan serializado

  
**Devuelve**: Un búfer con el plan serializado