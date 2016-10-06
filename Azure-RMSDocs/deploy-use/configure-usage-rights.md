---
title: "Configuración de los derechos de uso de Azure Rights Management | Azure Information Protection"
description: "Conozca e identifique los derechos específicos que se usan al proteger archivos o correos electrónicos con el servicio Azure Rights Management de Azure Information Protection."
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d5b6a1fc3fa0a19f3a6b65aa7b8815eda7432cd7
ms.openlocfilehash: a11d027789a63ae845812068e34f527f15a02314


---

# Configuración de los derechos de uso para Azure Rights Management

>*Se aplica a: Azure Information Protection y Office 365*

Cuando establezca protección en archivos o correos electrónicos con el servicio Azure Rights Management de Azure Information Protection y no use ninguna plantilla, deberá configurar los derechos de uso por su cuenta. Además, al configurar plantillas personalizadas para Azure Rights Management, se seleccionan los derechos de uso que se aplicarán automáticamente cuando los usuarios, los administradores o los servicios configurados seleccionen la plantilla. Por ejemplo, en el Portal de Azure clásico, puede seleccionar los roles que configuran una agrupación lógica de derechos de uso o puede configurar los derechos individuales.

Use este artículo como ayuda para configurar los derechos de uso que quiere para la aplicación que esté usando y para entender cómo las aplicaciones interpretan estos derechos.

## Derechos de uso y descripciones
En la tabla siguiente se enumeran y se describen los derechos de uso que admite Rights Management y cómo se usan y se interpretan. Se enumeran por su **Nombre común**, que es normalmente cómo se muestra o se referencia el derecho de uso, como una versión más descriptiva del valor de una sola palabra que se usa en el código (el valor **Codificación en la directiva**). **Constante o valor de API** es el nombre de SDK para una llamada de API de MSIPC, que se usa al escribir una aplicación habilitada para RMS que comprueba un derecho de uso o agrega un derecho de uso a una directiva.


