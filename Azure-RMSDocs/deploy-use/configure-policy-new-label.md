---
title: Nueva etiqueta de Azure Information Protection
description: "Aunque Azure Information Protection incluye etiquetas predeterminadas que se pueden personalizar, también puede crear sus propias etiquetas que los usuarios verán en la barra de Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
ms.openlocfilehash: 540cd59c2df0653c449f495124334920c2cff305
ms.sourcegitcommit: 13e95906c24687eb281d43b403dcd080912c54ec
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2017
---
# <a name="how-to-create-a-new-label-for-azure-information-protection"></a>Creación de una nueva etiqueta para Azure Information Protection

>*Se aplica a: Azure Information Protection*

Aunque Azure Information Protection incluye etiquetas predeterminadas que se pueden personalizar, también puede crear sus propias etiquetas que los usuarios verán en la barra de Information Protection.

Cuando necesite un nivel de clasificación adicional, puede agregar nuevas etiquetas o etiquetas secundarias a una etiqueta existente. Por ejemplo, la última etiqueta en la [directiva predeterminada](configure-policy-default.md) contiene subetiquetas.

Utilice las instrucciones siguientes para agregar una nueva etiqueta a la directiva de Azure Information Protection.

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e inicie sesión en [Azure Portal](https://portal.azure.com) como administrador de seguridad o administrador global. Después, vaya a la hoja **Azure Information Protection**. 
    
    Por ejemplo, en el menú del centro, haga clic en **Más servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. Si la nueva etiqueta que quiere agregar es para todos los usuarios, quédese en la hoja **Azure Information Protection - Global policy** (Azure Information Protection: directiva global).
    
    Si la nueva etiqueta que quiere agregar es para los usuarios seleccionados en una [directiva con ámbito](configure-policy-scope.md), en la selección del menú **DIRECTIVAS**, seleccione **Directivas con ámbito**. Después, seleccione la directiva con ámbito en la hoja **Azure Information Protection - Scoped policies** (Azure Information Protection: directivas con ámbito).

3. En la hoja **Azure Information Protection - Global policy** (Azure Information Protection: directiva global) o la hoja **Directiva:\<nombre>**, realice una de las acciones siguientes:
    
    - Para crear una nueva etiqueta: haga clic en **Add a new label** (Agregar una nueva etiqueta).
    
    - Para crear una nueva etiqueta secundaria: haga clic con el botón derecho o seleccione el menú contextual (**...**) correspondiente a la etiqueta para la que quiere crear una etiqueta secundaria y luego haga clic en **Add a sub-label** (Agregar una etiqueta secundaria).

4. En la hoja **Etiqueta** o **Sub-label** (Etiqueta secundaria), seleccione las opciones que quiere para esta etiqueta y luego haga clic en **Guardar**.
    
    Tenga en cuenta que a las etiquetas nuevas se les asigna automáticamente el color negro. Elija un color distintivo de la lista de colores, o especifique un código hexadecimal triple para los componentes de rojo, verde y azul (RGB) del color. Por ejemplo, **#DAA520**. Si necesita una referencia de estos códigos, [Colors by Name](https://msdn.microsoft.com/library/aa358802\(v=vs.85\).aspx) (Colores por nombre), que encontrará en la documentación de MSDN, es un buen lugar para empezar. También encontrará estos códigos en muchos programas de edición de imágenes, como Microsoft Paint, que le permite elegir un color personalizado a partir de una paleta y le muestra automáticamente sus valores RGB.

5. Para que los cambios estén disponibles para los usuarios, en la hoja inicial de **Azure Information Protection**, haga clic en **Publicar**.

6. Si desea que el nombre y la descripción de esta nueva etiqueta se muestren en distintos idiomas para los usuarios, siga los procedimientos que se encuentran en [Configuración de etiquetas para distintos idiomas](configure-policy-languages.md). 

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

