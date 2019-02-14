---
title: SDK de MIP para referencia de C++
description: SDK de MIP para referencia de C++
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 7e041062b92bad8b853bf5bcf55a23c6ad88a4b7
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56256608"
---
# <a name="mip-sdk-for-c-reference"></a>SDK de MIP para referencia de C++

El SDK de C++ de Microsoft Information Protection (MIP) permite a los desarrolladores administrar y aplicar directivas de protección de datos a los datos y otros activos digitales.  

El SDK de MIP para C++ incluye:

- [Enumeraciones y estructuras](mip-enums-and-structs.md)
- [Funciones](mip-functions.md)
- Las clases siguientes:

| Nombre de namespace::Class | Descripción |
| :----------|:------------|
[mip::AccessDeniedError](class_mip_AccessDeniedError.md)  |  El usuario no pudo obtener acceso al contenido. Por ejemplo, no hay permisos, se ha revocado el contenido, etc.
[mip::Action](class_mip_Action.md)  |  Interfaz para una acción. Cada acción se traduce en una medida que debe adoptar la aplicación para aplicar la etiqueta (como se define en la directiva).
[mip::AddContentFooterAction](class_mip_AddContentFooterAction.md)  |  Clase de acción que especifica que se agregue un pie de página de contenido al documento.
[mip::AddContentHeaderAction](class_mip_AddContentHeaderAction.md)  |  Una clase de acción que especifica agregar un encabezado de contenido.
[mip::AddWatermarkAction](class_mip_AddWatermarkAction.md)  |  Una clase de acción que especifica agregar una marca de agua.
[mip::ApplyLabelAction](class_mip_ApplyLabelAction.md)  |  La aplicación de acciones de la etiqueta requiere que la aplicación que realiza la llamada aplique una etiqueta específica.
[mip::AuthDelegate](class_mip_AuthDelegate.md)  |  Delegado de autenticación relacionadas con las operaciones.
[mip::BadInputError](class_mip_BadInputError.md)  |  Error de entrada incorrecta; se produce cuando la entrada a una API de SDK no es válida.
[mip::ClassificationRequest](class_mip_ClassificationRequest.md)  |  Clase que contiene la solicitud de una llamada de clasificación en el estado de ejecución.
[mip::ClassificationResult](class_mip_ClassificationResult.md)  |  Clase que contiene el resultado de una llamada de clasificación en el estado de ejecución.
[mip::ConsentDelegate](class_mip_ConsentDelegate.md)  |  Delegado para operaciones relacionadas con el consentimiento.
[mip::ConsentDeniedError](class_mip_ConsentDeniedError.md)  |  Una operación que necesitaba el consentimiento del usuario, pero que no lo ha recibido.
[mip::ContentLabel](class_mip_ContentLabel.md)  |  Abstracción para una etiqueta de Microsoft Information Protection que se aplica a un fragmento de contenido, normalmente un documento.
[mip::CustomAction](class_mip_CustomAction.md)  |  [CustomAction](class_mip_customaction.md) es una clase de acción genérica que captura todas las subpropiedades de la acción como un contenedor de propiedades. El autor de llamada es responsable de entender el significado de la acción.
[mip::Error](class_mip_Error.md)  |  La clase base para todos los errores que se notificarán (se producen o se devuelven) del SDK de MIP.
[mip::ExecutionState](class_mip_ExecutionState.md)  |  Interfaz a todos los estados necesarios para ejecutar el motor.
[mip::FileEngine](class_mip_FileEngine.md)  |  Esta clase proporciona una interfaz para todas las funciones de motor.
[mip::FileExecutionState](class_mip_FileExecutionState.md)  | _No se ha documentado todavía._
[mip::FileHandler](class_mip_FileHandler.md)  |  Interfaz a todas las funciones de control de archivos.
[mip::FileIOError](class_mip_FileIOError.md)  |  Error de E/S de archivo.
[mip::FileProfile](class_mip_FileProfile.md)  |  La clase [FileProfile](class_mip_fileprofile.md) es la clase raíz para el uso de las operaciones de Microsoft Information Protection.
[mip::HttpDelegate](class_mip_HttpDelegate.md)  |  Interfaz para reemplazar el control de HTTP.
[mip::HttpRequest](class_mip_HttpRequest.md)  |  Interfaz que describe una única solicitud HTTP.
[mip::HttpResponse](class_mip_HttpResponse.md)  |  Interfaz que describe una única respuesta HTTP, implementada por la aplicación cliente cuando se reemplaza [HttpDelegate](class_mip_httpdelegate.md).
[mip::Identity](class_mip_Identity.md)  |  Abstracción para la identidad.
[mip::InternalError](class_mip_InternalError.md)  |  Error interno. Este error se produce cuando ocurre algo inesperado durante la ejecución.
[mip::JustificationRequiredError](class_mip_JustificationRequiredError.md)  | _No se ha documentado todavía._
[mip::JustifyAction](class_mip_JustifyAction.md)  |  La [acción](class_mip_action.md) justificar requiere que se facilite una justificación para una degradación de la etiqueta y el establecimiento de la respuesta en el estado de ejecución.
[mip::Label](class_mip_Label.md)  |  Abstracción para una única etiqueta de Microsoft Information Protection.
[mip::LabelingOptions](class_mip_LabelingOptions.md)  |  Interfaz para configurar las opciones de etiquetado para los métodos SetLabel y DeleteLabel.
[mip::LoggerDelegate](class_mip_LoggerDelegate.md)  |  Una clase que define la interfaz para el registrador de SDK de MIP.
[mip::MetadataAction](class_mip_MetadataAction.md)  |  Una [acción](class_mip_action.md) que agrega información de metadatos al contenido.
[mip::NetworkError](class_mip_NetworkError.md)  |  Error de red. Se produjo por un comportamiento inesperado al realizar llamadas de red a los puntos de conexión de servicio.
[mip::NoAuthTokenError](class_mip_NoAuthTokenError.md)  |  El usuario no pudo obtener acceso al contenido porque falta el token de autenticación.
[mip::NoPermissionsError](class_mip_NoPermissionsError.md)  |  El usuario no pudo obtener acceso al contenido. Por ejemplo, no hay permisos, se ha revocado el contenido, etc.
[mip::NoPolicyError](class_mip_NoPolicyError.md)  |  Directiva de inquilino no está configurada para/etiquetas de clasificación.
[mip::NotSupportedError](class_mip_NotSupportedError.md)  |  La operación solicitada por la aplicación no es compatible con el SDK.
[mip::PolicyEngine](class_mip_PolicyEngine.md)  |  Esta clase proporciona una interfaz para todas las funciones de motor.
[mip::PolicyHandler](class_mip_PolicyHandler.md)  |  Esta clase proporciona una interfaz para todas las funciones de controlador de directiva de un archivo.
[mip::PolicyProfile](class_mip_PolicyProfile.md)  |  [PolicyProfile](class_mip_policyprofile.md) es la clase raíz para usar las operaciones de Microsoft Information Protection. Una aplicación típica solo necesitará un elemento [PolicyProfile](class_mip_policyprofile.md), pero puede crear varios perfiles si es necesario.
[mip::PolicySyncError](class_mip_PolicySyncError.md)  |  No se pudieron sincronizar los datos de la directiva.
[mip::PrivilegedRequiredError](class_mip_PrivilegedRequiredError.md)  |  Se asignó la etiqueta actual como una operación con privilegios (equivalente a una operación de administrador), por lo tanto, no puede reemplazarse.
[mip::ProtectAdhocAction](class_mip_ProtectAdhocAction.md)  |  Clase de acción que especifica que se agregue la protección ad hoc al documento.
[mip::ProtectByTemplateAction](class_mip_ProtectByTemplateAction.md)  |  Clase de acción que especifica que se agregue la protección por plantilla al documento.
[mip::ProtectDoNotForwardAction](class_mip_ProtectDoNotForwardAction.md)  |  Clase de acción que especifica que se agregue la protección de no reenvío al documento.
[mip::ProtectionDescriptor](class_mip_ProtectionDescriptor.md)  |  Descripción de la protección asociada a un contenido.
[mip::ProtectionDescriptorBuilder](class_mip_ProtectionDescriptorBuilder.md)  |  Crea un elemento [ProtectionDescriptor](class_mip_protectiondescriptor.md) que describe la protección asociada a un elemento de contenido.
[mip::ProtectionEngine](class_mip_ProtectionEngine.md)  |  Administra acciones relacionadas con la protección según una identidad específica.
[mip::ProtectionHandler](class_mip_ProtectionHandler.md)  |  Administrar las acciones relacionadas con la protección para una configuración de protección específica.
[mip::ProtectionProfile](class_mip_ProtectionProfile.md)  |  [ProtectionProfile](class_mip_protectionprofile.md) es la clase raíz para realizar las operaciones de protección.
[mip::ProxyAuthenticationError](class_mip_ProxyAuthenticationError.md)  |  Error de autenticación de proxy.
[mip::RecommendLabelAction](class_mip_RecommendLabelAction.md)  |  Las acciones de recomendación de etiquetas están pensadas para sugerir una etiqueta a los usuarios. La supresión de esta llamada después de que un usuario ignore la etiqueta recomendada debe realizarse a través de las acciones admitidas en el estado de ejecución.
[mip::RemoveContentFooterAction](class_mip_RemoveContentFooterAction.md)  |  Clase de acción que especifica que se quite el pie de página de contenido del documento.
[mip::RemoveContentHeaderAction](class_mip_RemoveContentHeaderAction.md)  |  Clase de acción que especifica que se quite el encabezado de contenido del documento.
[mip::RemoveProtectionAction](class_mip_RemoveProtectionAction.md)  |  Clase de acción que especifica que se quite la protección del documento.
[mip::RemoveWatermarkAction](class_mip_RemoveWatermarkAction.md)  |  Clase de acción que especifica que se quite la marca de agua del documento.
[mip::SensitivityTypesRulePackage](class_mip_SensitivityTypesRulePackage.md)  | _No se ha documentado todavía._
[mip::ServiceDisabledError](class_mip_ServiceDisabledError.md)  |  El usuario no pudo obtener acceso al contenido debido a un servicio que se va a deshabilitar.
[mip::Stream](class_mip_Stream.md)  |  Una clase que define la interfaz entre el SDK de MIP y el contenido basado en el flujo.
[mip::TransientNetworkError](class_mip_TransientNetworkError.md)  |  Error de red temporal. Se produjo por un comportamiento inesperado al realizar llamadas de red a los puntos de conexión de servicio. Se puede reintentar la operación porque este error es temporal.
[mip::UserRights](class_mip_UserRights.md)  |  Un grupo de usuarios y los derechos asociados a estos.
[mip::UserRoles](class_mip_UserRoles.md)  |  Un grupo de usuarios y los roles asociados a estos.
