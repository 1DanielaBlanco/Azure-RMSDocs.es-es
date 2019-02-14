---
title: Funciones
description: Funciones
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.date: 01/28/2019
ms.author: bryanla
ms.openlocfilehash: 614e4bdd589e8c7ad3efdbf9be2f807e6d4ec43a
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56254193"
---
# <a name="functions"></a>Funciones

## <a name="summary"></a>Resumen

| Ámbito de espacio de nombres a las funciones   | Descripciones                                |
|--------------------------------|---------------------------------------------|
**Namespace `mip` :** |
Public std:: String GetAssignmentMethodString (método AssignmentMethod)       |  Convierte una cadena de descripción AssignmentMethod enum.
público estático std:: String GetActionSourceString (ActionSource actionSource)       |  Obtiene el nombre de origen de la acción.
público estático std:: String GetContentStateString (mip::ContentState estado)       |  Obtiene el nombre del estado del contenido.
public const std::string& GetCustomSettingPolicyDataName()       |  Nombre de la configuración para especificar explícitamente los datos de la directiva.
public const std::string& GetCustomSettingExportPolicyFileName()       |  Nombre de la configuración para especificar explícitamente la ruta del archivo a la que exportar datos de la directiva SCC.
public const std::string& GetCustomSettingSensitivityTypesDataName()       |  Nombre de la configuración para especificar explícitamente los datos de sensibilidad.
public const std::string& GetCustomSettingPolicyDataFile()       |  Nombre de la configuración para especificar explícitamente la ruta del archivo de datos de la directiva.
public const std::string& GetCustomSettingSensitivityTypesDataFile()       |  Nombre de la configuración para especificar explícitamente la sensibilidad de los tipos de ruta de acceso de archivo de datos.
pública MIP_API a void __CDECL ReleaseAllResources()       |  Libera todos los recursos (subprocesos, etc.) antes de un apagado.
Public std:: shared_ptr MIP_API\<MIP:: Stream\> CreateStreamFromStdStream (const std:: shared_ptr\<std::istream\>& stdIStream)       |  Crea un [flujo](class_mip_stream.md) desde un std::istream.
Public std:: shared_ptr MIP_API\<MIP:: Stream\> CreateStreamFromStdStream (const std:: shared_ptr\<std::ostream\>& stdOStream)       |  Crea un [flujo](class_mip_stream.md) desde un std::ostream.
public MIP_API std::shared_ptr\<mip::Stream\> CreateStreamFromStdStream(const std::shared_ptr\<std::iostream\>& stdIOStream)       |  Crea un [flujo](class_mip_stream.md) desde un std::iostream.
Public std:: shared_ptr MIP_API\<MIP:: Stream\> CreateStreamFromBuffer (búfer de uint8_t, const tamaño int64_t)       |  Crea un [flujo](class_mip_stream.md) desde un búfer.
 | 
**Namespace `mip::auditmetadatakeys` :** |
Public std:: String Sender()       |  Auditar las claves de metadatos en la representación de cadena.
Public std:: String Recipients()       | _No se ha documentado todavía._
public std::string LastModifiedBy()       | _No se ha documentado todavía._
Public std:: String LastModifiedDate()       | _No se ha documentado todavía._
 | 
**Namespace `mip::rights` :** |
public std::string Owner()       |  Obtiene el identificador de cadena para el derecho "propietario".
public std::string View()       |  Obtiene el identificador de cadena para el derecho "ver".
public std::string AuditedExtract()       |  Obtiene el identificador de cadena para el derecho "extracto auditado".
public std::string Edit()       |  Obtiene el identificador de cadena para el derecho "editar".
public std::string Export()       |  Obtiene el identificador de cadena para el derecho "exportar".
public std::string Extract()       |  Obtiene el identificador de cadena para el derecho "extraer".
public std::string Print()       |  Obtiene el identificador de cadena para el derecho "imprimir".
public std::string Comment()       |  Obtiene el identificador de cadena para el derecho "comentar".
public std::string Reply()       |  Obtiene el identificador de cadena para el derecho "responder".
public std::string ReplyAll()       |  Obtiene el identificador de cadena para el derecho "responder a todos".
public std::string Forward()       |  Obtiene el identificador de cadena para el derecho "reenviar".
Public std:: vector\<std:: String\> EmailRights()       |  Obtiene una lista de derechos que se aplican a los correos electrónicos.
public std::vector\<std::string\> EditableDocumentRights()       |  Obtiene una lista de derechos que se aplican a los documentos.
public std::vector\<std::string\> CommonRights()       |  Obtiene una lista de derechos que se aplican en todos los escenarios.
 | 
