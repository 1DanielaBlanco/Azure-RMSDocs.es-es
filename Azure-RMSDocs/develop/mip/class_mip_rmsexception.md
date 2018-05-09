# <a name="class-miprmsexception"></a>clase mip::RMSException 
Excepción de RMS base.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public inline RMSException(const ExceptionTypes type, const int error, const std::string& message)  |  Constructor [RMSException](#classmip_1_1_r_m_s_exception).
public inline RMSException(const ExceptionTypes type, const int error, const char*const& message)  |  Constructor [RMSException](#classmip_1_1_r_m_s_exception).
public inline virtual const char* what() const  |  Obtiene el mensaje de excepción.
public inline virtual ExceptionTypes type() const  |  Obtiene el tipo de excepción.
public inline virtual int error() const  |  Obtiene el código de error.
  
## <a name="members"></a>Miembros
  
### <a name="rmsexception"></a>RMSException
Constructor [RMSException](#classmip_1_1_r_m_s_exception).
  
#### <a name="parameters"></a>Parámetros
* type Tipo de excepción 
* error Código de [error](#classmip_1_1_error) 
* message Mensaje de excepción
  
### <a name="rmsexception"></a>RMSException
Constructor [RMSException](#classmip_1_1_r_m_s_exception).
  
#### <a name="parameters"></a>Parámetros
* type Tipo de excepción 
* error Código de [error](#classmip_1_1_error) 
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