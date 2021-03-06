---
title: Preguntas más frecuentes sobre la clasificación y el etiquetado - AIP
description: ¿Tiene alguna pregunta que trate específicamente sobre clasificación y etiquetado con Azure Information Protection? Vea si se ha resuelto aquí.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 01/25/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.openlocfilehash: 37aea835e34c0db50d277922edbfd044e43afd71
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56256822"
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Preguntas más frecuentes sobre la clasificación y el etiquetado en Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

¿Tiene alguna pregunta sobre Azure Information Protection que trate específicamente sobre clasificación y etiquetado?  Vea si se ha resuelto aquí. 

## <a name="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection"></a>¿Qué puedo hacer con las funcionalidades de clasificación en Azure Information Protection?

Pruebe nuestro tutorial [Edit the policy and create a new label](infoprotect-quick-start-tutorial.md) (Edición de la directiva y creación de una etiqueta nueva) para ver esto en funcionamiento en cuestión de minutos.

Busque anuncios en el [blog de Enterprise Mobility + Security Blog](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/bg-p/enterprisemobilityandsecurity/label-name/Azure%20Information%20Protection) y en nuestro [sitio de Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all) para saber cuándo estarán disponibles las funcionalidades y características de clasificación adicionales. Existen algunas limitaciones con la versión actual, que incluyen las siguientes:

- No hay posibilidad de etiquetado en las aplicaciones web de Office (Office Online).

- No existe una integración de etiquetado y clasificación con Exchange Online o SharePoint Online.

