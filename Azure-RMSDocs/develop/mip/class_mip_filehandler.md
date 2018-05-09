# <a name="class-mipfilehandler"></a>clase mip::FileHandler 
Interfaz a todas las funciones de control de archivos.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public void GetLabelAsync(const std::shared_ptr<void>& context)  |  Inicia la recuperación de la etiqueta de confidencialidad del archivo.
public void GetProtectionAsync(const std::shared_ptr<void>& context)  |  Inicia la recuperación de la directiva de protección desde el archivo.
public void SetLabel(const std::string& labelId, const LabelingOptions& labelingOptions)  |  Establece la etiqueta de sensibilidad en el archivo.
public void DeleteLabel(AssignmentMethod method, const std::string& justificationMessage)  |  Elimina la etiqueta de sensibilidad del archivo.
public void SetCustomPermissions(const std::shared_ptr<PolicyDescriptor>& policyDescriptor)  |  Establece permisos personalizados en el archivo.
public void RemoveProtection()  |  Quita la protección del archivo. Si el archivo está etiquetado, la etiqueta se perderá.
public void CommitAsync(const std::string& outputFilePath, const std::shared_ptr<void>& context) | Escribe los cambios en el archivo especificado por el parámetro \|outputFilePath\ |  .
public void CommitAsync(const std::shared_ptr<Stream>& outputStream, const std::shared_ptr<void>& context) | Escribe los cambios en el flujo especificado por el parámetro \|outputStream\ |  .
public std::string GetOutputFileName()  |  Calcula el nombre y la extensión del archivo de salida basándose en el nombre del archivo original y en los cambios acumulados.
public inline virtual ~FileHandler()  |  
protected inline FileHandler()  |  
  
## <a name="members"></a>Miembros
  
### <a name="getlabelasync"></a>GetLabelAsync
Inicia la recuperación de la etiqueta de confidencialidad del archivo.
Se llamará a [FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer) después de la realización correcta o de un error.
  
#### <a name="parameters"></a>Parámetros
* context Contexto de cliente que se pasará de manera opaca hacia el observador.
  
### <a name="getprotectionasync"></a>GetProtectionAsync
Inicia la recuperación de la directiva de protección desde el archivo.
Se llamará a [FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer) después de la realización correcta o de un error.
  
#### <a name="parameters"></a>Parámetros
* context Contexto de cliente que se pasará de manera opaca hacia el observador.
  
### <a name="setlabel"></a>SetLabel
Establece la etiqueta de sensibilidad en el archivo.
Los cambios no se escribirán en el archivo hasta que se llame a CommitAsync.
Produce un error [JustificationRequiredError](#classmip_1_1_justification_required_error) cuando la configuración de la etiqueta requiere una justificación y no se ha proporcionado ningún mensaje de justificación mediante el parámetro labelingOptions.
  
### <a name="deletelabel"></a>DeleteLabel
Elimina la etiqueta de sensibilidad del archivo.
Los cambios no se escribirán en el archivo hasta que se llame a CommitAsync. El método Privilegd y Auto permite a la API invalidar cualquier etiqueta existente Produce el error [JustificationRequiredError](#classmip_1_1_justification_required_error) cuando la configuración de la etiqueta requiere una justificación y no se ha proporcionado ningún mensaje de justificación mediante el parámetro justificationMessage.
  
### <a name="setcustompermissions"></a>SetCustomPermissions
Establece permisos personalizados en el archivo.
Los cambios no se escribirán en el archivo hasta que se llame a CommitAsync.
  
### <a name="removeprotection"></a>RemoveProtection
Quita la protección del archivo. Si el archivo está etiquetado, la etiqueta se perderá.
Los cambios no se escribirán en el archivo hasta que se llame a CommitAsync.
  
### <a name="commitasync"></a>CommitAsync
Escribe los cambios en el archivo especificado por el parámetro |outputFilePath|.
Se llamará a [FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer) después de la realización correcta o de un error.
  
### <a name="commitasync"></a>CommitAsync
Escribe los cambios en el flujo especificado por el parámetro |outputStream|.
Se llamará a [FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer) después de la realización correcta o de un error.
  
### <a name="getoutputfilename"></a>GetOutputFileName
Calcula el nombre y la extensión del archivo de salida basándose en el nombre del archivo original y en los cambios acumulados.
  
### <a name="filehandler"></a>~FileHandler
  
### <a name="filehandler"></a>FileHandler