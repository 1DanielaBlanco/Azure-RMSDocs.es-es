---
title: "¿Qué es Azure Information Protection? | Azure Information Protection"
description: "Información general del servicio Azure Information Protection."
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: cd8a88e2-3555-4be2-9637-3cdee992f2c8
translationtype: Human Translation
ms.sourcegitcommit: c1279e6f2420711f921a8ccae256a80d619e8566
ms.openlocfilehash: 5891dfa423bb5e0b9871bc60a31572ed4f89a7c7


---

# ¿Qué es Azure Information Protection?

>*Se aplica a: Azure Information Protection*

Azure Information Protection es una solución basada en la nube que ayuda a una organización a clasificar, etiquetar y proteger sus documentos y correos electrónicos. Esto puede realizarse automáticamente por administradores que definen reglas y condiciones, manualmente por los usuarios o una combinación en la que los usuarios reciben recomendaciones. 

La siguiente imagen muestra un ejemplo de Azure Information Protection en funcionamiento. El administrador ha configurado reglas para detectar datos confidenciales (en este caso, información de tarjeta de crédito). Cuando un usuario guarda un documento de Word que contiene información de tarjeta de crédito, ve una información sobre herramientas personalizada que recomienda que aplique una etiqueta específica que el administrador ha configurado. Esta clasifica y, opcionalmente, protege el documento. 

![Ejemplo de clasificación recomendada para Azure Information Protection](../media/info-protect-recommend-callouts.png)

Después de que su contenido se clasifique (y se proteja opcionalmente), puede realizar un seguimiento posterior y controlar cómo se usa. Puede analizar los flujos de datos para obtener información sobre su negocio, detectar comportamientos de riesgo y tomar medidas correctivas, realizar un seguimiento del acceso a los documentos y evitar la pérdida o el uso indebido de datos entre otros.

## Cómo aplican la clasificación las etiquetas

Use las etiquetas de Azure Information Protection para aplicar la clasificación a los documentos y correos electrónicos. Al hacer esto, la clasificación se puede identificar en cualquier momento, independientemente de dónde se almacenen los datos o con quién se compartan. Las etiquetas persistentes incluyen distintivos visuales, como encabezados, pies de página o marcas de agua. Los metadatos se agregan a los archivos y a los encabezados de correo electrónico en texto no cifrado de forma que otros servicios (como las soluciones de prevención de pérdida de datos) puedan identificar la clasificación y tomar las medidas oportunas. 

Por ejemplo, el siguiente mensaje de correo electrónico se ha clasificado como "Interno". Esta etiqueta se agrega como un pie de página al mensaje de correo electrónico, como un indicador visual para todos los destinatarios de que está destinado a un uso interno y no debe enviarse fuera de la organización. Esta etiqueta también se inserta en los encabezados de correo electrónico de forma que los servicios de correo electrónico puedan inspeccionar este valor y puedan crear una entrada de auditoría o evitar que se envíen fuera de la organización.

![Encabezados y pie de página de correo electrónico de ejemplo que muestran la clasificación de Azure Information Protection](../media/example-email-footer-header.png)


## Cómo se protegen los datos

La tecnología de protección usa *Azure Rights Management* (a menudo abreviado como Azure RMS). Esta tecnología se integra en otros servicios en la nube de Microsoft y en las aplicaciones tales como Office 365 y Azure Active Directory. También lo puede usar con sus propias aplicaciones de línea de negocio y soluciones de protección de información de proveedores de software, tanto si estas aplicaciones y soluciones son locales como en la nube.

Esta tecnología de protección usa directivas de autorización, identidad y cifrado. De manera similar a las etiquetas persistentes, la protección que se aplica mediante Rights Management permanece con los documentos y los correos electrónicos, independientemente de la ubicación, ya sea dentro o fuera de la organización, las redes, los servidores de archivos y las aplicaciones. Esta solución de protección de información le permite seguir controlando sus datos, incluso cuando estos se comparten con otros usuarios.

