---
title: Cambio de una etiqueta de Azure Information Protection
description: "Puede cambiar o mejorar cualquiera de las etiquetas que ven los usuarios en la barra de Information Protection; para ello, configúrelas en la directiva de Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 332160a0b2403313acc66f9b196ac068e370fb5c
ms.lasthandoff: 02/24/2017


---

# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>Cambio o personalización de una etiqueta existente para Azure Information Protection

>*Se aplica a: Azure Information Protection*

Puede cambiar o mejorar cualquiera de las etiquetas que ven los usuarios en la barra de Information Protection; para ello, configúrelas en la directiva de Azure Information Protection.

Por ejemplo, puede cambiar el nombre de una etiqueta principal o secundaria, la información sobre herramientas, el color, el orden, si se aplican marcas visuales, como un pie de página o una marca de agua, si se aplica protección de Azure Rights Management y la clasificación automática o recomendada.

Para cambiar una etiqueta, utilice las instrucciones siguientes.


1. Si aún no lo ha hecho, abra una nueva ventana del explorador, inicie sesión en [Azure Portal](https://portal.azure.com) como administrador global y, después, navegue hasta la hoja **Azure Information Protection**. 
    
    Por ejemplo, en el menú del centro, haga clic en **Más servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. Para cambiar una etiqueta de la directiva global de modo que se aplique a todos los usuarios, seleccione la etiqueta que quiere cambiar en la hoja **Policy:Global** (Directiva: Global) y luego realice los cambios en la hoja **Etiqueta** y en cualquiera de las hojas posteriores si es necesario. Para cambiar una etiqueta de una [directiva de ámbito](configure-policy-scope.md) de modo que se aplique a los usuarios seleccionados, seleccione primero esa directiva en la hoja inicial de **Azure Information Protection**.

    La excepción es si quiere cambiar el orden de una etiqueta, que puede hacerlo en la hoja de la directiva global o en la directiva de ámbito seleccionada: haga clic con el botón derecho en la etiqueta o seleccione el menú contextual de la etiqueta y luego las opciones **Subir** o **Bajar**.

3. Siempre que realice cambios en una hoja, haga clic en **Guardar** en esa hoja si desea conservar los cambios.

4. Para que los cambios estén disponibles para los usuarios, en la hoja **Azure Information Protection**, haga clic en **Publicar**.

> [!TIP]
>Si quiere que alguna de las etiquetas vuelva a su valores predeterminados, use la información de [La directiva de Information Protection](configure-policy-default.md).

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre las opciones que puede cambiar para una etiqueta, así como otra configuración de la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



