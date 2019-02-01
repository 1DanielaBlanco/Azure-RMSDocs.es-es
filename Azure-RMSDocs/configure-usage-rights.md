---
title: Configuración de los derechos de uso para Azure Rights Management - AIP
description: Conozca e identifique los derechos específicos que se usan al proteger archivos o correos electrónicos con el servicio Azure Rights Management de Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2019
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 195700be6b1a2f7aecbdd4de333570669cf6d329
ms.sourcegitcommit: 4b1f204fd31bb9de05510b85b91304d9964a14c1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/30/2019
ms.locfileid: "55420799"
---
# <a name="configuring-usage-rights-for-azure-rights-management"></a>Configuración de los derechos de uso para Azure Rights Management

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Cuando establezca protección en archivos o correos electrónicos con el servicio Azure Rights Management de Azure Information Protection y no use ninguna plantilla, deberá configurar los derechos de uso por su cuenta. Además, al configurar plantillas o etiquetas para la protección de Azure Rights Management, se seleccionan los derechos de uso que se aplicarán automáticamente cuando los usuarios, los administradores o los servicios configurados seleccionen la plantilla o etiqueta. Por ejemplo, en Azure Portal, puede seleccionar los roles que configuran una agrupación lógica de derechos de uso o puede configurar los derechos individuales.

Use este artículo como ayuda para configurar los derechos de uso que quiere para la aplicación que esté usando y para entender cómo las aplicaciones interpretan estos derechos.

> [!NOTE] 
> Para más detalles, en este artículo se incluyen valores del portal clásico de Azure, que dejó de estar disponible el 8 de enero de 2018.
>
> Para ayudarle a migrar al portal nuevo, vea [Tareas que solía realizar con el portal clásico de Azure](migrate-portal.md).

## <a name="usage-rights-and-descriptions"></a>Derechos de uso y descripciones
En la tabla siguiente se enumeran y se describen los derechos de uso que admite Rights Management y cómo se usan y se interpretan. Se enumeran por su **nombre común**, que es normalmente cómo se muestra o se referencia el derecho de uso, como una versión más descriptiva del valor de una sola palabra que se usa en el código (el valor **Codificación en la directiva**). 

**Constante o valor de API** es el nombre de SDK para una llamada de API de MSIPC, que se usa al escribir una aplicación habilitada para RMS que comprueba un derecho de uso o agrega un derecho de uso a una directiva.


