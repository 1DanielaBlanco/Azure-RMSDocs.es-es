# <a name="functions"></a>Funciones

 Funciones (ámbito)                        | Descripciones                                
--------------------------------|---------------------------------------------
public const std::string& GetCustomSettingExportPolicyFileName()       |  Nombre de la configuración para especificar explícitamente la ruta del archivo a la que exportar datos de la directiva SCC.
public const std::string& GetCustomSettingPolicyDataFile()       |  Nombre de la configuración para especificar explícitamente la ruta del archivo de datos de la directiva.
public const std::string& GetCustomSettingPolicyDataName()       |  Nombre de la configuración para especificar explícitamente los datos de la directiva.
**funciones mip** |
public std::shared_ptr<mip::Stream> CreateStreamFromBuffer(uint8_t* buffer, const int64_t size)       |  Crea un [flujo](class_mip_stream.md) desde un búfer.
public std::shared_ptr<mip::Stream> CreateStreamFromStdStream(const std::shared_ptr<std::iostream>& stdIOStream)       |  Crea un [flujo](class_mip_stream.md) desde un std::iostream.
public std::shared_ptr<mip::Stream> CreateStreamFromStdStream(const std::shared_ptr<std::istream>& stdIStream)       |  Crea un [flujo](class_mip_stream.md) desde un std::istream.
public std::shared_ptr<mip::Stream> CreateStreamFromStdStream(const std::shared_ptr<std::ostream>& stdOStream)       |  Crea un [flujo](class_mip_stream.md) desde un std::ostream.
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

  
## <a name="enumeration-details"></a>Detalles de enumeración
  
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

### <a name="mipstream-istream"></a>mip::Stream (istream)

Crea un [flujo](class_mip_stream.md) desde un std::istream.

Parámetros:  

* **stdIStream**: flujo std::istream base
  
**Devuelve**: [flujo](class_mip_stream.md) que encapsula un std::istream
  
### <a name="mipstream-ostream"></a>mip::Stream (ostream)

Crea un [flujo](class_mip_stream.md) desde un std::ostream.

Parámetros:  
* **stdOStream**: flujo std::ostream base

  
**Devuelve**: [flujo](class_mip_stream.md) que encapsula un std::ostream
  
### <a name="mipstream-iostream"></a>mip::Stream (iostream)

Crea un [flujo](class_mip_stream.md) desde un std::iostream.

Parámetros:  
* **stdIOStream**: flujo std::iostream base
  
**Devuelve**: [flujo](class_mip_stream.md) que encapsula un std::iostream
  
### <a name="mipstream-buffer"></a>mip::Stream (búfer)

Crea un [flujo](class_mip_stream.md) desde un búfer.

Parámetros:  
* **buffer**: puntero a un búfer

**Devuelve**: tamaño de búfer
  
## <a name="functions-miprights"></a>Funciones (mip::rights)

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
  
### <a name="owner"></a>Propietario
Obtiene el identificador de cadena para el derecho "propietario".

  
**Devuelve**: identificador de cadena para el derecho "propietario"
  
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

  
**Devuelve**: identificador de cadena para el rol "autor" Un autor puede ver, editar, copiar e imprimir el contenido.
  
### <a name="coowner"></a>Copropietario
Obtiene el identificador de cadena para el rol "copropietario".

  
**Devuelve**: identificador de cadena para el rol "copropietario" Un copropietario tiene todos los permisos

### <a name="reviewer"></a>Revisor
Obtiene el identificador de cadena para el rol "revisor".

  
**Devuelve**: identificador de cadena para el rol "revisor" Un revisor puede ver y editar el contenido. No puede copiarlo ni imprimirlo.

### <a name="viewer"></a>Visor
Obtiene el identificador de cadena para el rol "visualizador".

  
**Devuelve**: identificador de cadena para el rol "visualizador" Un visualizador solo puede ver el contenido. No se puede editarlo, copiarlo ni imprimirlo.
  
  
