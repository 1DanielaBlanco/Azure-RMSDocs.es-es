---
title: Paso 4 del tutorial de inicio rápido - AIP
description: 'Paso 4 de un tutorial de introducción para probar rápidamente Azure Information Protection: consulte el etiquetado y la protección en acción.'
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/30/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 468748c1-49d6-4c3e-a612-9c584acdc782
ms.openlocfilehash: f92953acfe652238ef8a36f67cdd8051324c6f18
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="step-4-see-classification-labeling-and-protection-in-action"></a>Paso 4: ver la clasificación, el etiquetado y la protección en funcionamiento 

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Ahora que tiene un documento de Word abierto con el cliente de Azure Information Protection instalado, está listo para ver lo sencillo que es comenzar el etiquetado y la protección de su documento mediante la directiva que hemos configurado.

La clasificación y la protección tienen lugar cuando guarda el documento, pero antes de hacerlo, usaremos nuestro documento sin guardar para ver lo sencillo que es aplicar y cambiar etiquetas.

## <a name="to-manually-change-our-default-label"></a>Para cambiar de manera manual nuestra etiqueta predeterminada

En la barra de Information Protection, seleccione la última etiqueta y verá cómo se muestran las subetiquetas:

![Paso 4 del tutorial de inicio rápido de Azure Information Protection: elección de una subetiqueta](../media/info-protect-sub-labelsv2.png)

Seleccione una de estas subetiquetas y verá cómo las otras etiquetas ya no aparecen en la barra ahora que ha seleccionado una etiqueta para este documento. El valor **Sensibilidad** cambia para mostrar el nombre de la etiqueta y la subetiqueta, con un cambio de color de la etiqueta correspondiente. Por ejemplo:

![Paso 4 del tutorial de inicio rápido de Azure Information Protection: subetiqueta seleccionada](../media/info-protect-sub-label-selectedv2.png)

En la barra de Information Protection, haga clic en el icono **Editar etiqueta** junto al valor de etiqueta seleccionado actualmente:

![Paso 4 del tutorial de inicio rápido de Azure Information Protection: icono Editar etiqueta](../media/info-protect-edit-label-selectedv2.png)

Esto vuelva a mostrar las etiquetas disponibles.

Ahora seleccione la primera etiqueta, **Personal**. Puesto que ha seleccionado una etiqueta de una clasificación inferior a la etiqueta seleccionada anteriormente en este documento, deberá justificar por qué se reduce el nivel de clasificación:

![Paso 4 del tutorial de inicio rápido de Azure Information Protection: aviso para confirmar la reducción](../media/info-protect-lower-justification.png)

Seleccione **Ya no se aplica la etiqueta anterior** y haga clic en **Confirmar**. El valor **Sensibilidad** cambia a **Personal** y las demás etiquetas se vuelven a ocultar.

## <a name="to-remove-the-classification-completely"></a>Para quitar la clasificación completamente

En la barra de Information Protection, haga clic en el icono **Editar etiqueta**. En lugar de elegir una de las etiquetas, haga clic en el icono **Eliminar etiqueta**:

![Paso 4 del tutorial de inicio rápido de Azure Information Protection: icono Eliminar](../media/delete-icon-from-personalv2.png)

Esta vez, cuando se le solicite, escriba "Este documento no necesita clasificación" y haga clic en **Confirmar**.  

Ve que el valor **Confidencialidad** muestra **No establecido**, que es lo que los usuarios ven inicialmente si no establece una etiqueta predeterminada.

## <a name="to-see-a-recommendation-prompt-for-labeling-and-automatic-protection"></a>Para ver un aviso de recomendación para el etiquetado y la protección automática

1. En el documento de Word, escriba un número de tarjeta de crédito válido, por ejemplo: **4242-4242-4242-4242**. 

2. Guarde el documento de forma local, con cualquier nombre de archivo. 

3. Ahora verá un aviso para aplicar la etiqueta que ha configurado para la protección cuando se detectan los números de tarjeta de crédito. Si no estamos de acuerdo con la recomendación, nuestra configuración de directiva nos permite rechazarla, seleccionando **Descartar**. Proporcionar una recomendación pero permitir que un usuario la invalide facilita reducir los falsos positivos cuando se usa la clasificación automática. Para este tutorial, haga clic en **Cambiar ahora**.

    ![Paso 4 del tutorial de inicio rápido de Azure Information Protection: recomendar aviso](../media/change-nowv2.png)

    Además del documento que ahora muestra que se aplica nuestra etiqueta configurada (por ejemplo, **Confidencial \ Finanzas**), ve inmediatamente la marca de agua del nombre de su organización en la página, y también se aplica el pie de página **Clasificado como confidencial**. 

    El documento también está protegido con los permisos que ha especificado para esta etiqueta. Para confirmar que el documento está protegido, haga clic en la pestaña **Archivo** y vea la información de **Proteger documento**. Verá que el documento está protegido como **Confidencial \ Finanzas** y la descripción de la etiqueta. 
    
    Debido a la configuración de protección de la etiqueta, solo los empleados pueden abrir el documento y algunas acciones están restringidas para ellos. Por ejemplo, como no tienen permisos para imprimir, copiar y extraer contenido, no pueden imprimir el documento ni copiar datos de él. Estas restricciones ayudan a evitar la pérdida de datos. Como propietario del documento, puede imprimirlo y copiar datos de él, pero si lo envía por correo electrónico a otros usuarios de la organización, no podrán realizar estas acciones.

4. Ya puede cerrar este documento.

Ahora que ha visto la clasificación, el etiquetado y la protección en funcionamiento, veamos cómo puede proteger sus documentos incluso cuando se comparten con usuarios de otra organización. Incluso puede realizar un seguimiento de cómo se usan y revocar su acceso.

|Si desea obtener más información|Información adicional|
|--------------------------------|--------------------------|
|Instrucciones completas para etiquetar y proteger archivos |[Clasificación y protección de un archivo o una dirección de correo electrónico](../rms-client/client-classify-protect.md)|
|Ubicación de registro de la actividad de etiquetado |[Registro de uso del cliente de Azure Information Protection](../rms-client/client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client)|


>[!div class="step-by-step"]
[&#171; Paso 3](infoprotect-tutorial-step3.md)
[Paso 5 &#187;](infoprotect-tutorial-step5.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]