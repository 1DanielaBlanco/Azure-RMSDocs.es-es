# <a name="mip-sdk-for-c-preview-reference"></a>Referencia de SDK de MIP para C++ (versión preliminar)

El SDK de Microsoft Information Protection (MIP) para C++ (versión preliminar) permite a los desarrolladores administrar y aplicar políticas de protección de datos a datos y otros recursos digitales.  

Para obtener más información, consulte el [blog para desarrolladores de MIP](https://aka.ms/MIPDevelopers) y [ejemplos de MIP](https://aka.ms/mipsdksamples).

El SDK de MIP para C++ incluye:

- [Enumeraciones y estructuras](mip-enums-and-structs.md)
- [Funciones](mip-functions.md)
- Las clases siguientes:

| Nombre de clase | Descripción |
| :----------|:------------|
[ConsentDelegate](class_consentdelegate.md)  |  Delegado para operaciones relacionadas con el consentimiento.
[mip::AccessDeniedError](class_mip_accessdeniederror.md)  |  El usuario no pudo obtener acceso al contenido. Por ejemplo, no hay permisos, se ha revocado el contenido,etc.
[mip::Action](class_mip_action.md)  |  Interfaz para una acción. Cada acción se traduce en una medida que debe adoptar la aplicación para aplicar la etiqueta (como se define en la directiva).
[mip::AddContentFooterAction](class_mip_addcontentfooteraction.md)  |  Una clase de acción que especifica agregar un pie de página de contenido al documento.
[mip::AddContentHeaderAction](class_mip_addcontentheaderaction.md)  |  Una clase de acción que especifica agregar un encabezado de contenido.
[mip::AddWatermarkAction](class_mip_addwatermarkaction.md)  |  Una clase de acción que especifica agregar una marca de agua.
[mip::ApplyLabelAction](class_mip_applylabelaction.md)  |  La aplicación de acciones de la etiqueta requiere que la aplicación que realiza la llamada aplique una etiqueta específica.
[mip::BadInputError](class_mip_badinputerror.md)  |  Error de entrada incorrecta, se produce cuando la entrada a una API de SDK no es válida.
[mip::ClassificationResult](class_mip_classificationresult.md)  |  Clase que contiene el resultado de una llamada de clasificación en el estado de ejecución.
[mip::ContentLabel](class_mip_contentlabel.md)  |  Abstracción para una etiqueta de Microsoft Information Protection que se aplica a un fragmento de contenido, normalmente un documento.
[mip::CustomAction](class_mip_customaction.md)  |  [CustomAction](class_mip_customaction.md) es una clase de acción genérica que captura todas las subpropiedades de la acción como un contenedor de propiedades. El autor de llamada es responsable de entender el significado de la acción.
[mip::Error](class_mip_error.md)  |  La clase base para todos los errores que se notificarán (se producen o se devuelven) del SDK de MIP.
[mip::ExecutionState](class_mip_executionstate.md)  |  Interfaz a todos los estados necesarios para ejecutar el motor.
[mip::FileEngine](class_mip_fileengine.md)  |  Interfaz para todas las funciones de motor.
[mip::FileEngine::Settings](class_mip_fileengine::settings.md)  | _No se ha documentado todavía._
[mip::FileHandler](class_mip_filehandler.md)  |  Interfaz a todas las funciones de control de archivos.
[mip::FileHandler::Observer](class_mip_filehandler::observer.md)  |  Interfaz de [Observer](class_mip_filehandler_observer.md) para que los clientes obtengan notificaciones de eventos relacionados con el controlador de archivos.
[mip::FileIOError](class_mip_fileioerror.md)  |  Error de E/S de archivo.
[mip::FileProfile](class_mip_fileprofile.md)  |  La clase [FileProfile](class_mip_fileprofile.md) es la clase raíz para el uso de las operaciones de Microsoft Information Protection.
[mip::FileProfile::Observer](class_mip_fileprofile_observer.md)  |  Interfaz de [Observer](class_mip_fileprofile_observer.md) para que los clientes obtengan notificaciones de eventos relacionados con el perfil.
[mip::FileProfile::Settings](class_mip_fileprofile_settings.md)  |  [Configuración](class_mip_fileprofile_settings.md) utilizada por [FileProfile](class_mip_fileprofile.md) durante su creación y a lo largo de su vigencia.
[mip::InternalError](class_mip_internalerror.md)  |  Error interno. Este error se produce cuando ocurre algo inesperado durante la ejecución.
[mip::JustificationRequiredError](class_mip_justificationrequirederror.md)  | _No se ha documentado todavía._
[mip::JustifyAction](class_mip_justifyaction.md)  |  La [acción](class_mip_action.md) justificar requiere que se facilite una justificación para una degradación de la etiqueta y el establecimiento de la respuesta en el estado de ejecución.
[mip::Label](class_mip_label.md)  |  Abstracción para una única etiqueta de Microsoft Information Protection.
[mip::LabelingOptions](class_mip_labelingoptions.md)  |  Interfaz para configurar las opciones de etiquetado para el método SetLabel.
[mip::LoggerDelegate](class_mip_loggerdelegate.md)  |  Una clase que define la interfaz para el registrador de SDK de MIP.
[mip::MetadataAction](class_mip_metadataaction.md)  |  Una [acción](class_mip_action.md) que agrega información de metadatos al contenido.
[mip::NetworkError](class_mip_networkerror.md)  |  Error de red. Se produjo por un comportamiento inesperado al realizar llamadas de red a los puntos de conexión de servicio.
[mip::NotSupportedError](class_mip_notsupportederror.md)  |  La operación solicitada por la aplicación no es compatible con el SDK.
[mip::PolicyEngine](class_mip_policyengine.md)  |  Esta clase proporciona una interfaz para todas las funciones de motor.
[mip::PolicyEngine::Settings](class_mip_policyengine_settings.md)  |  Se debe proporcionar una instancia de esta clase con los parámetros apropiados para iniciar un motor.
[mip::PrivilegedRequiredError](class_mip_privilegedrequirederror.md)  |  Se asignó la etiqueta actual como una operación con privilegios (equivalente a una operación de administrador), por lo tanto, no puede reemplazarse.
[mip::Profile](class_mip_profile.md)  |  La clase [Profile](class_mip_profile.md) es la clase raíz para el uso de las operaciones de Microsoft Information Protection. Una aplicación típica solo necesitará un [perfil ](class_mip_profile.md) pero puede crear varios perfiles si es necesario.
[mip::Profile::Observer](class_mip_profile_observer.md)  |  Interfaz de [Observer](class_mip_profile_observer.md) para que los clientes obtengan notificaciones de eventos relacionados con el perfil.
[mip::Profile::Settings](class_mip_profile_settings.md)  |  [Configuración](class_mip_profile_settings.md) utilizada por [Profile](class_mip_profile.md) durante su creación y a lo largo de su vigencia.
[mip::ProtectAdhocAction](class_mip_protectadhocaction.md)  |  Una clase de acción que especifica agregar la protección ad-hoc al documento.
[mip::ProtectByTemplateAction](class_mip_protectbytemplateaction.md)  |  Una clase de acción que especifica agregar la protección por plantilla al documento.
[mip::ProtectDoNotForwardAction](class_mip_protectdonotforwardaction.md)  |  Una clase de acción que especifica agregar la protección de no reenvío al documento.
[mip::ProtectionDescriptor](class_mip_protectiondescriptor.md)  |  Representa una directiva ad-hoc asociada al contenido protegido.
[mip::ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md)  |  Representa una directiva ad-hoc asociada al contenido protegido.
[mip::ProtectionEngine](class_mip_protectionengine.md)  |  Realiza acciones relacionadas con la protección respecto de una identidad específica.
[mip::ProtectionEngine::Observer](class_mip_protectionengine_observer.md)  |  Interfaz que recibe las notificaciones relacionadas con [ProtectionEngine](class_mip_protectionengine.md).
[mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md)  |  [Configuración](class_mip_protectionengine_settings.md) utilizada por [ProtectionEngine](class_mip_protectionengine.md) durante su creación y a lo largo de su vigencia.
[mip::ProtectionHandler](class_mip_protectionhandler.md)  |  Realiza acciones relacionadas con la protección para una configuración de protección específica (es decir, usuarios, derechos, roles, etc.)
[mip::ProtectionHandler::Observer](class_mip_protectionhandler_observer.md)  |  Interfaz que recibe las notificaciones relacionadas con [ProtectionHandler](class_mip_protectionhandler.md).
[mip::ProtectionProfile](class_mip_protectionprofile.md)  |  [ProtectionProfile](class_mip_protectionprofile.md) es la clase raíz para realizar las operaciones de protección.
[mip::ProtectionProfile::Observer](class_mip_protectionprofile_observer.md)  |  Interfaz que recibe las notificaciones relacionadas con [ProtectionProfile](class_mip_protectionprofile.md).
[mip::ProtectionProfile::Settings](class_mip_protectionprofile_settings.md)  |  [Configuración](class_mip_protectionprofile_settings.md) utilizada por [ProtectionProfile](class_mip_protectionprofile.md) durante su creación y a lo largo de su vigencia.
[mip::RecommendLabelAction](class_mip_recommendlabelaction.md)  |  Las acciones de recomendación de etiquetas están pensadas para sugerir una etiqueta a los usuarios. La supresión de esta llamada después de que un usuario ignore la etiqueta recomendada debe realizarse a través de las acciones admitidas en el estado de ejecución.
[mip::RemoveContentFooterAction](class_mip_removecontentfooteraction.md)  |  Una clase de acción que especifica quitar el pie de página de contenido del documento.
[mip::RemoveContentHeaderAction](class_mip_removecontentheaderaction.md)  |  Una clase de acción que especifica quitar el encabezado de contenido del documento.
[mip::RemoveProtectionAction](class_mip_removeprotectionaction.md)  |  Una clase de acción que especifica quitar la protección del documento.
[mip::RemoveWatermarkAction](class_mip_removewatermarkaction.md)  |  Una clase de acción que especifica quitar la marca de agua del documento.
[mip::Stream](class_mip_stream.md)  |  Una clase que define la interfaz entre el SDK de MIP y el contenido basado en el flujo.
[mip::UserRights](class_mip_userrights.md)  |  Representa un grupo de usuarios y los derechos asociados con ellos.
[mip::UserRoles](class_mip_userroles.md)  |  Representa un grupo de usuarios y los roles asociados con ellos.

 
