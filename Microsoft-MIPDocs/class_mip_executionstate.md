# <a name="class-mipexecutionstate"></a>clase mip::ExecutionState 
Interfaz a todos los estados necesarios para ejecutar el motor.
Los clientes solo deben llamar a los métodos para obtener el estado que se necesita. Por lo tanto, por razones de eficiencia, los clientes pueden querer implementar esta interfaz de manera que el estado correspondiente se calcule dinámicamente en lugar de calcular por adelantado.
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public std::string GetNewLabelId | Obtiene el identificador de la etiqueta de confidencialidad que debe aplicarse en el documento.
public bool IsDowngradeJustified | La implementación debe aprobar si se ha dado o no una justificación para degradar una etiqueta existente.
public AssignmentMethod GetNewLabelAssignmentMethod | Obtiene el método de asignación de la nueva etiqueta.
public std::vector< std::pair< std::string, std::string > > GetContentMetadata | Obtiene los elementos de metadatos del contenido.
public std::string GetTemplateId | Obtiene el identificador de la plantilla de protección del servicio de Rights Management.
public ContentFormat GetContentFormat | Obtiene el formato del contenido.
public const ActionType GetSupportedActions
## <a name="members"></a>Miembros
### <a name="getnewlabelid"></a>GetNewLabelId
Obtiene el identificador de la etiqueta de confidencialidad que debe aplicarse en el documento.
#### <a name="returns"></a>Devuelve
El identificador de la etiqueta de sensibilidad que se va a aplicar al contenido si existe, en caso contrario, se quita la etiqueta.
### <a name="isdowngradejustified"></a>IsDowngradeJustified
La implementación debe aprobar si se ha dado o no una justificación para degradar una etiqueta existente.
#### <a name="returns"></a>Devuelve
True si la degradación ya está justificada, false si aún no se ha justificado. 
**Consulte también**: [mip::JustifyAction](#classmip_1_1_justify_action)
### <a name="getnewlabelassignmentmethod"></a>GetNewLabelAssignmentMethod
Obtiene el método de asignación de la nueva etiqueta.
#### <a name="returns"></a>Devuelve
El método de asignación STANDARD, PRIVILEGED, AUTO. 
**Consulte también**: mip::AssignmentMethod
### <a name="getcontentmetadata"></a>GetContentMetadata
Obtiene los elementos de metadatos del contenido.
#### <a name="returns"></a>Devuelve
Un vector de pares de clave-valor que representan los metadatos aplicados al contenido. Cada elemento de metadatos es un par de nombre y valor.
### <a name="gettemplateid"></a>GetTemplateId
Obtiene el identificador de la plantilla de protección del servicio de Rights Management.
#### <a name="returns"></a>Devuelve
El identificador de la plantilla de protección del servicio de Rights Management si existe; de lo contrario, en un formato GUID, devuelve una cadena vacía.
### <a name="getcontentformat"></a>GetContentFormat
Obtiene el formato del contenido.
#### <a name="returns"></a>Devuelve
DEFAULT, EMAIL **Consulte también**: mip::ContentFormat
### <a name="actiontype"></a>ActionType
Devuelve una lista de acciones que admite la aplicación. Se muestran todos los tipos de acciones en [mip/upe/action.h](#action_8h).