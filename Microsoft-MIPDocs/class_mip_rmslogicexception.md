# <a name="class-miprmslogicexception"></a>clase mip::RMSLogicException 
Excepción de lógica de RMS.
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public inline  RMSLogicExceptionErrorTypes error,const std::string & message) public inline  RMSLogicExceptionErrorTypes error,const char *const & message) public inline virtual const char * what | Obtiene el mensaje de excepción.
public inline virtual ExceptionTypes type | Obtiene el tipo de excepción.
public inline virtual int error | Obtiene el código de error.
## <a name="members"></a>Miembros
### <a name="rmslogicexception"></a>RMSLogicException
Constructor [RMSLogicException](#classmip_1_1_r_m_s_logic_exception).
#### <a name="parameters"></a>Parámetros
* error Código de [error](#classmip_1_1_error) 
* message Mensaje de excepción
### <a name="rmslogicexception"></a>RMSLogicException
Constructor [RMSLogicException](#classmip_1_1_r_m_s_logic_exception).
#### <a name="parameters"></a>Parámetros
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