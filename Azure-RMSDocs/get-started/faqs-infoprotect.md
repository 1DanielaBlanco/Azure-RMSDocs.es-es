---
title: "Preguntas más frecuentes sobre la clasificación y el etiquetado - AIP"
description: "¿Tiene alguna pregunta que trate específicamente sobre clasificación y etiquetado con Azure Information Protection? Vea si se ha resuelto aquí."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/12/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.openlocfilehash: 80efd633bc814af1ac28e4b6bf2d0b3062b27d01
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2017
---
<a id="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection" class="xliff"></a>

# Preguntas más frecuentes sobre la clasificación y el etiquetado en Azure Information Protection

>*Se aplica a: Azure Information Protection, Office 365*

¿Tiene alguna pregunta sobre Azure Information Protection que trate específicamente sobre clasificación y etiquetado?  Vea si se ha resuelto aquí. 

<a id="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection" class="xliff"></a>

## ¿Qué puedo hacer con las funcionalidades de clasificación en Azure Information Protection?

Pruebe nuestro tutorial de inicio rápido para ver esto en funcionamiento en unos minutos: [Tutorial de inicio rápido de Azure Information Protection](infoprotect-quick-start-tutorial.md).

Busque anuncios en el [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection) (Blog de seguridad y movilidad empresarial) y en nuestro [sitio de Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all) para saber cuándo estarán disponibles las funcionalidades y características de clasificación adicionales. Existen algunas limitaciones con la versión actual, que incluyen las siguientes:

- Los nombres de las etiquetas y la información sobre herramientas solo se admiten en un idioma. Sin embargo, la compatibilidad con varios idiomas ahora está en versión preliminar. Para más información, consulte [Configuración de etiquetas para distintos idiomas](../deploy-use/configure-policy-languages.md).

- No existe un registro centralizado para la clasificación y el etiquetado.

- Las condiciones para la clasificación automática deben ser frases o patrones.

- No hay capacidad de etiquetado para las aplicaciones de Office para los dispositivos móviles (iOS y Android) y los equipos Mac, y las aplicaciones web de Office (Office Online).

- No existe una integración de etiquetado y clasificación con Exchange Online o SharePoint Online.

- El SDK para asociados y desarrolladores todavía no incluye clasificación y etiquetado.

La versión de febrero quita muchas de las limitaciones anteriores. Para más información, vea el [anuncio de la entrada de blog](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/08/azure-information-protection-december-update-moves-to-general-availability/).

<a id="do-i-need-to-be-a-global-admin-to-configure-classification-and-labels" class="xliff"></a>

## ¿Es necesario ser un administrador global para configurar la clasificación y las etiquetas?

Para configurar la directiva de Azure Information Protection, ya no es necesario iniciar sesión en Azure Portal como administrador global de Azure Active Directory. Ahora también se puede usar una cuenta que tenga un rol de administrador de seguridad.

Si selecciona la opción para instalar la directiva de demostración cuando instale el [cliente de Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018), no necesita iniciar sesión en el portal para ver y probar la funcionalidad de etiquetado. La directiva de demostración instala localmente una directiva predeterminada para Azure Information Protection, de forma que pueda probar el etiquetado de documentos y correos electrónicos, pero no podrá cambiar ni agregar etiquetas nuevas sin iniciar sesión en Azure Portal. 

<a id="which-options-in-the-azure-portal-are-p2" class="xliff"></a>

## ¿Qué opciones en Azure Portal son P2?

Las opciones de Azure Portal que requieren una suscripción de **Azure Information Protection Premium 2** (P2) tienen ahora un mensaje emergente de información para identificarlas. Para obtener más información sobre qué características se incluyen en las suscripciones de P1 y P1, consulte la [lista de características](https://www.microsoft.com/cloud-platform/azure-information-protection-features) del sitio de Azure Information Protection.

<a id="can-a-file-have-more-than-one-classification" class="xliff"></a>

## ¿Puede un archivo tener más de una clasificación?

Los usuarios pueden seleccionar una sola etiqueta a la vez para cada documento o correo electrónico, lo que a menudo resulta en una sola clasificación. Sin embargo, si los usuarios seleccionan una subetiqueta, en realidad se aplican dos etiquetas a la vez: una principal y una secundaria. Con las subetiquetas, un archivo puede tener dos clasificaciones que denotan una relación entre elementos principal y secundario para así obtener un nivel adicional de control.

Por ejemplo, la etiqueta **Confidencial** podría contener subetiquetas como **Legal** y **Financiero**. Se pueden aplicar diferentes marcas visuales de clasificación y diferentes plantillas de Rights Management a estas subetiquetas. Un usuario no puede seleccionar la etiqueta **Confidencial** por sí misma, solo una de sus subetiquetas, como **Legal**. Como resultado, la etiqueta que ven es **Confidencial \ Legal**. Los metadatos de ese archivo incluyen una propiedad de texto personalizado para **Confidencial**, una propiedad de texto personalizado para **Legal** y otra que contiene los dos valores (**Confidential Legal**). 

Cuando use subetiquetas, no configure marcas visuales, protección o condiciones en la etiqueta principal. Si utiliza subniveles, configure estos valores únicamente en la subetiqueta. Si configura estas opciones en la etiqueta principal y en su subetiqueta, la configuración de la subetiqueta tiene prioridad.

<a id="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling" class="xliff"></a>

## Cuando se etiqueta un correo electrónico, ¿los datos adjuntos reciben automáticamente el mismo etiquetado?

No. Al etiquetar un mensaje de correo electrónico que tiene datos adjuntos, dichos datos adjuntos no heredan la misma etiqueta. Los datos adjuntos siguen sin etiqueta o conservan una etiqueta aplicada por separado. Sin embargo, si la etiqueta para el correo electrónico aplica protección, dicha protección se aplica a los datos adjuntos.

<a id="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection" class="xliff"></a>

## ¿Cómo pueden las soluciones DLP y otras aplicaciones integrarse con Azure Information Protection?

Como Azure Information Protection usa metadatos persistentes para la clasificación, que incluyen una etiqueta no cifrada, esta información puede leerse mediante soluciones DLP y otras aplicaciones. En los archivos, estos metadatos se almacenan en las propiedades personalizadas. En los correos electrónicos, esta información se encuentra en los encabezados del correo electrónico.

<a id="how-is-azure-information-protection-classification-for-emails-different-from-exchange-message-classification" class="xliff"></a>

## ¿En qué se diferencia la clasificación de los correos electrónicos de Azure Information Protection de la clasificación de mensajes de Exchange?

La clasificación de mensajes de Exchange es una característica antigua que puede clasificar los correos electrónicos y que se implementa con independencia de la clasificación de Azure Information Protection. 

Sin embargo, puede integrar las dos soluciones de modo que cuando los usuarios clasifiquen un correo electrónico mediante Outlook en la Web y a través de algunas aplicaciones de correo móviles, se agregue automáticamente la clasificación y las correspondientes marcas de etiqueta de Azure Information Protection. 

Puede usar esta misma técnica para usar las etiquetas con Outlook en la Web y estas aplicaciones de correo móviles.

Para los pasos de configuración, consulte [Integrate Exchange message classification with Azure Information Protection for a mobile device labeling solution](../rms-client/client-admin-guide-customizations.md#integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution) (Integración de clasificación de mensajes de Exchange con Azure Information Protection para una solución de etiquetado de dispositivos móviles). 



[!INCLUDE[Commenting house rules](../includes/houserules.md)]
