---
title: ¿Qué es Azure Information Protection? - AIP
description: Información general del servicio Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/13/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: cd8a88e2-3555-4be2-9637-3cdee992f2c8
ms.openlocfilehash: 147982a700f2b2033b77d0b02568990a164cf555
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56257865"
---
# <a name="what-is-azure-information-protection"></a>¿Qué es Azure Information Protection?

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Azure Information Protection, también conocido como AIP, es una solución basada en la nube que permite a las organizaciones clasificar y, opcionalmente, proteger sus documentos y correos electrónicos mediante la aplicación de etiquetas. Las etiquetas las pueden aplicar automáticamente los administradores, quienes definen reglas y condiciones, los usuarios manualmente, o bien una combinación en la que los usuarios reciben recomendaciones. 

En la siguiente imagen se muestra un ejemplo de Azure Information Protection en funcionamiento en el equipo de un usuario. El administrador ha configurado una etiqueta con reglas para detectar los datos confidenciales. En nuestro ejemplo, se trata de la información de la tarjeta de crédito. Cuando un usuario guarda un documento de Word que contiene el número de una tarjeta de crédito, puede ver información en pantalla en la que se le recomienda la etiqueta que el administrador ha configurado. Esta etiqueta clasifica el documento y lo protege. 

![Ejemplo de clasificación recomendada para Azure Information Protection](./media/info-protect-recommend-calloutsv2.png)

Después de que su contenido se clasifique (y se proteja opcionalmente), puede realizar un seguimiento posterior y controlar cómo se usa. Puede analizar los flujos de datos para obtener información sobre su negocio, detectar comportamientos de riesgo y tomar medidas correctivas, realizar un seguimiento del acceso a los documentos y evitar la pérdida o el uso indebido de datos entre otros.

## <a name="how-labels-apply-classification"></a>Cómo aplican la clasificación las etiquetas

Use las etiquetas de Azure Information Protection para aplicar la clasificación a los documentos y correos electrónicos. Al hacer esto, la clasificación se puede identificar, independientemente de dónde se almacenen los datos o con quién se compartan. Las etiquetas pueden incluir distintivos visuales, como encabezados, pies de página o marcas de agua. Se agregan metadatos a los archivos y encabezados de correo electrónico en texto no cifrado. El texto no cifrado garantiza que otros servicios, como las soluciones de prevención de pérdida de datos, puedan identificar la clasificación y tomar las medidas oportunas. 

Por ejemplo, el siguiente mensaje de correo electrónico se ha clasificado como "General". La etiqueta ha agregado el pie de página "Confidencialidad: General" al mensaje de correo electrónico. Este pie de página es un indicador visual para todos los destinatarios y está diseñado para los datos empresariales generales que no se pueden enviar fuera de la organización. La etiqueta se inserta en los encabezados de correo electrónico de forma que los servicios de correo electrónico puedan inspeccionar este valor y puedan crear una entrada de auditoría o evitar que se envíen fuera de la organización.

![Encabezados y pie de página de correo electrónico de ejemplo que muestran la clasificación de Azure Information Protection](./media/example-email-footerv2.png)


## <a name="how-data-is-protected"></a>Cómo se protegen los datos

La tecnología de protección usa *Azure Rights Management* (a menudo abreviado como Azure RMS). Esta tecnología se integra en otros servicios en la nube de Microsoft y en las aplicaciones tales como Office 365 y Azure Active Directory. También lo puede usar con sus propias aplicaciones de línea de negocio y soluciones de protección de información de proveedores de software, tanto si estas aplicaciones y soluciones son locales como en la nube.

Esta tecnología de protección usa directivas de autorización, identidad y cifrado. De manera similar a las etiquetas que se aplican, la protección que se aplica mediante Rights Management permanece con los documentos y los correos electrónicos, independientemente de la ubicación, ya sea dentro o fuera de la organización, las redes, los servidores de archivos y las aplicaciones. Esta solución de protección de información le permite seguir controlando sus datos, incluso cuando estos se comparten con otros usuarios.

