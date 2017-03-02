---
title: "Paso 4 del tutorial de inicio rápido - AIP"
description: "Paso 3 del tutorial introductorio para probar rápidamente Microsoft Azure Information Protection para su organización, que debería durar unos 20 minutos."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/02/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 468748c1-49d6-4c3e-a612-9c584acdc782
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 57a46c7afe34717dd4335b0f9a19bd539821fc72
ms.lasthandoff: 02/24/2017


---

# <a name="step-4-see-classification-labeling-and-protection-in-action"></a>Paso 4: ver la clasificación, el etiquetado y la protección en funcionamiento 

>*Se aplica a: Azure Information Protection*

Ahora que tiene un documento de Word abierto con el cliente de Azure Information Protection instalado, está listo para ver lo sencillo que es comenzar el etiquetado y la protección de su documento mediante la directiva que hemos configurado.

La clasificación y la protección tienen lugar cuando guarda el documento, pero antes de hacerlo, usaremos nuestro documento sin guardar para ver lo sencillo que es aplicar y cambiar etiquetas.

## <a name="to-manually-change-our-default-label"></a>Para cambiar de manera manual nuestra etiqueta predeterminada

En la barra Information Protection, seleccione la etiqueta **Personal** y se le pedirá que justifique por qué está reduciendo el nivel de clasificación:

![Paso 4 del tutorial de inicio rápido de Azure Information Protection: aviso para confirmar la reducción](../media/info-protect-lower-justification.png)

Seleccione **Ya no se aplica la etiqueta anterior** y haga clic en **Confirmar**. Verá que el valor **Confidencialidad** cambia a **Personal**.

## <a name="to-remove-the-classification-completely"></a>Para quitar la clasificación completamente

En la barra de Information Protection, haga clic en el icono **Editar etiqueta** junto a **Personal**. Esto muestra las etiquetas disponibles. En lugar de elegir una de las etiquetas, esta vez, haga clic en el icono **Eliminar etiqueta**. Esta vez, escriba "Este documento no necesita clasificación" y haga clic en **Confirmar**.  

Verá que el valor **Confidencialidad** muestra **No establecido**, que es lo que los usuarios ven inicialmente si no establece una etiqueta predeterminada:

![Paso 4 del tutorial de inicio rápido de Azure Information Protection: quitar clasificación](../media/sensitivity-not-set.png)


## <a name="to-see-a-recommendation-prompt-for-labeling-and-automatic-protection"></a>Para ver un aviso de recomendación para el etiquetado y la protección automática

1. En el documento de Word, escriba un número de tarjeta de crédito válido, por ejemplo: **4242-4242-4242-4242**. 

2. Guarde el documento (use cualquier nombre de archivo, cualquier ubicación). 

3. Ahora verá el aviso: **It is recommended to label this file as Confidential (Se recomienda etiquetar este archivo como Confidencial)**. Haga clic en **Cambiar ahora**.

    ![Paso 4 del tutorial de inicio rápido de Azure Information Protection: recomendar aviso](../media/change-now.png)

    Además del documento que tiene la etiqueta establecida como Confidencial, verá inmediatamente la marca de agua del nombre de su organización en la página, y también se aplica el pie de página **Confidencialidad: confidencial**. 

    El documento también está protegido con la plantilla de Azure Rights Management que ha especificado, que puede confirmar cuando haga clic en la pestaña **Archivo** y vea la información de **Proteger documento**. Si ha usado la plantilla Confidencial predeterminada, verá la información de que el documento está restringido a los usuarios internos (los usuarios externos a la organización no podrán abrir el documento) y su contenido no puede copiarse ni imprimirse. Como propietario del documento, puede copiar de este e imprimirlo, pero si lo envía por correo electrónico a otro usuario de su organización, no podrán realizar estas acciones.

4. Ya puede cerrar este documento.

Ahora que ha visto la clasificación, el etiquetado y la protección en funcionamiento, veamos cómo puede proteger sus documentos incluso cuando se comparten con usuarios de otra organización. Incluso puede realizar un seguimiento de cómo se usan y revocar su acceso.

|Si desea obtener más información|Información adicional|
|--------------------------------|--------------------------|
|Instrucciones completas para etiquetar y proteger archivos |[Clasificación y protección de un archivo o una dirección de correo electrónico](../rms-client/client-classify-protect.md)|





>[!div class="step-by-step"]
[&#171; Paso 3](infoprotect-tutorial-step3.md)
[Paso 5 &#187;](infoprotect-tutorial-step5.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
