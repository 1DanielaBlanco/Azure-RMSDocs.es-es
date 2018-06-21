# <a name="class-mipaddcontentheaderaction"></a>clase mip::AddContentHeaderAction 
Una clase de acción que especifica agregar un encabezado de contenido.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public const std::string& GetUIElementName()  |  Una API que se utiliza para marcar el elemento del encabezado de contenido.
 public const std::string& GetText() const  |  Obtiene el texto que está pensado para ir en el encabezado de contenido.
 public const std::string& GetFontName() const  |  Obtiene el nombre de la fuente utilizada para mostrar el encabezado de contenido.
 public int GetFontSize() const  |  Obtiene el tamaño de la fuente utilizada para mostrar el encabezado de contenido.
 public const std::string& GetFontColor() const  |  Obtiene el color de la fuente utilizada para mostrar el encabezado de contenido.
 public ContentMarkAlignment GetAlignment() const  |  Obtiene la alineación del encabezado.
 public int GetMargin() const  |  Obtiene el margen del encabezado de la parte inferior.
 public ActionType GetType() const  |  Obtiene el tipo de [Acción](class_mip_action.md).
  
## <a name="members"></a>Miembros
  
### <a name="getuielementname"></a>GetUIElementName
Una API que se utiliza para marcar el elemento del encabezado de contenido.

  
**Devuelve**: el nombre que debe utilizarse para el elemento de la interfaz de usuario que contiene el pie de página de contenido. El mismo nombre se devolverá en [RemoveContentHeaderAction](class_mip_removecontentheaderaction.md) en caso de que sea necesario quitar el encabezado de contenido.
  
### <a name="gettext"></a>GetText
Obtiene el texto que está pensado para ir en el encabezado de contenido.

  
**Devuelve**: texto de encabezado de contenido.
  
### <a name="getfontname"></a>GetFontName
Obtiene el nombre de la fuente utilizada para mostrar el encabezado de contenido.

  
**Devuelve**: nombre de la fuente, valor predeterminado si no se establece por directiva Calibri.
  
### <a name="getfontsize"></a>GetFontSize
Obtiene el tamaño de la fuente utilizada para mostrar el encabezado de contenido.

  
**Devuelve**: tamaño de fuente como un entero.
  
### <a name="getfontcolor"></a>GetFontColor
Obtiene el color de la fuente utilizada para mostrar el encabezado de contenido.

  
**Devuelve**: color de fuente como una cadena (por ejemplo, "#000000").
  
### <a name="getalignment"></a>GetAlignment
Obtiene la alineación del encabezado.

  
**Devuelve**: el enumerador ContentMarkAlignment, LEFT|RIGHT|CENTER. 
**Consulte también**: ContentMarkAlignment
  
### <a name="getmargin"></a>GetMargin
Obtiene el margen del encabezado de la parte inferior.

  
**Devuelve**: un número entero que representa los márgenes desde la parte inferior del documento (por ejemplo, 10 mm).
  
### <a name="actiontype"></a>ActionType
Obtiene el tipo de [Acción](class_mip_action.md).

  
**Devuelve**: ActionType. El tipo de acción derivada a la que puede convertirse esta clase base.