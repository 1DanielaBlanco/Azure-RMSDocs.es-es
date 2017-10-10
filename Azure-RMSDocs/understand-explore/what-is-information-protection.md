---
title: "¿Qué es Azure Information Protection?"
description: "Información general del servicio Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/27/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: cd8a88e2-3555-4be2-9637-3cdee992f2c8
ms.openlocfilehash: ba39c332437e2710554d1e8f69c3f676f0d870db
ms.sourcegitcommit: faaab68064f365c977dfd1890f7c8b05a144a95c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2017
---
# <a name="what-is-azure-information-protection"></a>¿Qué es Azure Information Protection?

>*Se aplica a: Azure Information Protection*

Azure Information Protection es una solución basada en la nube que ayuda a una organización a clasificar, etiquetar y proteger sus documentos y correos electrónicos. Esto puede realizarse automáticamente por administradores que definen reglas y condiciones, manualmente por los usuarios o una combinación en la que los usuarios reciben recomendaciones. 

La siguiente imagen muestra un ejemplo de Azure Information Protection en funcionamiento. El administrador ha configurado reglas para detectar datos confidenciales (en este caso, información de tarjeta de crédito). Cuando un usuario guarda un documento de Word que contiene información de tarjeta de crédito, ve una información sobre herramientas personalizada que recomienda que aplique una etiqueta específica que el administrador ha configurado. Esta clasifica y, opcionalmente, protege el documento, en función de la configuración. 

![Ejemplo de clasificación recomendada para Azure Information Protection](../media/info-protect-recommend-calloutsv2.png)

Después de que su contenido se clasifique (y se proteja opcionalmente), puede realizar un seguimiento posterior y controlar cómo se usa. Puede analizar los flujos de datos para obtener información sobre su negocio, detectar comportamientos de riesgo y tomar medidas correctivas, realizar un seguimiento del acceso a los documentos y evitar la pérdida o el uso indebido de datos entre otros.

## <a name="how-labels-apply-classification"></a>Cómo aplican la clasificación las etiquetas

Use las etiquetas de Azure Information Protection para aplicar la clasificación a los documentos y correos electrónicos. Al hacer esto, la clasificación se puede identificar en cualquier momento, independientemente de dónde se almacenen los datos o con quién se compartan. Las etiquetas incluyen distintivos visuales, como encabezados, pies de página o marcas de agua. Se agregan metadatos a los archivos y encabezados de correo electrónico en texto no cifrado. El texto no cifrado garantiza que otros servicios, como las soluciones de prevención de pérdida de datos, puedan identificar la clasificación y tomar las medidas oportunas. 

Por ejemplo, el siguiente mensaje de correo electrónico se ha clasificado como "General". Esta etiqueta se agrega como pie de página al mensaje de correo electrónico. Este pie de página es un indicador visual para todos los destinatarios y está diseñado para los datos empresariales generales que no se pueden enviar fuera de la organización. La etiqueta también se inserta en los encabezados de correo electrónico de forma que los servicios de correo electrónico puedan inspeccionar este valor y puedan crear una entrada de auditoría o evitar que se envíen fuera de la organización.

![Encabezados y pie de página de correo electrónico de ejemplo que muestran la clasificación de Azure Information Protection](../media/example-email-footerv2.png)


## <a name="how-data-is-protected"></a>Cómo se protegen los datos

La tecnología de protección usa *Azure Rights Management* (a menudo abreviado como Azure RMS). Esta tecnología se integra en otros servicios en la nube de Microsoft y en las aplicaciones tales como Office 365 y Azure Active Directory. También lo puede usar con sus propias aplicaciones de línea de negocio y soluciones de protección de información de proveedores de software, tanto si estas aplicaciones y soluciones son locales como en la nube.

Esta tecnología de protección usa directivas de autorización, identidad y cifrado. De manera similar a las etiquetas que se aplican, la protección que se aplica mediante Rights Management permanece con los documentos y los correos electrónicos, independientemente de la ubicación, ya sea dentro o fuera de la organización, las redes, los servidores de archivos y las aplicaciones. Esta solución de protección de información le permite seguir controlando sus datos, incluso cuando estos se comparten con otros usuarios.

Por ejemplo, puede configurar un informe o una hoja de cálculo de previsión de ventas para que solamente pueda tener acceso gente de la organización, y controlar si se puede editar un documento, si se restringe a solo lectura o si se impide que se pueda imprimir. Puede configurar los correos electrónicos de forma similar y, además, evitar que se puedan reenviar o que se use la opción Responder a todos. Estas tareas de protección se pueden simplificar mediante el uso de *plantillas de Microsoft Azure AD Rights Management*.

### <a name="rights-management-templates"></a>Plantillas de Microsoft Azure AD Rights Management

Tan pronto como active el servicio Azure Rights Management, tendrá disponibles dos plantillas predeterminadas que restringen el acceso a los datos de los usuarios de su organización. Puede usar estas plantillas para ayudar a evitar inmediatamente la pérdida de datos de su organización. También puede complementar estas plantillas predeterminadas con plantillas de protección personalizadas que aplican controles más restrictivos.

