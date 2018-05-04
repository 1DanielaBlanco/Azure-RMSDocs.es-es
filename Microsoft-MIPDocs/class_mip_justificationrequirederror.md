# <a name="class-mipjustificationrequirederror"></a>clase mip::JustificationRequiredError 
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public inline  JustificationRequiredError | 
public inline virtual std::shared_ptr< Error > Clone | Clona el error.
public inline char const  * what | Obtiene un mensaje de error de cstring.
public inline virtual ErrorType GetErrorType | Obtiene el tipo de error.
public inline virtual const std::string & GetErrorName | Obtiene el nombre del error.
public inline virtual const std::string & GetMessage | Obtiene el mensaje de error.
public inline virtual void SetMessage | Establece el mensaje de error.
## <a name="members"></a>Miembros
### <a name="justificationrequirederror"></a>JustificationRequiredError
### <a name="error"></a>Error
Clona el error.
#### <a name="returns"></a>Devuelve
Un clon del error.
### <a name="what"></a>what
Obtiene un mensaje de error de cstring.
#### <a name="returns"></a>Devuelve
Un mensaje de error de un objeto cstring
### <a name="errortype"></a>ErrorType
Obtiene el tipo de error.
#### <a name="returns"></a>Devuelve
El tipo de error.
### <a name="geterrorname"></a>GetErrorName
Obtiene el nombre del error.
#### <a name="returns"></a>Devuelve
El nombre del error.
### <a name="getmessage"></a>GetMessage
Obtiene el mensaje de error.
#### <a name="returns"></a>Devuelve
El mensaje de error.
### <a name="setmessage"></a>SetMessage
Establece el mensaje de error.
#### <a name="parameters"></a>Parámetros
* msg El mensaje de error.