|Right|Descripción|Implementación|
|-------------------------------|---------------------------|-----------------|
|Nombre común: **Editar contenido, Editar** <br /><br />Codificación en la directiva: **DOCEDIT**|Permite al usuario modificar, reorganizar, formatear o filtrar el contenido dentro de la aplicación. No concede el derecho a guardar la copia modificada.|Derechos personalizados de Office: como parte de las opciones **Cambiar** y **Control total**. <br /><br />Nombre en el Portal de Azure clásico: **Editar contenido**<br /><br />Nombre en las plantillas de AD RMS: **Editar** <br /><br />Constante o valor de API: no aplicable.|
|Nombre común: **Guardar** <br /><br />Codificación en la directiva: **EDIT**|Permite al usuario guardar el documento en su ubicación actual.<br /><br />En las aplicaciones de Office, este derecho también permite al usuario modificar el documento.|Derechos personalizados de Office: como parte de las opciones **Cambiar** y **Control total**. <br /><br />Nombre en el Portal de Azure clásico: **Guardar archivo**<br /><br />Nombre en las plantillas de AD RMS: **Guardar** <br /><br />Constante o valor de API: `IPC_GENERIC_WRITE L"EDIT"`|
|Nombre común: **Comentario** <br /><br />Codificación en la directiva: **COMMENT**|Habilita la opción para agregar anotaciones o comentarios al contenido.<br /><br />Este derecho está disponible en el SDK como directiva ad hoc en el módulo de protección de RMS para Windows PowerShell y se implementó en algunas aplicaciones de proveedores de software. Sin embargo, no se usa extensamente y no es compatible actualmente con las aplicaciones de Office.|Derechos personalizados de Office: no implementados. <br /><br />Nombre en el Portal de Azure clásico: no implementado.<br /><br />Nombre en las plantillas de AD RMS: no implementado. <br /><br />Constante o valor de API: `IPC_GENERIC_COMMENT L"COMMENT`|
|Nombre común: **Guardar como, Exportar** <br /><br />Codificación en la directiva: **EXPORT**|Habilita la opción para guardar el contenido con un nombre de archivo diferente (Guardar como). En el caso de los documentos de Office, el archivo puede guardarse sin protección.<br /><br />Este derecho también permite al usuario realizar otras opciones de exportación en las aplicaciones, como **Enviar a OneNote**.|Derechos personalizados de Office: como parte de las opciones **Cambiar** y **Control total**. <br /><br />Nombre en el Portal de Azure clásico: **Exportar contenido (Guardar como)**<br /><br />Nombre en las plantillas de AD RMS: **Exportar (Guardar como)** <br /><br />Constante o valor de API: `IPC_GENERIC_EXPORT L"EXPORT"`|
|Nombre común: **Reenviar** <br /><br />Codificación en la directiva: **FORWARD**|Habilita la opción para reenviar un mensaje de correo electrónico y agregar destinatarios a las líneas **Para** y **CO** . Este derecho no se aplica a documentos, solo a mensajes de correo electrónico.<br /><br />No permite que el reenviador conceda derechos a otros usuarios como parte de la acción de reenvío.|Derechos personalizados de Office: se deniega al usar la directiva estándar **No reenviar**.<br /><br />Nombre en el Portal de Azure clásico: **Reenviar**<br /><br />Nombre en las plantillas de AD RMS: **Reenviar** <br /><br />Constante o valor de API: `IPC_EMAIL_FORWARD L"FORWARD"`|
|Nombre común: **Control total** <br /><br />Codificación en la directiva: **OWNER**|Concede todos los derechos para el documento; se pueden realizar todas las acciones disponibles.<br /><br />Incluye la capacidad de quitar la protección de un documento y volver a protegerlo.|Derechos personalizados de Office: como parte de la opción personalizada **Control total**.<br /><br />Nombre en el Portal de Azure clásico: **Control total**<br /><br />Nombre en las plantillas de AD RMS: **Control total** <br /><br />Constante o valor de API: `IPC_GENERIC_ALL L"OWNER"`|
|Nombre común: **Imprimir** <br /><br />Codificación en la directiva: **PRINT**|Habilita las opciones para imprimir el contenido.|Derechos personalizados de Office: como la opción **Imprimir contenido** de los permisos personalizados. No se trata de un valor por destinatario.<br /><br />Nombre en el Portal de Azure clásico: **Imprimir**<br /><br />Nombre en las plantillas de AD RMS: **Imprimir** <br /><br />Constante o valor de API: `IPC_GENERIC_PRINT L"PRINT"`|
|Nombre común: **Responder** <br /><br />Codificación en la directiva: **REPLY**|Habilita la opción **Responder** en un cliente de correo electrónico, sin permitir que se realicen cambios en las líneas **Para** o **CC**.|Derechos personalizados de Office: no aplicables.<br /><br />Nombre en el Portal de Azure clásico: **Responder**<br /><br />Nombre en las plantillas de AD RMS: **Responder** <br /><br />Constante o valor de API: `IPC_EMAIL_REPLY`|
|Nombre común: **Responder a todos** <br /><br />Codificación en la directiva: **REPLYALL**|Habilita la opción **Responder a todos** en un cliente de correo electrónico, pero no permite al usuario agregar a destinatarios a las líneas **Para** o **CO** .|Derechos personalizados de Office: no aplicables.<br /><br />Nombre en el Portal de Azure clásico: **Responder a todos**<br /><br />Nombre en las plantillas de AD RMS: **Responder a todos** <br /><br />Constante o valor de API: `IPC_EMAIL_REPLYALL L"REPLYALL"`|
|Nombre común: **Ver, Abrir, Leer** <br /><br />Codificación en la directiva: **VIEW**|Permite al usuario abrir el documento y ver el contenido.|Derechos personalizados de Office: como la opción **Ver** de la directiva personalizada **Leer**.<br /><br />Nombre en el Portal de Azure clásico: **Ver**<br /><br />Nombre en las plantillas de AD RMS: **Responder a todos** <br /><br />Constante o valor de API: `IPC_GENERIC_READ L"VIEW"`|
|Nombre común: **Copiar** <br /><br />Codificación en la directiva: **EXTRACT**|Habilita las opciones para copiar los datos (incluidas las capturas de pantalla) del documento en el mismo documento o en otro documento.<br /><br />En algunas aplicaciones, también permite que todo el documento se guarde en sin protección.|Derechos personalizados de Office: como la opción de directiva personalizada **Permitir que los usuarios con acceso de lectura copien el contenido**.<br /><br />Nombre en el Portal de Azure clásico: **Copiar y extraer contenido**<br /><br />Nombre en las plantillas de AD RMS: **Extraer** <br /><br />Constante o valor de API: `IPC_GENERIC_EXTRACT L"EXTRACT"`|
|Nombre común: **Permitir macros** <br /><br />Codificación en la directiva: **OBJMODEL**|Habilita la opción para ejecutar macros u obtener acceso remoto o mediante programación al contenido de un documento.|Derechos personalizados de Office: como la opción de directiva personalizada **Permitir el acceso mediante programación**. No se trata de un valor por destinatario.<br /><br />Nombre en el Portal de Azure clásico: **Permitir macros**<br /><br />Nombre en las plantillas de AD RMS: **Permitir macros** <br /><br />Constante o valor de API: no implementado.|



## Derechos incluidos en los niveles de permisos

Algunas aplicaciones agrupan derechos de uso en niveles de permisos para facilitar la selección de derechos de uso que suelen utilizarse de forma conjunta. Estos niveles de permisos ayudan a resumir un nivel de complejidad de los usuarios para que puedan elegir opciones basadas en roles.  Por ejemplo, **Revisor** y **Coautor**. Aunque estas opciones suelen mostrar a los usuarios un resumen de los derechos, puede que no incluyan todos los derechos enumerados en la tabla anterior.

Utilice la tabla siguiente para ver una lista de estos niveles de permisos y una lista completa de los derechos que contienen.

