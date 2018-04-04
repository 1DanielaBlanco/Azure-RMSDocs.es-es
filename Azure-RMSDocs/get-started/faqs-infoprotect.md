---
title: Preguntas más frecuentes sobre la clasificación y el etiquetado - AIP
description: ¿Tiene alguna pregunta que trate específicamente sobre clasificación y etiquetado con Azure Information Protection? Vea si se ha resuelto aquí.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/22/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.openlocfilehash: 543abf11ce2d107c3d2a52a24c6c2a474b80cfbd
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Preguntas más frecuentes sobre la clasificación y el etiquetado en Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

¿Tiene alguna pregunta sobre Azure Information Protection que trate específicamente sobre clasificación y etiquetado?  Vea si se ha resuelto aquí. 

## <a name="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection"></a>¿Qué puedo hacer con las funcionalidades de clasificación en Azure Information Protection?

Pruebe nuestro tutorial de inicio rápido para ver esto en funcionamiento en unos minutos: [Tutorial de inicio rápido de Azure Information Protection](infoprotect-quick-start-tutorial.md).

Busque anuncios en el [Enterprise Mobility and Security Blog](https://cloudblogs.microsoft.com/enterprisemobility/?product=azure-information-protection) (Blog de seguridad y movilidad empresarial) y en nuestro [sitio de Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all) para saber cuándo estarán disponibles las funcionalidades y características de clasificación adicionales. Existen algunas limitaciones con la versión actual, que incluyen las siguientes:

- No existe un registro centralizado para la clasificación y el etiquetado.

- No hay capacidad de etiquetado en las aplicaciones de Office para los dispositivos móviles (iOS y Android) y los equipos Mac, ni en las aplicaciones web de Office (Office Online).

- No existe una integración de etiquetado y clasificación con Exchange Online o SharePoint Online.

Solicite características nuevas y vote las solicitudes existentes en el [sitio de UserVoice](https://msip.uservoice.com/) de Azure Information Protection.

## <a name="do-i-need-to-be-a-global-admin-to-configure-classification-and-labels"></a>¿Es necesario ser un administrador global para configurar la clasificación y las etiquetas?

Gracias al nuevo rol de administrador de Information Protection recientemente incorporado, esta pregunta ya está solucionada en la página principal de preguntas frecuentes: [¿Hay ser un administrador global para configurar Azure Information Protection o puedo delegar a otros administradores?](faqs.md#do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators)

Si selecciona la opción para instalar la directiva de demostración cuando instale el [cliente de Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018), no necesita iniciar sesión en el portal para ver y probar la funcionalidad de etiquetado. La directiva de demostración instala localmente una directiva predeterminada de Azure Information Protection, de forma que podrá probar el etiquetado de documentos y correos electrónicos, pero no cambiar ni agregar etiquetas nuevas sin iniciar sesión en Azure Portal. 

## <a name="which-options-in-the-azure-portal-are-p2"></a>¿Qué opciones en Azure Portal son P2?

Las opciones de Azure Portal que requieren una suscripción de **Azure Information Protection Premium 2** (P2) tienen ahora un mensaje emergente de información para identificarlas. Para obtener más información sobre qué características se incluyen en las suscripciones de P1 y P1, consulte la [lista de características](https://www.microsoft.com/cloud-platform/azure-information-protection-features) del sitio de Azure Information Protection.

## <a name="can-a-file-have-more-than-one-classification"></a>¿Puede un archivo tener más de una clasificación?

Los usuarios pueden seleccionar una sola etiqueta a la vez para cada documento o correo electrónico, lo que a menudo resulta en una sola clasificación. Sin embargo, si los usuarios seleccionan una subetiqueta, en realidad se aplican dos etiquetas a la vez: una principal y una secundaria. Con las subetiquetas, un archivo puede tener dos clasificaciones que denotan una relación entre elementos principal y secundario para, así, obtener un nivel extra de control.

Por ejemplo, la etiqueta **Confidencial** podría contener subetiquetas como **Legal** y **Financiero**. Se pueden aplicar diferentes marcas visuales de clasificación y diferentes plantillas de Rights Management a estas subetiquetas. Un usuario no puede seleccionar la etiqueta **Confidencial** por sí misma, sino solo una de sus subetiquetas, como **Legal**. Como resultado, la etiqueta que ven es **Confidencial \ Legal**. Los metadatos de ese archivo incluyen una propiedad de texto personalizado para **Confidencial**, una propiedad de texto personalizado para **Legal** y otra que contiene los dos valores (**Confidential Legal**). 

Cuando use subetiquetas, no configure distintivos visuales, protección o condiciones en la etiqueta principal. Si usa subniveles, configure estos valores únicamente en la subetiqueta. Si configura estas opciones en la etiqueta principal y en su subetiqueta, la configuración de la subetiqueta tendrá prioridad.

## <a name="how-do-i-prevent-somebody-from-removing-or-changing-a-label"></a>¿Cómo se evita que alguien quite o cambie una etiqueta?

Aunque hay una [configuración de directiva](../deploy-use/configure-policy-settings.md) que requiere que los usuarios indiquen el motivo por el que reducen una etiqueta de clasificación, quitan una etiqueta o quitan la protección, esta opción no impide realizar estas acciones. Para impedir que los usuarios quiten o cambien una etiqueta, el contenido debe estar protegido y los permisos de protección no deben conceder al usuario el [derecho de uso](../deploy-use/configure-usage-rights.md) Exportar o Control total. 

# <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>Cuando se etiqueta un correo electrónico, ¿los datos adjuntos reciben automáticamente el mismo etiquetado?

No. Al etiquetar un mensaje de correo electrónico que tiene datos adjuntos, dichos datos adjuntos no heredan la misma etiqueta. Los datos adjuntos siguen sin etiqueta o conservan una etiqueta aplicada por separado. Sin embargo, si la etiqueta para el correo electrónico aplica protección, dicha protección se aplica a los datos adjuntos.

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>¿Cómo pueden las soluciones DLP y otras aplicaciones integrarse con Azure Information Protection?

Como Azure Information Protection usa metadatos persistentes para la clasificación, que incluyen una etiqueta no cifrada, esta información puede leerse mediante soluciones DLP y otras aplicaciones. 

- Para documentos de Word (.doc y .docx), hojas de cálculo de Excel (.xls y .xlsx), presentaciones de PowerPoint (.ppt y .pptx) y documentos PDF (.pdf), estos metadatos se almacenan en la siguiente propiedad personalizada: **MSIP_Label_\<GUID>_Enabled=True**  

- En los correos electrónicos, esta información se almacena en el encabezado X: **msip_labels: MSIP_Label_\<GUID>_Enabled=True;**  

Para identificar el GUID de una etiqueta, busque el valor de identificador de etiqueta en la hoja Etiqueta, al ver o configurar la directiva de Azure Information Protection en Azure Portal. En el caso de los archivos que tienen etiquetas aplicadas, también puede ejecutar el cmdlet de PowerShell [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) para identificar el GUID (MainLabelId o SubLabelId). Si una etiqueta tiene subetiquetas, especifique únicamente el GUID de una subetiqueta, no el de la etiqueta principal.

## <a name="how-is-azure-information-protection-classification-for-emails-different-from-exchange-message-classification"></a>¿En qué se diferencia la clasificación de los correos electrónicos de Azure Information Protection de la clasificación de mensajes de Exchange?

La clasificación de mensajes de Exchange es una característica antigua que puede clasificar los correos electrónicos y que se implementa con independencia de la clasificación de Azure Information Protection. 

Sin embargo, puede integrar las dos soluciones de modo que cuando los usuarios clasifiquen un correo electrónico mediante Outlook en la Web y a través de algunas aplicaciones de correo móviles, se agregue automáticamente la clasificación y las correspondientes marcas de etiqueta de Azure Information Protection. 

Puede usar esta misma técnica para usar las etiquetas con Outlook en la Web y estas aplicaciones de correo móviles.

Para los pasos de configuración, consulte [Integrate Exchange message classification with Azure Information Protection for a mobile device labeling solution](../rms-client/client-admin-guide-customizations.md#integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution) (Integración de clasificación de mensajes de Exchange con Azure Information Protection para una solución de etiquetado de dispositivos móviles). 



[!INCLUDE[Commenting house rules](../includes/houserules.md)]