> [!NOTE]
> **Ahora en versión preliminar**:
> - Informes centralizados para clasificación y etiquetado. Para más información, consulte [Central reporting for Azure Information Protection](reports-aip.md) (Informes centrales para Azure Information Protection).
>
>**Publicado recientemente**:
> - Capacidad de etiquetado integrada en las aplicaciones de Office para los dispositivos móviles (iOS y Android) y los equipos Mac. Para más información, consulte [Aplicar etiquetas de confidencialidad a los documentos y al correo electrónico en Office](https://aka.ms/officemipdocs).

Solicite nuevas características y vote las solicitudes existentes en el [sitio de UserVoice](https://msip.uservoice.com/) de Azure Information Protection.

## <a name="do-i-need-to-be-a-global-admin-to-configure-classification-and-labels"></a>¿Es necesario ser un administrador global para configurar la clasificación y las etiquetas?

Con el rol de Administrador de Information Protection recientemente incorporado, ahora esta pregunta se responde en la página principal de Preguntas más frecuentes: [¿Hay que ser un administrador global para configurar Azure Information Protection o puedo delegar a otros administradores?](faqs.md#do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators)

Si selecciona la opción para instalar la directiva de demostración cuando instale el [cliente de Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018), no necesita iniciar sesión en el portal para ver y probar la funcionalidad de etiquetado. La directiva de demostración instala localmente una directiva predeterminada de Azure Information Protection, de forma que podrá probar el etiquetado de documentos y correos electrónicos, pero no cambiar ni agregar etiquetas nuevas sin iniciar sesión en Azure Portal. 

## <a name="can-a-file-have-more-than-one-classification"></a>¿Puede un archivo tener más de una clasificación?

Los usuarios pueden seleccionar una sola etiqueta a la vez para cada documento o correo electrónico, lo que a menudo resulta en una sola clasificación. Sin embargo, si los usuarios seleccionan una subetiqueta, en realidad se aplican dos etiquetas a la vez: una principal y una secundaria. Con las subetiquetas, un archivo puede tener dos clasificaciones que denotan una relación entre elementos principal y secundario para, así, obtener un nivel extra de control.

Por ejemplo, la etiqueta **Confidencial** podría contener subetiquetas como **Legal** y **Financiero**. Se pueden aplicar diferentes marcas visuales de clasificación y diferentes plantillas de Rights Management a estas subetiquetas. Un usuario no puede seleccionar la etiqueta **Confidencial** por sí misma, sino solo una de sus subetiquetas, como **Legal**. Como resultado, la etiqueta que ven es **Confidencial \ Legal**. Los metadatos de ese archivo incluyen una propiedad de texto personalizado para **Confidencial**, una propiedad de texto personalizado para **Legal** y otra que contiene los dos valores (**Confidential Legal**). 

Cuando use subetiquetas, no configure distintivos visuales, protección o condiciones en la etiqueta principal. Si usa subniveles, configure estos valores únicamente en la subetiqueta. Si configura estas opciones en la etiqueta principal y en su subetiqueta, la configuración de la subetiqueta tendrá prioridad.

## <a name="how-do-i-prevent-somebody-from-removing-or-changing-a-label"></a>¿Cómo se evita que alguien quite o cambie una etiqueta?

Aunque hay una [configuración de directiva](configure-policy-settings.md) que requiere que los usuarios indiquen el motivo por el que reducen una etiqueta de clasificación, quitan una etiqueta o quitan la protección, esta opción no impide realizar estas acciones. Para impedir que los usuarios quiten o cambien una etiqueta, el contenido debe estar protegido y los permisos de protección no deben conceder al usuario el [derecho de uso](configure-usage-rights.md) Exportar o Control total. 

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>Cuando se etiqueta un correo electrónico, ¿los datos adjuntos reciben automáticamente el mismo etiquetado?

No. Al etiquetar un mensaje de correo electrónico que tiene datos adjuntos, dichos datos adjuntos no heredan la misma etiqueta. Los datos adjuntos siguen sin etiqueta o conservan una etiqueta aplicada por separado. Sin embargo, si la etiqueta para el correo electrónico aplica protección, dicha protección se aplica a los datos adjuntos de Office.

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>¿Cómo pueden las soluciones DLP y otras aplicaciones integrarse con Azure Information Protection?

Como Azure Information Protection usa metadatos persistentes para la clasificación, que incluyen una etiqueta no cifrada, esta información puede leerse mediante soluciones DLP y otras aplicaciones. 

Para obtener más información y ejemplos del uso de estos metadatos con reglas de flujo de correo de Exchange Online, consulte [Configuración de reglas de flujo de correo de Exchange Online para etiquetas de Azure Information Protection](configure-exo-rules.md).

## <a name="can-i-create-a-document-template-that-automatically-includes-the-classification"></a>¿Puedo crear una plantilla de documento que incluya automáticamente la clasificación?

Sí. Puede configurar una etiqueta para [aplicar un encabezado o pie de página que incluye el nombre de etiqueta](configure-policy-markings.md). Pero si no cumple sus requisitos, puede crear una plantilla de documento que tenga el formato que desee y agregar la clasificación como un código de campo. 

Por ejemplo, podría tener una tabla en el encabezado del documento que muestra la clasificación. O bien, podría utilizar una redacción específica para una introducción que hace referencia a la clasificación del documento.

Para agregar este código de campo en el documento:

1. Etiquete el documento y guárdelo. Esta acción crea nuevos campos de metadatos que ahora puede usar para el código de campo.

2. En el documento, coloque el cursor donde desea agregar la clasificación de la etiqueta y, a continuación, en la pestaña **Insertar**, seleccione **Texto** > **Elementos rápidos** > **Campo**.

3. En el cuadro de diálogo **Campo**, en el menú desplegable **Categorías**, seleccione **Información del documento**. A continuación, en la lista desplegable **Nombres de campo**, seleccione **DocProperty**.

4. En la lista desplegable **Propiedad**, seleccione **Sensibilidad** y luego **Aceptar**.

La clasificación de la etiqueta actual se muestra en el documento y este valor se actualizará automáticamente cada vez que abra el documento o use la plantilla. Así pues, si cambia la etiqueta, la clasificación que se muestra en el código de este campo se actualizará automáticamente en el documento.

## <a name="how-is-azure-information-protection-classification-for-emails-different-from-exchange-message-classification"></a>¿En qué se diferencia la clasificación de los correos electrónicos de Azure Information Protection de la clasificación de mensajes de Exchange?

La clasificación de mensajes de Exchange es una característica antigua que puede clasificar los correos electrónicos y que se implementa con independencia de la clasificación de Azure Information Protection. 

Sin embargo, puede integrar las dos soluciones de modo que cuando los usuarios clasifiquen un correo electrónico mediante Outlook en la Web y a través de algunas aplicaciones de correo móviles, se agregue automáticamente la clasificación y las correspondientes marcas de etiqueta de Azure Information Protection. 

Puede usar esta misma técnica para usar las etiquetas con Outlook en la Web y estas aplicaciones de correo móviles.

Para los pasos de configuración, consulte [Integrate Exchange message classification with Azure Information Protection for a mobile device labeling solution](./rms-client/client-admin-guide-customizations.md#integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution) (Integración de clasificación de mensajes de Exchange con Azure Information Protection para una solución de etiquetado de dispositivos móviles). 