Por ejemplo, puede configurar un informe o una hoja de cálculo de previsión de ventas para que solamente puedan acceder gente de la organización, y controlar si ese documento se puede editar, restringir a solo lectura o impedir que se pueda imprimir. Puede configurar los correos electrónicos de forma similar y, además, evitar que se puedan reenviar o el uso de la opción Responder a todos. 

Esta configuración de protección puede formar parte de la configuración de la etiqueta, de modo que los usuarios pueden clasificar y proteger documentos y correos electrónicos simplemente aplicando una etiqueta. Sin embargo, la misma configuración de protección también la pueden utilizar aplicaciones y servicios que admiten la protección, pero no el etiquetado. En estas aplicaciones y servicios, la configuración de protección aparece disponible como *plantillas de Rights Management*.

### <a name="rights-management-templates"></a>Plantillas de Microsoft Azure AD Rights Management

En cuanto active el servicio Azure Rights Management, tendrá disponibles dos plantillas predeterminadas que permiten restringir el acceso a los datos a usuarios de la organización. Puede usar estas plantillas para ayudar a evitar inmediatamente la pérdida de datos de su organización. También puede complementar estas plantillas predeterminadas con plantillas de protección personalizadas que aplican controles más restrictivos.

Cuando crea una etiqueta para Azure Information Protection que incluye opciones de protección, esta acción crea entre bastidores una plantilla de Rights Management correspondiente. Luego, puede usar esa plantilla con aplicaciones y servicios que admiten Azure Rights Management.

Por ejemplo, desde el centro de administración de Exchange, puede configurar las reglas de flujo de correo de Exchange Online para utilizar estas plantillas:

![Ejemplo de seleccionar plantillas para Exchange Online](./media/templates-exchangeonline-callouts.png)

Para más información sobre la protección de Azure Rights Management, vea [¿Qué es Azure Rights Management?](what-is-azure-rms.md)

## <a name="integration-with-end-user-workflows-for-documents-and-emails"></a>Integración con los flujos de trabajo del usuario final de documentos y correos electrónicos

Azure Information Protection se integra con los flujos de trabajo existentes de usuarios finales cuando se instala el cliente de Azure Information Protection. Este cliente instala la barra de Information Protection en aplicaciones de Office, como ya hemos visto en la primera imagen, en la que se mostraba dicha barra en Word. Se agrega la misma barra de Information Protection a Excel, PowerPoint y Outlook. Por ejemplo:

![Ejemplo de la barra de Azure Information Protection en Excel](./media/excel2016-infoprotect-barv2.png)

Esta barra de Information Protection facilita a los usuarios finales seleccionar etiquetas para una clasificación correcta. Si es necesario, las etiquetas también se pueden aplicar automáticamente para evitar las conjeturas de los usuarios o para cumplir las directivas de su organización.

Para clasificar y proteger otros tipos de archivo y para admitir varios archivos a la vez, los usuarios pueden hacer clic con el botón derecho en los archivos o en una carpeta en el Explorador de archivos de Windows:

![Explorador de archivos Menú contextual Clasificar y proteger con Azure Information Protection](./media/right-click-classify-protect-folder.png)

Cuando los usuarios seleccionan la opción de menú **Clasificar y proteger** en el Explorador de archivos, pueden seleccionar una etiqueta de forma similar a como usan la barra de Information Protection en las aplicaciones de escritorio de Office. También pueden establecer permisos personalizados, si es necesario.

A los usuarios de PowerShell (y administradores) les puede resultar más eficaz utilizar los comandos de PowerShell para administrar y configurar la clasificación y protección de varios archivos. Los comandos de PowerShell que permiten hacerlo se incluyen automáticamente con el cliente, aunque también puede instalar el módulo de PowerShell por separado.

