---
title: Cambio de una etiqueta de Microsoft Azure Information Protection
description: Para cambiar o mejorar cualquiera de las etiquetas que los usuarios ven en la barra de Information Protection, puede configurarlas en la directiva de Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.openlocfilehash: f1ffd4c459f2fa194372450f5713c920422f744d
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/29/2018
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>Procedimiento para cambiar o personalizar una etiqueta existente para Azure Information Protection

>*Válido para: Azure Information Protection*

Para cambiar o mejorar cualquiera de las etiquetas que los usuarios ven en la barra de Information Protection, puede configurarlas en la directiva de Azure Information Protection.

Por ejemplo, puede cambiar el nombre de una etiqueta principal o secundaria, la información sobre herramientas, el color y el orden. Puede cambiar si la etiqueta aplica marcas visuales, como una marca de agua o un pie de página. También puede cambiar si aplica protección y la clasificación automática o recomendada.

Para cambiar una etiqueta, siga estas instrucciones:

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e inicie sesión en [Azure Portal](https://portal.azure.com) como administrador de seguridad o administrador global. Después, vaya a la hoja **Azure Information Protection**. 
    
    Por ejemplo, en el menú del concentrador, haga clic en **Más servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. Para cambiar una etiqueta de la directiva global de modo que se aplique a todos los usuarios, seleccione la etiqueta que quiere cambiar en la hoja **Azure Information Protection: Directiva Global** y en las hojas posteriores, si es necesario. Para cambiar una etiqueta de una [directiva con ámbito](configure-policy-scope.md) de forma que se aplique solo a los usuarios seleccionados, primero seleccione **Directivas con ámbito** en la selección del menú **DIRECTIVAS**. Después, seleccione la directiva con ámbito en la hoja **Azure Information Protection: Directivas con ámbito**.

    Hay una excepción si desea cambiar el orden de una etiqueta. En la hoja de la directiva en la directiva global o en la directiva con ámbito seleccionada, haga clic con el botón derecho en la etiqueta o seleccione el menú contextual de la etiqueta. A continuación, seleccione las opciones **Subir** o **Bajar**.

3. Siempre que realice cambios en una hoja, haga clic en **Guardar** en esa hoja, si desea conservar los cambios.

4. Para que los cambios estén disponibles para los usuarios, en la hoja **Azure Information Protection**, haga clic en **Publicar**.

5. Si cambió el nombre para mostrar o la descripción de una etiqueta, y los ha configurado para idiomas adicionales, exporte de nuevo la directiva de Azure Information Protection, proporcione nuevas traducciones e importe los cambios. Para más información, consulte [Cómo configurar etiquetas y plantillas para distintos idiomas en Azure Information Protection](configure-policy-languages.md).

> [!TIP]
>Si desea que alguna de las etiquetas predeterminadas vuelva a su valor predeterminado, use la información de [Directiva predeterminada de Azure Information Protection](configure-policy-default.md).

## <a name="next-steps"></a>Pasos siguientes

Para más información acerca de cómo configurar las opciones disponibles para una etiqueta y otras opciones de la directiva de Azure Information Protection, use los vínculos de la sección [Configuración de la directiva de la organización](configure-policy.md#configuring-your-organizations-policy).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