|Nivel de permisos|Aplicaciones|Derechos incluidos (nombre común)|
|---------------------|----------------|---------------------------------|
|Visor|Portal de Azure clásico<br /><br />Aplicación de uso compartido Rights Management para Windows|Ver, Abrir, Leer; Responder; Responder a todos|
|Revisor|Portal de Azure clásico<br /><br />Aplicación de uso compartido Rights Management para Windows|Ver, Abrir, Leer; Guardar; Editar contenido, Editar; Responder [[1]](#footnote-1); Responder a todos [[1]](#footnote-1); Reenviar [[1]](#footnote-1)|
|Coautor|Portal de Azure clásico<br /><br />Aplicación de uso compartido Rights Management para Windows|Ver, Abrir, Leer; Guardar; Editar contenido, Editar; Copiar; Ver derechos; Permitir macros; Guardar como, Exportar; Imprimir; Responder [[1]](#footnote-1); Responder a todos [[1]](#footnote-1); Reenviar [[1]](#footnote-1)|
|Copropietario|Portal de Azure clásico<br /><br />Aplicación de uso compartido Rights Management para Windows|Ver, Abrir, Leer; Guardar; Editar contenido, Editar; Copiar; Ver derechos; Permitir macros; Guardar como, Exportar; Imprimir; Responder [[1]](#footnote-1); Responder a todos [[1]](#footnote-1); Reenviar [[1]](#footnote-1); Control total|

----

###### Nota al pie 1
No aplicable a la aplicación Rights Management sharing para Windows.

## Derechos incluidos en las plantillas predeterminadas
Los derechos que se incluyen con las plantillas predeterminadas son los siguientes:

|Nombre para mostrar|Derechos incluidos (nombre común)|
|----------------|---------------------------------|
|&lt;*nombre de organización*&gt; *- Solo vista confidencial*|Ver, Abrir, Leer|
|&lt;*nombre de organización*&gt; *- Confidencial*|Ver, Abrir, Leer; Guardar; Editar contenido, Editar; Ver derechos; Permitir macros; Reenviar; Responder; Responder a todos|

## Opción No reenviar para correos electrónicos

Los clientes y servicios de Exchange (por ejemplo, el cliente de Outlook, la aplicación Outlook Web Access y las reglas de transporte de Exchange) tienen una opción adicional de protección de derechos de información para correos electrónicos: **No reenviar**. 

Aunque esta opción aparece para los usuarios (y los administradores de Exchange) como si fuera una plantilla predeterminada de Rights Management que se puede seleccionar, **No reenviar** no es una plantilla. Esto explica por qué no se ve en el Portal de Azure clásico cuando se visualizan y se administran las plantillas de Azure Rights Management. En realidad, la opción **No reenviar** es un conjunto de derechos que los usuarios aplican dinámicamente a los destinatarios de correo electrónico.

Cuando se aplica la opción **No reenviar** a un correo electrónico, los destinatarios no pueden reenviarlo, imprimirlo, copiar contenido, guardar datos adjuntos ni guardarlo con un nombre diferente. Por ejemplo, en el cliente de Outlook, el botón Reenviar no está disponible, tampoco están disponibles las opciones de menú **Guardar como**, **Guardar datos adjuntos** e **Imprimir**, y no se pueden agregar ni cambiar destinatarios de los cuadros **Para**, **CC** o **CCO**.

Hay una diferencia importante entre aplicar la opción **No reenviar** y aplicar una plantilla que no concede el derecho Reenviar a un correo electrónico: la opción **No reenviar** usa una lista dinámica de usuarios autorizados basada en los destinatarios del mensaje original que elige el usuario, mientras que los derechos de la plantilla tienen una lista estática de usuarios autorizados que el administrador ha especificado anteriormente. ¿Cuál es la diferencia? Veamos un ejemplo: 

Un usuario quiere enviar información por correo electrónico a personas concretas del departamento de marketing que no debe compartirse con nadie más. ¿Debe proteger el correo electrónico con una plantilla que restringe los derechos (ver, responder y guardar) al departamento de marketing?  ¿O debe elegir la opción **No reenviar**? Ambas opciones harían que los destinatarios no pudieran reenviar el correo electrónico. 

- Si aplica la plantilla, los destinatarios pueden seguir compartiendo la información con otros usuarios del departamento de marketing. Por ejemplo, un destinatario puede usar el Explorador para arrastrar y colocar el correo electrónico en una ubicación compartida o en una unidad USB. De este modo, cualquier persona del departamento de marketing (y el propietario del correo electrónico) que tenga acceso a esta ubicación podrá ver la información del correo electrónico.
 
- Si aplica la opción **No reenviar**, los destinatarios no podrán compartir la información con ninguna persona del departamento de marketing si mueven el correo electrónico a otra ubicación. En este caso, solo los destinatarios originales (y el propietario del correo electrónico) podrán ver la información del correo electrónico.

> [!NOTE] 
> Use **No reenviar** cuando sea importante que solo los destinatarios que elige el remitente puedan ver la información del correo electrónico. Use una plantilla para correos electrónicos para restringir los derechos a un grupo de personas especificadas de antemano por el administrador, independientemente de los destinatarios que elija el remitente.




## Véase también
[Configuración de plantillas personalizadas para Azure Rights Management](configure-custom-templates.md)




<!--HONumber=Sep16_HO4-->


