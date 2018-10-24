---
title: clase mipFileHandler
description: Referencia de la clase mip FileHandler
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: efae18bdc10f8878f255f35c608a50482a29887b
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446131"
---
# <a name="class-mipfilehandler"></a>clase mip::FileHandler 
Interfaz a todas las funciones de control de archivos.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public void GetLabelAsync(const std::shared_ptr<void>& context)  |  Inicia la recuperación de la etiqueta de confidencialidad del archivo.
public void GetProtectionAsync(const std::shared_ptr<void>& context)  |  Inicia la recuperación de la directiva de protección desde el archivo.
 public void SetLabel(const std::string& labelId, const LabelingOptions& labelingOptions)  |  Establece la etiqueta de sensibilidad en el archivo.
 public void DeleteLabel(const LabelingOptions& labelingOptions)  |  Elimina la etiqueta de sensibilidad del archivo.
public void SetProtection(const std::shared_ptr<ProtectionDescriptor>& protectionDescriptor)  |  Establece los permisos basados en plantilla o personalizados (en función de protectionDescriptor->GetProtectionType) en el archivo.
 public void RemoveProtection()  |  Quita la protección del archivo. Si el archivo está etiquetado, la etiqueta se perderá.
public void CommitAsync(const std::string& outputFilePath, const std::shared_ptr<void>& context) | Escribe los cambios en el archivo especificado por el parámetro \|outputFilePath\ |  .
public void CommitAsync(const std::shared_ptr<Stream>& outputStream, const std::shared_ptr<void>& context) | Escribe los cambios en el flujo especificado por el parámetro \|outputStream\ |  .
 public void NotifyCommitSuccessful(const std::string& contentIdentifier)  |  Se llama cuando se confirman los cambios en el disco.
 public std::string GetOutputFileName()  |  Calcula el nombre y la extensión del archivo de salida basándose en el nombre del archivo original y en los cambios acumulados.
  
## <a name="members"></a>Miembros
  
### <a name="getlabelasync"></a>GetLabelAsync
Inicia la recuperación de la etiqueta de confidencialidad del archivo.
Se llamará a [FileHandler::Observer](class_mip_filehandler_observer.md) después de la realización correcta o de un error.

Parámetros:  
* **context**: contexto de cliente que se pasará de manera opaca hacia el observador.


  
### <a name="getprotectionasync"></a>GetProtectionAsync
Inicia la recuperación de la directiva de protección desde el archivo.
Se llamará a [FileHandler::Observer](class_mip_filehandler_observer.md) después de la realización correcta o de un error.

Parámetros:  
* **context**: contexto de cliente que se pasará de manera opaca hacia el observador.


  
### <a name="setlabel"></a>SetLabel
Establece la etiqueta de sensibilidad en el archivo.
Los cambios no se escribirán en el archivo hasta que se realice una llamada a CommitAsync. El método automático y con privilegios permite a la API reemplazar cualquier etiqueta existente y genera [JustificationRequiredError](class_mip_justificationrequirederror.md) al establecer la etiqueta; es necesario justificar la operación (mediante el parámetro labelingOptions).
  
### <a name="deletelabel"></a>DeleteLabel
Elimina la etiqueta de sensibilidad del archivo.
Los cambios no se escribirán en el archivo hasta que se realice una llamada a CommitAsync. El método automático y con privilegios permite a la API reemplazar cualquier etiqueta existente y genera [JustificationRequiredError](class_mip_justificationrequirederror.md) al establecer la etiqueta; es necesario justificar la operación (mediante el parámetro labelingOptions).
  
### <a name="setprotection"></a>SetProtection
Establece los permisos basados en plantilla o personalizados (en función de protectionDescriptor->GetProtectionType) en el archivo.
Los cambios no se escribirán en el archivo hasta que se realice una llamada a CommitAsync.
  
### <a name="removeprotection"></a>RemoveProtection
Quita la protección del archivo. Si el archivo está etiquetado, la etiqueta se perderá.
Los cambios no se escribirán en el archivo hasta que se realice una llamada a CommitAsync.
  
### <a name="commitasync"></a>CommitAsync
Escribe los cambios en el archivo especificado por el parámetro |outputFilePath|.
Se llamará a [FileHandler::Observer](class_mip_filehandler_observer.md) después de la realización correcta o de un error.
  
### <a name="commitasync"></a>CommitAsync
Escribe los cambios en el flujo especificado por el parámetro |outputStream|.
Se llamará a [FileHandler::Observer](class_mip_filehandler_observer.md) después de la realización correcta o de un error.
  
### <a name="notifycommitsuccessful"></a>NotifyCommitSuccessful
Se llama cuando se confirman los cambios en el disco.

Parámetros:  
* **contentIdentifier**: ejemplo de un archivo: "C:\mip-sdk-for-cpp\files\audit.docx" [ruta] ejemplo de un correo electrónico: "RE: Auditar design:user1@contoso.com" [Asunto:Remitente] 


Desencadena un evento de auditoría.
  
### <a name="getoutputfilename"></a>GetOutputFileName
Calcula el nombre y la extensión del archivo de salida basándose en el nombre del archivo original y en los cambios acumulados.