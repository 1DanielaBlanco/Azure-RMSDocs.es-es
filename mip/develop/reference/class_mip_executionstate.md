---
title: Clase mip ExecutionState
description: Referencia de la clase mip ExecutionState
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 976bca60f3f494a0fbf196e6512b00bdcdd63992
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446318"
---
# <a name="class-mipexecutionstate"></a>clase mip::ExecutionState 
Interfaz a todos los estados necesarios para ejecutar el motor.
Los clientes solo deben llamar a los métodos para obtener el estado que se necesita. Por lo tanto, por razones de eficiencia, los clientes pueden querer implementar esta interfaz de manera que el estado correspondiente se calcule dinámicamente en lugar de calcular por adelantado.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public std::string GetNewLabelId() const  |  Obtiene el identificador de la etiqueta de confidencialidad que debe aplicarse en el documento.
 public ActionSource GetNewLabelActionSource() const  |  Obtiene el origen de una nueva acción de etiqueta.
 public std::string GetContentIdentifier() const  |  Obtiene el identificador de contenido que describe el documento. Ejemplo de un archivo: [ruta]; ejemplo de un correo electrónico: [Asunto:Remitente].
 public ContentState GetContentState() const  |  Obtiene el estado del contenido mientras la aplicación interactúa con este.
public std::pair<bool, std::string> IsDowngradeJustified() const  |  La implementación tiene que pasar si se ha proporcionado o no una justificación para degradar una etiqueta existente.
 public AssignmentMethod GetNewLabelAssignmentMethod() const  |  Obtiene el método de asignación de la nueva etiqueta.
public std::vector<std::pair<std::string, std::string>> GetNewLabelExtendedProperties() const  |  Devuelve las propiedades extendidas de la nueva etiqueta.
public std::vector<std::pair<std::string, std::string>> GetContentMetadata(const std::vector<std::string>& names, const std::vector<std::string>& namePrefixes) const  |  Obtiene los elementos de metadatos del contenido.
public std::shared_ptr<ProtectionDescriptor> GetProtectionDescriptor() const  |  Obtiene el descriptor de protección.
 public ContentFormat GetContentFormat() const  |  Obtiene el formato del contenido.
 public ActionType GetSupportedActions() const  |  Obtiene una enumeración enmascarada que describe todos los tipos de acción admitidos.
public virtual std::map<std::string, std::shared_ptr<ClassificationResult>> GetClassificationResults(const std::vector<std::string> &) const  |  Devuelve un mapa de los resultados de la clasificación.
  
## <a name="members"></a>Miembros
  
### <a name="getnewlabelid"></a>GetNewLabelId
Obtiene el identificador de la etiqueta de confidencialidad que debe aplicarse en el documento.

  
**Devuelve**: identificador de etiqueta de confidencialidad que se aplicará al contenido, si existe; de lo contrario, está vacío para quitar la etiqueta.
  
### <a name="getnewlabelactionsource"></a>GetNewLabelActionSource
Obtiene el origen de una nueva acción de etiqueta.

  
**Devuelve**: origen de la acción.
  
### <a name="getcontentidentifier"></a>GetContentIdentifier
Obtiene el identificador de contenido que describe el documento. Ejemplo de un archivo: [ruta]; ejemplo de un correo electrónico: [Asunto:Remitente].

  
**Devuelve**: identificador de contenido que se aplicará al contenido.
Este valor se usa en la auditoría como una descripción en lenguaje natural del contenido.
  
### <a name="getcontentstate"></a>GetContentState
Obtiene el estado del contenido mientras la aplicación interactúa con este.

  
**Devuelve**: estado de los datos de contenido.
  
### <a name="isdowngradejustified"></a>IsDowngradeJustified
La implementación tiene que pasar si se ha proporcionado o no una justificación para degradar una etiqueta existente.

  
**Devuelve**: “true” si la degradación está justificada, además del mensaje de justificación; de lo contrario, “false”. 
  
**Consulte también**: [mip::JustifyAction](class_mip_justifyaction.md)
  
### <a name="getnewlabelassignmentmethod"></a>GetNewLabelAssignmentMethod
Obtiene el método de asignación de la nueva etiqueta.

  
**Devuelve**: el método de asignación STANDARD, PRIVILEGED, AUTO. 
  
**Consulte también**: mip::AssignmentMethod
  
### <a name="getnewlabelextendedproperties"></a>GetNewLabelExtendedProperties
Devuelve las propiedades extendidas de la nueva etiqueta.

  
**Devuelve**: las propiedades extendidas aplicadas al contenido.
  
### <a name="getcontentmetadata"></a>GetContentMetadata
Obtiene los elementos de metadatos del contenido.

  
**Devuelve**: los metadatos aplicados al contenido. Cada elemento de metadatos es un par de nombre y valor.
  
### <a name="protectiondescriptor"></a>ProtectionDescriptor
Obtiene el descriptor de protección.

  
**Devuelve**: el descriptor de protección.
  
### <a name="getcontentformat"></a>GetContentFormat
Obtiene el formato del contenido.

  
**Devuelve**: de forma predeterminada, el correo electrónico 
  
**Vea también**: mip::ContentFormat
  
### <a name="actiontype"></a>ActionType
Obtiene una enumeración enmascarada que describe todos los tipos de acción admitidos.

  
**Devuelve**: una enumeración enmascarada que describe todos los tipos de acción admitidos.
ActionType::Justify tiene que admitirse. Cuando un cambio de etiqueta y directiva necesita una justificación, siempre se devolverá una acción de justificación.
  
### <a name="classificationresult"></a>ClassificationResult
Devuelve un mapa de los resultados de la clasificación.

Parámetros:  
* **classificationId**: lista de los identificadores de clasificación. 



  
**Devuelve**: una lista de resultados de clasificación.