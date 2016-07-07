---
title: "Configuración de los derechos de uso para Azure Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/16/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d
ms.reviewer: esaggese
ms.suite: ems
ms.sourcegitcommit: 3883a46440f016138dd50d061a58089253721719
ms.openlocfilehash: 21b92fae5fd00d80f9afd2e80d21c08bfa47b7b2


---

# Configuración de los derechos de uso para Azure Rights Management

*Se aplica a: Azure Rights Management, Office 365*

Cuando establece la protección en archivos o correos electrónicos con Azure Rights Management (Azure RMS) y no usa ninguna plantilla, debe configurar los derechos de uso usted mismo. Además, al configurar plantillas personalizadas para Azure RMS, se seleccionan los derechos de uso que se aplicarán automáticamente cuando los usuarios, administradores o servicios configurados seleccionen la plantilla. Por ejemplo, en el Portal de Azure clásico, puede seleccionar los roles que configuran una agrupación lógica de derechos de uso o puede configurar los derechos individuales.

Use este artículo como ayuda para configurar los derechos de uso que quiere para la aplicación que esté usando y para entender cómo las aplicaciones interpretan estos derechos.

## Derechos de uso y descripciones
En las secciones siguientes se enumeran y se describen los derechos de uso que admite Rights Management y cómo se usan y se interpretan. Se enumeran por su **Nombre común**, que es normalmente cómo se muestra o se referencia el derecho de uso, como una versión más descriptiva del valor de una sola palabra que se usa en el código (el valor **Codificación en la directiva**). **Constante o valor de API** es el nombre de SDK para una llamada de API de MSIPC, que se usa al escribir una aplicación habilitada para RMS que comprueba un derecho de uso o agrega un derecho de uso a una directiva.


### Editar contenido, Editar

Permite al usuario modificar, reorganizar, formatear o filtrar el contenido dentro de la aplicación. No concede el derecho a guardar la copia modificada.

**Codificación en la directiva**: DOCEDIT

**Implementación en los derechos personalizados de Office**: como parte de las opciones *Cambiar* y *Control total*.

**Nombre en el Portal de Azure clásico**: *Editar contenido*

**Nombre en las plantillas de AD RMS**: *Editar*

**Constante o valor de API**: *no aplicable*

---

### Guardar

Permite al usuario guardar el documento en su ubicación actual.

**Codificación en la directiva**: EDIT

**Implementación en los derechos personalizados de Office**: como parte de las opciones *Cambiar* y *Control total*.

**Nombre en el Portal de Azure clásico**: *Guardar archivo*

**Nombre en las plantillas de AD RMS**: *Guardar*

**Constante o valor de API**: IPC_GENERIC_WRITE L"EDIT"

En las aplicaciones de Office, este derecho también permite al usuario modificar el documento.

---

### Comentario

Habilita la opción para agregar anotaciones o comentarios al contenido.

**Codificación en la directiva**: COMMENT

**Implementación en los derechos personalizados de Office**: no implementado.

**Nombre en el Portal de Azure clásico**: no implementado.

**Nombre en las plantillas de AD RMS:** no implementado.

**Constante o valor de API:** IPC_GENERIC_COMMENT L"COMMENT

Este derecho está disponible en el SDK como directiva ad hoc en el módulo de protección de RMS para Windows PowerShell y se implementó en algunas aplicaciones de proveedores de software. Sin embargo, no se usa extensamente y no es compatible actualmente con las aplicaciones de Office.

---

### Guardar como, Exportar

Habilita la opción para guardar el contenido con un nombre de archivo diferente (Guardar como). En el caso de los documentos de Office, el archivo puede guardarse sin protección.

**Codificación en la directiva**: EXPORT

**Implementación en los derechos personalizados de Office**: como parte de las opciones *Cambiar* y *Control total*.

**Nombre en el Portal de Azure clásico**: *Exportar contenido (guardar como)*

**Nombre en las plantillas de AD RMS:** *Exportar (guardar como)*

**Constante o valor de API:** IPC_GENERIC_EXPORT L"EXPORT"

Este derecho también permite al usuario realizar otras opciones de exportación en las aplicaciones, como *Enviar a OneNote*.

---

### Reenviar

Habilita la opción para reenviar un mensaje de correo electrónico y agregar destinatarios a las líneas *Para* y *CO*. Este derecho no se aplica a documentos, solo a mensajes de correo electrónico.

**Codificación en la directiva:** FORWARD

**Implementación en los derechos personalizados de Office:** se deniega al usar la directiva estándar *No reenviar*.

