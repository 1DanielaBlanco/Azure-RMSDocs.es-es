---
title: "Preguntas más frecuentes sobre la clasificación y el etiquetado - AIP"
description: "¿Tiene alguna pregunta que trate específicamente sobre clasificación y etiquetado con Azure Information Protection? Vea si se ha resuelto aquí."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.openlocfilehash: b6980bdcecb02471159f7873e80a05d234726d0e
ms.sourcegitcommit: 85aaded97659bbc0a3932569aab29b1bf472fea4
translationtype: HT
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Preguntas más frecuentes sobre la clasificación y el etiquetado en Azure Information Protection

>*Se aplica a: Azure Information Protection, Office 365*

¿Tiene alguna pregunta sobre Azure Information Protection que trate específicamente sobre clasificación y etiquetado?  Vea si se ha resuelto aquí. 

## <a name="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection"></a>¿Qué puedo hacer con las funcionalidades de clasificación en Azure Information Protection?

Pruebe nuestro tutorial de inicio rápido para ver esto en funcionamiento en unos minutos: [Tutorial de inicio rápido de Azure Information Protection](infoprotect-quick-start-tutorial.md).

Busque anuncios en el [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection) (Blog de seguridad y movilidad empresarial) y en nuestro [sitio de Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all) para saber cuándo estarán disponibles las funcionalidades y características de clasificación adicionales. Existen algunas limitaciones con la versión actual, que incluyen las siguientes:

- Los nombres de las etiquetas y la información sobre herramientas solo se admiten en un idioma.

- No existe un registro centralizado para la clasificación y el etiquetado.

- Las condiciones para la clasificación automática deben ser frases o patrones.

- No hay capacidad de etiquetado para las aplicaciones de Office para los dispositivos móviles (iOS y Android) y los equipos Mac, y las aplicaciones web de Office (Office Online).

- No existe una integración de etiquetado y clasificación con Exchange Online o SharePoint Online.

- El SDK para asociados y desarrolladores todavía no incluye clasificación y etiquetado.

La versión de febrero quita muchas de las limitaciones anteriores. Para más información, vea el [anuncio de la entrada de blog](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/08/azure-information-protection-december-update-moves-to-general-availability/).

## <a name="do-i-need-to-be-a-global-admin-to-configure-classification-and-labels"></a>¿Es necesario ser un administrador global para configurar la clasificación y las etiquetas?

Para configurar la directiva de Azure Information Protection, debe iniciar sesión en Azure Portal como administrador global de Azure Active Directory.

Si selecciona la opción para instalar la directiva de demostración cuando instale el [cliente de Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018), no necesita iniciar sesión en el portal para ver y probar la funcionalidad de etiquetado. La directiva de demostración instala localmente una directiva predeterminada para Azure Information Protection, de forma que pueda probar el etiquetado de documentos y correos electrónicos, pero no podrá cambiar ni agregar etiquetas nuevas sin iniciar sesión en Azure Portal. 

## <a name="which-options-in-the-azure-portal-are-p1-or-p2"></a>¿Qué opciones en Azure Portal son P1 o P2?

Para comprobar qué características se incluyen en la suscripción **Azure Information Protection Premium 1** (P1) en comparación con la suscripción **Azure Information Protection Premium 2** (P2), consulte la [lista de características](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features) en el sitio de Azure Information Protection. Sin embargo, como regla general, las características avanzadas, como clasificación automática y mantener su propia clave (HYOK) son específicas de la suscripción Premium 2 de Azure Information Protection.

## <a name="can-a-file-have-more-than-one-classification"></a>¿Puede un archivo tener más de una clasificación?

Los usuarios pueden seleccionar una sola etiqueta a la vez para cada documento o correo electrónico, lo que a menudo resulta en una sola clasificación. Sin embargo, si los usuarios seleccionan una subetiqueta, en realidad se aplican dos etiquetas a la vez: una principal y una secundaria. Con las subetiquetas, un archivo puede tener dos clasificaciones que denotan una relación entre elementos principal y secundario para así obtener un nivel adicional de control.

Por ejemplo, la etiqueta **Confidencial** podría contener subetiquetas como **Legal** y **Financiero**. Se pueden aplicar diferentes marcas visuales de clasificación y diferentes plantillas de Rights Management a estas subetiquetas. Un usuario no puede seleccionar la etiqueta **Confidencial** por sí misma, solo una de sus subetiquetas, como **Legal**. Como resultado, la etiqueta que ven es **Confidencial \ Legal**. Los metadatos de ese archivo incluyen una propiedad de texto personalizado para **Confidencial**, una propiedad de texto personalizado para **Legal** y otra que contiene los dos valores (**Confidencial Legal**). 

Cuando use subetiquetas, no configure marcas visuales, protección o condiciones en la etiqueta principal. Si utiliza subniveles, configure estos valores únicamente en la subetiqueta. Si configura estas opciones en la etiqueta principal y en su subetiqueta, la configuración de la subetiqueta tiene prioridad.

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>Cuando se etiqueta un correo electrónico, ¿los datos adjuntos reciben automáticamente el mismo etiquetado?

