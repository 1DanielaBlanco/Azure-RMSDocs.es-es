---
title: Nueva etiqueta de Azure Information Protection
description: "Aunque Azure Information Protection incluye etiquetas predeterminadas que se pueden personalizar, también puede crear sus propias etiquetas que los usuarios verán en la barra de Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/25/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
ms.openlocfilehash: ee5366826f77403246b7e0b302220236dbe04298
ms.sourcegitcommit: d814d2876cf56e8fff0b107a5e3ec6df2aeda9ae
translationtype: HT
---
# <a name="how-to-create-a-new-label-for-azure-information-protection"></a>Creación de una nueva etiqueta para Azure Information Protection

>*Se aplica a: Azure Information Protection*

Aunque Azure Information Protection incluye etiquetas predeterminadas que se pueden personalizar, también puede crear sus propias etiquetas que los usuarios verán en la barra de Information Protection.

Cuando necesite un nivel de clasificación adicional, puede agregar nuevas etiquetas o etiquetas secundarias a una etiqueta existente. Por ejemplo, la última etiqueta en la [directiva predeterminada](configure-policy-default.md) contiene subetiquetas.

Utilice las instrucciones siguientes para agregar una nueva etiqueta a la directiva de Azure Information Protection.

1. Si aún no lo ha hecho, abra una nueva ventana del explorador, inicie sesión en [Azure Portal](https://portal.azure.com) como administrador de seguridad o administrador global y, después, navegue hasta la hoja **Azure Information Protection**. 
    
    Por ejemplo, en el menú del centro, haga clic en **Más servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. Si la nueva etiqueta que quiere agregar se va a aplicar a todos los usuarios, haga lo siguiente desde la hoja **Policy: Global** (Directiva: Global). 

    - Para crear una nueva etiqueta: haga clic en **Add a new label** (Agregar una nueva etiqueta).

    - Para crear una nueva etiqueta secundaria: haga clic con el botón derecho o seleccione el menú contextual (**...**) correspondiente a la etiqueta para la que quiere crear una etiqueta secundaria y luego haga clic en **Add a sub-label** (Agregar una etiqueta secundaria).
    
     Si la nueva etiqueta que quiere agregar va a estar en una [directiva de ámbito](configure-policy-scope.md) de modo que se aplica solo a los usuarios seleccionados, seleccione primero esa directiva de ámbito en la hoja inicial de **Azure Information Protection**.

3. En la hoja **Etiqueta** o **Sub-label** (Etiqueta secundaria), seleccione las opciones que quiere para esta etiqueta y luego haga clic en **Guardar**.

    > [!NOTE]
    >Para más información sobre la configuración de la protección, consulte [How to configure a label to apply protection](configure-policy-protection.md) (Configuración de una etiqueta para aplicar protección).

4. Para que los cambios estén disponibles para los usuarios, en la hoja **Azure Information Protection**, haga clic en **Publicar**.

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

