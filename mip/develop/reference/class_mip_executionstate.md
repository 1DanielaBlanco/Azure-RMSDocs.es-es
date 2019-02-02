---
title: clase mip::ExecutionState
description: 'Documenta la clase MIP:: executionstate de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 86f06a8fab5600f0bc72f60272864a2ce2fab15e
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650721"
---
# <a name="class-mipexecutionstate"></a>clase mip::ExecutionState 
Interfaz a todos los estados necesarios para ejecutar el motor.
Los clientes solo deben llamar a los métodos para obtener el estado que se necesita. Por lo tanto, por razones de eficiencia, los clientes pueden querer implementar esta interfaz de manera que el estado correspondiente se calcule dinámicamente en lugar de calcular por adelantado.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public std::string GetNewLabelId() const  |  Obtiene el identificador de la etiqueta de confidencialidad que debe aplicarse en el documento.
public ActionSource GetNewLabelActionSource() const  |  Obtiene el origen de una nueva acción de etiqueta.
public std::string GetContentIdentifier() const  |  Obtiene el identificador de contenido que describe el documento. ejemplo de un archivo: [ruta\nombre_archivo] de ejemplo para un correo electrónico: [Asunto: remitente].
public ContentState GetContentState() const  |  Obtiene el estado del contenido mientras la aplicación interactúa con este.
public std::pair\<bool, std::string\> IsDowngradeJustified() const  |  La implementación tiene que pasar si se ha proporcionado o no una justificación para degradar una etiqueta existente.
public AssignmentMethod GetNewLabelAssignmentMethod() const  |  Obtiene el método de asignación de la nueva etiqueta.
public std::vector\<std::pair\<std::string, std::string\>\> GetNewLabelExtendedProperties() const  |  Devuelve las propiedades extendidas de la nueva etiqueta.
public std::vector\<std::pair\<std::string, std::string\>\> GetContentMetadata(const std::vector\<std::string\>& names, const std::vector\<std::string\>& namePrefixes) const  |  Obtiene los elementos de metadatos del contenido.
Public std:: shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor() const  |  Obtiene el descriptor de protección.
public ContentFormat GetContentFormat() const  |  Obtiene el formato del contenido.
public ActionType GetSupportedActions() const  |  Obtiene una enumeración enmascarada que describe todos los tipos de acción admitidos.
public virtual std::map\<std::string, std::shared_ptr\<ClassificationResult\>\> GetClassificationResults(const std::vector\<std::shared_ptr\<ClassificationRequest\>\> &) const  |  Devuelve un mapa de los resultados de la clasificación.
std:: Map virtual pública\<std:: String, std:: String\> GetAuditMetadata() const  |  Devuelve un mapa de pares clave-valor de auditoría específica de aplicación.
  
## <a name="members"></a>Miembros
  
### <a name="getnewlabelid-function"></a>Función GetNewLabelId
Obtiene el identificador de la etiqueta de confidencialidad que debe aplicarse en el documento.

  
**Devuelve**: Identificador de la etiqueta de sensibilidad se puede aplicar al contenido si existe otro vacía para quitar la etiqueta.
  
### <a name="getnewlabelactionsource-function"></a>Función GetNewLabelActionSource
Obtiene el origen de una nueva acción de etiqueta.

  
**Devuelve**: Origen de la acción.
  
### <a name="getcontentidentifier-function"></a>Función GetContentIdentifier
Obtiene el identificador de contenido que describe el documento. ejemplo de un archivo: [ruta\nombre_archivo] de ejemplo para un correo electrónico: [Asunto: remitente].

  
**Devuelve**: Identificador de contenido para aplicarse al contenido.
Este valor se usa en la auditoría como una descripción en lenguaje natural del contenido.
  
### <a name="getcontentstate-function"></a>Función GetContentState
Obtiene el estado del contenido mientras la aplicación interactúa con este.

  
**Devuelve**: Estado de los datos de contenido
  
### <a name="isdowngradejustified-function"></a>Función IsDowngradeJustified
La implementación tiene que pasar si se ha proporcionado o no una justificación para degradar una etiqueta existente.

  
**Devuelve**: Es True si degradación es justifiedalong con el false messageelse justificación 
  
**Consulte también**: [mip::JustifyAction](class_mip_justifyaction.md)
  
### <a name="getnewlabelassignmentmethod-function"></a>Función GetNewLabelAssignmentMethod
Obtiene el método de asignación de la nueva etiqueta.

  
**Devuelve**: El método de asignación STANDARD, PRIVILEGED, AUTO. 
  
**Vea también**: [MIP:: assignmentmethod](mip-enums-and-structs.md#assignmentmethod-enum)
  
### <a name="getnewlabelextendedproperties-function"></a>Función GetNewLabelExtendedProperties
Devuelve las propiedades extendidas de la nueva etiqueta.

  
**Devuelve**: Las propiedades extendidas que se aplica al contenido.
  
### <a name="getcontentmetadata-function"></a>Función GetContentMetadata
Obtiene los elementos de metadatos del contenido.

  
**Devuelve**: Los metadatos que se aplica al contenido. Cada elemento de metadatos es un par de nombre y valor.
  
### <a name="getprotectiondescriptor-function"></a>Función GetProtectionDescriptor
Obtiene el descriptor de protección.

  
**Devuelve**: El Descriptor de protección
  
### <a name="getcontentformat-function"></a>Función GetContentFormat
Obtiene el formato del contenido.

  
**Devuelve**: DE FORMA PREDETERMINADA, CORREO ELECTRÓNICO 
  
**Vea también**: [MIP:: contentformat](mip-enums-and-structs.md#contentformat-enum)
  
### <a name="getsupportedactions-function"></a>Función GetSupportedActions
Obtiene una enumeración enmascarada que describe todos los tipos de acción admitidos.

  
**Devuelve**: Una enumeración enmascarada que describe todos los tipos de acción admitida.
ActionType::Justify tiene que admitirse. Cuando un cambio de etiqueta y directiva necesita una justificación, siempre se devolverá una acción de justificación.
  
### <a name="getclassificationresults-function"></a>Función GetClassificationResults
Devuelve un mapa de los resultados de la clasificación.

Parámetros:  
* **classificationId**: lista de los identificadores de clasificación. 



  
**Devuelve**: Una lista de resultados de clasificación.
  
### <a name="getauditmetadata-function"></a>Función GetAuditMetadata
Devuelve un mapa de pares clave-valor de auditoría específica de aplicación.

  
**Devuelve**: Una lista de pares de clave-valor registrado de metadatos de auditoría específica de aplicación remitente: Id. de correo electrónico para el remitente, destinatarios: Representa una matriz JSON de los destinatarios de un correo electrónico LastModifiedBy: Id. de correo electrónico del usuario que modificó por última vez el contenido LastModifiedDate: Fecha de que última modificación del contenido