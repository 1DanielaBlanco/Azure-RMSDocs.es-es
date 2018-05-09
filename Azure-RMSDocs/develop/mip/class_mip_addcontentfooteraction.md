# <a name="class-mipaddcontentfooteraction"></a>clase mip::AddContentFooterAction 
Una clase de acción que especifica agregar un pie de página de contenido al documento.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  Una API que se utiliza para marcar el elemento del pie de página de contenido.
public const std::string& GetText() const  |  Obtiene el texto que está pensado para ir en el pie de página de contenido.
public const std::string& GetFontName() const  |  Obtiene el nombre de la fuente utilizada para mostrar el pie de página de contenido.
public int GetFontSize() const  |  Obtiene el tamaño de la fuente utilizada para mostrar el pie de página de contenido.
public const std::string& GetFontColor() const  |  Obtiene el color de la fuente utilizada para mostrar el pie de página de contenido.
public ContentMarkAlignment GetAlignment() const  |  Obtiene la alineación del pie de página.
public int GetMargin() const  |  Obtiene el margen del pie de página de la parte inferior.
public ActionType GetType() const  |  Obtiene el tipo de [Acción](#classmip_1_1_action).
  
## <a name="members"></a>Miembros
  
### <a name="getuielementname"></a>GetUIElementName
Una API que se utiliza para marcar el elemento del pie de página de contenido.
  
#### <a name="returns"></a>Devuelve
El nombre que debe utilizarse para el elemento de la interfaz de usuario que contiene el pie de página de contenido. El mismo nombre se devolverá en [RemoveContentFooterAction](#classmip_1_1_remove_content_footer_action) en caso de que sea necesario quitar el pie de página de contenido.
  
### <a name="gettext"></a>GetText
Obtiene el texto que está pensado para ir en el pie de página de contenido.
  
#### <a name="returns"></a>Devuelve
texto de pie de página de contenido.
  
### <a name="getfontname"></a>GetFontName
Obtiene el nombre de la fuente utilizada para mostrar el pie de página de contenido.
  
#### <a name="returns"></a>Devuelve
Nombre de la fuente, valor predeterminado si no se establece por directiva Calibri.
  
### <a name="getfontsize"></a>GetFontSize
Obtiene el tamaño de la fuente utilizada para mostrar el pie de página de contenido.
  
#### <a name="returns"></a>Devuelve
Tamaño de fuente como un entero.
  
### <a name="getfontcolor"></a>GetFontColor
Obtiene el color de la fuente utilizada para mostrar el pie de página de contenido.
  
#### <a name="returns"></a>Devuelve
Color de fuente como una cadena (por ejemplo, "#000000").
  
### <a name="getalignment"></a>GetAlignment
Obtiene la alineación del pie de página.
  
#### <a name="returns"></a>Devuelve
El enumerador ContentMarkAlignment, LEFT|RIGHT|CENTER. 
**Consulte también**: ContentMarkAlignment
  
### <a name="getmargin"></a>GetMargin
Obtiene el margen del pie de página de la parte inferior.
  
#### <a name="returns"></a>Devuelve
Un número entero que representa los márgenes desde la parte inferior del documento (por ejemplo, 10 mm).
  
### <a name="actiontype"></a>ActionType
Obtiene el tipo de [Acción](#classmip_1_1_action).
  
#### <a name="returns"></a>Devuelve
ActionType El tipo de acción derivada a la que puede convertirse esta clase base.