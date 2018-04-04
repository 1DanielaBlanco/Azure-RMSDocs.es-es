---
title: Cambio de una etiqueta de Azure Information Protection
description: Puede cambiar o mejorar cualquiera de las etiquetas que ven los usuarios en la barra de Information Protection; para ello, configúrelas en la directiva de Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/20/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.openlocfilehash: aac1d87fb76848e31a21a046f14442293d29aa9f
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>Cambio o personalización de una etiqueta existente para Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Puede cambiar o mejorar cualquiera de las etiquetas que ven los usuarios en la barra de Information Protection; para ello, configúrelas en la directiva de Azure Information Protection.

Por ejemplo, puede cambiar el nombre de una etiqueta o subetiqueta, la información sobre herramientas, el color y el orden. Puede modificar si la etiqueta va a aplicar distintivos visuales como una marca de agua o un pie de página. También puede cambiar si la etiqueta va a agregar protección y la clasificación automática o recomendada.

Haga lo siguiente para cambiar una etiqueta:

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e [inicie sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal). Después, vaya a la hoja **Azure Information Protection**. 
    
    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. Para cambiar una etiqueta de la directiva global de modo que se aplique a todos los usuarios, seleccione la etiqueta que quiere cambiar en la hoja **Azure Information Protection - Global policy** (Azure Information Protection: directiva global) y en las hojas posteriores si es necesario. Para cambiar una etiqueta de una [directiva con ámbito](configure-policy-scope.md) para que se aplique únicamente a los usuarios seleccionados, primero seleccione **Directivas con ámbito** en la selección del menú **DIRECTIVAS**. Después, seleccione la directiva con ámbito en la hoja **Azure Information Protection - Scoped policies** (Azure Information Protection: directivas con ámbito).

    La excepción es si quiere cambiar el orden de una etiqueta, lo que puede hacer en la hoja de la directiva global o en la directiva con ámbito seleccionada: haga clic con el botón derecho en la etiqueta o seleccione el menú contextual de la etiqueta. Luego, seleccione las opciones **Subir** o **Bajar**.

3. Siempre que realice cambios en una hoja, haga clic en **Guardar** en esa hoja si desea conservar los cambios.

4. Para que los cambios estén disponibles para los usuarios, en la hoja **Azure Information Protection**, haga clic en **Publicar**.

5. Si cambió el nombre para mostrar o la descripción de la etiqueta y los configuró para más idiomas: vuelva a exportar la directiva de Azure Information Protection, proporcione traducciones nuevas e importe los cambios. Para más información, consulte [Configuración de etiquetas para distintos idiomas](configure-policy-languages.md).

> [!TIP]
>Si quiere que alguna de las etiquetas vuelva a su valores predeterminados, use la información de [La directiva de Information Protection](configure-policy-default.md).

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre las opciones que puede cambiar para una etiqueta, así como otra configuración de la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


