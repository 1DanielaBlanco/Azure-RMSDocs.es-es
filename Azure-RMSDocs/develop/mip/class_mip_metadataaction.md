# <a name="class-mipmetadataaction"></a>clase mip::MetadataAction 
Una [acción](class_mip_action.md) significaba que especificaba la información de metadatos que debía agregarse al contenido.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const std::vector<std::string>& GetMetadataToRemove() const  |  Obtiene la lista de nombres de metadatos que deben quitarse del contenido.
public const std::vector<std::pair<std::string, std::string>>& GetMetadataToAdd() const  |  Obtiene la lista de metadatos como pares de clave valor. Los metadatos deben agregarse a los metadatos de contenido.
 public ActionType GetType() const  |  Obtiene el tipo de [Acción](class_mip_action.md).
  
## <a name="members"></a>Miembros
  
### <a name="getmetadatatoremove"></a>GetMetadataToRemove
Obtiene la lista de nombres de metadatos que deben quitarse del contenido.

  
**Devuelve**: un vector de cadenas para quitar. Que la eliminación de metadatos debe realizarse antes de agregar los metadatos.
  
### <a name="getmetadatatoadd"></a>GetMetadataToAdd
Obtiene la lista de metadatos como pares de clave valor. Los metadatos deben agregarse a los metadatos de contenido.

  
**Devuelve**: Const std::vector<std::pair<std::string, std::string>>& hay que quitar los metadatos antes de agregar otros.
  
### <a name="actiontype"></a>ActionType
Obtiene el tipo de [Acción](class_mip_action.md).

  
**Devuelve**: ActionType. El tipo de acción derivada a la que puede convertirse esta clase base.