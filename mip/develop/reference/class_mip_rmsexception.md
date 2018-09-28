# <a name="class-miprmsexception"></a>clase mip::RMSException 
Excepción de RMS base.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public RMSException(const ExceptionTypes type, const int error, const std::string& message)  |  Constructor [RMSException](class_mip_rmsexception.md).
 public RMSException(const ExceptionTypes type, const int error, const char*const& message)  |  Constructor [RMSException](class_mip_rmsexception.md).
 public virtual const char* what() const  |  Obtiene el mensaje de excepción.
 public virtual ExceptionTypes type() const  |  Obtiene el tipo de excepción.
 public virtual int error() const  |  Obtiene el código de error.
  
## <a name="members"></a>Miembros
  
### <a name="rmsexception"></a>RMSException
Constructor [RMSException](class_mip_rmsexception.md).

Parámetros:  
* **type**: tipo de excepción 


* **error**: código de [error](class_mip_error.md) 


* **message**: mensaje de excepción


  
### <a name="rmsexception"></a>RMSException
Constructor [RMSException](class_mip_rmsexception.md).

Parámetros:  
* **type**: tipo de excepción 


* **error**: código de [error](class_mip_error.md) 


* **message**: mensaje de excepción


  
### <a name="what"></a>what
Obtiene el mensaje de excepción.

  
**Devuelve**: mensaje de excepción
  
### <a name="exceptiontypes"></a>ExceptionTypes
Obtiene el tipo de excepción.

  
**Devuelve**: tipo de excepción
  
### <a name="error"></a>error
Obtiene el código de error.

  
**Devuelve**: código de [error](class_mip_error.md)