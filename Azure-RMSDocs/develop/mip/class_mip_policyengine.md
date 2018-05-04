# <a name="class-mippolicyengine"></a>clase mip::PolicyEngine 
Esta clase proporciona una interfaz para todas las funciones de motor.
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const Settings & GetSettings public const std::vector< std::shared_ptr< Label > > & ListSensitivityLabels | Muestra las etiquetas de confidencialidad asociadas con el motor de directivas.
public std::shared_ptr< ContentLabel > GetSensitivityLabelExecutionState & state) | Obtiene la etiqueta de confidencialidad del contenido existente.
public std::shared_ptr< Label > GetDefaultSensitivityLabel | Obtiene la etiqueta de confidencialidad predeterminada.
public std::vector< std::shared_ptr< Action > > ComputeActionsExecutionState & state) | Ejecuta las reglas en el motor según el estado proporcionado y devuelve la lista de acciones que se van a ejecutar.
## <a name="members"></a>Miembros
### <a name="settings"></a>Configuración
Obtiene la [configuración](#classmip_1_1_policy_engine_1_1_settings) del motor de directivas.
#### <a name="returns"></a>Devuelve
La configuración del motor de directivas. 
**Consulte también**: [mip::PolicyEngine::Settings](#classmip_1_1_policy_engine_1_1_settings)
### <a name="label"></a>Etiqueta
Muestra las etiquetas de confidencialidad asociadas con el motor de directivas.
#### <a name="returns"></a>Devuelve
Una lista de etiquetas de confidencialidad.
### <a name="contentlabel"></a>ContentLabel
Obtiene la etiqueta de confidencialidad del contenido existente.
La información necesaria para recuperar la etiqueta se obtendrá utilizando el estado de ejecución proporcionado. 
#### <a name="parameters"></a>Parámetros
* state 
#### <a name="returns"></a>Devuelve
Un objeto de etiqueta de contenido que contiene la etiqueta de confidencialidad, así como información adicional. Devuelve empty si no existe. 
**Consulte también**: [mip::ContentLabel](#classmip_1_1_content_label).
### <a name="label"></a>Etiqueta
Obtiene la etiqueta de confidencialidad predeterminada.
#### <a name="returns"></a>Devuelve
La etiqueta de confidencialidad predeterminada si existe, nullptr si no hay ningún conjunto de etiquetas predeterminado.
### <a name="action"></a>Acción
Ejecuta las reglas en el motor según el estado proporcionado y devuelve la lista de acciones que se van a ejecutar.
#### <a name="parameters"></a>Parámetros
* state el estado de ejecución actual del contenido en donde se ejecutan las reglas. 
#### <a name="returns"></a>Devuelve
La lista de acciones que deben aplicarse en el contenido.