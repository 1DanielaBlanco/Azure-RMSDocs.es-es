# <a name="class-miprmsofficefileexception"></a>clase mip::RMSOfficeFileException 
Excepción de archivo de Office de RMS.
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public inline  RMSOfficeFileExceptionReason reason) public inline  RMSOfficeFileExceptionReason reason) public inline virtual Reason reason | Obtiene la clasificación de errores del archivo de Office.
public inline virtual const char * what | Obtiene el mensaje de excepción.
public inline virtual ExceptionTypes type | Obtiene el tipo de excepción.
public inline virtual int error | Obtiene el código de error.
## <a name="members"></a>Miembros
### <a name="rmsofficefileexception"></a>RMSOfficeFileException
Constructor [RMSOfficeFileException](#classmip_1_1_r_m_s_office_file_exception).
#### <a name="parameters"></a>Parámetros
* message Mensaje de excepción 
* reason Clasificación de errores de archivos de Office
### <a name="rmsofficefileexception"></a>RMSOfficeFileException
Constructor [RMSOfficeFileException](#classmip_1_1_r_m_s_office_file_exception).
#### <a name="parameters"></a>Parámetros
* message Mensaje de excepción 
* reason Clasificación de errores de archivos de Office
### <a name="reason"></a>Motivo
Obtiene la clasificación de errores de archivos de Office.
#### <a name="returns"></a>Devuelve
Clasificación de errores de archivos de Office
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