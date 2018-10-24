---
title: Resumen
description: Resumen
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 5af209d5a627263399c8c60f474495dcadab24a0
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446505"
---
# <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
**common** |
enum Consent       |  La respuesta de un usuario cuando se solicita el consentimiento para conectarse a un punto de conexión de servicio.
struct ApplicationInfo  |  Una estructura donde se incluye información específica de la aplicación.
**mip** |
enum ErrorType       | _No se ha documentado todavía._
enum HttpRequestType       |  Tipo de solicitud HTTP.
enum LogLevel       |  Diferentes niveles de registro usados en el SDK de MIP.
enum ProtectionHandlerCreationOptions       |  Marcas de bits que determinan el comportamiento de creación de directivas adicionales.
enum ProtectionType       |  Describe si la protección se basa en una plantilla o se determina ad hoc (personalizada)
enum ActionType       |  Diferentes tipos de acción.
struct mip::PublishingLicenseContext | Contiene los detalles de una licencia de publicación usada para crear un controlador de protección.

  
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

Diferentes tipos de acción.

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

CUSTOM es el tipo de acción genérico. Todos los demás tipos de acción son una acción específica con un significado específico.

Los valores de ActionType se pueden combinar con los operadores siguientes:

- Operador AND (&) para [Action](class_mip_action.md) (`operator &(ActionType a, ActionType b)`)
- Operador OR lógico (XOR) (^) para [Action](class_mip_action.md). (`operator ^(ActionType a, ActionType b)`)


### <a name="errortype"></a>ErrorType
 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
BAD_INPUT_ERROR            | El autor de la llamada pasó una entrada incorrecta.
FILE_IO_ERROR            | Error de E/S de archivo general.
NETWORK_ERROR            | Problemas generales de red; por ejemplo, servicio inaccesible.
TRANSIENT_NETWORK_ERROR            | Problemas temporales de red (por ejemplo, puerta de enlace incorrecta).
INTERNAL_ERROR            | Errores internos inesperados. Por ejemplo, en el protocolo cliente/servidor (se recibió una respuesta no esperada).
JUSTIFICATION_REQUIRED            | Para completar la acción en el archivo se debe proporcionar una justificación.
NOT_SUPPORTED_OPERATION            | Aún no se admite la operación solicitada.
PRIVILEGED_REQUIRED            | No se puede invalidar la etiqueta con privilegios si el nuevo método de etiqueta es estándar.
ACCESS_DENIED            | El usuario no pudo obtener acceso al contenido. Por ejemplo, no hay permisos, se ha revocado el contenido,etc.
CONSENT_DENIED            | Una operación que necesitaba el consentimiento del usuario, pero que no lo ha recibido.
  
### <a name="httprequesttype"></a>HttpRequestType
Tipo de solicitud HTTP.

 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
Get            | GET
POST            | POST
  
### <a name="loglevel"></a>LogLevel

Diferentes niveles de registro usados en el SDK de MIP.

 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
Trace            | 
Info            | 
Advertencia            | 
Error            | 
Diferentes niveles de registro utilizados en el SDK de mip.
  
### <a name="protectionhandlercreationoptions"></a>ProtectionHandlerCreationOptions

Marcas de bits que determinan el comportamiento de creación de directivas adicionales.

 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
Ninguno            | Ninguno
OfflineOnly            | No se permiten operaciones de red e interfaz de usuario.
AllowAuditedExtraction            | El contenido se puede abrir en una aplicación no compatible con el SDK de protección.
PreferDeprecatedAlgorithms            | Use algoritmos criptográficos en desuso para la compatibilidad con versiones anteriores


### <a name="protectiontype"></a>ProtectionType
Describe si la protección se basa en una plantilla o se determina ad hoc (personalizada)

 Valores                         | Descripciones                                
--------------------------------|---------------------------------------------
TemplateBased            | Se creó un controlador a partir de una plantilla
Personalizada            | Se creó un controlador ad hoc

  
### <a name="protectionhandlercreationoptions"></a>ProtectionHandlerCreationOptions
Operador OR bit a bit de ProtectionHandlerCreationOptions.

Parámetros:  
* **a**: valor izquierdo 

* **b**: valor derecho

### <a name="releaseallresources"></a>ReleaseAllResources
Libera todos los recursos (subprocesos, etc.) antes de un apagado.
Si una aplicación carga con retraso las bibliotecas dinámicas de MIP, es necesario llamar a esta función antes de que la aplicación descargue de forma explícita esas bibliotecas de MIP para evitar un interbloqueo. Por ejemplo, en win32, es necesario llamar a esta función antes de realizar cualquier llamada para descargar de forma explícita DLL de MIP mediante FreeLibrary o \__FUnloadDelayLoadedDLL2. Las aplicaciones tienen que liberar las referencias a todos los objetos de MIP (por ejemplo, perfiles, motores, controladores) antes de llamar a esta función.
  
**Devuelve**: operador OR bit a bit de parámetros
  
## <a name="structures"></a>Estructuras

### <a name="applicationinfo"></a>ApplicationInfo 
Una estructura donde se incluye información específica de la aplicación.

 Campos                        | Descripciones                                
--------------------------------|---------------------------------------------
 public std::string applicationId  |  Identificador de la aplicación como se establece en el portal de Azure AD.
 public std::string applicationName  |  Nombre de aplicación
 public std::string applicationVersion  |  La versión de la aplicación usada.
  
### <a name="mippublishinglicensecontext"></a>mip::PublishingLicenseContext 
Contiene los detalles de una licencia de publicación usada para crear un controlador de protección.
  
 Campos                        | Descripciones                                
--------------------------------|---------------------------------------------
public const std::vector<uint8_t> licenseInfo  | _No se ha documentado todavía._
public const std::vector<uint8_t> serializedPublishingLicense  | _No se ha documentado todavía._
public PublishingLicenseContext(const std::vector<uint8_t>& licenseInfo, const std::vector<uint8_t>& serializedPublishingLicense)  | _No se ha documentado todavía._
  
