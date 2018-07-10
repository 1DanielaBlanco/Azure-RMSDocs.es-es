# <a name="class-miploggerdelegate"></a>clase mip::LoggerDelegate 
Una clase que define la interfaz para el registrador de SDK de mip.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public void Init(const std::string& storagePath)  |  Inicialice el registrador.
 public void Flush()  |  Vacíe el registrador.
 public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const uint64_t line)  |  Escriba una instrucción de registro en el archivo de registro.
  
## <a name="members"></a>Miembros
  
### <a name="init"></a>Init
Inicialice el registrador.

Parámetros:  
* **storagePath**: la ruta de acceso a la ubicación donde se puede almacenar el estado persistente, incluidos los registros,.


  
### <a name="flush"></a>Vaciar
Vacíe el registrador.
  
### <a name="writetolog"></a>WriteToLog
Escriba una instrucción de registro en el archivo de registro.

Parámetros:  
* **level**: el nivel de registro para la instrucción de registro. 


* **message**: el mensaje para la instrucción de registro. 


* **function**: el nombre de función para la instrucción de registro. 


* **file**: el nombre de archivo donde se generó la instrucción de registro. 


* **line**: el número de línea donde se generó la instrucción de registro.