Por ejemplo, puede configurar un informe o una hoja de cálculo de previsión de ventas para que solamente pueda tener acceso gente de la organización, y controlar si se puede editar un documento, si se restringe a solo lectura o si se impide que se pueda imprimir. Puedes configurar los correos electrónicos de forma similar y, además, evitar que se puedan reenviar o evitar que se use la opción Responder a todos. Estas tareas de protección se pueden simplificar mediante el uso de *plantillas de administración de derechos*.

### Plantillas de administración de derechos

Tan pronto como active el servicio Azure Rights Management, se crean dos plantillas predeterminadas que restringen el acceso a los datos de los usuarios de su organización. Puede usar estas plantillas para ayudar a evitar inmediatamente la pérdida de datos de su organización. También puede complementar estas plantillas determinadas al configurar sus propias plantillas personalizadas que aplican controles más restrictivos.

Estas plantillas pueden ser parte de una configuración de etiqueta, de forma que cuando una etiqueta específica se aplique a un documento (o mensaje de correo electrónico), los datos se clasifican y se protegen automáticamente. Las plantillas también pueden seleccionarse por usuarios o administradores en productos y servicios que admiten la tecnología de Azure Rights Management.

En este ejemplo se muestra cómo puede seleccionar una plantilla para una etiqueta cuando configura la directiva de Azure Information Protection desde Azure Portal:

![Ejemplo de seleccionar plantillas en Azure Portal](../media/templates-infoprotection-callouts.png)

Las mismas plantillas pueden seleccionarse desde el Centro de administración de Exchange para configurar reglas de flujo del correo de Exchange Online, que admiten la tecnología de Azure Rights Management:

![Ejemplo de seleccionar plantillas para Exchange Online](../media/templates-exchangeonline-callouts.png)

Para más información sobre la protección de Azure Rights Management, vea [¿Qué es Azure Rights Management?](what-is-azure-rms.md).

## Integración con flujos de trabajo del usuario final

Azure Information Protection se integra con los flujos de trabajo existentes de usuarios finales cuando se instala el cliente de Azure Information Protection. Este cliente instala la barra de Information Protection en aplicaciones de Office, que hemos visto en la primera imagen. Se agrega la misma barra en Excel, PowerPoint y Outlook. Por ejemplo:

![Ejemplo de la barra de Azure Information Protection en Excel](../media/excel2013-infoprotect-bar2.png)

Esta barra de Information Protection facilita a los usuarios finales la selección de etiquetas para la correcta clasificación, y donde se necesite, estas etiquetas también pueden proteger automáticamente sus documentos y correos electrónicos.

Cuando los usuarios comparten sus documentos protegidos por correo electrónico, pueden usar un sitio de seguimiento de documentos para supervisar quién está teniendo acceso a estos documentos y cuándo. Si se sospecha de uso indebido, también pueden revocar el acceso a estos documentos.


## Recursos de Azure Information Protection

- Anuncio de versión preliminar: [Azure Information Protection, ahora disponible en la versión preliminar pública](https://blogs.technet.microsoft.com/enterprisemobility/2016/07/12/azure-information-protection-public-preview-available-now/)

- Descargar el cliente: [cliente de Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018)

- Preguntas más frecuentes: [Preguntas más frecuentes de Azure Information Protection](../get-started/faqs.md)

- Yammer: [Azure Information Protection](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)

- Presentación en vídeo:

    <iframe width="560" height="315" src="https://www.youtube.com/embed/N9Ip0m6d3G0" frameborder="0" allowfullscreen></iframe>


## Pasos siguientes

Configure y vea Azure Information Protection con nuestro [Tutorial de inicio rápido de Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md) en cinco pasos.

¿Conoce Azure Information Protection o Azure Rights Management por otro nombre? Consulte [nuestra lista de términos alternativos para el servicio](azure-rms-aka.md).


<!--HONumber=Sep16_HO4-->

