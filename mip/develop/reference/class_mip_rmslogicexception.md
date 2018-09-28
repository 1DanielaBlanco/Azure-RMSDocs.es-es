# <a name="class-miprmslogicexception"></a>clase mip::RMSLogicException 
Excepción de lógica de RMS.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public RMSLogicException(const ErrorTypes error, const std::string& message)  |  Constructor [RMSLogicException](class_mip_rmslogicexception.md).
 public RMSLogicException(const ErrorTypes error, const char*const& message)  |  Constructor [RMSLogicException](class_mip_rmslogicexception.md).
 public virtual const char* what() const  |  Obtiene el mensaje de excepción.
 public virtual ExceptionTypes type() const  |  Obtiene el tipo de excepción.
 public virtual int error() const  |  Obtiene el código de error.
  
## <a name="members"></a>Miembros
  
### <a name="rmslogicexception"></a>RMSLogicException
Constructor [RMSLogicException](class_mip_rmslogicexception.md).

Parámetros:  
* **error**: código de [error](class_mip_error.md) 


* **message**: mensaje de excepción


  
### <a name="rmslogicexception"></a>RMSLogicException
Constructor [RMSLogicException](class_mip_rmslogicexception.md).

Parámetros:  
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