# <a name="class-mipfileengine"></a>clase mip::FileEngine 
Interfaz para todas las funciones de motor.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public inline virtual ~FileEngine()  |  
public const Settings& GetSettings() const  |  Devuelve la configuración del motor.
public const std::vector<std::shared_ptr<Label>>& ListSensitivityLabels()  |  Devuelve una lista de etiquetas de confidencialidad.
public std::shared_ptr<FileHandler> CreateFileHandler(const std::string& inputFilePath, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver)  |  Devuelve el controlador de archivos para una ruta de acceso de archivo determinada.
public std::shared_ptr<FileHandler> CreateFileHandler(const std::shared_ptr<Stream>& inputStream, const std::string& inputFileName, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver)  |  Devuelve el controlador de archivos para un flujo de archivo determinado.
protected inline FileEngine()  |  
  
## <a name="members"></a>Miembros
  
### <a name="fileengine"></a>~FileEngine
  
### <a name="settings"></a>Configuración
Devuelve la configuración del motor.
  
### <a name="label"></a>Etiqueta
Devuelve una lista de etiquetas de confidencialidad.
  
### <a name="filehandler"></a>FileHandler
Devuelve el controlador de archivos para una ruta de acceso de archivo determinada.
  
#### <a name="parameters"></a>Parámetros
* El archivo que se va a abrir. La ruta de acceso debe incluir el nombre de archivo y, si existe, la extensión de nombre de archivo. 
* Una clase que implementa la interfaz [FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer).
  
### <a name="filehandler"></a>FileHandler
Devuelve el controlador de archivos para un flujo de archivo determinado.
  
#### <a name="parameters"></a>Parámetros
* Una flujo que representa el archivo. 
* La ruta de acceso al archivo. La ruta de acceso debe incluir el nombre de archivo y, si existe, la extensión de nombre de archivo. 
* Una clase que implementa la interfaz [FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer).
  
### <a name="fileengine"></a>FileEngine