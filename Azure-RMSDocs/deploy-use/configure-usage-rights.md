---
title: "Configuración de los derechos de uso para Azure Rights Management - AIP"
description: "Conozca e identifique los derechos específicos que se usan al proteger archivos o correos electrónicos con el servicio Azure Rights Management de Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/26/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 526a0ef3bcc5ebf07c4993b9e5dd602683593a45
ms.sourcegitcommit: 85261fbc9e6ce71a2001d954cb2fc2d190695f6a
translationtype: HT
---
# <a name="configuring-usage-rights-for-azure-rights-management"></a>Configuración de los derechos de uso para Azure Rights Management

>*Se aplica a: Azure Information Protection, Office 365*

Cuando establezca protección en archivos o correos electrónicos con el servicio Azure Rights Management de Azure Information Protection y no use ninguna plantilla, deberá configurar los derechos de uso por su cuenta. Además, al configurar plantillas personalizadas para Azure Rights Management, se seleccionan los derechos de uso que se aplicarán automáticamente cuando los usuarios, los administradores o los servicios configurados seleccionen la plantilla. Por ejemplo, en el Portal de Azure clásico, puede seleccionar los roles que configuran una agrupación lógica de derechos de uso o puede configurar los derechos individuales.

Use este artículo como ayuda para configurar los derechos de uso que quiere para la aplicación que esté usando y para entender cómo las aplicaciones interpretan estos derechos.

## <a name="usage-rights-and-descriptions"></a>Derechos de uso y descripciones
En la tabla siguiente se enumeran y se describen los derechos de uso que admite Rights Management y cómo se usan y se interpretan. Se enumeran por su **Nombre común**, que es normalmente cómo se muestra o se referencia el derecho de uso, como una versión más descriptiva del valor de una sola palabra que se usa en el código (el valor **Codificación en la directiva**). 

**Constante o valor de API** es el nombre de SDK para una llamada de API de MSIPC, que se usa al escribir una aplicación habilitada para RMS que comprueba un derecho de uso o agrega un derecho de uso a una directiva.


