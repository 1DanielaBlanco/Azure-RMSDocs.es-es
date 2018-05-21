# <a name="class-mipfileengine"></a>clase mip::FileEngine 
Interfaz para todas las funciones de motor.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public virtual ~FileEngine()  | _Not yet documented._
 public const Settings& GetSettings() const  |  Devuelve la configuración del motor.
public const std::vector<std::shared_ptr<Label>>& ListSensitivityLabels()  |  Devuelve una lista de etiquetas de confidencialidad.
public std::shared_ptr<FileHandler> CreateFileHandler(const std::string& inputFilePath, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver)  |  Devuelve el controlador de archivos para una ruta de acceso de archivo determinada.
public std::shared_ptr<FileHandler> CreateFileHandler(const std::shared_ptr<Stream>& inputStream, const std::string& inputFileName, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver)  |  Devuelve el controlador de archivos para un flujo de archivo determinado.
 protected FileEngine()  | _Not yet documented._
  
## <a name="members"></a>Miembros
  
### <a name="fileengine"></a>~FileEngine
_No se ha documentado todavía._

  
### <a name="settings"></a>Configuración
Devuelve la configuración del motor.
  
### <a name="label"></a>Etiqueta
Devuelve una lista de etiquetas de confidencialidad.
  
### <a name="filehandler"></a>FileHandler
Devuelve el controlador de archivos para una ruta de acceso de archivo determinada.

Parámetros:  
* **The**: archivo que se va a abrir. La ruta de acceso debe incluir el nombre de archivo y, si existe, la extensión de nombre de archivo. 


* **A**: clase que implementa la interfaz [FileHandler::Observer](class_mip_filehandler_observer.md).


  
### <a name="filehandler"></a>FileHandler
Devuelve el controlador de archivos para un flujo de archivo determinado.

Parámetros:  
* **A**: flujo que representa el archivo. 


* **The**: ruta de acceso al archivo. La ruta de acceso debe incluir el nombre de archivo y, si existe, la extensión de nombre de archivo. 


* **A**: clase que implementa la interfaz [FileHandler::Observer](class_mip_filehandler_observer.md).


  
### <a name="fileengine"></a>FileEngine
_No se ha documentado todavía._