**Namespace `mip::roles` :** |
public std::string Viewer()       |  Obtiene el identificador de cadena para el rol "visualizador".
public std::string Reviewer()       |  Obtiene el identificador de cadena para el rol "revisor".
public std::string Author()       |  Obtiene el identificador de cadena para el rol "autor".
public std::string CoOwner()       |  Obtiene el identificador de cadena para el rol "copropietario".



## <a name="namespace-mip"></a>Namespace `mip`

### <a name="getassignmentmethodstring-function"></a>Función GetAssignmentMethodString
Convierte una cadena de descripción AssignmentMethod enum.

Parámetros:  
* **método**: un método de asignación. 



  
**Devuelve**: Una descripción de cadena del método de asignación.
  
### <a name="getactionsourcestring-function"></a>Función GetActionSourceString
Obtiene el nombre de origen de la acción.

Parámetros:  
* **actionSource**: El origen de la acción. 



  
**Devuelve**: Representación de cadena del origen de la acción.
  
### <a name="getcontentstatestring-function"></a>Función GetContentStateString
Obtiene el nombre del estado del contenido.

Parámetros:  
* **actionSource**: El estado del contenido que se está trabajando. 



  
**Devuelve**: Representación de cadena del estado del contenido.
  
### <a name="getcustomsettingpolicydataname-function"></a>Función GetCustomSettingPolicyDataName
Nombre de la configuración para especificar explícitamente los datos de la directiva.

  
**Devuelve**: La clave de configuración personalizada.
  
### <a name="getcustomsettingexportpolicyfilename-function"></a>GetCustomSettingExportPolicyFileName function
Nombre de la configuración para especificar explícitamente la ruta del archivo a la que exportar datos de la directiva SCC.

  
**Devuelve**: La clave de configuración personalizada.
  
### <a name="getcustomsettingsensitivitytypesdataname-function"></a>Función GetCustomSettingSensitivityTypesDataName
Nombre de la configuración para especificar explícitamente los datos de sensibilidad.

  
**Devuelve**: La clave de configuración personalizada.
  
### <a name="getcustomsettingpolicydatafile-function"></a>Función GetCustomSettingPolicyDataFile
Nombre de la configuración para especificar explícitamente la ruta del archivo de datos de la directiva.

  
**Devuelve**: La clave de configuración personalizada.
  
### <a name="getcustomsettingsensitivitytypesdatafile-function"></a>Función GetCustomSettingSensitivityTypesDataFile
Nombre de la configuración para especificar explícitamente la sensibilidad de los tipos de ruta de acceso de archivo de datos.

  
**Devuelve**: La clave de configuración personalizada.
  
### <a name="releaseallresources-function"></a>Función ReleaseAllResources
Libera todos los recursos (subprocesos, etc.) antes de un apagado.
Si una aplicación carga con retraso las bibliotecas dinámicas de MIP, es necesario llamar a esta función antes de que la aplicación descargue de forma explícita esas bibliotecas de MIP para evitar un interbloqueo. Por ejemplo, en win32, esta función debe llamarse antes de llamar a explícitamente descarga archivos DLL de MIP a través de FreeLibrary o __FUnloadDelayLoadedDLL2. Las aplicaciones tienen que liberar las referencias a todos los objetos de MIP (por ejemplo, perfiles, motores, controladores) antes de llamar a esta función.
  
### <a name="operator-function"></a>operador | función
Operador OR bit a bit de ProtectionHandlerCreationOptions.

Parámetros:  
* **a**: Valor de la izquierda 


* **b**: Valor correcto



  
**Devuelve**: Operación OR bit a bit de ProtectionHandlerCreationOptions
  
### <a name="createstreamfromstdstream-function"></a>Función CreateStreamFromStdStream
Crea un [flujo](class_mip_stream.md) desde un std::istream.

Parámetros:  
* **stdIStream**: Respaldo std::istream



  
**Devuelve**: [Stream](class_mip_stream.md) un std::istream de ajuste
  
### <a name="createstreamfromstdstream-function"></a>Función CreateStreamFromStdStream
Crea un [flujo](class_mip_stream.md) desde un std::ostream.

Parámetros:  
* **stdOStream**: Respaldo std::ostream



  
**Devuelve**: [Stream](class_mip_stream.md) un std::ostream de ajuste
  
### <a name="createstreamfromstdstream-function"></a>Función CreateStreamFromStdStream
Crea un [flujo](class_mip_stream.md) desde un std::iostream.

Parámetros:  
* **stdIOStream**: Respaldo std::iostream



  
**Devuelve**: [Stream](class_mip_stream.md) un std::iostream de ajuste
  
