# <a name="class-mippolicyengine"></a>clase mip::PolicyEngine 
Esta clase proporciona una interfaz para todas las funciones de motor.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Obtiene la [configuración](class_mip_policyengine_settings.md) del motor de directivas.
public const std::vector<std::shared_ptr<Label>>& ListSensitivityLabels()  |  Muestra las etiquetas de confidencialidad asociadas con el motor de directivas.
public std::shared_ptr<ContentLabel> GetSensitivityLabel(const ExecutionState& state)  |  Obtiene la etiqueta de confidencialidad del contenido existente.
public std::shared_ptr<Label> GetDefaultSensitivityLabel()  |  Obtiene la etiqueta de confidencialidad predeterminada.
public std::vector<std::shared_ptr<Action>> ComputeActions(const ExecutionState& state)  |  Ejecuta las reglas en el motor según el estado proporcionado y devuelve la lista de acciones que se van a ejecutar.
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Obtiene la [configuración](class_mip_policyengine_settings.md) del motor de directivas.

  
**Devuelve**: configuración del motor de directivas. 
**Consulte también**: [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md)
  
### <a name="label"></a>Etiqueta
Muestra las etiquetas de confidencialidad asociadas con el motor de directivas.

  
**Devuelve**: una lista de etiquetas de confidencialidad.
  
### <a name="contentlabel"></a>ContentLabel
Obtiene la etiqueta de confidencialidad del contenido existente.
La información necesaria para recuperar la etiqueta se obtendrá utilizando el estado de ejecución proporcionado. 

Parámetros:  
* **state**: 



  
**Devuelve**: un objeto de etiqueta de contenido que contiene la etiqueta de confidencialidad, así como información adicional. Devuelve empty si no existe. 
**Consulte también**: [mip::ContentLabel](class_mip_contentlabel.md).
  
### <a name="label"></a>Etiqueta
Obtiene la etiqueta de confidencialidad predeterminada.

  
**Devuelve**: la etiqueta de confidencialidad predeterminada si existe, nullptr si no hay ningún conjunto de etiquetas predeterminado.
  
### <a name="action"></a>Acción
Ejecuta las reglas en el motor según el estado proporcionado y devuelve la lista de acciones que se van a ejecutar.

Parámetros:  
* **state**: el estado de ejecución actual del contenido en donde se ejecutan las reglas. 



  
**Devuelve**: la lista de acciones que deben aplicarse en el contenido.