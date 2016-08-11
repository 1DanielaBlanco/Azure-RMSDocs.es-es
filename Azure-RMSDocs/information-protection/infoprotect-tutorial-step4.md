---
title: "Paso 4 del tutorial de inicio rápido de Azure Information Protection | Azure Rights Management"
description: "Paso 4 del tutorial introductorio para probar rápidamente Microsoft Azure Information Protection para su organización, que contiene solo 4 pasos que deberían tardar menos de 15 minutos."
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 468748c1-49d6-4c3e-a612-9c584acdc782
translationtype: Human Translation
ms.sourcegitcommit: 93444affe94b280db2c9e4e2960c6902e491dec6
ms.openlocfilehash: cdd8dee1837c34caaeb0f8a1947dea37504e422a


---

# Paso 4: ver la clasificación, el etiquetado y la protección en funcionamiento 

>*Se aplica a: Azure Information Protection (versión preliminar)*

**[Esta información es preliminar y está sujeta a cambios. ]**

Ahora que tiene un documento de Word abierto con el cliente de Azure Information Protection instalado, está listo para ver lo sencillo que es comenzar el etiquetado y la protección de su documento mediante la directiva que hemos configurado.

La clasificación y la protección tienen lugar cuando guarda el documento, pero antes de hacerlo, usaremos nuestro documento sin guardar para ver lo sencillo que es aplicar y cambiar etiquetas.

### Para cambiar de manera manual nuestra etiqueta predeterminada:

- En la barra de Information Protection, haga clic en el icono Editar etiqueta junto a **Interno**. Esto muestra las etiquetas disponibles. Elija **Personal** y se le solicitará que justifique por qué está reduciendo el nivel de clasificación. Seleccione **Este archivo ya no requiere esa clasificación** y haga clic en **Confirmar**.  

    Verá que el valor **Confidencialidad** cambia a **Personal**.

    ![Paso 4 del tutorial de inicio rápido de Azure Information Protection: aviso para confirmar la reducción](../media/confirm-lowering.png)

### Para quitar la clasificación completamente:

- En la barra de Information Protection, haga clic en el icono Editar etiqueta junto a **Personal**. Esto muestra las etiquetas disponibles. Pero, el lugar de elegir una de las etiquetas, esta vez, haga clic en el icono Quitar etiqueta. Haga clic en **Aceptar** para confirmar y proporcionar una justificación para esta acción.  

    Verá que el valor **Confidencialidad** muestra **No establecido**, que es lo que los usuarios ven inicialmente si no establece una etiqueta predeterminada.

    ![Paso 4 del tutorial de inicio rápido de Azure Information Protection: quitar clasificación](../media/sensitivity-not-set.png)


### Para ver un aviso de recomendación para el etiquetado y la protección automática:

1. En el documento de Word, escriba un número de tarjeta de crédito válido, por ejemplo: **4242-4242-4242-4242**. 

2. Guarde el documento (use cualquier nombre de archivo, cualquier ubicación). 

3. Ahora verá el aviso: **It is recommended to label this file as Confidential (Se recomienda etiquetar este archivo como Confidencial)**. Haga clic en **Cambiar ahora**.

    ![Paso 4 del tutorial de inicio rápido de Azure Information Protection: recomendar aviso](../media/change-now.png)

    Inmediatamente, verá la marca de agua del nombre de su organización en la página, además del pie de página de **Confidencialidad: confidencial**. 

    Si ha elegido la opción para aplicar una plantilla de RMS, el documento también está protegido con la plantilla de Azure Rights Management que ha especificado, que puede confirmar cuando haga clic en la pestaña **Archivo** y vea la información de **Proteger documento**. Si ha usado la plantilla Confidencial predeterminada, verá la información de que el documento está restringido a los usuarios internos (los usuarios externos a la organización no podrán abrir el documento) y su contenido no puede copiarse ni imprimirse. Como propietario del documento, puede copiar de este e imprimirlo, pero si lo envía por correo electrónico a otro usuario de su organización, no podrán realizar estas acciones.

> [!NOTE]
>Si tiene cualquier problema para completar estos pasos, en la pestaña **Inicio**, en el grupo **Protección**, haga clic en **Proteger** y, después, haga clic en **Ayuda y comentarios**. 
>
>En el cuadro de diálogo **Microsoft Azure Information Protection**, haga clic en **Enviar comentarios**. Esto se envía por correo electrónico al equipo de Information Protection y, automáticamente, adjunta los archivos de registro de su equipo PC para ayudar en el diagnóstico de cualquier problema.

##  Pasos siguientes

Ahora que ha visto la directiva predeterminada de Azure Information Protection, cómo personalizarla y cómo funciona el etiquetado en un documento de Word, pruebe algunas de las otras opciones y vea cómo funcionan en otras aplicaciones de Office que son compatibles con Azure Information Protection: Excel, PowerPoint u Outlook. Si estas aplicaciones estaban abiertas al instalar el cliente de Azure Information Protection, ciérrelas y vuelva a abrirlas antes de intentar usarlas con Azure Information Protection.

Por ejemplo, puede cambiar el título predeterminado de **Confidencialidad** en la barra de Information Protection a un título de su elección. Puede cambiar la información sobre herramientas, los colores de las etiquetas, el orden de estas y sus nombres. Puede crear etiquetas nuevas y definir sus propias reglas automáticas. Puede ajustar las marcas de agua mediante la configuración del tamaño, el color y cambiar de diagonal a horizontal.

Tenga en cuenta que si está usando marcas de agua con Excel, solo son visibles en los modos de vista previa Diseño de página e Imprimir, y cuando se imprimen.

Cada vez que cambie cualquier opción del Portal de Azure para la directiva de Information Protection, acuérdese de **guardar** la directiva y, después, **publicarla**. Como puede realizar cambios en varias hojas, es una buena idea comprobar que ninguna muestra el botón **Guardar** como habilitado, lo que indica que tiene cambios sin guardar. Si su aplicación de Office estaba abierta cuando publicó cambios nuevos, cierre su aplicación y vuelva a abrirla para descargar la última directiva.

Cuando haya terminado su propia prueba, le puede resultar útil ver las [preguntas más frecuentes de Azure Information Protection](faq.md).




<!--HONumber=Jul16_HO5-->