**Nombre en el Portal de Azure clásico:** *Reenviar*

**Nombre en las plantillas de AD RMS:** *Reenviar*

**Constante o valor de API:** IPC_EMAIL_FORWARD L"FORWARD"

No permite que el reenviador conceda derechos a otros usuarios como parte de la acción de reenvío.

---

### Control total

Concede todos los derechos para el documento; se pueden realizar todas las acciones disponibles.

**Codificación en la directiva**: OWNER

**Implementación en los derechos personalizados de Office**: como parte de la opción personalizada *Control total*.

**Nombre en el Portal de Azure clásico:** *Control total*

**Nombre en las plantillas de AD RMS:** *Control total*

**Constante o valor de API:** IPC_GENERIC_ALL L"OWNER"

Incluye la capacidad de quitar la protección.

---

### Imprimir

Habilita las opciones para imprimir el contenido.

**Codificación en la directiva**: PRINT

**Implementación en los derechos personalizados de Office:** como la opción *Imprimir contenido* de los permisos personalizados. No se trata de un valor por destinatario.

**Nombre en el Portal de Azure clásico:** *Imprimir*

**Nombre en las plantillas de AD RMS:** *Imprimir*

**Constante o valor de API:** IPC_GENERIC_PRINT L"PRINT

---

### Responder

Habilita la opción Responder en un cliente de correo electrónico, sin permitir que se realicen cambios en las líneas *Para* o *CO*.

**Codificación en la directiva**: REPLY

**Implementación en los derechos personalizados de Office**: no aplicable.

**Nombre en el Portal de Azure clásico:** *Responder*

**Nombre en las plantillas de AD RMS:** *Responder*

**Constante o valor de API:** IPC_EMAIL_REPLY

---

### Responder a todos

Habilita la opción *Responder a todos* en un cliente de correo electrónico, pero no permite al usuario agregar destinatarios a las líneas *Para* o *CO*.

**Codificación en la directiva**: REPLYALL

**Implementación en los derechos personalizados de Office**: no aplicable.

**Nombre en el Portal de Azure clásico:** *Responder a todos*

**Nombre en las plantillas de AD RMS:** *Responder a todos*

**Constante o valor de API:** IPC_EMAIL_REPLYALL L"REPLYALL"

---

### Ver, Abrir, Leer

Permite al usuario abrir el documento y ver el contenido.

**Codificación en la directiva**: VIEW

**Implementación en los derechos personalizados de Office**: como la opción *Ver* de la directiva personalizada *Leer*.

**Nombre en el Portal de Azure clásico**: *Ver contenido*

**Nombre en las plantillas de AD RMS:** *Ver*

**Constante o valor de API:** IPC_GENERIC_READ L"VIEW"

---

### Copiar

Habilita las opciones para copiar los datos (incluidas las capturas de pantalla) del documento en el mismo documento o en otro documento.

**Codificación en la directiva**: EXTRACT

**Implementación en los derechos personalizados de Office:** como la opción de directiva personalizada *Permitir que los usuarios con acceso de lectura copien el contenido*.

**Nombre en el Portal de Azure clásico**: *Copiar y extraer contenido*

**Nombre en las plantillas de AD RMS**: *Extraer*

**Constante o valor de API:** IPC_GENERIC_EXTRACT L"EXTRACT"

En algunas aplicaciones, también permite que todo el documento se guarde en sin protección.

---


### Permitir macros

Habilita la opción para ejecutar macros u obtener acceso remoto o mediante programación al contenido de un documento.

**Codificación en la directiva**: OBJMODEL

**Implementación en los derechos personalizados de Office**: como la opción de directiva personalizada *Permitir el acceso mediante programación*. No se trata de un valor por destinatario.

**Nombre en el Portal de Azure clásico:** *Permitir macros*

**Nombre en las plantillas de AD RMS:** *Permitir macros*

**Constante o valor de API**: no aplicable


## Derechos incluidos en los niveles de permisos

Algunas aplicaciones agrupan derechos de uso en niveles de permisos para facilitar la selección de derechos de uso que suelen utilizarse de forma conjunta. Estos niveles de permisos ayudan a resumir un nivel de complejidad de los usuarios para que puedan elegir opciones basadas en roles.  Por ejemplo, **Revisor** y **Coautor**. Aunque estas opciones suelen mostrar a los usuarios un resumen de los derechos, puede que no incluyan todos los derechos enumerados en la tabla anterior.

Utilice la tabla siguiente para ver una lista de estos niveles de permisos y una lista completa de los derechos que contienen.

