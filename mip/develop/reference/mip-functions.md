---
title: Funciones
description: Funciones
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 3bb9cd594022085c24c45bde428cb11f6734caab
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446522"
---
# <a name="functions"></a>Funciones

| Funciones (ámbito)              | Descripciones                                |
|--------------------------------|---------------------------------------------|
**common** |
public const std::string& GetCustomSettingPolicyDataName()       |  Nombre de la configuración para especificar explícitamente los datos de la directiva.
public const std::string& GetCustomSettingExportPolicyFileName()       |  Nombre de la configuración para especificar explícitamente la ruta del archivo a la que exportar datos de la directiva SCC.
public const std::string& GetCustomSettingPolicyDataFile()       |  Nombre de la configuración para especificar explícitamente la ruta del archivo de datos de la directiva.
 **funciones mip** |
public std::shared_ptr<mip::Stream> CreateStreamFromBuffer(uint8_t* buffer, const int64_t size)       |  Crea un [flujo](class_mip_stream.md) desde un búfer.
public std::shared_ptr<mip::Stream> CreateStreamFromStdStream(const std::shared_ptr<std::iostream>& stdIOStream)       |  Crea un [flujo](class_mip_stream.md) desde un std::iostream.
public std::shared_ptr<mip::Stream> CreateStreamFromStdStream(const std::shared_ptr<std::istream>& stdIStream)       |  Crea un [flujo](class_mip_stream.md) desde un std::istream.
public std::shared_ptr<mip::Stream> CreateStreamFromStdStream(const std::shared_ptr<std::ostream>& stdOStream)       |  Crea un [flujo](class_mip_stream.md) desde un std::ostream.
public void ReleaseAllResources()       |  Libera todos los recursos (subprocesos, etc.) antes de un apagado.
**funciones mip::Rights**|
public std::string AuditedExtract()       |  Obtiene el identificador de cadena para el derecho "extracto auditado".
public std::string Comment()       |  Obtiene el identificador de cadena para el derecho "comentar".
public std::vector<std::string> CommonRights()       |  Obtiene una lista de derechos que se aplican en todos los escenarios.
public std::string Edit()       |  Obtiene el identificador de cadena para el derecho "editar".
public std::vector<std::string> EditableDocumentRights()       |  Obtiene una lista de derechos que se aplican a los documentos.
public std::vector<std::string> EmailRights()       |  Obtiene una lista de derechos que se aplican a los correos electrónicos.
public std::string Export()       |  Obtiene el identificador de cadena para el derecho "exportar".
public std::string Extract()       |  Obtiene el identificador de cadena para el derecho "extraer".
public std::string Forward()       |  Obtiene el identificador de cadena para el derecho "reenviar".
public std::string Owner()       |  Obtiene el identificador de cadena para el derecho "propietario".
public std::string Print()       |  Obtiene el identificador de cadena para el derecho "imprimir".
public std::string Reply()       |  Obtiene el identificador de cadena para el derecho "responder".
public std::string ReplyAll()       |  Obtiene el identificador de cadena para el derecho "responder a todos".
public std::string View()       |  Obtiene el identificador de cadena para el derecho "ver".
**funciones mip::Roles**|
public std::string Author()       |  Obtiene el identificador de cadena para el rol "autor".
public std::string CoOwner()       |  Obtiene el identificador de cadena para el rol "copropietario".
public std::string Reviewer()       |  Obtiene el identificador de cadena para el rol "revisor".
public std::string Viewer()       |  Obtiene el identificador de cadena para el rol "visualizador".

  
## <a name="functions-common"></a>Funciones (común)

### <a name="getcustomsettingpolicydataname"></a>GetCustomSettingPolicyDataName
Nombre de la configuración para especificar explícitamente los datos de la directiva.

  
**Devuelve**: la clave de configuración personalizada.
  
### <a name="getcustomsettingexportpolicyfilename"></a>GetCustomSettingExportPolicyFileName
Nombre de la configuración para especificar explícitamente la ruta del archivo a la que exportar datos de la directiva SCC.

  
**Devuelve**: la clave de configuración personalizada.
  
### <a name="getcustomsettingpolicydatafile"></a>GetCustomSettingPolicyDataFile
Nombre de la configuración para especificar explícitamente la ruta del archivo de datos de la directiva.

  
**Devuelve**: la clave de configuración personalizada.

## <a name="functions-mip"></a>Funciones (mip)

### <a name="mipcreatestreamfrombufferbuffer"></a>mip::CreateStreamFromBuffer(buffer)

Crea un [flujo](class_mip_stream.md) desde un búfer.

Parámetros:  
* **buffer**: puntero a un búfer

**Devuelve**: **tamaño** del búfer.
  

### <a name="mipcreatestreamfromstdstreamistream"></a>mip::CreateStreamFromStdStream(istream)

Crea un [flujo](class_mip_stream.md) desde un std::istream.

Parámetros:  

* **stdIStream**: flujo std::istream base
  
**Devuelve**: [flujo](class_mip_stream.md) que encapsula un std::istream
  
