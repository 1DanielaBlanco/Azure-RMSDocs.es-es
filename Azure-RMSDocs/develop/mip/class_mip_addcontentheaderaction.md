# <a name="class-mipaddcontentheaderaction"></a>clase mip::AddContentHeaderAction 
Una clase de acción que especifica agregar un encabezado de contenido.
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const std::string & GetUIElementName | Una API que se utiliza para marcar el elemento del encabezado de contenido.
public const std::string & GetText | Obtiene el texto que está pensado para ir en el encabezado de contenido.
public const std::string & GetFontName | Obtiene el nombre de la fuente utilizada para mostrar el encabezado de contenido.
public int GetFontSize | Obtiene el tamaño de la fuente utilizada para mostrar el encabezado de contenido.
public const std::string & GetFontColor | Obtiene el color de la fuente utilizada para mostrar el encabezado de contenido.
public ContentMarkAlignment GetAlignment | Obtiene la alineación del encabezado.
public int GetMargin | Obtiene el margen del encabezado de la parte inferior.
public ActionType GetType
## <a name="members"></a>Miembros
### <a name="getuielementname"></a>GetUIElementName
Una API que se utiliza para marcar el elemento del encabezado de contenido.
#### <a name="returns"></a>Devuelve
El nombre que debe utilizarse para el elemento de la interfaz de usuario que contiene en encabezado de contenido. El mismo nombre se devolverá en [RemoveContentHeaderAction](#classmip_1_1_remove_content_header_action) en caso de que sea necesario quitar el encabezado de contenido.
### <a name="gettext"></a>GetText
Obtiene el texto que está pensado para ir en el encabezado de contenido.
#### <a name="returns"></a>Devuelve
texto de encabezado de contenido.
### <a name="getfontname"></a>GetFontName
Obtiene el nombre de la fuente utilizada para mostrar el encabezado de contenido.
#### <a name="returns"></a>Devuelve
Nombre de la fuente, valor predeterminado si no se establece por directiva Calibri.
### <a name="getfontsize"></a>GetFontSize
Obtiene el tamaño de la fuente utilizada para mostrar el encabezado de contenido.
#### <a name="returns"></a>Devuelve
Tamaño de fuente como un entero.
### <a name="getfontcolor"></a>GetFontColor
Obtiene el color de la fuente utilizada para mostrar el encabezado de contenido.
#### <a name="returns"></a>Devuelve
Color de fuente como una cadena (por ejemplo, "#000000").
### <a name="getalignment"></a>GetAlignment
Obtiene la alineación del encabezado.
#### <a name="returns"></a>Devuelve
El enumerador ContentMarkAlignment, LEFT|RIGHT|CENTER. 
**Consulte también**: ContentMarkAlignment
### <a name="getmargin"></a>GetMargin
Obtiene el margen del encabezado de la parte inferior.
#### <a name="returns"></a>Devuelve
Un número entero que representa los márgenes desde la parte inferior del documento (por ejemplo, 10 mm).
### <a name="actiontype"></a>ActionType
Obtiene el tipo de [Acción](#classmip_1_1_action).
#### <a name="returns"></a>Devuelve
ActionType El tipo de acción derivada a la que puede convertirse esta clase base.