|Right|Descripción|Implementación|
|-------------------------------|---------------------------|-----------------|
|Nombre común: **Editar contenido, Editar** <br /><br />Codificación en la directiva: **DOCEDIT**|Permite al usuario modificar, reorganizar, formatear o filtrar el contenido dentro de la aplicación. No concede el derecho a guardar la copia modificada.|Derechos personalizados de Office: como parte de las opciones **Cambiar** y **Control total**. <br /><br />Nombre en el Portal de Azure clásico: **Editar contenido**<br /><br />Nombre en Azure Portal: incluido en **Editar y guardar**<br /><br />Nombre en las plantillas de AD RMS: **Editar** <br /><br />Constante o valor de API: no aplicable.|
|Nombre común: **Guardar** <br /><br />Codificación en la directiva: **EDIT**|Permite al usuario guardar el documento en su ubicación actual.<br /><br />En las aplicaciones de Office, este derecho también permite al usuario modificar el documento.|Derechos personalizados de Office: como parte de las opciones **Cambiar** y **Control total**. <br /><br />Nombre en el Portal de Azure clásico: **Guardar archivo**<br /><br />Nombre en Azure Portal: incluido en **Editar y guardar**<br /><br />Nombre en las plantillas de AD RMS: **Guardar** <br /><br />Constante o valor de API: `IPC_GENERIC_WRITE L"EDIT"`|
|Nombre común: **Comentario** <br /><br />Codificación en la directiva: **COMMENT**|Habilita la opción para agregar anotaciones o comentarios al contenido.<br /><br />Este derecho está disponible en el SDK como directiva ad hoc en el módulo de Azure Information Protection y RMS Protection para Windows PowerShell y se implementó en algunas aplicaciones de proveedores de software. Sin embargo, no se usa extensamente y no es compatible actualmente con las aplicaciones de Office.|Derechos personalizados de Office: no implementados. <br /><br />Nombre en el Portal de Azure clásico: no implementado.<br /><br />Nombre en Azure Portal: no implementado.<br /><br />Nombre en las plantillas de AD RMS: no implementado. <br /><br />Constante o valor de API: `IPC_GENERIC_COMMENT L"COMMENT`|
|Nombre común: **Guardar como, Exportar** <br /><br />Codificación en la directiva: **EXPORT**|Habilita la opción para guardar el contenido con un nombre de archivo diferente (Guardar como). En los documentos de Office y el cliente de Azure Information Protection, el archivo se puede guardar sin protección.<br /><br />Este derecho también permite al usuario realizar otras opciones de exportación en las aplicaciones, como **Enviar a OneNote**.<br /><br /> Nota: Si no se concede este derecho, las aplicaciones de Office permiten a un usuario guardar un documento en un nuevo nombre si el formato de archivo seleccionado admite la protección de Rights Management de forma nativa.|Derechos personalizados de Office: como parte de las opciones **Cambiar** y **Control total**. <br /><br />Nombre en el Portal de Azure clásico: **Exportar contenido (Guardar como)** <br /><br />Nombre en Azure Portal: incluido en **Control total**<br /><br />Nombre en las plantillas de AD RMS: **Exportar (Guardar como)** <br /><br />Constante o valor de API: `IPC_GENERIC_EXPORT L"EXPORT"`|
|Nombre común: **Reenviar** <br /><br />Codificación en la directiva: **FORWARD**|Habilita la opción para reenviar un mensaje de correo electrónico y agregar destinatarios a las líneas **Para** y **CO** . Este derecho no se aplica a documentos, solo a mensajes de correo electrónico.<br /><br />No permite que el reenviador conceda derechos a otros usuarios como parte de la acción de reenvío. <br /><br />Cuando conceda este derecho, conceda también el derecho **Editar contenido, Editar** (nombre común) para asegurarse de que el correo electrónico original forma parte del mensaje de correo reenviado y no es un archivo adjunto. Este derecho también es obligatorio cuando se envía un correo a otra organización que usa el cliente de Outlook u Outlook Web App.|Derechos personalizados de Office: se deniega al usar la directiva estándar **No reenviar**.<br /><br />Nombre en el Portal de Azure clásico: **Reenviar**<br /><br />Nombre en Azure Portal: **Reenviar**<br /><br />Nombre en las plantillas de AD RMS: **Reenviar** <br /><br />Constante o valor de API: `IPC_EMAIL_FORWARD L"FORWARD"`|
|Nombre común: **Control total** <br /><br />Codificación en la directiva: **OWNER**|Concede todos los derechos para el documento; se pueden realizar todas las acciones disponibles.<br /><br />Incluye la capacidad de quitar la protección de un documento y volver a protegerlo. <br /><br />Tenga en cuenta que este derecho de uso no es el mismo que el [propietario de Rights Management](#rights-management-issuer-and-rights-management-owner).|Derechos personalizados de Office: como parte de la opción personalizada **Control total**.<br /><br />Nombre en el Portal de Azure clásico: **Control total**<br /><br />Nombre en Azure Portal: **Control total**<br /><br />Nombre en las plantillas de AD RMS: **Control total** <br /><br />Constante o valor de API: `IPC_GENERIC_ALL L"OWNER"`|
|Nombre común: **Imprimir** <br /><br />Codificación en la directiva: **PRINT**|Habilita las opciones para imprimir el contenido.|Derechos personalizados de Office: como la opción **Imprimir contenido** de los permisos personalizados. No se trata de un valor por destinatario.<br /><br />Nombre en el Portal de Azure clásico: **Imprimir**<br /><br />Nombre en Azure Portal: **Imprimir**<br /><br />Nombre en las plantillas de AD RMS: **Imprimir** <br /><br />Constante o valor de API: `IPC_GENERIC_PRINT L"PRINT"`|
|Nombre común: **Responder** <br /><br />Codificación en la directiva: **REPLY**|Habilita la opción **Responder** en un cliente de correo electrónico, sin permitir que se realicen cambios en las líneas **Para** o **CC**.<br /><br />Cuando conceda este derecho, conceda también el derecho **Editar contenido, Editar** (nombre común) para asegurarse de que el correo electrónico original forma parte del mensaje de correo reenviado y no es un archivo adjunto. Este derecho también es obligatorio cuando se envía un correo a otra organización que usa el cliente de Outlook u Outlook Web App.|Derechos personalizados de Office: no aplicables.<br /><br />Nombre en el Portal de Azure clásico: **Responder**<br /><br />Nombre en las plantillas de AD RMS: **Responder** <br /><br />Constante o valor de API: `IPC_EMAIL_REPLY`|
|Nombre común: **Responder a todos** <br /><br />Codificación en la directiva: **REPLYALL**|Habilita la opción **Responder a todos** en un cliente de correo electrónico, pero no permite al usuario agregar a destinatarios a las líneas **Para** o **CO** .<br /><br />Cuando conceda este derecho, conceda también el derecho **Editar contenido, Editar** (nombre común) para asegurarse de que el correo electrónico original forma parte del mensaje de correo reenviado y no es un archivo adjunto. Este derecho también es obligatorio cuando se envía un correo a otra organización que usa el cliente de Outlook u Outlook Web App.|Derechos personalizados de Office: no aplicables.<br /><br />Nombre en el Portal de Azure clásico: **Responder a todos**<br /><br />Nombre en Azure Portal: **Responder a todos**<br /><br />Nombre en las plantillas de AD RMS: **Responder a todos** <br /><br />Constante o valor de API: `IPC_EMAIL_REPLYALL L"REPLYALL"`|
|Nombre común: **Ver, Abrir, Leer** <br /><br />Codificación en la directiva: **VIEW**|Permite al usuario abrir el documento y ver el contenido.|Derechos personalizados de Office: como la opción **Ver** de la directiva personalizada **Leer**.<br /><br />Nombre en el Portal de Azure clásico: **Ver**<br /><br />Nombre en Azure Portal: **Ver contenido**<br /><br />Nombre en las plantillas de AD RMS: **Responder a todos** <br /><br />Constante o valor de API: `IPC_GENERIC_READ L"VIEW"`|
|Nombre común: **Copiar** <br /><br />Codificación en la directiva: **EXTRACT**|Habilita las opciones para copiar los datos (incluidas las capturas de pantalla) del documento en el mismo documento o en otro documento.<br /><br />En algunas aplicaciones, también permite que todo el documento se guarde en sin protección.|Derechos personalizados de Office: como la opción de directiva personalizada **Permitir que los usuarios con acceso de lectura copien el contenido**.<br /><br />Nombre en el Portal de Azure clásico: **Copiar y extraer contenido**<br /><br />Nombre en Azure Portal: **Copiar y extraer contenido**<br /><br />Nombre en las plantillas de AD RMS: **Extraer** <br /><br />Constante o valor de API: `IPC_GENERIC_EXTRACT L"EXTRACT"`|
|Nombre común: **Permitir macros** <br /><br />Codificación en la directiva: **OBJMODEL**|Habilita la opción para ejecutar macros u obtener acceso remoto o mediante programación al contenido de un documento.|Derechos personalizados de Office: como la opción de directiva personalizada **Permitir el acceso mediante programación**. No se trata de un valor por destinatario.<br /><br />Nombre en el Portal de Azure clásico: **Permitir macros**<br /><br />Nombre en Azure Portal: se incluye en todos los derechos que se pueden seleccionar porque este derecho es necesario para la barra de Azure Information Protection en las aplicaciones de Office.<br /><br />Nombre en las plantillas de AD RMS: **Permitir macros** <br /><br />Constante o valor de API: no implementado.|

## <a name="rights-included-in-permissions-levels"></a>Derechos incluidos en los niveles de permisos

Algunas aplicaciones agrupan derechos de uso en niveles de permisos para facilitar la selección de derechos de uso que suelen utilizarse de forma conjunta. Estos niveles de permisos ayudan a resumir un nivel de complejidad de los usuarios para que puedan elegir opciones basadas en roles.  Por ejemplo, **Revisor** y **Coautor**. Aunque estas opciones suelen mostrar a los usuarios un resumen de los derechos, puede que no incluyan todos los derechos enumerados en la tabla anterior.

Utilice la tabla siguiente para ver una lista de estos niveles de permisos y una lista completa de los derechos que contienen.


|Nivel de permisos|Aplicaciones|Derechos incluidos (nombre común)|
|---------------------|----------------|---------------------------------|
|Visor|Portal de Azure clásico<br /><br />Aplicación de uso compartido Rights Management para Windows<br /><br />Cliente de Azure Information Protection para Windows|Ver, Abrir, Leer; Responder; Responder a todos<br /><br />Nota: Para los mensajes de correo, use Revisor en lugar de este nivel de permiso para asegurarse de que se recibe una respuesta de correo electrónico como un mensaje de correo en lugar de un archivo adjunto. Revisor también es obligatorio cuando se envía un correo a otra organización que usa el cliente de Outlook u Outlook Web App.|
|Revisor|Portal de Azure clásico<br /><br />Aplicación de uso compartido Rights Management para Windows<br /><br />Cliente de Azure Information Protection para Windows|Ver, Abrir, Leer; Guardar; Editar contenido, Editar; Responder [[1]](#footnote-1); Responder a todos [[1]](#footnote-1); Reenviar [[1]](#footnote-1)|
|Coautor|Portal de Azure clásico<br /><br />Aplicación de uso compartido Rights Management para Windows<br /><br />Cliente de Azure Information Protection para Windows|Ver, Abrir, Leer; Guardar; Editar contenido, Editar; Copiar; Ver derechos; Permitir macros; Guardar como, Exportar [[2]](#footnote-2); Imprimir; Responder [[1]](#footnote-1); Responder a todos [[1]](#footnote-1); Reenviar [[1]](#footnote-1)|
|Copropietario|Portal de Azure clásico<br /><br />Aplicación de uso compartido Rights Management para Windows<br /><br />Cliente de Azure Information Protection para Windows|Ver, Abrir, Leer; Guardar; Editar contenido, Editar; Copiar; Ver derechos; Permitir macros; Guardar como, Exportar; Imprimir; Responder [[1]](#footnote-1); Responder a todos [[1]](#footnote-1); Reenviar [[1]](#footnote-1); Control total|

----

###### <a name="footnote-1"></a>Nota al pie 1
No es aplicable al cliente de Azure Information Protection para Windows ni a la aplicación Rights Management sharing para Windows.

###### <a name="footnote-2"></a>Nota al pie 2
No se incluye en el cliente de Azure Information Protection para Windows. En este cliente, el derecho de uso de exportación incluye la posibilidad de quitar la protección.


## <a name="rights-included-in-the-default-templates"></a>Derechos incluidos en las plantillas predeterminadas
Los derechos que se incluyen con las plantillas predeterminadas son los siguientes:

|Nombre para mostrar|Derechos incluidos (nombre común)|
|----------------|---------------------------------|
|&lt;*nombre de organización*&gt; *- Solo vista confidencial*|Ver, Abrir, Leer|
|&lt;*nombre de organización*&gt; *- Confidencial*|Ver, Abrir, Leer; Guardar; Editar contenido, Editar; Ver derechos; Permitir macros; Reenviar; Responder; Responder a todos|

## <a name="do-not-forward-option-for-emails"></a>Opción No reenviar para correos electrónicos

Los clientes y servicios de Exchange (por ejemplo, el cliente de Outlook, la aplicación Outlook Web Access y las reglas de transporte de Exchange) tienen una opción adicional de protección de derechos de información para correos electrónicos: **No reenviar**. 

Aunque esta opción aparece para los usuarios (y los administradores de Exchange) como si fuera una plantilla predeterminada de Rights Management que se puede seleccionar, **No reenviar** no es una plantilla. Esto explica por qué no se ve en el Portal de Azure clásico cuando se visualizan y se administran las plantillas de Azure Rights Management. En realidad, la opción **No reenviar** es un conjunto de derechos que los usuarios aplican dinámicamente a los destinatarios de correo electrónico.

Cuando se aplica la opción **No reenviar** a un correo electrónico, los destinatarios no pueden reenviarlo, imprimirlo, copiar contenido, guardar datos adjuntos ni guardarlo con un nombre diferente. Por ejemplo, en el cliente de Outlook, el botón Reenviar no está disponible, tampoco están disponibles las opciones de menú **Guardar como**, **Guardar datos adjuntos** e **Imprimir**, y no se pueden agregar ni cambiar destinatarios de los cuadros **Para**, **CC** o **CCO**.

Hay una diferencia importante entre aplicar la opción **No reenviar** y aplicar una plantilla que no concede el derecho Reenviar a un correo electrónico: la opción **No reenviar** usa una lista dinámica de usuarios autorizados basada en los destinatarios del mensaje original que elige el usuario, mientras que los derechos de la plantilla tienen una lista estática de usuarios autorizados que el administrador ha especificado anteriormente. ¿Cuál es la diferencia? Veamos un ejemplo: 

Un usuario quiere enviar información por correo electrónico a personas concretas del departamento de marketing que no debe compartirse con nadie más. ¿Debe proteger el correo electrónico con una plantilla que restringe los derechos (ver, responder y guardar) al departamento de marketing?  ¿O debe elegir la opción **No reenviar**? Ambas opciones harían que los destinatarios no pudieran reenviar el correo electrónico. 

- Si aplica la plantilla, los destinatarios pueden seguir compartiendo la información con otros usuarios del departamento de marketing. Por ejemplo, un destinatario puede usar el Explorador para arrastrar y colocar el correo electrónico en una ubicación compartida o en una unidad USB. De este modo, cualquier persona del departamento de marketing (y el propietario del correo electrónico) que tenga acceso a esta ubicación podrá ver la información del correo electrónico.
 
- Si aplica la opción **No reenviar**, los destinatarios no podrán compartir la información con ninguna persona del departamento de marketing si mueven el correo electrónico a otra ubicación. En este caso, solo los destinatarios originales (y el propietario del correo electrónico) podrán ver la información del correo electrónico.

> [!NOTE] 
> Use **No reenviar** cuando sea importante que solo los destinatarios que elige el remitente puedan ver la información del correo electrónico. Use una plantilla para correos electrónicos para restringir los derechos a un grupo de personas especificadas de antemano por el administrador, independientemente de los destinatarios que elija el remitente.

## <a name="rights-management-issuer-and-rights-management-owner"></a>Emisor de Rights Management y propietario de Rights Management

Cuando un documento o mensaje de correo está protegido mediante el servicio Azure Rights Management, la cuenta que protege el contenido se convierte automáticamente en el emisor de Rights Management para ese contenido. Esta cuenta se ha registrado como el campo **emisor** en los [registros de uso](log-analyze-usage.md#how-to-interpret-your-azure-rights-management-usage-logs). 

Al emisor de Rights Management siempre se le concede el derecho de uso Control total para el documento o mensaje de correo, y además:

- Si la configuración de protección incluye una fecha de expiración, el emisor de Rights Management todavía puede abrir y editar el documento o mensaje de correo después de esa fecha.

- El emisor de Rights Management siempre puede obtener acceso al documento o mensaje de correo electrónico sin conexión.

- El emisor de Rights Management todavía puede abrir un documento después de que se revoque. 

De forma predeterminada, esta cuenta es también el **propietario de Rights Management** de ese contenido, como sucede cuando el usuario que ha creado el documento o mensaje de correo inicia la protección. Pero hay algunos escenarios donde un administrador o un servicio puede proteger el contenido en nombre de los usuarios. Por ejemplo:

- Un administrador protege de forma masiva los archivos en un recurso compartido: la cuenta de administrador en Azure AD protege los documentos de los usuarios.

- El conector Rights Management protege los documentos de Office en una carpeta de Windows Server: la cuenta de la entidad de servicio en Azure AD que se ha creado para el conector RMS protege los documentos de los usuarios.

En estos escenarios, el emisor de Rights Management puede asignar al propietario de Rights Management a otra cuenta mediante los SDK de Azure Information Protection o PowerShell. Por ejemplo, cuando se usa el cmdlet de PowerShell [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) con el cliente de Azure Information Protection, se puede especificar el parámetro **OwnerEmail** para asignar el propietario de Rights Management a otra cuenta. 

Cuando el emisor de Rights Management protege en nombre de los usuarios, la asignación del propietario de Rights Management garantiza que el propietario del documento o mensaje de correo original tiene el mismo nivel de control del contenido protegido como si hubiera iniciado la protección él mismo. 

Por ejemplo, el usuario que ha creado el documento puede imprimirlo, aunque ahora está protegido con una plantilla que no incluye el derecho de uso Imprimir. El mismo usuario siempre puede tener acceso a sus documentos, independientemente de la configuración de acceso sin conexión o la fecha de expiración que se hayan configurado en esa plantilla. Además, dado que el propietario de Rights Management tiene el derecho de uso Control total, este usuario también puede volver a proteger el documento para conceder el acceso a usuarios adicionales (momento en que el usuario se convierte entonces en el emisor de Rights Management, así como en el propietario de Rights Management) y este usuario puede incluso quitar la protección. Pero solo el emisor de Rights Management puede realizar un seguimiento y revocar un documento.

El propietario de Rights Management de un documento o mensaje correo se ha registrado como el campo **owner-email** en los [registros de uso](log-analyze-usage.md#how-to-interpret-your-azure-rights-management-usage-logs).

Tenga en cuenta que el propietario de Rights Management es independiente del propietario del sistema de archivos de Windows. A menudo son los mismos, pero pueden ser diferentes, incluso si no se usan los SDK o PowerShell.

## <a name="see-also"></a>Véase también
[Configuración de plantillas personalizadas para el servicio Azure Rights Management](configure-custom-templates.md)

[Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos](configure-super-users.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