### <a name="createstreamfrombuffer-function"></a>Función CreateStreamFromBuffer
Crea un [flujo](class_mip_stream.md) desde un búfer.

Parámetros:  
* **buffer**: Puntero a un búfer



  
**Devuelve**: Tamaño del búfer
  



## <a name="namespace-mipauditmetadatakeys"></a>Namespace `mip::auditmetadatakeys`

### <a name="sender-function"></a>Función de remitente
Auditar las claves de metadatos en la representación de cadena.
  
### <a name="recipients-function"></a>Función de los destinatarios
_No se ha documentado todavía._

  
### <a name="lastmodifiedby-function"></a>Función LastModifiedBy
_No se ha documentado todavía._
  
### <a name="lastmodifieddate-function"></a>Función LastModifiedDate & gt
_No se ha documentado todavía._





## <a name="namespace-miprights"></a>Namespace `mip::rights`

### <a name="owner-function"></a>Función propietaria
Obtiene el identificador de cadena para el derecho "propietario".

  
**Devuelve**: Identificador de cadena de "propietario" derecho
  
### <a name="view-function"></a>Función de vista
Obtiene el identificador de cadena para el derecho "ver".

  
**Devuelve**: Cadena de identificador de 'view' derecha
  
### <a name="auditedextract-function"></a>Función AuditedExtract
Obtiene el identificador de cadena para el derecho "extracto auditado".

  
**Devuelve**: Identificador de cadena para "extracto auditado" derecha
  
### <a name="edit-function"></a>Editar función
Obtiene el identificador de cadena para el derecho "editar".

  
**Devuelve**: Identificador de cadena para 'Editar' derecha
  
### <a name="export-function"></a>Función de exportación
Obtiene el identificador de cadena para el derecho "exportar".

  
**Devuelve**: Identificador de cadena para "export" derecha
  
### <a name="extract-function"></a>Extraer función
Obtiene el identificador de cadena para el derecho "extraer".

  
**Devuelve**: Identificador de cadena para "extraer" derecha
  
### <a name="print-function"></a>Print (función)
Obtiene el identificador de cadena para el derecho "imprimir".

  
**Devuelve**: Identificador de cadena de la derecha 'impresión'
  
### <a name="comment-function"></a>Función de comentario
Obtiene el identificador de cadena para el derecho "comentar".

  
**Devuelve**: Identificador de cadena para "comment" derecha
  
### <a name="reply-function"></a>Función de respuesta
Obtiene el identificador de cadena para el derecho "responder".

  
**Devuelve**: Cadena derecha identificador 'respuesta'
  
### <a name="replyall-function"></a>Función ReplyAll
Obtiene el identificador de cadena para el derecho "responder a todos".

  
**Devuelve**: Identificador de cadena para el derecho "responder a todos"
  
### <a name="forward-function"></a>Función hacia delante
Obtiene el identificador de cadena para el derecho "reenviar".

  
**Devuelve**: Identificador de cadena de la derecha 'directa'
  
### <a name="emailrights-function"></a>Función EmailRights
Obtiene una lista de derechos que se aplican a los correos electrónicos.

  
**Devuelve**: Una lista de derechos que se aplican a los correos electrónicos
  
### <a name="editabledocumentrights-function"></a>Función EditableDocumentRights
Obtiene una lista de derechos que se aplican a los documentos.

  
**Devuelve**: Una lista de derechos que se aplican a documentos
  
### <a name="commonrights-function"></a>Función CommonRights
Obtiene una lista de derechos que se aplican en todos los escenarios.

  
**Devuelve**: Una lista de derechos que se aplican en todos los escenarios




## <a name="namespace-miproles"></a>Namespace `mip::roles`

### <a name="viewer-function"></a>Función de Visor
Obtiene el identificador de cadena para el rol "visualizador".

  
**Devuelve**: Identificador de cadena para la función 'Visor' un visor solo puede ver el contenido. No se puede editarlo, copiarlo ni imprimirlo.
  
### <a name="reviewer-function"></a>Función de revisor
Obtiene el identificador de cadena para el rol "revisor".

  
**Devuelve**: Identificador de cadena para la función 'revisor' un revisor puede ver y editar el contenido. No puede copiarlo ni imprimirlo.
  
### <a name="author-function"></a>Función autor
Obtiene el identificador de cadena para el rol "autor".

  
**Devuelve**: Identificador de rol de 'author' un autor puede ver, editar, copiar e imprimir el contenido de cadena.
  
### <a name="coowner-function"></a>Función coOwner
Obtiene el identificador de cadena para el rol "copropietario".

  
**Devuelve**: Identificador de cadena para la función 'copropietario' copropietario tiene todos los permisos
