---
title: class mip::FileExecutionState
description: Documenta la clase mip::fileexecutionstate de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 380e5f6732a2662d83b9bb37af5763ef30ffa3bf
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259225"
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