|Derecho de uso|Descripción|Implementación|
|-------------------------------|---------------------------|-----------------|
|Nombre común: **Editar contenido, Editar** <br /><br />Codificación en la directiva: **DOCEDIT**|Permite al usuario modificar, reorganizar, formatear u ordenar el contenido dentro de la aplicación. No concede el derecho a guardar la copia modificada.<br /><br />En Word, a menos que tenga Office 365 ProPlus con una versión mínima de [1807](https://docs.microsoft.com/officeupdates/monthly-channel-2018#version-1807-july-25), este derecho no basta para activar o desactivar el **Control de cambios** ni para usar todas las características de seguimiento de cambios como revisor. Para usar todas las opciones de control de cambios, se necesita este derecho: **Control total**. |Permisos personalizados de Office: Como parte de las opciones **Cambiar** y **Control total** . <br /><br />Nombre en el Portal de Azure clásico: **Editar contenido**<br /><br />Nombre en Azure Portal: **Editar contenido, Editar (DOCEDIT)**<br /><br />Nombre en las plantillas de AD RMS: **Editarar** <br /><br />Constante o valor de API: No aplicable.|
|Nombre común: **Guardar** <br /><br />Codificación en la directiva: **EDITAR**|Permite al usuario guardar el documento en la ubicación actual.<br /><br />En las aplicaciones de Office, este derecho también permite al usuario modificar el documento y guardarlo en una nueva ubicación con un nuevo nombre si el formato de archivo seleccionado admite la protección de Rights Management de forma nativa. La restricción de formato de archivo garantiza que la protección original no se puede quitar del archivo.|Permisos personalizados de Office: Como parte de las opciones **Cambiar** y **Control total** . <br /><br />Nombre en el Portal de Azure clásico: **Guardar archivo**<br /><br />Nombre en Azure Portal: **Guardar (EDIT)**<br /><br />Nombre en las plantillas de AD RMS: **Guardar** <br /><br />Constante o valor de API: `IPC_GENERIC_WRITE L"EDIT"`|
|Nombre común: **Comentario** <br /><br />Codificación en la directiva: **COMMENT**|Habilita la opción para agregar anotaciones o comentarios al contenido.<br /><br />Este derecho está disponible en el SDK como directiva ad hoc en el módulo de Azure Information Protection y RMS Protection para Windows PowerShell y se implementó en algunas aplicaciones de proveedores de software. Sin embargo, no se usa extensamente y no es compatible actualmente con las aplicaciones de Office.|Permisos personalizados de Office: Sin implementar. <br /><br />Nombre en el Portal de Azure clásico: Sin implementar.<br /><br />Nombre en Azure Portal: Sin implementar.<br /><br />Nombre en las plantillas de AD RMS: Sin implementar. <br /><br />Constante o valor de API: `IPC_GENERIC_COMMENT L"COMMENT`|
|Nombre común: **Guardar como, Exportar** <br /><br />Codificación en la directiva: **EXPORT**|Habilita la opción para guardar el contenido con un nombre de archivo diferente (Guardar como). <br /><br />En los documentos de Office y el cliente de Azure Information Protection, el archivo se puede guardar sin protección y también se puede volver a proteger con nuevos permisos y configuración. Estas acciones permitidas significan que un usuario que tenga este derecho puede cambiar o quitar una etiqueta de Azure Information Protection de un documento o correo electrónico protegido. <br /><br />Este derecho también permite al usuario realizar otras opciones de exportación en las aplicaciones, como **Enviar a OneNote**.<br /><br /> Nota: Si no se concede este derecho, las aplicaciones de Office permiten a un usuario guardar un documento en un nuevo nombre si el formato de archivo seleccionado admite la protección de Rights Management de forma nativa.|Permisos personalizados de Office: Como parte de la opción **Control total**. <br /><br />Nombre en el Portal de Azure clásico: **Exportar contenido (Guardar como)** <br /><br />Nombre en Azure Portal: **Guardar como, Exportar (EXPORT)**<br /><br />Nombre en las plantillas de AD RMS: **Exportar (Guardar como)** <br /><br />Constante o valor de API: `IPC_GENERIC_EXPORT L"EXPORT"`|
|Nombre común: **Reenviar** <br /><br />Codificación en la directiva: **FORWARD**|Habilita la opción para reenviar un mensaje de correo electrónico y agregar destinatarios a las líneas **Para** y **CO** . Este derecho no se aplica a documentos, solo a mensajes de correo electrónico.<br /><br />No permite que el reenviador conceda derechos a otros usuarios como parte de la acción de reenvío. <br /><br />Cuando conceda este derecho, conceda también el derecho **Editar contenido, Editar** (nombre común) y, adicionalmente, el derecho **Guardar** (nombre común) para asegurarse de que el mensaje de correo electrónico original no se entrega como un archivo adjunto. Especifique también estos derechos cuando envíe un correo a otra organización que usa el cliente de Outlook u Outlook Web App. O bien, los usuarios de su organización que no pueden usar el servicio Azure Rights Management porque se han implementado [controles de incorporación](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy).|Permisos personalizados de Office: Se deniega al usar la directiva estándar **No reenviar** .<br /><br />Nombre en el Portal de Azure clásico: **Reenviar**<br /><br />Nombre en Azure Portal: **Reenviar (FORWARD)**<br /><br />Nombre en las plantillas de AD RMS: **Reenviar** <br /><br />Constante o valor de API: `IPC_EMAIL_FORWARD L"FORWARD"`|
|Nombre común: **Control total** <br /><br />Codificación en la directiva: **OWNER**|Concede todos los derechos para el documento; se pueden realizar todas las acciones disponibles.<br /><br />Incluye la capacidad de quitar la protección de un documento y de volver a protegerlo. <br /><br />Tenga en cuenta que este derecho de uso no es el mismo que el [propietario de Rights Management](#rights-management-issuer-and-rights-management-owner).|Permisos personalizados de Office: Como la opción personalizada **Control total** .<br /><br />Nombre en el Portal de Azure clásico: **Control total**<br /><br />Nombre en Azure Portal: **Control total (OWNER)**<br /><br />Nombre en las plantillas de AD RMS: **Control total** <br /><br />Constante o valor de API: `IPC_GENERIC_ALL L"OWNER"`|
|Nombre común: **Imprimir** <br /><br />Codificación en la directiva: **PRINT**|Habilita las opciones para imprimir el contenido.|Permisos personalizados de Office: Como la opción **Imprimir contenido** en los permisos personalizados. No se trata de un valor por destinatario.<br /><br />Nombre en el Portal de Azure clásico: **Imprimir**<br /><br />Nombre en Azure Portal: **Imprimir (PRINT)**<br /><br />Nombre en las plantillas de AD RMS: **Imprimir** <br /><br />Constante o valor de API: `IPC_GENERIC_PRINT L"PRINT"`|
|Nombre común: **Responder** <br /><br />Codificación en la directiva: **REPLY**|Habilita la opción **Responder** en un cliente de correo electrónico, sin permitir que se realicen cambios en las líneas **Para** o **CC**.<br /><br />Cuando conceda este derecho, conceda también el derecho **Editar contenido, Editar** (nombre común) y, adicionalmente, el derecho **Guardar** (nombre común) para asegurarse de que el mensaje de correo electrónico original no se entrega como un archivo adjunto. Especifique también estos derechos cuando envíe un correo a otra organización que usa el cliente de Outlook u Outlook Web App. O bien, los usuarios de su organización que no pueden usar el servicio Azure Rights Management porque se han implementado [controles de incorporación](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy).|Permisos personalizados de Office: No aplicable.<br /><br />Nombre en el Portal de Azure clásico: **Responder**<br /><br />Nombre en el Portal de Azure clásico: **Responder (REPLY)**<br /><br />Nombre en las plantillas de AD RMS: **Responder** <br /><br />Constante o valor de API: `IPC_EMAIL_REPLY`|
|Nombre común: **Responder a todos** <br /><br />Codificación en la directiva: **REPLYALL**|Habilita la opción **Responder a todos** en un cliente de correo electrónico, pero no permite al usuario agregar a destinatarios a las líneas **Para** o **CO** .<br /><br />Cuando conceda este derecho, conceda también el derecho **Editar contenido, Editar** (nombre común) y, adicionalmente, el derecho **Guardar** (nombre común) para asegurarse de que el mensaje de correo electrónico original no se entrega como un archivo adjunto. Especifique también estos derechos cuando envíe un correo a otra organización que usa el cliente de Outlook u Outlook Web App. O bien, los usuarios de su organización que no pueden usar el servicio Azure Rights Management porque se han implementado [controles de incorporación](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy).|Permisos personalizados de Office: No aplicable.<br /><br />Nombre en el Portal de Azure clásico: **Responder a todos**<br /><br />Nombre en Azure Portal: **Responder a todos (REPLY ALL)**<br /><br />Nombre en las plantillas de AD RMS: **Responder a todos** <br /><br />Constante o valor de API: `IPC_EMAIL_REPLYALL L"REPLYALL"`|
|Nombre común: **Ver, Abrir, Leer** <br /><br />Codificación en la directiva: **VIEW**|Permite al usuario abrir el documento y ver el contenido.<br /><br /> En Excel, este derecho no basta para ordenar los datos, lo que requiere el derecho siguiente: **Editar contenido, Editar**. Para filtrar datos en Excel, necesita estos dos derechos: **Editar contenido, Editar** y **Copiar**.|Permisos personalizados de Office: Como la opción **Ver** de la directiva personalizada **Leer** .<br /><br />Nombre en el Portal de Azure clásico: **Vista**<br /><br />Nombre en Azure Portal: **Ver, Abrir, Leer (VIEW)**<br /><br />Nombre en las plantillas de AD RMS: **Lectura** <br /><br />Constante o valor de API: `IPC_GENERIC_READ L"VIEW"`|
|Nombre común: **Copiar** <br /><br />Codificación en la directiva: **EXTRACT**|Habilita las opciones para copiar los datos (incluidas las capturas de pantalla) del documento en el mismo documento o en otro documento.<br /><br />En algunas aplicaciones, también permite que todo el documento se guarde en formato desprotegido.<br /><br />En Skype Empresarial y en aplicaciones de uso compartido de pantalla similares, el moderador debe tener este derecho para moderar correctamente un documento protegido. Si el moderador no tiene este de derecho, los asistentes no pueden ver el documento y se muestra como oscurecido para ellos.|Permisos personalizados de Office: Como la opción de directiva personalizada **Permitir a los usuarios con acceso de lectura copiar contenido** .<br /><br />Nombre en el Portal de Azure clásico: **Copiar y extraer contenido**<br /><br />Nombre en Azure Portal: **Copiar (EXTRACT)**<br /><br />Nombre en las plantillas de AD RMS: **Extraer** <br /><br />Constante o valor de API: `IPC_GENERIC_EXTRACT L"EXTRACT"`|
|Nombre común: **Ver derechos** <br /><br />Codificación en la directiva: **VIEWRIGHTSDATA**|Permite al usuario ver la directiva que se aplica al documento.|Permisos personalizados de Office: Sin implementar.<br /><br />Nombre en el Portal de Azure clásico: **Ver derechos asignados**<br /><br />Nombre en Azure Portal: **Ver derechos (VIEWRIGHTSDATA)**.<br /><br />Nombre en las plantillas de AD RMS: **Ver derechos** <br /><br />Constante o valor de API: `IPC_READ_RIGHTS L"VIEWRIGHTSDATA"`|
|Nombre común: **Cambiar derechos** <br /><br />Codificación en la directiva: **EDITRIGHTSDATA**|Permite al usuario cambiar la directiva que se aplica al documento. Incluye la eliminación de la protección.|Permisos personalizados de Office: Sin implementar.<br /><br />Nombre en el Portal de Azure clásico: **Cambiar derechos**<br /><br />Nombre en Azure Portal: **Editar derechos (EDITRIGHTSDATA)**.<br /><br />Nombre en las plantillas de AD RMS: **Editar derechos** <br /><br />Constante o valor de API: `PC_WRITE_RIGHTS L"EDITRIGHTSDATA"`|
|Nombre común: **Permitir macros** <br /><br />Codificación en la directiva: **OBJMODEL**|Habilita la opción para ejecutar macros u obtener acceso remoto o mediante programación al contenido de un documento.|Permisos personalizados de Office: Como la opción de directiva personalizada **Permitir el acceso mediante programación** . No se trata de un valor por destinatario.<br /><br />Nombre en el Portal de Azure clásico: **Permitir macros**<br /><br />Nombre en Azure Portal: **Permitir Macros (OBJMODEL)**<br /><br />Nombre en las plantillas de AD RMS: **Permitir macros** <br /><br />Constante o valor de API: Sin implementar.|

## <a name="rights-included-in-permissions-levels"></a>Derechos incluidos en los niveles de permisos

Algunas aplicaciones agrupan derechos de uso en niveles de permisos para facilitar la selección de derechos de uso que suelen utilizarse de forma conjunta. Estos niveles de permisos ayudan a resumir un nivel de complejidad de los usuarios para que puedan elegir opciones basadas en roles.  Por ejemplo, **Revisor** y **Coautor**. Aunque estas opciones suelen mostrar a los usuarios un resumen de los derechos, puede que no incluyan todos los derechos enumerados en la tabla anterior.

Use la tabla siguiente para ver una lista de estos niveles de permisos y una lista completa de los derechos que contienen. Los derechos de uso se enumeran por su [nombre común](#usage-rights-and-descriptions).

|Nivel de permisos|Aplicaciones|Derechos de uso incluidos|
|---------------------|----------------|---------------------------------|
|Visor|Portal de Azure clásico <br /><br />Portal de Azure<br /><br /> Aplicación de uso compartido Rights Management para Windows<br /><br />Cliente de Azure Information Protection para Windows|Ver, abrir, Leer; Ver derechos; Responder [[1]](#footnote-1); Responder a todos [[1]](#footnote-1); Permitir macros [[2]](#footnote-2)<br /><br />Nota: Para los mensajes de correo, use Revisor en lugar de este nivel de permiso para asegurarse de que se recibe una respuesta de correo electrónico como un mensaje de correo en lugar de un archivo adjunto. Revisor también es obligatorio cuando se envía un correo a otra organización que usa el cliente de Outlook u Outlook Web App. O bien, los usuarios de su organización que no pueden usar el servicio Azure Rights Management porque se han implementado [controles de incorporación](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy).|
|Revisor|Portal de Azure clásico <br /><br />Portal de Azure<br /><br />Aplicación de uso compartido Rights Management para Windows<br /><br />Cliente de Azure Information Protection para Windows|Ver, Abrir, Leer; Guardar; Editar contenido, Editar; Ver derechos; Responder: Responder a todos [[3]](#footnote-3); Reenviar [[3]](#footnote-3); Permitir macros [[2]](#footnote-2)|
|Coautor|Portal de Azure clásico <br /><br />Portal de Azure<br /><br />Aplicación de uso compartido Rights Management para Windows<br /><br />Cliente de Azure Information Protection para Windows|Ver, Abrir, Leer; Guardar; Editar contenido, Editar; Copiar; Ver derechos; Permitir macros; Guardar como, Exportar [[4]](#footnote-4); Imprimir; Responder [[3]](#footnote-3); Responder a todos [[3]](#footnote-3); Reenviar [[3]](#footnote-3)|
|Copropietario|Portal de Azure clásico <br /><br />Portal de Azure<br /><br />Aplicación de uso compartido Rights Management para Windows<br /><br />Cliente de Azure Information Protection para Windows|Ver, Abrir, Leer; Guardar; Editar contenido, Editar; Copiar; Ver derechos; Cambiar derechos; Permitir macros; Guardar como, Exportar; Imprimir; Responder [[3]](#footnote-3); Responder a todos [[3]](#footnote-3); Reenviar [[3]](#footnote-3); Control total|

----

###### <a name="footnote-1"></a>Nota al pie 1

No se incluye en Azure Portal.

###### <a name="footnote-2"></a>Nota al pie 2

Para el cliente de Azure Information Protection para Windows, este derecho es actualmente necesario para la barra de Information Protection en las aplicaciones de Office.

###### <a name="footnote-3"></a>Nota al pie 3
No es aplicable al cliente de Azure Information Protection para Windows ni a la aplicación Rights Management sharing para Windows.

###### <a name="footnote-4"></a>Nota al pie 4
No se incluye en Azure Portal ni en el cliente de Azure Information Protection para Windows.

## <a name="rights-included-in-the-default-templates"></a>Derechos incluidos en las plantillas predeterminadas
En la tabla siguiente se enumeran los derechos de uso incluidos al crear las plantillas predeterminadas. Los derechos de uso se enumeran por su [nombre común](#usage-rights-and-descriptions).

Estas plantillas predeterminadas se crean al adquirir la suscripción. Los nombres y los derechos de uso se pueden [modificar](configure-policy-templates.md) en Azure Portal. 

|Nombre para mostrar de la plantilla|Derechos de uso desde el 6 de octubre de 2017 hasta la fecha actual|Derechos de uso antes del 6 de octubre de 2017|
|----------------|--------------------|----------|
|\<*nombre de organización> - Solo vista confidencial* <br /><br />o<br /><br /> *Extremadamente confidencial\Todos los empleados*|Ver, Abrir, Leer; Copiar; Ver derechos; Permitir macros; Imprimir, Reenviar; Responder; Responder a todos; Guardar; Editar contenido, Editar|Ver, Abrir, Leer|
|\<*nombre de organización>- Confidencial* <br /><br />o <br /><br />*Confidencial\Todos los empleados*|Ver, Abrir, Leer; Guardar como, Exportar; Copiar; Ver derechos; Cambiar derechos; Permitir macros; Imprimir, Reenviar; Responder; Responder a todos; Guardar; Editar contenido, Editar; Control total|Ver, Abrir, Leer; Guardar como, Exportar; Editar contenido, Editar; Ver derechos; Permitir macros; Reenviar; Responder; Responder a todos|

## <a name="do-not-forward-option-for-emails"></a>Opción No reenviar para correos electrónicos

Los clientes y servicios de Exchange (por ejemplo, el cliente de Outlook, Outlook en la web, las reglas de flujo de correo de Exchange y las acciones de DLP para Exchange) tienen una opción adicional de protección de derechos de información para correos electrónicos: **No reenviar**. 

Aunque esta opción aparece para los usuarios (y los administradores de Exchange) como si fuera una plantilla predeterminada de Rights Management que se puede seleccionar, **No reenviar** no es una plantilla. Esto explica por qué no se ve en Azure Portal al visualizar y administrar las plantillas de protección. En realidad, la opción **No reenviar** es un conjunto de derechos de uso que los usuarios aplican dinámicamente a los destinatarios de correo electrónico.

Cuando se aplica la opción **No reenviar** a un correo electrónico, el correo electrónico se cifra y se deben autenticar los destinatarios. Por eso, los destinatarios no pueden reenviarlo, imprimirlo ni copiarlo. Por ejemplo, en el cliente de Outlook, el botón Reenviar no está disponible, como tampoco lo están las opciones de menú **Guardar como** e **Imprimir** y no se pueden agregar ni cambiar los destinatarios de los cuadros **Para**, **CC** o **CCO**.

Los [documentos de Office](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM) sin protección que se adjuntan automáticamente al correo electrónico heredan las mismas restricciones. Los derechos de uso que se aplican a estos documentos son los siguientes: **Editar contenido, Editar**; **Guardar**; **Ver, Abrir, Leer**; y **Permitir macros**. Si quiere que cada archivo adjunto tenga derechos de uso diferentes, o en el caso de que el archivo adjunto sea un documento de Office incompatible con esta protección heredada, proteja el archivo antes de adjuntarlo al correo electrónico. Luego, puede asignar los derechos de uso específicos que necesite para el archivo. 

### <a name="difference-between-do-not-forward-and-not-granting-the-forward-usage-right"></a>Diferencia entre la opción No reenviar y no conceder el derecho de uso Reenviar

Hay una diferencia importante entre aplicar la opción **No reenviar** y aplicar una plantilla que no concede el derecho de uso **Reenviar** a un correo electrónico: la opción **No reenviar** usa una lista dinámica de usuarios autorizados basada en los destinatarios del mensaje original que elige el usuario, mientras que los derechos de la plantilla tienen una lista estática de usuarios autorizados que el administrador ha especificado anteriormente. ¿Cuál es la diferencia? Veamos un ejemplo: 

Un usuario quiere enviar información por correo electrónico a personas concretas del departamento de marketing que no debe compartirse con nadie más. ¿Debe proteger el correo electrónico con una plantilla que restringe los derechos (ver, responder y guardar) al departamento de marketing?  ¿O debe elegir la opción **No reenviar**? Ambas opciones harían que los destinatarios no pudieran reenviar el correo electrónico. 

- Si aplica la plantilla, los destinatarios pueden seguir compartiendo la información con otros usuarios del departamento de marketing. Por ejemplo, un destinatario puede usar el Explorador para arrastrar y colocar el correo electrónico en una ubicación compartida o en una unidad USB. De este modo, cualquier persona del departamento de marketing (y el propietario del correo electrónico) que tenga acceso a esta ubicación podrá ver la información del correo electrónico.
 
- Si aplica la opción **No reenviar**, los destinatarios no podrán compartir la información con ninguna persona del departamento de marketing si mueven el correo electrónico a otra ubicación. En este caso, solo los destinatarios originales (y el propietario del correo electrónico) podrán ver la información del correo electrónico.

> [!NOTE] 
> Use **No reenviar** cuando sea importante que solo los destinatarios que elige el remitente puedan ver la información del correo electrónico. Use una plantilla para correos electrónicos para restringir los derechos a un grupo de personas especificadas de antemano por el administrador, independientemente de los destinatarios que elija el remitente.

## <a name="encrypt-only-option-for-emails"></a>Opción Solo cifrar para los correos electrónicos

Cuando Exchange Online usa las nuevas capacidades para el cifrado de mensajes de Office 365, está disponible una nueva opción de correo electrónico: **Solo cifrar**.

Esta opción está disponible para los inquilinos que usan Exchange Online y se puede seleccionar en Outlook en la web, como otra opción de protección de derechos para una regla de flujo de correo, como una acción de DLP de Office 365, y en Outlook (versión mínima de [1804](/officeupdates/monthly-channel-2018#outlook-feature-updates-4) para Office 365 ProPlus, y una versión mínima de 1805 cuando tiene [aplicaciones de Office 365 que admiten Azure RMS](requirements-applications.md#windows-computers-for-information-rights-management-irm). Para obtener más información sobre la opción Solo cifrar, vea el siguiente anuncio de la entrada de blog del equipo de Office: [Encrypt only rolling out in Office 365 Message Encryption](https://aka.ms/omefeb2018) (Despliegue de la directiva Cifrar solo del cifrado de mensajes de Office 365).

Cuando se selecciona esta opción, se cifra el correo electrónico y los destinatarios deben autenticarse. Así, los destinatarios tienen todos los derechos de uso salvo **Guardar como, Exportar** y **Control total**. Esta combinación de derechos de uso implica que los destinatarios no tienen restricciones, excepto que no pueden eliminar la protección. Por ejemplo, un destinatario puede copiar del correo electrónico, imprimirlo y reenviarlo. 

Del mismo modo, de manera predeterminada, los [documentos de Office](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM) sin protección que se adjuntan al correo electrónico heredan los mismos permisos. Estos documentos se protegen de manera automática y cuando los destinatarios los descargan, pueden guardarlos, editarlos, copiarlos e imprimirlos desde las aplicaciones de Office. Cuando un destinatario guarda el documento, se puede guardar con un nombre nuevo e incluso con un formato distinto, pero solo están disponibles los formatos de archivo compatibles con la protección para que el documento no se pueda guardar sin la protección original. Si quiere que cada archivo adjunto tenga derechos de uso diferentes, o en el caso de que el archivo adjunto sea un documento de Office incompatible con esta protección heredada, proteja el archivo antes de adjuntarlo al correo electrónico. Luego, puede asignar los derechos de uso específicos que necesite para el archivo.

Como alternativa, puede cambiar esta herencia de protección de documentos si especifica `Set-IRMConfiguration -DecryptAttachmentForEncryptOnly $true` con [Exchange Online PowerShell](/powershell/exchange/exchange-online/connect-to-exchange-online-powershell/connect-to-exchange-online-powershell?view=exchange-ps). Use esta configuración cuando no sea necesario conservar la protección original del documento una vez que se autentica el usuario. Si los destinatarios abren el mensaje de correo, el documento no está protegido.

Si es necesario que el documento adjunto conserve la protección original, consulte [Protección de la colaboración con documentos mediante Azure Information Protection](secure-collaboration-documents.md).

Nota: Si ve referencias a **DecryptAttachmentFromPortal**, sepa que este parámetro está en desuso para [Set-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/set-irmconfiguration?view=exchange-ps). A menos que haya establecido previamente este parámetro, no estará disponible. 

## <a name="rights-management-issuer-and-rights-management-owner"></a>Emisor de Rights Management y propietario de Rights Management

Cuando un documento o mensaje de correo está protegido mediante el servicio Azure Rights Management, la cuenta que protege el contenido se convierte automáticamente en el emisor de Rights Management para ese contenido. Esta cuenta se ha registrado como el campo **emisor** en los [registros de uso](log-analyze-usage.md#how-to-interpret-your-azure-rights-management-usage-logs). 

Al emisor de Rights Management siempre se le concede el derecho de uso Control total para el documento o mensaje de correo, y además:

- Si la configuración de protección incluye una fecha de expiración, el emisor de Rights Management todavía puede abrir y editar el documento o mensaje de correo después de esa fecha.

- El emisor de Rights Management siempre puede obtener acceso al documento o mensaje de correo electrónico sin conexión.

- El emisor de Rights Management todavía puede abrir un documento después de que se revoque. 

De forma predeterminada, esta cuenta es también el **propietario de Rights Management** de ese contenido, como sucede cuando el usuario que ha creado el documento o mensaje de correo inicia la protección. Pero hay algunos escenarios donde un administrador o un servicio puede proteger el contenido en nombre de los usuarios. Por ejemplo:

- Un administrador protege de forma masiva archivos en un recurso compartido de archivos: La cuenta de administrador en Azure AD protege los documentos de los usuarios.

- El conector Rights Management protege los documentos de Office en una carpeta de Windows Server: La cuenta de entidad de servicio de Azure AD que se crea para el conector RMS protege los documentos de los usuarios.

En estos escenarios, el emisor de Rights Management puede asignar al propietario de Rights Management a otra cuenta mediante los SDK de Azure Information Protection o PowerShell. Por ejemplo, cuando se usa el cmdlet de PowerShell [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) con el cliente de Azure Information Protection, se puede especificar el parámetro **OwnerEmail** para asignar el propietario de Rights Management a otra cuenta. 

Cuando el emisor de Rights Management protege en nombre de los usuarios, la asignación del propietario de Rights Management garantiza que el propietario del documento o mensaje de correo original tiene el mismo nivel de control del contenido protegido como si hubiera iniciado la protección él mismo. 

Por ejemplo, el usuario que ha creado el documento puede imprimirlo, aunque ahora está protegido con una plantilla que no incluye el derecho de uso Imprimir. El mismo usuario siempre puede tener acceso a sus documentos, independientemente de la configuración de acceso sin conexión o la fecha de expiración que se hayan configurado en esa plantilla. Además, dado que el propietario de Rights Management tiene el derecho de uso Control total, este usuario también puede volver a proteger el documento para conceder acceso a usuarios adicionales (momento en que el usuario se convierte entonces en el emisor de Rights Management, así como en el propietario de Rights Management) y este usuario puede incluso quitar la protección. Pero solo el emisor de Rights Management puede realizar un seguimiento y revocar un documento.

El propietario de Rights Management de un documento o mensaje correo se ha registrado como el campo **owner-email** en los [registros de uso](log-analyze-usage.md#how-to-interpret-your-azure-rights-management-usage-logs).

Tenga en cuenta que el propietario de Rights Management es independiente del propietario del sistema de archivos de Windows. A menudo son los mismos, pero pueden ser diferentes, incluso si no se usan los SDK o PowerShell.

## <a name="rights-management-use-license"></a>Licencia de uso de Rights Management

Cuando un usuario abre un documento o correo electrónico que se ha protegido con Azure Rights Management, se concede al usuario una licencia de uso de Rights Management para ese contenido. Esta licencia de uso es un certificado que contiene los derechos de uso del usuario para el documento o mensaje de correo electrónico y la clave de cifrado que se ha usado para cifrar el contenido. La licencia de uso, además, contiene una fecha de expiración, si se ha establecido, y el período de validez de la licencia de uso.

Un usuario debe tener una licencia de uso válida para abrir el contenido además de su certificado de cuenta de derechos (RAC), que es un certificado que se otorga cuando [se inicializa el entorno de usuario](how-does-it-work.md#initializing-the-user-environment) y se renueva cada 31 días.

Mientras la licencia de uso esté en vigor, no es necesario autenticar ni volver a autorizar al usuario para el contenido. Esto permite al usuario seguir abriendo el documento o el correo electrónico protegido sin conexión a Internet. Una vez que el período de validez de la licencia de uso haya expirado, la siguiente vez que el usuario acceda al documento o correo electrónico protegido, deberá volver a autenticarse y autorizarse. 

Si los documentos y mensajes de correo electrónico se protegen mediante una etiqueta o una plantilla que define la configuración de protección, puede cambiar esta configuración en la plantilla o etiqueta sin tener que volver a proteger el contenido. Si el usuario ya ha accedido al contenido, los cambios se aplican una vez que la licencia de uso haya expirado. Sin embargo, si los usuarios aplican permisos personalizados (también conocidos como directiva de permisos "ad-hoc") y estos permisos deben cambiarse después de haber protegido el documento o correo electrónico, ese contenido se debe volver a proteger con los nuevos permisos. Los permisos personalizados para un mensaje de correo electrónico se implementan con la opción No reenviar.

El valor predeterminado del período de validez de la licencia de uso de un inquilino es de 30 días. Este valor se puede configurar con el cmdlet de PowerShell [Set-AadrmMaxUseLicenseValidityTime](/powershell/module/aadrm/set-aadrmmaxuselicensevaliditytime). Puede establecer una configuración más restrictiva para el momento en el que se aplique la protección mediante una etiqueta o plantilla:

- Al configurar una etiqueta o una plantilla en Azure Portal, el período de validez de la licencia de uso toma su valor de la opción **Permitir el acceso sin conexión**. 
    
    Para obtener más información y orientaciones para configurar este valor en Azure Portal, vea la tabla [Información sobre la configuración de protección](configure-policy-protection.md#information-about-the-protection-settings) a fin de conocer cómo configurar una etiqueta para la protección de Rights Management.

- Al configurar una plantilla mediante PowerShell, el período de validez de la licencia de uso toma su valor del parámetro *LicenseValidityDuration* de los cmdlets [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty) y [Add-AadrmTemplate](/powershell/module/aadrm/add-aadrmtemplate).
    
    Para obtener más información e instrucciones para configurar este valor mediante PowerShell, vea la ayuda de cada cmdlet.

## <a name="see-also"></a>Consulte también
[Configuración y administración de plantillas para Azure Information Protection](configure-policy-templates.md)

[Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos](configure-super-users.md)
