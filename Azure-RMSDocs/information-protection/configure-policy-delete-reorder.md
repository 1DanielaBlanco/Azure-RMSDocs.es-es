---
title: "Eliminación o cambio de orden de una etiqueta en Azure Information Protection | Azure Information Protection"
description: "Puede eliminar o cambiar el orden de las etiquetas que ven los usuarios en la barra de Information Protection; para ello, configúrelas en la directiva de Azure Information Protection."
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ae0f603f-a632-4ac5-a3f7-6358d4255eff
translationtype: Human Translation
ms.sourcegitcommit: 6bbac611f9c8bba96fbbba69e8044e494134d792
ms.openlocfilehash: 14863f7fcd4df2e8baaddc7837649fa3efe59019


---

# Eliminación o cambio de orden de una etiqueta en Azure Information Protection

>*Se aplica a: Azure Information Protection (versión preliminar)*

**[Esta información es preliminar y está sujeta a cambios. ]**

Puede eliminar o cambiar el orden de las etiquetas que ven los usuarios en la barra de Information Protection; para ello, configúrelas en la directiva de Azure Information Protection.

![Eliminación o cambio de orden de las etiquetas en la directiva de Azure Information Protection](../media/info-protect-contextmenu.png)

En lugar de eliminar una etiqueta, puede que simplemente quiera deshabilitarla para mantener su configuración pero impedir que se muestre en la barra de Information Protection.

Ordene las etiquetas para que los usuarios las vean en una progresión lógica en la barra de Information Protection. Por ejemplo, puede ordenarlas en sentido de confidencialidad ascendente para que los usuarios vean al principio la etiqueta menos confidencial y al final la más confidencial. La [directiva predeterminada](configure-policy-default.md) emplea esta configuración.

> [!IMPORTANT]
>Si configura [condiciones](configure-policy-classification.md) para las etiquetas que se pueden aplicar a más de una, deberá ordenar las etiquetas de la menos a la más confidencial. Este orden garantiza que cuando se evalúan las condiciones se aplica la etiqueta más confidencial.


Utilice las instrucciones siguientes para realizar estos cambios.

1. Si aún no lo ha hecho, inicie sesión en el [portal de Azure](https://portal.azure.com) y, después, navegue hasta la hoja **Azure Information Protection**. 
    
    Por ejemplo, en el menú del concentrador, haga clic en **Examinar** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. En la hoja **Azure Information Protection**, realice una de las siguientes acciones, en función de si quiere eliminar, deshabilitar o cambiar el orden de una etiqueta:

    - Para eliminar una etiqueta: haga clic con el botón derecho o seleccione el menú contextual (**...**) de la etiqueta que quiere eliminar, haga clic en **Delete this label** (Eliminar esta etiqueta) y haga clic en **Sí** para confirmar. A continuación, haga clic en **Guardar**. 

    - Para deshabilitar una etiqueta: seleccione la etiqueta que quiera deshabilitar. En la hoja **Etiqueta**, en **Habilitado**, haga clic en **Off** (Desactivado) y luego haga clic en **Guardar**.

    - Para cambiar el orden de una etiqueta: haga clic con el botón derecho o seleccione el menú contextual (**...**) de la etiqueta cuyo orden desea cambiar y haga clic en **Subir** o **Bajar** hasta que la etiqueta se sitúe en el orden deseado. A continuación, haga clic en **Guardar**. 

3. Para que los cambios estén disponibles para los usuarios, en la hoja **Azure Information Protection**, haga clic en **Publicar**.

## Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organization-s-policy) (Configuración de la directiva de la organización).  





<!--HONumber=Sep16_HO1-->


