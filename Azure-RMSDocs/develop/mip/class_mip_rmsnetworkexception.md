# <a name="class-miprmsnetworkexception"></a>clase mip::RMSNetworkException 
Excepción de red de RMS.
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public inline  RMSNetworkExceptionReason reason) public inline  RMSNetworkExceptionReason reason) public inline virtual Reason reason | Obtiene la clasificación del error de red.
public inline virtual const char * what | Obtiene el mensaje de excepción.
public inline virtual ExceptionTypes type | Obtiene el tipo de excepción.
public inline virtual int error | Obtiene el código de error.
## <a name="members"></a>Miembros
### <a name="rmsnetworkexception"></a>RMSNetworkException
Constructor [RMSNetworkException](#classmip_1_1_r_m_s_network_exception).
#### <a name="parameters"></a>Parámetros
* message Mensaje de excepción 
* reason Clasificación del error de red
### <a name="rmsnetworkexception"></a>RMSNetworkException
Constructor [RMSNetworkException](#classmip_1_1_r_m_s_network_exception).
#### <a name="parameters"></a>Parámetros
* message Mensaje de excepción 
* reason Clasificación del error de red
### <a name="reason"></a>Motivo
Obtiene la clasificación del error de red
#### <a name="returns"></a>Devuelve
Clasificación del error de red
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