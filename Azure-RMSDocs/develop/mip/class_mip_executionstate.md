# <a name="class-mipexecutionstate"></a>clase mip::ExecutionState 
Interfaz a todos los estados necesarios para ejecutar el motor.
Los clientes solo deben llamar a los métodos para obtener el estado que se necesita. Por lo tanto, por razones de eficiencia, los clientes pueden querer implementar esta interfaz de manera que el estado correspondiente se calcule dinámicamente en lugar de calcular por adelantado.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public std::string GetNewLabelId() const  |  Obtiene el identificador de la etiqueta de confidencialidad que debe aplicarse en el documento.
 public bool IsDowngradeJustified() const  |  La implementación debe aprobar si se ha dado o no una justificación para degradar una etiqueta existente.
 public AssignmentMethod GetNewLabelAssignmentMethod() const  |  Obtiene el método de asignación de la nueva etiqueta.
public std::vector<std::pair<std::string, std::string>> GetContentMetadata(const std::vector<std::string>& names, const std::vector<std::string>& namePrefixes) const  |  Obtiene los elementos de metadatos del contenido.
 public std::string GetTemplateId() const  |  Obtiene el identificador de la plantilla de protección del servicio de Rights Management.
 public ContentFormat GetContentFormat() const  |  Obtiene el formato del contenido.
 public const ActionType GetSupportedActions() const  |  Devuelve una lista de acciones que admite la aplicación. Se muestran todos los tipos de acciones en [mip/upe/action.h](#action).
  
## <a name="members"></a>Miembros
  
### <a name="getnewlabelid"></a>GetNewLabelId
Obtiene el identificador de la etiqueta de confidencialidad que debe aplicarse en el documento.

  
**Devuelve**: identificador de la etiqueta de confidencialidad que se va a aplicar al contenido, si existe; en caso contrario, está vacío para quitar la etiqueta.
  
### <a name="isdowngradejustified"></a>IsDowngradeJustified
La implementación debe aprobar si se ha dado o no una justificación para degradar una etiqueta existente.

  
**Devuelve**: true si la degradación ya está justificada, false si aún no se ha justificado. 
**Consulte también**: [mip::JustifyAction](class_mip_justifyaction.md)
  
### <a name="getnewlabelassignmentmethod"></a>GetNewLabelAssignmentMethod
Obtiene el método de asignación de la nueva etiqueta.

  
**Devuelve**: el método de asignación STANDARD, PRIVILEGED, AUTO. 
**Consulte también**: mip::AssignmentMethod
  
### <a name="getcontentmetadata"></a>GetContentMetadata
Obtiene los elementos de metadatos del contenido.

  
**Devuelve**: un vector de pares de clave-valor que representan los metadatos aplicados al contenido. Cada elemento de metadatos es un par de nombre y valor.
  
### <a name="gettemplateid"></a>GetTemplateId
Obtiene el identificador de la plantilla de protección del servicio de Rights Management.

  
**Devuelve**: el identificador de la plantilla de protección del servicio de Rights Management si existe; de lo contrario, en un formato GUID, devuelve una cadena vacía.
  
### <a name="getcontentformat"></a>GetContentFormat
Obtiene el formato del contenido.

  
**Devuelve**: DEFAULT, EMAIL. **Consulte también**: mip::ContentFormat
  
### <a name="actiontype"></a>ActionType
Devuelve una lista de acciones que admite la aplicación. Se muestran todos los tipos de acciones en [mip/upe/action.h](#action).