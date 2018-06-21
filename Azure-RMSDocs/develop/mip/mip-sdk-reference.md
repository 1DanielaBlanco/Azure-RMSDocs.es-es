# <a name="mip-sdk-for-c-preview-reference"></a>Referencia de SDK de MIP para C++ (versión preliminar)

El SDK de Microsoft Information Protection (MIP) para C++ (versión preliminar) permite a los desarrolladores administrar y aplicar políticas de protección de datos a datos y otros recursos digitales.  

Para obtener más información, consulte el [blog para desarrolladores de MIP](https://aka.ms/MIPDevelopers) y [ejemplos de MIP](https://aka.ms/mipsdksamples).

El SDK de MIP para C++ incluye las siguientes clases:

| Nombre de clase | Descripción |
| :----------|:------------|
[mip::Action](class_mip_action.md) | Clase base para todas las acciones. |
[mip::AddContentFooterAction](class_mip_addcontentfooteraction.md) | Una clase de acción que especifica agregar un pie de página de contenido al documento.
[mip::addContentHeaderAction](class_mip_addcontentheaderaction.md) | Una clase de acción que especifica agregar un encabezado de contenido.
[mip::AddWatermarkAction](class_mip_addwatermarkaction.md) | Una clase de acción que especifica agregar una marca de agua.
[mip::BadInputError](class_mip_badinputerror.md) | Error de entrada incorrecta, la entrada a la API no era válida.
[mip::CommonRights](class_mip_commonrights.md) | Derechos universalmente admitidos.
[mip::Consent](class_mip_consent.md) | Representa la aceptación o rechazo de un usuario para permitir una acción.
[mip::ConsentCallback](class_mip_consentcallback.md) | Interfaz para las notificaciones de solicitud de consentimiento.
[mip::ConsentResult](class_mip_consentresult.md) | Describe el resultado de la solicitud de consentimiento tras la interacción del usuario.
[mip::ContentLabel](class_mip_contentlabel.md) | Abstracción para una etiqueta de Microsoft Information Protection que se aplica a un fragmento de contenido, normalmente un documento.
[mip::CustomAction](class_mip_customaction.md) | Clase de acción genérica que captura todas las subpropiedades de la acción como un contenedor de propiedades.
[mip::CustomProtectedStream](class_mip_customprotectedstream.md) | Ajusta un flujo para proporcionar cifrado y descifrado transparente en la lectura y escritura.
[mip::EditableDocumentRights](class_mip_editabledocumentrights.md) | Derechos que se aplican a documentos editables.
[mip::EmailRights](class_mip_emailrights.md) | Derechos que se aplican al correo electrónico.
[mip::Error](class_mip_error.md) | La clase base para todos los errores que se notificarán (se producen o se devuelven) del SDK de MIP.
[mip::ExecutionState](class_mip_executionstate.md) | Interfaz a todos los estados necesarios para ejecutar el motor.
[mip::FileEngine](class_mip_fileengine.md) | Interfaz para todas las funciones de motor.
[mip::FileEngine::Settings](class_mip_fileengine_settings.md) | 
[mip::FileHandler](class_mip_filehandler.md) | Interfaz a todas las funciones de control de archivos.
[mip::FileHandler::Observer](class_mip_filehandler_observer.md) | Interfaz de Observer para que los clientes obtengan notificaciones de eventos relacionados con el controlador de archivos.
[mip::FileIOError](class_mip_fileioerror.md) | Error de E/S de archivo.
[mip::FileProfile](class_mip_fileprofile.md) | Clase raíz para las operaciones de Microsoft Information Protection.
[mip::FileProfile::Observer](class_mip_fileprofile_observer.md) | Interfaz de Observer que se utiliza para recibir las notificaciones de eventos relacionados con los perfiles.
[mip::FileProfile::Settings](class_mip_fileprofile_settings.md) | Interfaz para administrar la configuración de perfil de archivo.
[mip::GetUserPolicyResult](class_mip_getuserpolicyresult.md) | Describe los resultados de una solicitud de adquisición de directiva de usuario.
[mip::InternalError](class_mip_internalerror.md) | Error de sdk interno. Se produjo un problema inesperado.
[mip::IStream](class_mip_istream.md) | Interfaz base para los flujos protegidos.
[mip::JustificationRequiredError](class_mip_justificationrequirederror.md) | El cambio solicitado requiere una explicación del cambio.
[mip::JustifyAction](class_mip_justifyaction.md) | La solicitud requiere la justificación a una degradación de la etiqueta y el establecimiento de la respuesta en el estado de ejecución.
[mip::Label](class_mip_label.md) | Abstracción para una única etiqueta de Microsoft Information Protection.
[mip::LabelingOptions](class_mip_labelingoptions.md) | Interfaz para configurar las opciones de etiquetado para el método SetLabel.
[mip::MetadataAction](class_mip_metadataaction.md) | Una acción que especifica la información de metadatos que se agregará al contenido.
[mip::NetworkError](class_mip_networkerror.md) | Error de red.
[mip::NotSupportedError](class_mip_notsupportederror.md) | Error de operación no admitida.
[mip::PolicyDescriptor](class_mip_policydescriptor.md) | Representa una directiva ad-hoc asociada al contenido protegido.
[mip::PolicyEngine](class_mip_policyengine.md) | Esta clase proporciona una interfaz para todas las funciones de motor.
[mip::PolicyEngine::Settings](class_mip_policyengine_settings.md) | Se debe proporcionar una instancia de esta clase con los parámetros apropiados para iniciar un motor.
[mip::PrivilegedRequiredError](class_mip_privilegedrequirederror.md) | La etiqueta actual se estableció por el método de asignación con privilegios y no se puede reemplazar.
[mip::Profile](class_mip_profile.md) | Clase raíz para las operaciones de Microsoft Information Protection.
[mip::Profile::Observer](class_mip_profile_observer.md) | Interfaz que se utiliza para recibir las notificaciones de eventos relacionados con los perfiles.
[mip::Profile::Settings](class_mip_profile_settings.md) | Configura los ajustes de perfil.
[mip::ProtectAdhocAction](class_mip_protectadhocaction.md) | Una clase de acción que especifica agregar la protección ad-hoc al documento.  
[mip::ProtectbyTemplateAction](class_mip_protectbytemplateaction.md) | Una clase de acción que especifica agregar la protección por plantilla al documento.
[mip::ProtectDoNotForwardAction](class_mip_protectdonotforwardaction.md) | Una clase de acción que especifica agregar la protección de no reenvío al documento.
[mip::ProtectionProfile](class_mip_protectionprofile.md) | Clase base utilizada para realizar las operaciones de protección.
[mip::ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) | Se utiliza para recibir notificaciones de perfil de protección.
[mip::ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) | Configuración de perfil de protección utilizada durante la vigencia de la instancia.
[mip::RemoveContentFooterAction](class_mip_removecontentfooteraction.md) | Una clase de acción que especifica quitar el pie de página de contenido del documento.
[mip::RemoveContentHeaderAction](class_mip_removecontentheaderaction.md) | Una clase de acción que especifica quitar el encabezado de contenido del documento.
[mip::RemoveProtectionAction](class_mip_removeprotectionaction.md) | Una clase de acción que especifica quitar la protección del documento.
[mip::RemoveWatermarkAction](class_mip_removewatermarkaction.md) | Una clase de acción que especifica quitar la marca de agua del documento.
[mip::RMSCryptographyException](class_mip_rmscryptographyexception.md) | Excepción de criptografía de RMS.
[mip::RMSException](class_mip_rmsexception.md) | Excepción de RMS base.
[mip::RMSInvalidArgumentException](class_mip_rmsinvalidargumentexception.md) | Excepción de argumento no válido de RMS.
[mip::RMSLogicException](class_mip_rmslogicexception.md) | Excepción de lógica de RMS.
[mip::RMSNetworkException](class_mip_rmsnetworkexception.md) | Excepción de red de RMS.
[mip::RMSNotFoundException](class_mip_rmsnotfoundexception.md) | RMS no encontró la excepción.
[mip::RMSNullPointerException](class_mip_rmsnullpointerexception.md) | Excepción de puntero nulo de RMS.
[mip::RMSOfficeFileException](class_mip_rmsofficefileexception.md) | Excepción de archivo de Office de RMS.
[mip::RMSPFileException](class_mip_rmspfileexception.md) | Excepción de PFile de RMS.
[mip::RMSRightsException](class_mip_rmsrightsexception.md) | Excepción de derechos de RMS.
[mip::RMSStreamException](class_mip_rmsstreamexception.md) | Excepción de flujo de RMS
[mip::Roles](class_mip_roles.md) | Define los roles para proteger los datos.
[mip::Stream](class_mip_stream.md) | Una clase que define la interfaz entre el SDK de MIP y el contenido basado en el flujo.
[mip::TemplateDescriptor](class_mip_templatedescriptor.md) | Describe una plantilla de RMS.
[mip::UserPolicy](class_mip_userpolicy.md) | Representa una directiva asociada al contenido protegido.
[mip::UserRights](class_mip_userrights.md) | Representa un grupo de usuarios y los derechos asociados con ellos.
[mip::UserRoles](class_mip_userroles.md) | Representa un grupo de usuarios y los roles asociados con ellos.
 
