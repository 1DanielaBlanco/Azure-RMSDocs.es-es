---
title: "Cómo crear una nueva etiqueta | Azure Information Protection"
description: "Aunque Azure Information Protection incluye etiquetas predeterminadas que se pueden personalizar, también puede crear sus propias etiquetas que los usuarios verán en la barra de Information Protection."
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
translationtype: Human Translation
ms.sourcegitcommit: ebb11148718f22c79bb49c82b9855f5e6f2a5b18
ms.openlocfilehash: 5cf6237f33d0818c8411cbb5126fc825c3c411d7


---

# Creación de una nueva etiqueta para Azure Information Protection

>*Se aplica a: Azure Information Protection*

Aunque Azure Information Protection incluye etiquetas predeterminadas que se pueden personalizar, también puede crear sus propias etiquetas que los usuarios verán en la barra de Information Protection.

Cuando necesite un nivel de clasificación adicional, puede agregar nuevas etiquetas o etiquetas secundarias a una etiqueta existente. Por ejemplo, la etiqueta **Secreto**, que se encuentra en la [directiva predeterminada](configure-policy-default.md), contiene etiquetas secundarias.

Utilice las instrucciones siguientes para agregar una nueva etiqueta a la directiva de Azure Information Protection.

1. Si aún no lo ha hecho, abra una nueva ventana del explorador, inicie sesión en [Azure Portal](https://portal.azure.com) como administrador global y, después, navegue hasta la hoja **Azure Information Protection**. 
    
    Por ejemplo, en el menú del centro, haga clic en **Más servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. En la hoja **Azure Information Protection**, realice una de las acciones siguientes:

    - Para crear una nueva etiqueta: haga clic en **Add a new label** (Agregar una nueva etiqueta).

    - Para crear una nueva etiqueta secundaria: haga clic con el botón derecho o seleccione el menú contextual (**...**) correspondiente a la etiqueta para la que quiere crear una etiqueta secundaria y luego haga clic en **Add a sub-label** (Agregar una etiqueta secundaria).

3. En la hoja **Etiqueta** o **Sub-label** (Etiqueta secundaria), seleccione las opciones que quiere para esta etiqueta y luego haga clic en **Guardar**.

    > [!NOTE]
    >Para más información sobre la configuración de la protección, consulte [How to configure a label to apply protection](configure-policy-protection.md) (Configuración de una etiqueta para aplicar protección).

4. Para que los cambios estén disponibles para los usuarios, en la hoja **Azure Information Protection**, haga clic en **Publicar**.

## Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organization-s-policy) (Configuración de la directiva de la organización).  





<!--HONumber=Sep16_HO4-->

