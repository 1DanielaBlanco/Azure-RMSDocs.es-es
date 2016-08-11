---
title: "Configuración de una etiqueta para marcas visuales de Azure Information Protection | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
translationtype: Human Translation
ms.sourcegitcommit: 93444affe94b280db2c9e4e2960c6902e491dec6
ms.openlocfilehash: 9f2d28e4f162891497a7b0518322338628118b9d


---

# Configuración de una etiqueta para marcas visuales de Azure Information Protection

>*Se aplica a: Azure Information Protection (versión preliminar)*

**[Esta información es preliminar y está sujeta a cambios. ]**

Cuando se asigna una etiqueta a un documento o a un mensaje de correo electrónico, puede seleccionar varias opciones para hacer visible la clasificación elegida. Estos marcadores visuales son un encabezado, un pie de página y una marca de agua:

Las marcas visuales se aplican a documentos de Word, Excel y PowerPoint cuando se aplica la etiqueta y cuando se guarda el documento. En los mensajes de correo electrónico, las marcas visuales se aplican cuando se envía el mensaje de correo electrónico.

Más información sobre estos marcadores visuales:

- Los encabezados y pies de página se aplican a Word, Excel, PowerPoint y Outlook.

- Las marcas de agua se aplican a Word, Excel y PowerPoint:

    - Excel: las marcas de agua son solo visibles en los modos Diseño de página y Vista previa de impresión y cuando se imprimen.

    - PowerPoint: las marcas de agua se aplican a la diapositiva patrón, como una imagen de fondo.

Utilice las siguientes instrucciones para configurar las marcas visuales para una etiqueta.

1. Inicie sesión en el [Portal de Azure](https://portal.azure.com).
 
2. En el menú del concentrador, haga clic en **Examinar** y comience a escribir **Información** en el cuadro Filtro. Seleccione **Azure Information Protection**.

3. En la hoja **Azure Information Protection**, seleccione la etiqueta que quiere configurar para marcas visuales.

4. En la hoja **Etiqueta**, en la sección **Set visual marking (such as header or footer)** (Establecer marcas visuales [como encabezado y pie de página]), configure los marcadores visuales que quiera y luego haga clic en **Guardar**:

    - Para configurar un encabezado: en **Documents with this label have a header** (Los documentos con esta etiqueta tienen un encabezado), seleccione **On** (Activado) si quiere un encabezado y **Off** (Desactivado) si no. Si selecciona **On** (Desactivado), especifique el texto, el tamaño, el color y la alineación del encabezado.

    - Para configurar un pie de página: en **Documents with this label have a footer** (Los documentos con esta etiqueta tienen un pie de página), seleccione **On** (Activado) si quiere un pie de página y **Off** (Desactivado) si no. Si selecciona **On** (Activado), especifique el texto, el tamaño, el color y la alineación del pie de página del encabezado.

    - Para configurar una marca de agua: en **Documents with this label have a watermark** (Los documentos con esta etiqueta tienen una marca de agua), seleccione **On** (Activado) si quiere una marca de agua y **Off** (Desactivado) si no. Si selecciona **On** (Activado), especifique el texto, el tamaño, el color y el diseño de la marca de agua del encabezado.

5. Para que los cambios estén disponibles para los usuarios, en la hoja **Azure Information Protection**, haga clic en **Publicar**.

## Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organization-s-policy) (Configuración de la directiva de la organización).  





<!--HONumber=Jul16_HO5-->