Las plantillas pueden formar parte de la configuración de una etiqueta. Cuando esa etiqueta se aplica a un mensaje de correo electrónico o documento, los datos se clasifican y se protegen automáticamente. Las plantillas también pueden seleccionarse por usuarios o administradores en productos y servicios que admiten la tecnología de Azure Rights Management.

En este ejemplo se muestra cómo puede seleccionar una plantilla para una etiqueta cuando configura la directiva de Azure Information Protection desde Azure Portal:

![Ejemplo de seleccionar plantillas en Azure Portal](../media/info-protect-template-callout.png)

Se pueden seleccionar las mismas plantillas en el centro de administración de Exchange. Por ejemplo, puede configurar reglas de flujo de correo electrónico de Exchange Online para utilizar estas plantillas, ya que Exchange es compatible con la tecnología de Azure Rights Management:

![Ejemplo de seleccionar plantillas para Exchange Online](../media/templates-exchangeonline-callouts.png)

Para más información sobre la protección de Azure Rights Management, vea [¿Qué es Azure Rights Management?](what-is-azure-rms.md).

## <a name="integration-with-end-user-workflows"></a>Integración con flujos de trabajo del usuario final

Azure Information Protection se integra con los flujos de trabajo existentes de usuarios finales cuando se instala el cliente de Azure Information Protection. Este cliente instala la barra de Information Protection en aplicaciones de Office, como ya hemos visto en la primera imagen, en la que se mostraba dicha barra en Word. Se agrega la misma barra de Information Protection a Excel, PowerPoint y Outlook. Por ejemplo:

![Ejemplo de la barra de Azure Information Protection en Excel](../media/excel2016-infoprotect-barv2.png)

Esta barra de Information Protection facilita a los usuarios finales seleccionar etiquetas para una clasificación correcta. Si es necesario, las etiquetas también se pueden aplicar automáticamente para evitar las conjeturas de los usuarios o para cumplir las directivas de su organización.

Para clasificar y proteger otros tipos de archivo y para admitir varios archivos a la vez, los usuarios pueden hacer clic con el botón derecho en los archivos o en una carpeta en el Explorador de archivos de Windows:

![Explorador de archivos Menú contextual Clasificar y proteger con Azure Information Protection](../media/right-click-classify-protect-folder.png)

Cuando los usuarios seleccionan la opción de menú **Clasificar y proteger** en el Explorador de archivos, pueden seleccionar una etiqueta de forma similar a como usan la barra de Information Protection en las aplicaciones de escritorio de Office. También pueden establecer permisos personalizados, si es necesario.

A los usuarios de PowerShell (y administradores) les puede resultar más eficaz utilizar los comandos de PowerShell para administrar y configurar la clasificación y protección de varios archivos. Para que los comandos de PowerShell permitan hacer esto, se incluyen automáticamente con el cliente, aunque también puede instalar el módulo de PowerShell por separado.

Después de haber protegido un documento, los usuarios y administradores pueden usar un sitio de Seguimiento de documentos para supervisar quién accede a los documentos y cuándo. Si se sospecha de uso indebido, también pueden revocar el acceso a estos documentos:

![Icono de revocación de acceso en el sitio de Seguimiento de documentos](../media/tracking-site-revoke-access-icon.png)


## <a name="resources-for-azure-information-protection"></a>Recursos de Azure Information Protection

- Prueba gratuita: [Enterprise Mobility + Security E5](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)

- Descargar el cliente: [cliente de Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018)

- Preguntas más frecuentes: [Preguntas más frecuentes de Azure Information Protection](../get-started/faqs.md)

- Yammer: [Azure Information Protection](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)

- Vídeo: "Top 5 Tips for Information Protection" (5 sugerencias para Information Protection)

    <iframe width="560" height="315" src="https://www.youtube.com/embed/GWcnZFMPcnE" frameborder="0" allowfullscreen></iframe>

Además, **Microsoft Ignite 2017** tiene muchas sesiones para Azure Information Protection que estarán disponibles a petición. También puede [buscar y encontrar](https://myignite.microsoft.com/videos?q=%2522azure%2520information%2520protection%2522) estas sesiones en el sitio web de Ignite en cuanto estén disponibles. Para un resumen de los anuncios, vea [What’s new in Azure Information Protection @ Ignite 2017](https://blogs.technet.microsoft.com/enterprisemobility/2017/09/27/whats-new-in-azure-information-protection-ignite-2017/) (Novedades en Azure Information Protection @ Ignite 2017).


## <a name="next-steps"></a>Pasos siguientes

Lea la entrada del blob, [Azure Information Protection: Ready, set, protect!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/) (Azure Information Protection: preparado, listo, protege)

Configure y vea Azure Information Protection con nuestro [Tutorial de inicio rápido de Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md) en cinco pasos.

¿Quizá conoce Azure Information Protection o Azure Rights Management por otro nombre? Consulte [nuestra lista de términos alternativos para el servicio](azure-rms-aka.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]