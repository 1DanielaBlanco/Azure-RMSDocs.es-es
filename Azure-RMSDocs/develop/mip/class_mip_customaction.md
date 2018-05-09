# <a name="class-mipcustomaction"></a>clase mip::CustomAction 
[CustomAction](#classmip_1_1_custom_action) es una clase de acción genérica que captura todas las subpropiedades de la acción como un contenedor de propiedades. El autor de llamada es responsable de entender el significado de la acción.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const std::vector<std::pair<std::string, std::string>>& GetProperties() const  |  Obtiene la lista de pares de clave-valor de propiedades.
public ActionType GetType() const  |  Obtiene el tipo de [Acción](#classmip_1_1_action).
  
## <a name="members"></a>Miembros
  
### <a name="getproperties"></a>GetProperties
Obtiene la lista de pares de clave-valor de propiedades.
  
#### <a name="returns"></a>Devuelve
Una lista de pares de clave-valor.
  
### <a name="actiontype"></a>ActionType
Obtiene el tipo de [Acción](#classmip_1_1_action).
  
#### <a name="returns"></a>Devuelve
ActionType El tipo de acción derivada a la que puede convertirse esta clase base.