# <a name="class-miprmspfileexception"></a>clase mip::RMSPFileException 
Excepción de PFile de RMS.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public RMSPFileException(const std::string& message, Reason reason)  |  Constructor [RMSPFileException](class_mip_rmspfileexception.md).
 public RMSPFileException(const char*const& message, Reason reason)  |  Constructor [RMSPFileException](class_mip_rmspfileexception.md).
 public virtual Reason reason() const  |  Obtiene la clasificación del error de PFile.
 public virtual const char* what() const  |  Obtiene el mensaje de excepción.
 public virtual ExceptionTypes type() const  |  Obtiene el tipo de excepción.
 public virtual int error() const  |  Obtiene el código de error.
  
## <a name="members"></a>Miembros
  
### <a name="rmspfileexception"></a>RMSPFileException
Constructor [RMSPFileException](class_mip_rmspfileexception.md).

Parámetros:  
* **message**: mensaje de excepción 


* **reason**: clasificación del error de PFile


  
### <a name="rmspfileexception"></a>RMSPFileException
Constructor [RMSPFileException](class_mip_rmspfileexception.md).

Parámetros:  
* **message**: mensaje de excepción 


* **reason**: clasificación del error de PFile


  
### <a name="reason"></a>Motivo
Obtiene la clasificación del error de PFile.

  
**Devuelve**: clasificación del error de PFile
  
### <a name="what"></a>what
Obtiene el mensaje de excepción.

  
**Devuelve**: mensaje de excepción
  
### <a name="exceptiontypes"></a>ExceptionTypes
Obtiene el tipo de excepción.

  
**Devuelve**: tipo de excepción
  
### <a name="error"></a>error
Obtiene el código de error.

  
**Devuelve**: código de [error](class_mip_error.md)