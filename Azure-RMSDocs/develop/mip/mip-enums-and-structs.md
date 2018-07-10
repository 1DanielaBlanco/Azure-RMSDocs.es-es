# <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 enum Consent       |  Representa de decisión de un usuario de consentir la conexión a un punto de conexión de servicio.
 struct ApplicationInfo  |  Identificador de la aplicación como se establece en el portal de Azure AD.
**mip** |
 enum ActionType       |  Diferentes tipos de acción
 enum ErrorType       | _No se ha documentado todavía._
 enum LogLevel       |  Diferentes niveles de registro utilizados en el SDK de mip.
 enum ProtectionHandlerCreationOptions       |  Marcas de bits que determinan el comportamiento de creación de directivas adicionales.
 enum ProtectionType       |  Describe si la protección se basa en una plantilla o se determina ad hoc (personalizada)

  
## <a name="enumerations-common"></a>Enumeraciones (común)
  
### <a name="consent"></a>Consentimiento
Representa de decisión de un usuario de consentir la conexión a un punto de conexión de servicio.

 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
AcceptAlways            | Consentir y recordar esta decisión
Aceptar            | Consentir, una sola vez
Rechazar            | No consentir
  
## <a name="enumerations-mip"></a>Enumeraciones (mip)

### <a name="actiontype"></a>ActionType

 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
ADD_CONTENT_FOOTER            | Agregue un pie de página de contenido al tipo de acción del documento.
ADD_CONTENT_HEADER            | Agregue un encabezado de contenido al tipo de acción del documento.
ADD_WATERMARK            | Agregue una marca de agua a todo el tipo de acción del documento.
PERSONALIZADO            | Un tipo de acción definida personalizado.
JUSTIFY            | Un tipo de acción de justificar.
METADATA            | Un tipo de acción de cambio de metadatos.
PROTECT_ADHOC            | Una protección por tipo de acción de directiva ad hoc.
PROTECT_BY_TEMPLATE            | Una protección por tipo de acción de plantilla.
PROTECT_DO_NOT_FORWARD            | Una protección por tipo de acción de no reenviar.
REMOVE_CONTENT_FOOTER            | Quite el tipo de acción de pie de página de contenido.
REMOVE_CONTENT_HEADER            | Quite el tipo de acción de encabezado de contenido.
REMOVE_PROTECTION            | Quite el tipo de acción de protección.
REMOVE_WATERMARK            | Quite el tipo de acción de marca de agua.
APPLY_LABEL            | Aplique el tipo de acción de etiqueta.
RECOMMEND_LABEL            | Recomiende el tipo de acción de etiqueta.
Diferentes tipos de acción.
CUSTOM es el tipo de acción genérico. Todos los demás tipos de acción son una acción específica con un significado específico.
  
Los valores de **ActionType** admiten los siguientes operadores:

* Operador Or (|) para la enumeración de tipo [Action](class_mip_action.md)  
* Operador And (&) para la enumeración de tipo [Action](class_mip_action.md)  
* Operador Xor (^) para la enumeración de tipo [Action](class_mip_action.md)  

### <a name="errortype"></a>ErrorType

 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
BAD_INPUT_ERROR            | El autor de la llamada pasó una entrada incorrecta.
FILE_IO_ERROR            | Error de E/S de archivo general.
NETWORK_ERROR            | Problemas generales de red; por ejemplo, servicio inaccesible.
INTERNAL_ERROR            | Errores internos inesperados. Por ejemplo, en el protocolo cliente/servidor (se recibió una respuesta no esperada).
JUSTIFICATION_REQUIRED            | Para completar la acción en el archivo se debe proporcionar una justificación.
NOT_SUPPORTED_OPERATION            | Aún no se admite la operación solicitada.
PRIVILEGED_REQUIRED            | No se puede invalidar la etiqueta con privilegios si el nuevo método de etiqueta es estándar.
ACCESS_DENIED            | El usuario no pudo obtener acceso al contenido. Por ejemplo, no hay permisos, se ha revocado el contenido,etc.
  
### <a name="loglevel"></a>LogLevel

 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
Trace            | 
Info            | 
Advertencia            | 
Error            | 
Diferentes niveles de registro utilizados en el SDK de mip.
  
### <a name="protectionhandlercreationoptions"></a>ProtectionHandlerCreationOptions

 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
Ninguno            | Ninguno
OfflineOnly            | No se permiten operaciones de red e interfaz de usuario.
AllowAuditedExtraction            | Se puede abrir contenido en una aplicación ajena al SDK de protección.
PreferDeprecatedAlgorithms            | Use algoritmos criptográficos en desuso para la compatibilidad con versiones anteriores
Marcas de bits que determinan el comportamiento de creación de directivas adicionales.
  
### <a name="protectiontype"></a>ProtectionType

 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
TemplateBased            | Se creó un controlador a partir de una plantilla
Personalizada            | Se creó un controlador ad hoc
Describe si la protección se basa en una plantilla o se determina ad hoc (personalizada)
  
### <a name="protectionhandlercreationoptions"></a>ProtectionHandlerCreationOptions

Operador OR bit a bit de ProtectionHandlerCreationOptions.

Parámetros: 
 
* **a**: valor izquierdo 

* **b**: valor derecho
  
**Devuelve**: operador OR bit a bit de parámetros
  


## <a name="structures"></a>Estructuras

### <a name="applicationinfo"></a>ApplicationInfo 
Identificador de la aplicación como se establece en el portal de Azure AD.
  
 Campos                        | Descripciones                                
--------------------------------|---------------------------------------------
 public std::string applicationId  | Identificador de la aplicación en el portal de Azure AD.
 public std::string friendlyName  | Nombre descriptivo de la aplicación, como se especifica en el portal.
  