### <a name="mipcreatestreamfromstdstreamiostream"></a>mip::CreateStreamFromStdStream(iostream)

Crea un [flujo](class_mip_stream.md) desde un std::iostream.

Parámetros:  
* **stdIOStream**: flujo std::iostream base
  
**Devuelve**: [flujo](class_mip_stream.md) que encapsula un std::iostream
  
### <a name="mipcreatestreamfromstdstreamostream"></a>mip::CreateStreamFromStdStream(ostream)

Crea un [flujo](class_mip_stream.md) desde un std::ostream.

Parámetros:  
* **stdOStream**: flujo std::ostream base
  
**Devuelve**: [flujo](class_mip_stream.md) que encapsula un std::ostream
  
### <a name="mipreleaseallresources"></a>mip::ReleaseAllResources

Libera todos los recursos (subprocesos, etc.) antes de un apagado.  

Si una aplicación carga con retraso las bibliotecas dinámicas de MIP, es necesario llamar a esta función antes de que la aplicación descargue de forma explícita esas bibliotecas de MIP para evitar un interbloqueo. Por ejemplo, en win32, es necesario llamar a esta función antes de realizar cualquier llamada para descargar de forma explícita DLL de MIP mediante FreeLibrary o \__FUnloadDelayLoadedDLL2. Las aplicaciones tienen que liberar las referencias a todos los objetos de MIP (por ejemplo, perfiles, motores, controladores) antes de llamar a esta función.

## <a name="functions-miprights"></a>Funciones (mip::rights)

### <a name="owner"></a>Propietario
Obtiene el identificador de cadena para el derecho "propietario".

  
**Devuelve**: identificador de cadena para el derecho "propietario"
  
### <a name="auditedextract"></a>AuditedExtract
Obtiene el identificador de cadena para el derecho "extracto auditado".

  
**Devuelve**: identificador de cadena para el derecho "extracto auditado"
  
### <a name="comment"></a>Comentario
Obtiene el identificador de cadena para el derecho "comentar".

  
**Devuelve**: identificador de cadena para el derecho "comentar"
  
### <a name="commonrights"></a>CommonRights
Obtiene una lista de derechos que se aplican en todos los escenarios.

  
**Devuelve**: una lista de derechos que se aplican en todos los escenarios

### <a name="edit"></a>Editar
Obtiene el identificador de cadena para el derecho "editar".

  
**Devuelve**: identificador de cadena para el derecho "editar"
  
### <a name="editabledocumentrights"></a>EditableDocumentRights
Obtiene una lista de derechos que se aplican a los documentos.

  
**Devuelve**: una lista de derechos que se aplican a los documentos
  
### <a name="emailrights"></a>EmailRights
Obtiene una lista de derechos que se aplican a los correos electrónicos.

  
**Devuelve**: una lista de derechos que se aplican a los correos electrónicos
  
### <a name="export"></a>Exportar
Obtiene el identificador de cadena para el derecho "exportar".

  
**Devuelve**: identificador de cadena para el derecho "exportar"
  
### <a name="extract"></a>Extracción
Obtiene el identificador de cadena para el derecho "extraer".

  
**Devuelve**: identificador de cadena para el derecho "extraer"
  
### <a name="forward"></a>Reenviar
Obtiene el identificador de cadena para el derecho "reenviar".

  
**Devuelve**: identificador de cadena para el derecho "reenviar"
  
### <a name="print"></a>Imprimir
Obtiene el identificador de cadena para el derecho "imprimir".

  
**Devuelve**: identificador de cadena para el derecho "imprimir"
  
### <a name="reply"></a>Responder
Obtiene el identificador de cadena para el derecho "responder".

  
**Devuelve**: identificador de cadena para el derecho "responder"
  
### <a name="replyall"></a>Responder a todos
Obtiene el identificador de cadena para el derecho "responder a todos".

  
**Devuelve**: identificador de cadena para el derecho "responder a todos"
  
### <a name="view"></a>Vista
Obtiene el identificador de cadena para el derecho "ver".

  
**Devuelve**: identificador de cadena para el derecho "ver"
  

## <a name="functions-miproles"></a>Funciones (mip::roles)

### <a name="author"></a>Autor
Obtiene el identificador de cadena para el rol "autor".

Un autor puede ver, editar, copiar e imprimir el contenido.
  
**Devuelve**: identificador de cadena para el rol “autor”.
  
### <a name="coowner"></a>Copropietario
Obtiene el identificador de cadena para el rol "copropietario".

Un copropietario tiene todos los permisos.
  
**Devuelve**: identificador de cadena para el rol “copropietario”.

### <a name="reviewer"></a>Revisor
Obtiene el identificador de cadena para el rol "revisor".

Un revisor puede ver y editar el contenido. No puede copiarlo ni imprimirlo.
  
**Devuelve**: identificador de cadena para el rol “revisor”.
  
### <a name="viewer"></a>Visor
Obtiene el identificador de cadena para el rol "visualizador".

Un visor solo puede ver el contenido. No se puede editarlo, copiarlo ni imprimirlo.
  
**Devuelve**: identificador de cadena para el rol “visor”.
  