|Nivel de permisos|Aplicaciones|Derechos incluidos (nombre común)|
|---------------------|----------------|---------------------------------|
|Visor|Portal de Azure clásico<br /><br />Aplicación de uso compartido Rights Management para Windows|Ver, Abrir, Leer; Responder; Responder a todos|
|Revisor|Portal de Azure clásico<br /><br />Aplicación de uso compartido Rights Management para Windows|Ver, Abrir, Leer; Guardar; Editar contenido, Editar; Responder [[1]](#footnote-1); Responder a todos [[1]](#footnote-1); Reenviar [[1]](#footnote-1)|
|Coautor|Portal de Azure clásico<br /><br />Aplicación de uso compartido Rights Management para Windows|Ver, Abrir, Leer; Guardar; Editar contenido, Editar; Copiar; Ver derechos; Cambiar derechos; Permitir macros; Guardar como, Exportar; Imprimir; Responder [[1]](#footnote-1); Responder a todos [[1]](#footnote-1); Reenviar [[1]](#footnote-1)|
|Copropietario|Portal de Azure clásico<br /><br />Aplicación de uso compartido Rights Management para Windows|Ver, Abrir, Leer; Guardar; Editar contenido, Editar; Copiar; Ver derechos; Cambiar derechos; Permitir macros; Guardar como, Exportar; Imprimir; Responder [[1]](#footnote-1); Responder a todos [[1]](#footnote-1); Reenviar [[1]](#footnote-1); Control total|

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

Aunque esta opción aparece para los usuarios (y los administradores de Exchange) como si fuera una plantilla predeterminada de Rights Management que se puede seleccionar, **No reenviar** no es una plantilla. Esto explica por qué no se ve en el Portal de Azure clásico cuando se visualizan y se administran las plantillas de Azure RMS. En realidad, la opción **No reenviar** es un conjunto de derechos que los usuarios aplican dinámicamente a los destinatarios de correo electrónico.

Cuando se aplica la opción **No reenviar** a un correo electrónico, los destinatarios no pueden reenviarlo, imprimirlo, copiar contenido, guardar datos adjuntos ni guardarlo con un nombre diferente. Por ejemplo, en el cliente de Outlook, el botón Reenviar no está disponible, tampoco están disponibles las opciones de menú **Guardar como**, **Guardar datos adjuntos** e **Imprimir**, y no se pueden agregar ni cambiar destinatarios de los cuadros **Para**, **CC** o **CCO**.

Hay una diferencia importante entre aplicar la opción **No reenviar** y aplicar una plantilla que no concede el derecho Reenviar a un correo electrónico: la opción **No reenviar** usa una lista dinámica de usuarios autorizados basada en los destinatarios del mensaje original que elige el usuario, mientras que los derechos de la plantilla tienen una lista estática de usuarios autorizados que el administrador ha especificado anteriormente. ¿Cuál es la diferencia? Veamos un ejemplo: 

Un usuario quiere enviar información por correo electrónico a personas concretas del departamento de marketing que no debe compartirse con nadie más. ¿Debe proteger el correo electrónico con una plantilla que restringe los derechos (ver, responder y guardar) al departamento de marketing?  ¿O debe elegir la opción **No reenviar**? Ambas opciones harían que los destinatarios no pudieran reenviar el correo electrónico. 

- Si aplica la plantilla, los destinatarios pueden seguir compartiendo la información con otros usuarios del departamento de marketing. Por ejemplo, un destinatario puede usar el Explorador para arrastrar y colocar el correo electrónico en una ubicación compartida o en una unidad USB. De este modo, cualquier persona del departamento de marketing (y el propietario del correo electrónico) que tenga acceso a esta ubicación podrá ver la información del correo electrónico.
 
- Si aplica la opción **No reenviar**, los destinatarios no podrán compartir la información con ninguna persona del departamento de marketing si mueven el correo electrónico a otra ubicación. En este caso, solo los destinatarios originales (y el propietario del correo electrónico) podrán ver la información del correo electrónico.

> [!NOTE] Use **No reenviar** cuando sea importante que solo los destinatarios que elige el remitente puedan ver la información del correo electrónico. Use una plantilla para correos electrónicos para restringir los derechos a un grupo de personas especificadas de antemano por el administrador, independientemente de los destinatarios que elija el remitente.




## Véase también
[Configuración de plantillas personalizadas para Azure Rights Management](configure-custom-templates.md)




<!--HONumber=Jun16_HO3-->


