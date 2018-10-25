---
title: Referencia de SDK de MIP para C++ (versión preliminar)
description: Referencia de SDK de MIP para C++ (versión preliminar)
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 06d8bb26a8e3026562006d68d4ae8d1630eba81c
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446335"
---
# <a name="mip-sdk-for-c-preview-reference"></a>Referencia de SDK de MIP para C++ (versión preliminar)

El SDK de Microsoft Information Protection (MIP) para C++ (versión preliminar) permite a los desarrolladores administrar y aplicar políticas de protección de datos a datos y otros recursos digitales.  

Para obtener más información, consulte el [blog para desarrolladores de MIP](https://aka.ms/MIPDevelopers)<!-- and [MIP samples](https://aka.ms/mipsdksamples)-->.

El SDK de MIP para C++ incluye:

- [Enumeraciones y estructuras](mip-enums-and-structs.md)
- [Funciones](mip-functions.md)
- Las clases siguientes:

| Nombre de clase | Descripción |
| :----------|:------------|
[AccessDeniedError](class_mip_accessdeniederror.md)  |  El usuario no pudo obtener acceso al contenido. Por ejemplo, no hay permisos, se ha revocado el contenido, etc.
[Acción](class_mip_action.md)  |  Interfaz para una acción. Cada acción se traduce en una medida que debe adoptar la aplicación para aplicar la etiqueta (como se define en la directiva).
[AddContentFooterAction](class_mip_addcontentfooteraction.md)  |  Clase de acción que especifica que se agregue un pie de página de contenido al documento.
[AddContentHeaderAction](class_mip_addcontentheaderaction.md)  |  Una clase de acción que especifica agregar un encabezado de contenido.
[AddWatermarkAction](class_mip_addwatermarkaction.md)  |  Una clase de acción que especifica agregar una marca de agua.
[ApplyLabelAction](class_mip_applylabelaction.md)  |  La aplicación de acciones de la etiqueta requiere que la aplicación que realiza la llamada aplique una etiqueta específica.
[BadInputError](class_mip_badinputerror.md)  |  Error de entrada incorrecta; se produce cuando la entrada a una API de SDK no es válida.
[ClassificationResult](class_mip_classificationresult.md)  |  Clase que contiene el resultado de una llamada de clasificación en el estado de ejecución.
[ConsentDelegate](class_consentdelegate.md)  |  Delegado para operaciones relacionadas con el consentimiento.
[ConsentDeniedError](class_mip_consentdeniederror.md)  |  Una operación que necesitaba el consentimiento del usuario, pero que no lo ha recibido.
[ContentLabel](class_mip_contentlabel.md)  |  Abstracción para una etiqueta de Microsoft Information Protection que se aplica a un fragmento de contenido, normalmente un documento.
[CustomAction](class_mip_customaction.md)  |  [CustomAction](class_mip_customaction.md) es una clase de acción genérica que captura todas las subpropiedades de la acción como un contenedor de propiedades. El autor de llamada es responsable de entender el significado de la acción.
[Error](class_mip_error.md)  |  La clase base para todos los errores que se notificarán (se producen o se devuelven) del SDK de MIP.
[ExecutionState](class_mip_executionstate.md)  |  Interfaz a todos los estados necesarios para ejecutar el motor.
[FileEngine::Settings](class_mip_fileengine_settings.md)  | _No se ha documentado todavía._
[FileEngine](class_mip_fileengine.md)  |  Esta clase proporciona una interfaz para todas las funciones de motor.
[FileHandler::Observer](class_mip_filehandler_observer.md)  |  Interfaz de [Observer](class_mip_filehandler_observer.md) para que los clientes obtengan eventos de notificaciones relacionados con el controlador de archivos.
[FileHandler](class_mip_filehandler.md)  |  Interfaz a todas las funciones de control de archivos.
[FileIOError](class_mip_fileioerror.md)  |  Error de E/S de archivo.
[FileProfile::Observer](class_mip_fileprofile_observer.md)  |  Interfaz de [Observer](class_mip_fileprofile_observer.md) para que los clientes obtengan notificaciones de eventos relacionados con el perfil.
[FileProfile::Settings](class_mip_fileprofile_settings.md)  |  [Configuración](class_mip_fileprofile_settings.md) utilizada por [FileProfile](class_mip_fileprofile.md) durante su creación y a lo largo de su vigencia.
[FileProfile](class_mip_fileprofile.md)  |  La clase [FileProfile](class_mip_fileprofile.md) es la clase raíz para el uso de las operaciones de Microsoft Information Protection.
[HttpDelegate](class_mip_httpdelegate.md)  |  Interfaz para reemplazar el control de HTTP.
[HttpRequest](class_mip_httprequest.md)  |  Interfaz que describe una única solicitud HTTP.
[HttpResponse](class_mip_httpresponse.md)  |  Interfaz que describe una única respuesta HTTP, implementada por la aplicación cliente cuando se reemplaza [HttpDelegate](class_mip_httpdelegate.md).
[InternalError](class_mip_internalerror.md)  |  Error interno. Este error se produce cuando ocurre algo inesperado durante la ejecución.
[JustificationRequiredError](class_mip_justificationrequirederror.md)  | _No se ha documentado todavía._
[JustifyAction](class_mip_justifyaction.md)  |  La [acción](class_mip_action.md) justificar requiere que se facilite una justificación para una degradación de la etiqueta y el establecimiento de la respuesta en el estado de ejecución.
[Etiqueta](class_mip_label.md)  |  Abstracción para una única etiqueta de Microsoft Information Protection.
[LabelingOptions](class_mip_labelingoptions.md)  |  Interfaz para configurar las opciones de etiquetado para los métodos SetLabel y DeleteLabel.
[LoggerDelegate](class_mip_loggerdelegate.md)  |  Una clase que define la interfaz para el registrador de SDK de MIP.
[MetadataAction](class_mip_metadataaction.md)  |  Una [acción](class_mip_action.md) que agrega información de metadatos al contenido.
[NetworkError](class_mip_networkerror.md)  |  Error de red. Se produjo por un comportamiento inesperado al realizar llamadas de red a los puntos de conexión de servicio.
[NotSupportedError](class_mip_notsupportederror.md)  |  La operación solicitada por la aplicación no es compatible con el SDK.
[PolicyEngine::Settings](class_mip_policyengine_settings.md)  |  Define la configuración asociada a un elemento [PolicyEngine](class_mip_policyengine.md).
[PolicyEngine](class_mip_policyengine.md)  |  Esta clase proporciona una interfaz para todas las funciones de motor.
[PolicyHandler](class_mip_policyhandler.md)  |  Esta clase proporciona una interfaz para todas las funciones de controlador de directiva de un archivo.
[PolicyProfile::Observer](class_mip_policyprofile_observer.md)  |  Interfaz de [Observer](class_mip_policyprofile_observer.md) para que los clientes obtengan notificaciones de eventos relacionados con el perfil.
[PolicyProfile::Settings](class_mip_policyprofile_settings.md)  |  [Configuración](class_mip_policyprofile_settings.md) que usa [PolicyProfile](class_mip_policyprofile.md) durante su creación y vigencia.
[PolicyProfile](class_mip_policyprofile.md)  |  [PolicyProfile](class_mip_policyprofile.md) es la clase raíz para usar las operaciones de Microsoft Information Protection. Una aplicación típica solo necesitará un elemento [PolicyProfile](class_mip_policyprofile.md), pero puede crear varios perfiles si es necesario.
[PolicySyncError](class_mip_policysyncerror.md)  |  No se pudieron sincronizar los datos de la directiva.
[PrivilegedRequiredError](class_mip_privilegedrequirederror.md)  |  Se asignó la etiqueta actual como una operación con privilegios (equivalente a una operación de administrador), por lo tanto, no puede reemplazarse.
[ProtectAdhocAction](class_mip_protectadhocaction.md)  |  Clase de acción que especifica que se agregue la protección ad hoc al documento.
[ProtectByTemplateAction](class_mip_protectbytemplateaction.md)  |  Clase de acción que especifica que se agregue la protección por plantilla al documento.
[ProtectDoNotForwardAction](class_mip_protectdonotforwardaction.md)  |  Clase de acción que especifica que se agregue la protección de no reenvío al documento.
[ProtectionDescriptor](class_mip_protectiondescriptor.md)  |  Descripción de la protección asociada a un contenido.
[ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md)  |  Crea un elemento [ProtectionDescriptor](class_mip_protectiondescriptor.md) que describe la protección asociada a un elemento de contenido.
[ProtectionEngine::Observer](class_mip_protectionengine_observer.md)  |  Interfaz que recibe las notificaciones relacionadas con [ProtectionEngine](class_mip_protectionengine.md).
[ProtectionEngine::Settings](class_mip_protectionengine_settings.md)  |  [Configuración](class_mip_protectionengine_settings.md) utilizada por [ProtectionEngine](class_mip_protectionengine.md) durante su creación y a lo largo de su vigencia.
[ProtectionEngine](class_mip_protectionengine.md)  |  Administra acciones relacionadas con la protección según una identidad específica.
[ProtectionHandler::Observer](class_mip_protectionhandler.md)  |  Interfaz que recibe las notificaciones relacionadas con [ProtectionHandler](class_mip_protectionhandler.md).
[ProtectionHandler](class_mip_protectionhandler.md)  |  Administrar las acciones relacionadas con la protección para una configuración de protección específica.
[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md)  |  Interfaz que recibe las notificaciones relacionadas con [ProtectionProfile](class_mip_protectionprofile.md).
[ProtectionProfile::Settings](class_mip_protectionprofile_settings.md)  |  [Configuración](class_mip_protectionprofile_settings.md) utilizada por [ProtectionProfile](class_mip_protectionprofile.md) durante su creación y a lo largo de su vigencia.
[ProtectionProfile](class_mip_protectionprofile.md)  |  [ProtectionProfile](class_mip_protectionprofile.md) es la clase raíz para realizar las operaciones de protección.
[RecommendLabelAction](class_mip_recommendlabelaction.md)  |  Las acciones de recomendación de etiquetas están pensadas para sugerir una etiqueta a los usuarios. La supresión de esta llamada después de que un usuario ignore la etiqueta recomendada debe realizarse a través de las acciones admitidas en el estado de ejecución.
[RemoveContentFooterAction](class_mip_removecontentfooteraction.md)  |  Clase de acción que especifica que se quite el pie de página de contenido del documento.
[RemoveContentHeaderAction](class_mip_removecontentheaderaction.md)  |  Clase de acción que especifica que se quite el encabezado de contenido del documento.
[RemoveProtectionAction](class_mip_removeprotectionaction.md)  |  Clase de acción que especifica que se quite la protección del documento.
[RemoveWatermarkAction](class_mip_removewatermarkaction.md)  |  Clase de acción que especifica que se quite la marca de agua del documento.
[Stream](class_mip_stream.md)  |  Una clase que define la interfaz entre el SDK de MIP y el contenido basado en el flujo.
[TransientNetworkError](class_mip_transientnetworkerror.md)  |  Error de red temporal. Se produjo por un comportamiento inesperado al realizar llamadas de red a los puntos de conexión de servicio. Se puede reintentar la operación porque este error es temporal.
[UserRights](class_mip_userrights.md)  |  Un grupo de usuarios y los derechos asociados a estos.
[UserRoles](class_mip_userroles.md)  |  Un grupo de usuarios y los roles asociados a estos.