Después de haber protegido un documento, los usuarios y administradores pueden usar un sitio de Seguimiento de documentos para supervisar quién accede a los documentos y cuándo. Si se sospecha de uso indebido, también pueden revocar el acceso a estos documentos:

![Icono de revocación de acceso en el sitio de Seguimiento de documentos](./media/tracking-site-revoke-access-icon.png)

### <a name="additional-integration-for-email"></a>Integración adicional con el correo electrónico

Cuando usa Azure Information Protection con Exchange Online, obtiene una ventaja adicional: la capacidad de enviar correos electrónicos protegidos a cualquier usuario, con la certeza de que puedan leerlos en cualquier dispositivo.

Por ejemplo, usuarios que han de enviar información confidencial a direcciones de correo electrónico personales que usan una cuenta de **Gmail**, **Hotmail** o **Microsoft**. O bien, a usuarios que no tienen una cuenta de Office 365 o de Azure AD. Estos mensajes de correo electrónico deben estar cifrados tanto cuando se almacenan como en tránsito, y solo deben poder leerlos los destinatarios originales.

En este escenario son necesarias las [nuevas capacidades de cifrado de mensajes de Office 365](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801). Si los destinatarios no pueden abrir el correo electrónico protegido en su cliente de correo electrónico nativo, pueden emplear un código de acceso de un solo uso para leer la información confidencial en un explorador.

Por ejemplo, un usuario de Gmail ve lo siguiente en un mensaje de correo electrónico:

![Experiencia de destinatario de Gmail en OME y AIP](./media/ome-message.png)

El flujo de trabajo de los usuarios que envían el correo electrónico no es distinto del envío de un correo electrónico protegido a un usuario en su propia organización. Así, por ejemplo, pueden seleccionar el botón **No reenviar**, que el cliente de Azure Information Protection puede agregar a la cinta de opciones de Outlook. Esta función No reenviar también se puede integrar en una etiqueta que los usuarios seleccionan, de modo que el correo electrónico se clasifica también como protegido:

![Selección de una etiqueta configurada de No reenviar](./media/recipients-only-label.png)

Como alternativa, puede proporcionar protección a los usuarios automáticamente por medio de reglas de flujo de correo electrónico que aplican la protección de derechos. 

Cuando se adjunten documentos de Office a estos correos electrónicos, dichos documentos también se protegen automáticamente.

## <a name="classifying-and-protecting-existing-documents"></a>Clasificación y protección de documentos existentes

Lo ideal es etiquetar los documentos y los correos electrónicos al crearlos. Aunque lo más probable es que ya tenga muchos documentos en almacenes de datos y también quiera clasificarlos y protegerlos. Dichos almacenes de datos pueden ser locales o encontrarse en la nube.

En el caso de los almacenes de datos locales, use el analizador de Azure Information Protection para detectar, clasificar y proteger los documentos de las carpetas locales, los recursos de red compartidos, los sitios y las bibliotecas de SharePoint Server. El analizador se ejecuta como servicio en Windows Server. Puede usar las mismas reglas de la directiva para detectar información confidencial y aplicar etiquetas específicas a los documentos. Otra opción es aplicar una etiqueta predeterminada a todos los documentos de un repositorio de datos sin inspeccionar el contenido de los archivos. También puede usar el analizador solo en modo de informes para ayudarle a detectar información confidencial que no supiera que tenía. 

Para obtener más información sobre la implementación y el uso del analizador, consulte [Implementación del analizador de Azure Information Protection para clasificar y proteger automáticamente los archivos](deploy-aip-scanner.md).

En el caso de los almacenes de datos en la nube, use Microsoft Cloud App Security para aplicar sus etiquetas a los documentos que tenga en Box, SharePoint Online, y OneDrive para la Empresa. Para obtener más información, consulte [Aplicar automáticamente etiquetas de clasificación de Azure Information Protection](/cloud-app-security/use-case-information-protection) e [Integración de Azure Information Protection](/cloud-app-security/azip-integration).


## <a name="resources-for-azure-information-protection"></a>Recursos de Azure Information Protection

