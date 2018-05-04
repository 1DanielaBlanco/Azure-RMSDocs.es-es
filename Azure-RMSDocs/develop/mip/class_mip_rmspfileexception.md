# <a name="class-miprmspfileexception"></a>clase mip::RMSPFileException 
Excepción de PFile de RMS.
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public inline  RMSPFileExceptionReason reason) public inline  RMSPFileExceptionReason reason) public inline virtual Reason reason | Obtiene la clasificación del error de PFile.
public inline virtual const char * what | Obtiene el mensaje de excepción.
public inline virtual ExceptionTypes type | Obtiene el tipo de excepción.
public inline virtual int error | Obtiene el código de error.
## <a name="members"></a>Miembros
### <a name="rmspfileexception"></a>RMSPFileException
Constructor [RMSPFileException](#classmip_1_1_r_m_s_p_file_exception).
#### <a name="parameters"></a>Parámetros
* message Mensaje de excepción 
* reason Clasificación del error de PFile
### <a name="rmspfileexception"></a>RMSPFileException
Constructor [RMSPFileException](#classmip_1_1_r_m_s_p_file_exception).
#### <a name="parameters"></a>Parámetros
* message Mensaje de excepción 
* reason Clasificación del error de PFile
### <a name="reason"></a>Motivo
Obtiene la clasificación del error de PFile.
#### <a name="returns"></a>Devuelve
Clasificación del error de PFile.
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