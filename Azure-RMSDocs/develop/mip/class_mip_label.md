# <a name="class-miplabel"></a>clase mip::Label 
Abstracción para una única etiqueta de Microsoft Information Protection.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Obtiene el identificador de la etiqueta.
public const std::string& GetName() const  |  Obtiene el nombre de la etiqueta.
public const std::string& GetDescription() const  |  Obtiene la descripción de la etiqueta.
public const std::string& GetColor() const  |  Obtiene el color que debe mostrar la etiqueta.
public const std::string& GetOrder() const  |  Obtiene el orden de la etiqueta.
public const std::string& GetTooltip() const  |  Obtiene la descripción de la información sobre herramientas de la etiqueta.
public bool IsActive() const  |  Obtiene un valor booleano de señalización si la etiqueta está activa.
public std::weak_ptr<Label> GetParent() const  |  Obtiene la etiqueta principal.
public const std::vector<std::shared_ptr<Label>>& GetChildren() const  |  Obtiene los elementos secundarios de la etiqueta actual.
  
## <a name="members"></a>Miembros
  
### <a name="getid"></a>GetId
Obtiene el identificador de la etiqueta.
  
#### <a name="returns"></a>Devuelve
El identificador de la etiqueta.
  
### <a name="getname"></a>GetName
Obtiene el nombre de la etiqueta.
  
#### <a name="returns"></a>Devuelve
El nombre de la etiqueta.
  
### <a name="getdescription"></a>GetDescription
Obtiene la descripción de la etiqueta.
  
#### <a name="returns"></a>Devuelve
La descripción de la etiqueta.
  
### <a name="getcolor"></a>GetColor
Obtiene el color que debe mostrar la etiqueta.
  
#### <a name="returns"></a>Devuelve
color value Formato de la cadena. "#RRGGBB" donde cada RR, GG, BB es un valor hexadecimal 0-f.
  
### <a name="getorder"></a>GetOrder
Obtiene el orden de la etiqueta.
  
#### <a name="returns"></a>Devuelve
Un valor numérico atribuido como una cadena.
  
### <a name="gettooltip"></a>GetTooltip
Obtiene la descripción de la información sobre herramientas de la etiqueta.
  
#### <a name="returns"></a>Devuelve
Una cadena de información sobre herramientas.
  
### <a name="isactive"></a>IsActive
Obtiene un valor booleano de señalización si la etiqueta está activa.
Solo se pueden aplicar etiquetas activas. Las etiquetas inactivas no se puede aplicar y se usan solo con fines de visualización. 
  
#### <a name="returns"></a>Devuelve
True si la etiqueta esta activa; de lo contrario, false.
  
### <a name="label"></a>Etiqueta
Obtiene la etiqueta principal.
  
#### <a name="returns"></a>Devuelve
Un puntero débil a la etiqueta principal si existe; de lo contrario, un puntero vacío.
  
### <a name="label"></a>Etiqueta
Obtiene los elementos secundarios de la etiqueta actual.
  
#### <a name="returns"></a>Devuelve
Un vector de punteros compartidos a las etiquetas.