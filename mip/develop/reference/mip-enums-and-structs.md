---
title: SDK de MIP para enumeraciones y estructuras de referencia de C++
description: Documentación de referencia para las enumeraciones y estructuras de SDK de MIP de C++.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: d3ca101d3141f2a1e36fcfec11e805907c125b8e
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651775"
---
# <a name="summary"></a>Resumen

 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
**Namespace `mip` :** |
enumeración ActionSource       |  define lo que desencadenó el evento SetLabel
enum ActionType       |  Diferentes tipos de acción.
enumeración AssignmentMethod       |  El método de asignación de la etiqueta en el documento. Si la asignación de la etiqueta se realiza automáticamente, estándar o como una operación con privilegios (equivalente a una operación de administrador).
enum Consent       |  La respuesta de un usuario cuando se solicita el consentimiento para conectarse a un punto de conexión de servicio.
enumeración ContentFormat       |  Formato del contenido.
enumeración ContentMarkAlignment       |  Marca de alineación de contenido (content encabezado o pie de página de contenido).
enumeración ContentState       |  Define el estado de los datos de la aplicación actúa.
enum ErrorType       | _No se ha documentado todavía._
enum HttpRequestType       |  Tipo de solicitud HTTP.
enum LogLevel       |  Diferentes niveles de registro usados en el SDK de MIP.
enum ProtectionHandlerCreationOptions       |  Marcas de bits que determinan el comportamiento de creación de directivas adicionales.
enum ProtectionType       |  Describe si la protección se basa en una plantilla o se determina ad hoc (personalizada)
enumeración WatermarkLayout       |  Diseño de las marcas de agua.
struct ApplicationInfo  |  Una estructura donde se incluye información específica de la aplicación.
struct PublishingLicenseContext | Contiene los detalles de una licencia de publicación usada para crear un controlador de protección.
  
## <a name="enumerations-mip"></a>Enumeraciones (`mip`)

### <a name="actionsource-enum"></a>Enumeración ActionSource

Define lo que desencadenó el evento SetLabel

 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
MANUAL            | Seleccionar manualmente por el usuario
AUTOMÁTICO            | Establecer condiciones de directiva
RECOMIENDA            | Establecido por el usuario después de etiqueta se recomienda por las condiciones de directiva
VALOR PREDETERMINADO            | Establece de forma predeterminada en la directiva
OBLIGATORIO            | Establecer usuario después de la directiva aplicada para establecer una etiqueta


### <a name="actiontype-enum"></a>ActionType enum

Diferentes tipos de acción. CUSTOM es el tipo de acción genérico. Todos los demás tipos de acción son una acción específica con un significado específico.

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

### <a name="assignmentmethod-enum"></a>Enumeración AssignmentMethod

El método de asignación de la etiqueta en el documento. Si la asignación de la etiqueta se realiza automáticamente, estándar o como una operación con privilegios (equivalente a una operación de administrador).

 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
ESTÁNDAR            | [Etiqueta](class_mip_label.md) es el método de asignación estándar
CON PRIVILEGIOS            | [Etiqueta](class_mip_label.md) tiene privilegios el método de asignación
AUTO            | [Etiqueta](class_mip_label.md) método de asignación es automático


### <a name="consent-enum"></a>Enumeración de consentimiento

La respuesta de un usuario cuando se solicita el consentimiento para conectarse a un punto de conexión de servicio.

 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
AcceptAlways            | Consentir y recordar esta decisión
Aceptar            | Consentir, una sola vez
Rechazar            | No consentir


### <a name="contentformat-enum"></a>Enumeración ContentFormat

Formato del contenido.

 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
VALOR PREDETERMINADO            | Formato de contenido es el formato de archivo estándar
CORREO ELECTRÓNICO            | Formato de contenido es el formato de correo electrónico

### <a name="contentmarkalignment-enum"></a>Enumeración ContentMarkAlignment

Marca de alineación de contenido (content encabezado o pie de página de contenido).

 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
IZQUIERDA            | Marcar contenido se alinea a la izquierda
CORRECTO            | Marcar contenido se alinea a la derecha
CENTRO            | Se centra marcar contenido

### <a name="contentstate-enum"></a>Enumeración ContentState

Define el estado de los datos de la aplicación actúa.

 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