No. Al etiquetar un mensaje de correo electrónico que tiene datos adjuntos, dichos datos adjuntos no heredan la misma etiqueta. Los datos adjuntos siguen sin etiqueta o conservarán una etiqueta aplicada por separado. Sin embargo, si la etiqueta para el correo electrónico aplica protección, dicha protección se aplica a los datos adjuntos.

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>¿Cómo pueden las soluciones DLP y otras aplicaciones integrarse con Azure Information Protection?

Como Azure Information Protection usa metadatos persistentes para la clasificación, que incluyen una etiqueta no cifrada, esta información puede leerse mediante soluciones DLP y otras aplicaciones. En los archivos, estos metadatos se almacenan en propiedades personalizadas; en los correos electrónicos, esta información se encuentra en los encabezados del correo.

## <a name="how-is-azure-information-protection-classification-for-emails-different-from-exchange-message-classification"></a>¿En qué se diferencia la clasificación de los correos electrónicos de Azure Information Protection de la clasificación de mensajes de Exchange?

La clasificación de mensajes de Exchange es una característica antigua que puede clasificar los correos electrónicos y que se implementa con independencia de la clasificación de Azure Information Protection. Sin embargo, puede integrar las dos soluciones de modo que cuando los usuarios clasifiquen un correo electrónico mediante la aplicación web de Outlook en algunas aplicaciones de correo móviles, se agregue automáticamente la clasificación y las correspondientes marcas de etiqueta de Azure Information Protection. Exchange agrega la clasificación y el cliente de Azure Information Protection aplica la configuración de etiquetas correspondiente para esa clasificación.

Aunque la aplicación web de Outlook no admite aún la clasificación y la protección de Azure Information Protection de forma nativa, puede usar esta misma técnica para utilizar las etiquetas con este cliente de correo electrónico, además del cliente de escritorio de Outlook.

Para lograr esta solución: 

1. Use el cmdlet [New-MessageClassification](https://technet.microsoft.com/library/bb124400) de Exchange PowerShell para crear clasificaciones de mensajes con la propiedad Name que se asigna a los nombres de sus etiquetas en la directiva de Azure Information Protection. 

2. Cree una regla de transporte de Exchange para cada etiqueta. Aplique la regla cuando las propiedades del mensaje incluyan la clasificación que ha configurado, y modifique las propiedades del mensaje para establecer un encabezado de mensaje. 

    En el caso del encabezado del mensaje, encontrará la información que es necesario especificar inspeccionando los encabezados de Internet de un correo electrónico que haya enviado y clasificado con una etiqueta de Azure Information Protection. Busque el encabezado **msip_labels** y la cadena inmediatamente posterior, hasta e incluido el punto y coma. En el ejemplo anterior:
    
    **msip_labels: MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;**
    
    Luego, para el encabezado del mensaje en la regla, especifique **msip_labels** para el encabezado y el resto de la cadena para el valor del encabezado. Por ejemplo:
    
    ![Ejemplo de regla de transporte de Exchange Online que establece el encabezado del mensaje para una etiqueta de Azure Information Protection](../media/exchange-rule-for-message-header.png)

Antes de probar esto, recuerde que, al crear o editar reglas de transporte, normalmente se produce un retraso (espere una hora, por ejemplo). Sin embargo, cuando la regla está aplicada y los usuarios usan la aplicación web de Outlook o un cliente de dispositivo móvil que admite la protección de Rights Management, ocurre lo siguiente: 

- Los usuarios seleccionan la clasificación de mensajes de Exchange y envían el correo electrónico.

- La regla de Exchange detecta la clasificación de Exchange y, en función de esta, modifica el encabezado del mensaje para agregar la clasificación de Azure Information Protection.

- Cuando los destinatarios que ejecutan el cliente de Azure Information Protection ven el correo electrónico en Outlook, verán asignada la etiqueta de Azure Information Protection, así como los correspondientes encabezado, pie de página o marca de agua del correo electrónico. 

Si las etiquetas de Azure Information Protection aplican protección de administración de derechos, agregue dicha protección a la configuración de reglas mediante la selección de la opción para modificar la seguridad de los mensajes, aplique la protección de derechos y luego seleccione la plantilla de RMS o la opción No reenviar.

También puede configurar reglas de transporte para realizar la asignación inversa: al detectar una etiqueta de Information Protection, establezca una clasificación de mensajes de Exchange correspondiente. Para ello:

- Para cada etiqueta de Azure Information Protection, cree una regla de transporte que se aplique cuando el encabezado **msip_labels** incluya el nombre de la etiqueta (por ejemplo, **General**) y aplique una clasificación de mensajes que se asigne a ella.


[!INCLUDE[Commenting house rules](../includes/houserules.md)]