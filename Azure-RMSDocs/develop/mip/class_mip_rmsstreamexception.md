# <a name="class-miprmsstreamexception"></a>clase mip::RMSStreamException 
Excepción de flujo de RMS
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public inline RMSStreamException(const std::string& message)  |  Constructor [RMSStreamException](#classmip_1_1_r_m_s_stream_exception).
public inline RMSStreamException(const char*const& message)  |  Constructor [RMSStreamException](#classmip_1_1_r_m_s_stream_exception).
public inline virtual const char* what() const  |  Obtiene el mensaje de excepción.
public inline virtual ExceptionTypes type() const  |  Obtiene el tipo de excepción.
public inline virtual int error() const  |  Obtiene el código de error.
  
## <a name="members"></a>Miembros
  
### <a name="rmsstreamexception"></a>RMSStreamException
Constructor [RMSStreamException](#classmip_1_1_r_m_s_stream_exception).
  
#### <a name="parameters"></a>Parámetros
* message Mensaje de excepción
  
### <a name="rmsstreamexception"></a>RMSStreamException
Constructor [RMSStreamException](#classmip_1_1_r_m_s_stream_exception).
  
#### <a name="parameters"></a>Parámetros
* message Mensaje de excepción
  
### <a name="what"></a>what
Obtiene el mensaje de excepción.
  
#### <a name="returns"></a>Devuelve
Mensaje de excepción
  
### <a name="exceptiontypes"></a>ExceptionTypes
Obtiene el tipo de excepción.
  
#### <a name="returns"></a>Devuelve
Tipo de excepción
  
### <a name="error"></a>error
Obtiene el código de error.
  
#### <a name="returns"></a>Devuelve
Código de [error](#classmip_1_1_error)