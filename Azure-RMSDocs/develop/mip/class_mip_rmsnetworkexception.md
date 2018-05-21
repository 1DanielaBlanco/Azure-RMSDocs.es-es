# <a name="class-miprmsnetworkexception"></a>clase mip::RMSNetworkException 
Excepción de red de RMS.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public RMSNetworkException(const std::string& message, Reason reason)  |  Constructor [RMSNetworkException](class_mip_rmsnetworkexception.md).
 public RMSNetworkException(const char*const& message, Reason reason)  |  Constructor [RMSNetworkException](class_mip_rmsnetworkexception.md).
 public virtual Reason reason() const  |  Obtiene la clasificación del error de red.
 public virtual const char* what() const  |  Obtiene el mensaje de excepción.
 public virtual ExceptionTypes type() const  |  Obtiene el tipo de excepción.
 public virtual int error() const  |  Obtiene el código de error.
  
## <a name="members"></a>Miembros
  
### <a name="rmsnetworkexception"></a>RMSNetworkException
Constructor [RMSNetworkException](class_mip_rmsnetworkexception.md).

Parámetros:  
* **message**: mensaje de excepción 


* **reason**: clasificación del error de red


  
### <a name="rmsnetworkexception"></a>RMSNetworkException
Constructor [RMSNetworkException](class_mip_rmsnetworkexception.md).

Parámetros:  
* **message**: mensaje de excepción 


* **reason**: clasificación del error de red


  
### <a name="reason"></a>Motivo
Obtiene la clasificación del error de red.

  
**Devuelve**: clasificación del error de red
  
### <a name="what"></a>what
Obtiene el mensaje de excepción.

  
**Devuelve**: mensaje de excepción
  
### <a name="exceptiontypes"></a>ExceptionTypes
Obtiene el tipo de excepción.

  
**Devuelve**: tipo de excepción
  
### <a name="error"></a>error
Obtiene el código de error.

  
**Devuelve**: código de [error](class_mip_error.md)