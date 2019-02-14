---
title: clase mip::FileHandler
description: 'Documenta la clase MIP:: filehandler de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 664478f074334196b78b5583867224e1a9f482d2
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56253074"
---
# <a name="class-mipfilehandler"></a>clase mip::FileHandler 
Interfaz a todas las funciones de control de archivos.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
Public std:: shared_ptr\<ContentLabel\> GetLabel()  |  Inicia la recuperación de la etiqueta de confidencialidad del archivo.
public std::shared_ptr\<ProtectionHandler\> GetProtection()  |  Inicia la recuperación de la directiva de protección desde el archivo.
pública ClassifyAsync void (const std:: shared_ptr\<void\>& contexto)  |  Ejecuta las reglas en el controlador y devuelve la lista de acciones que se ejecutan.
public void SetLabel(const std::string& labelId, const LabelingOptions& labelingOptions)  |  Establece la etiqueta de sensibilidad en el archivo.
public void DeleteLabel(const LabelingOptions& labelingOptions)  |  Elimina la etiqueta de sensibilidad del archivo.
pública SetProtection void (const std:: shared_ptr\<ProtectionDescriptor\>& protectionDescriptor)  |  Establece los permisos basados en plantilla o personalizados (en función de protectionDescriptor->GetProtectionType) en el archivo.
pública SetProtection void (const std:: vector\<uint8_t\>& serializedPublishingLicense, const std:: vector\<uint8_t\>& serializedProtectionInfo)  |  Establece permisos personalizados o basados en plantillas (según serializedPublishingLicense y serializedProtectionInfo) en el archivo.
public void RemoveProtection()  |  Quita la protección del archivo. Si el archivo está etiquetado, la etiqueta se perderá.
pública CommitAsync void (const std:: String & outputFilePath, const std:: shared_ptr\<void\>& contexto) | Escribe los cambios en el archivo especificado por el parámetro \|outputFilePath\ |  parámetro.
pública CommitAsync void (const std:: shared_ptr\<Stream\>& outputStream, const std:: shared_ptr\<void\>& contexto) | Escribe los cambios en el flujo especificado por el parámetro \|outputStream\ |  parámetro.
pública GetDecryptedTemporaryFileAsync void (const std:: shared_ptr\<void\>& contexto)  |  Devuelve una ruta de acceso a un archivo temporal (que se eliminarán si es posible) - que representa el contenido descifrado.
public void NotifyCommitSuccessful(const std::string& contentIdentifier)  |  Se llama cuando se confirman los cambios en el disco.
public std::string GetOutputFileName()  |  Calcula el nombre y la extensión del archivo de salida basándose en el nombre del archivo original y en los cambios acumulados.
  
## <a name="members"></a>Miembros
  
### <a name="getlabel-function"></a>GetLabel (función)
Inicia la recuperación de la etiqueta de confidencialidad del archivo.
  
### <a name="getprotection-function"></a>Función GetProtection
Inicia la recuperación de la directiva de protección desde el archivo.
  
### <a name="classifyasync-function"></a>Función ClassifyAsync
Ejecuta las reglas en el controlador y devuelve la lista de acciones que se ejecutan.

  
**Devuelve**: Lista de acciones que deben aplicarse en el contenido.
  
### <a name="setlabel-function"></a>Función SetLabel
Establece la etiqueta de sensibilidad en el archivo.
Los cambios no se escribirán en el archivo hasta que se realice una llamada a CommitAsync. El método automático y con privilegios permite a la API reemplazar cualquier etiqueta existente y genera [JustificationRequiredError](class_mip_justificationrequirederror.md) al establecer la etiqueta; es necesario justificar la operación (mediante el parámetro labelingOptions).
  
### <a name="deletelabel-function"></a>Función DeleteLabel
Elimina la etiqueta de sensibilidad del archivo.
Los cambios no se escribirán en el archivo hasta que se realice una llamada a CommitAsync. El método automático y con privilegios permite a la API reemplazar cualquier etiqueta existente y genera [JustificationRequiredError](class_mip_justificationrequirederror.md) al establecer la etiqueta; es necesario justificar la operación (mediante el parámetro labelingOptions).
  
### <a name="setprotection-function"></a>Función SetProtection
Establece los permisos basados en plantilla o personalizados (en función de protectionDescriptor->GetProtectionType) en el archivo.
Los cambios no se escribirán en el archivo hasta que se realice una llamada a CommitAsync.
  
### <a name="setprotection-function"></a>Función SetProtection
Establece permisos personalizados o basados en plantillas (según serializedPublishingLicense y serializedProtectionInfo) en el archivo.
Los cambios no se escribirán en el archivo hasta que se realice una llamada a CommitAsync.
  
### <a name="removeprotection-function"></a>Función RemoveProtection
Quita la protección del archivo. Si el archivo está etiquetado, la etiqueta se perderá.
Los cambios no se escribirán en el archivo hasta que se realice una llamada a CommitAsync.
  
### <a name="commitasync-function"></a>CommitAsync (función)
Escribe los cambios en el archivo especificado por el parámetro |outputFilePath|.
Se llamará a [FileHandler::Observer](class_mip_filehandler_observer.md) después de la realización correcta o de un error.
  
### <a name="commitasync-function"></a>CommitAsync (función)
Escribe los cambios en el flujo especificado por el parámetro |outputStream|.
Se llamará a [FileHandler::Observer](class_mip_filehandler_observer.md) después de la realización correcta o de un error.
  
### <a name="getdecryptedtemporaryfileasync-function"></a>Función GetDecryptedTemporaryFileAsync
Devuelve una ruta de acceso a un archivo temporal (que se eliminarán si es posible) - que representa el contenido descifrado.
Se llamará a [FileHandler::Observer](class_mip_filehandler_observer.md) después de la realización correcta o de un error.
  
### <a name="notifycommitsuccessful-function"></a>Función NotifyCommitSuccessful
Se llama cuando se confirman los cambios en el disco.

Parámetros:  
* **contentIdentifier**: ejemplo de un archivo: Ejemplo de "C:\mip-sdk-for-cpp\files\audit.docx" [ruta\nombre_archivo] para un correo electrónico: "RE: Auditoría design:user1@contoso.com"[Asunto: remitente] 


Desencadena un evento de auditoría.
  
### <a name="getoutputfilename-function"></a>Función GetOutputFileName
Calcula el nombre y la extensión del archivo de salida basándose en el nombre del archivo original y en los cambios acumulados.