REST            | Almacenada físicamente en las bases de datos, archivo o almacenes de datos inactivos
MOVIMIENTO            | Recorrer una red o temporalmente que residen en memoria del equipo para leer o actualizar datos
USE            | Datos activos en constante cambio que se almacenan físicamente en las bases de datos/archivo/almacenes etcetera

### <a name="errortype-enum"></a>Enumeración ErrorType

 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
BAD_INPUT_ERROR            | El autor de la llamada pasó una entrada incorrecta.
FILE_IO_ERROR            | Error de E/S de archivo general.
NETWORK_ERROR            | Problemas generales de red; Por ejemplo, servicio inaccesible.
TRANSIENT_NETWORK_ERROR            | Problemas de red transitorios; Por ejemplo, la puerta de enlace incorrecta.
INTERNAL_ERROR            | Errores internos inesperados.
JUSTIFICATION_REQUIRED            | Para completar la acción en el archivo se debe proporcionar una justificación.
NOT_SUPPORTED_OPERATION            | Aún no se admite la operación solicitada.
PRIVILEGED_REQUIRED            | No se puede invalidar la etiqueta con privilegios si el nuevo método de etiqueta es estándar.
ACCESS_DENIED            | El usuario no pudo obtener acceso a los servicios.
CONSENT_DENIED            | Una operación que necesitaba el consentimiento del usuario, pero que no lo ha recibido.
POLICY_SYNC_ERROR            | No se pudieron sincronizar los datos de la directiva.
NO_PERMISSIONS            | El usuario no pudo obtener acceso al contenido. Por ejemplo, no revocado ningún permiso, contenido
NO_AUTH_TOKEN            | El usuario no pudo obtener acceso al contenido debido a un token de autenticación vacía.
DISABLED_SERVICE            | El usuario no pudo obtener acceso al contenido debido a que el servicio está deshabilitado
PROXY_AUTH_ERROR            | Error de autenticación de proxy.
NO_POLICY_ERROR            | No hay ninguna directiva está configurada para el usuario/inquilino
  
### <a name="httprequesttype-enum"></a>Enumeración HttpRequestType

Tipo de solicitud HTTP.

 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
Get            | GET
POST            | EXPONER

  
### <a name="loglevel-enum"></a>Enumeración LogLevel

Diferentes niveles de registro usados en el SDK de MIP.

 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
seguimiento            | 
Info            | 
Advertencia            | 
Error            | 

  
### <a name="protectionhandlercreationoptions-enum"></a>Enumeración ProtectionHandlerCreationOptions

Marcas de bits que determinan el comportamiento de creación de directivas adicionales.

 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
Ninguno            | Ninguno
OfflineOnly            | No se permiten operaciones de red e interfaz de usuario.
AllowAuditedExtraction            | El contenido se puede abrir en una aplicación no compatible con el SDK de protección.
PreferDeprecatedAlgorithms            | Use algoritmos criptográficos en desuso para la compatibilidad con versiones anteriores
  
### <a name="protectiontype-enum"></a>ProtectionType enum

Describe si protección se basa en una plantilla o ad hoc (personalizada).

 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
TemplateBased            | Se creó un controlador a partir de una plantilla
Personalizada            | Se creó un controlador ad hoc
  
### <a name="watermarklayout-enum"></a>WatermarkLayout enum

Diseño de las marcas de agua.

 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
HORIZONTAL            | Diseño de la marca de agua es horizontal
DIAGONAL            | Diseño de la marca de agua es diagonal


## <a name="structures"></a>Estructuras 

### `mip::ApplicationInfo` 

Una estructura donde se incluye información específica de la aplicación.
  
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public std::string applicationId  |  Identificador de aplicación que establezca en el portal AAD, (debe ser un GUID sin corchetes).
 public std::string applicationName  |  Nombre de la aplicación (solo debe contener la exclusión de carácter ASCII válido ';')
 public std::string applicationVersion  |  La versión de la aplicación se usa, (solo debe contener la exclusión de carácter ASCII válido ';')
  
### `mip::PublishingLicenseContext` 

Contiene los detalles de una licencia de publicación usada para crear un controlador de protección.
  
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
Public const std:: vector\<uint8_t\> licenseInfo  | _No se ha documentado todavía._
Public const std:: vector\<uint8_t\> serializedPublishingLicense  | _No se ha documentado todavía._
PublishingLicenseContext pública (const std:: vector\<uint8_t\>& licenseInfo, const std:: vector\<uint8_t\>& serializedPublishingLicense)  | _No se ha documentado todavía._
  
