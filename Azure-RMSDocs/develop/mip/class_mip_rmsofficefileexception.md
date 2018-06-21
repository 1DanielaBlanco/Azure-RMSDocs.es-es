# <a name="class-miprmsofficefileexception"></a>clase mip::RMSOfficeFileException 
Excepción de archivo de Office de RMS.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public RMSOfficeFileException(const std::string& message, Reason reason)  |  Constructor [RMSOfficeFileException](class_mip_rmsofficefileexception.md).
 public RMSOfficeFileException(const char*const& message, Reason reason)  |  Constructor [RMSOfficeFileException](class_mip_rmsofficefileexception.md).
 public virtual Reason reason() const  |  Obtiene la clasificación del error del archivo de Office.
 public virtual const char* what() const  |  Obtiene el mensaje de excepción.
 public virtual ExceptionTypes type() const  |  Obtiene el tipo de excepción.
 public virtual int error() const  |  Obtiene el código de error.
  
## <a name="members"></a>Miembros
  
### <a name="rmsofficefileexception"></a>RMSOfficeFileException
Constructor [RMSOfficeFileException](class_mip_rmsofficefileexception.md).

Parámetros:  
* **message**: mensaje de excepción 


* **reason**: clasificación de errores de archivos de Office


  
### <a name="rmsofficefileexception"></a>RMSOfficeFileException
Constructor [RMSOfficeFileException](class_mip_rmsofficefileexception.md).

Parámetros:  
* **message**: mensaje de excepción 


* **reason**: clasificación de errores de archivos de Office


  
### <a name="reason"></a>Motivo
Obtiene la clasificación del error del archivo de Office.

  
**Devuelve**: clasificación de errores de archivos de Office
  
### <a name="what"></a>what
Obtiene el mensaje de excepción.

  
**Devuelve**: mensaje de excepción
  
### <a name="exceptiontypes"></a>ExceptionTypes
Obtiene el tipo de excepción.

  
**Devuelve**: tipo de excepción
  
### <a name="error"></a>error
Obtiene el código de error.

  
**Devuelve**: código de [error](class_mip_error.md)