- Evaluación gratuita: [Enterprise Mobility + Security E5](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)

- Precios y opciones de suscripción: [precios de Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)

- Descargue el cliente: [Cliente de Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018)

- Descargue una guía de implementación para los responsables de toma de decisiones empresariales: [Azure Information Protection Deployment Acceleration Guide](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-Deployment-Acceleration-Guide/ba-p/334423) (Guía de aceleración de la implementación de Azure Information Protection)

- Descargue una guía de usuario personalizable: [Guía de adopción del usuario final de Azure Information Protection](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf)

- Preguntas más frecuentes: [Preguntas más frecuentes sobre Azure Information Protection](faqs.md)

- Yammer: [Azure Information Protection](https://www.yammer.com/AskIPTeam)

Recursos adicionales: [Información y soporte técnico para Azure Information Protection](information-support.md)

### <a name="microsoft-ignite"></a>Microsoft Ignite

Microsoft Ignite 2018 en Orlando tenía muchas sesiones que se etiquetaron como [Azure Information Protection](https://myignite.techcommunity.microsoft.com/sessions?q=Azure%2520Information%2520Protection). Todas las sesiones se grabaron, por lo que si no pudo participar allí, podrá verlas más adelante. Las cinco sesiones principales que recomendamos:

- [BRK2006 - Use Microsoft Information Protection (MIP) to help protect your sensitive data everywhere, throughout its lifecycle](https://myignite.techcommunity.microsoft.com/sessions/64297) (Uso de Microsoft Information Protection (MIP) para proteger los datos confidenciales en todas partes, durante su ciclo de vida): vea el [vídeo de YouTube](https://youtu.be/gmHVF-1cLXA)
 
- [BRK3002 - Understanding how Microsoft Information Protection capabilities work together to protect sensitive information across devices, apps, and services](https://myignite.techcommunity.microsoft.com/sessions/64299) (BRK3002: Descripción del funcionamiento conjunto de las funciones de Microsoft Information Protection para proteger la información confidencial entre dispositivos, aplicaciones y servicios): vea el [vídeo de YouTube](https://youtu.be/kL9Y7NGTyQQ)

- [BRK3009 - Accelerate deployment and adoption of Microsoft Information Protection solutions](https://myignite.techcommunity.microsoft.com/sessions/64283) (BRK3009: Acelerar la implementación y adopción de soluciones de Microsoft Information Protection): vea el [vídeo de YouTube](https://www.youtube.com/watch?v=JsCyIVyQJmE)

- [BRK3397 - Protect and control your sensitive emails with Office 365 Message Encryption](https://myignite.techcommunity.microsoft.com/sessions/64327) (BRK3397: Protección y control de los correos electrónicos confidenciales con Cifrado de mensajes de Office 365): vea el [vídeo de YouTube](https://www.youtube.com/watch?v=Ld4b4pFua0g)

- [THR2003 - Data discovery, Usage reporting and analytics for all your data with Microsoft Information Protection](https://myignite.techcommunity.microsoft.com/sessions/64301) (THR2003: Detección de datos, informes de uso y análisis de todos los datos con Microsoft Information Protection): vea el [vídeo de YouTube](https://www.youtube.com/watch?v=nzDIXd0XaeA)

Para obtener un paquete acumulativo de los anuncios que se realizaron en esta conferencia de Ignite, vea la entrada de blog [Announcing availability of information protection capabilities to help protect your sensitive data](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967) (Anuncio de la disponibilidad de funciones de protección de la información para ayudar a proteger los datos confidenciales).


## <a name="next-steps"></a>Pasos siguientes

Configure Azure Information Protection y véalo usted mismo con nuestros [inicios rápidos](quickstart-viewpolicy.md) y [tutoriales](infoprotect-quick-start-tutorial.md). O bien, si está listo para implementar este servicio para su organización, avance por las [guías de procedimientos para escenarios comunes](how-to-guides.md).
