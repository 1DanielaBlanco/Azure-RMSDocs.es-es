---
title: Cambio de una etiqueta de Azure Information Protection
description: Puede cambiar o mejorar cualquiera de las etiquetas que ven los usuarios en la barra de Information Protection; para ello, configúrelas en la directiva de Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/22/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3b6d95f-334b-4d17-80a9-7d5487ab5d32
ms.openlocfilehash: 9bd9c249cdd969a2742390831c2feef8d515b837
ms.sourcegitcommit: 94d1c7c795e305444e9fde17ad73e46f242bcfa9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2018
---
# <a name="how-to-change-or-customize-an-existing-label-for-azure-information-protection"></a>Cambio o personalización de una etiqueta existente para Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

>[!NOTE]
> En este artículo se reflejan las actualizaciones más recientes para Azure Portal, que le permiten crear una etiqueta de forma independiente de la directiva global o de una directiva de ámbito. También se quita la opción para publicar las directivas. Si el inquilino aún no está actualizado para estos cambios, por ejemplo, todavía se ve una opción **Publicar** para Azure Information Protection y no ve la opción de menú **CLASIFICACIONES**, espere unos días y luego vuelva a estas instrucciones.
 
Puede cambiar o mejorar cualquiera de las etiquetas que ven los usuarios en la barra de Information Protection o en el botón **Proteger** en la cinta de Office; para ello, configure las etiquetas en Azure Portal.

Por ejemplo, puede cambiar el nombre de una etiqueta o subetiqueta, la información sobre herramientas, el color y el orden. Puede modificar si la etiqueta va a aplicar distintivos visuales como una marca de agua o un pie de página. También puede cambiar si la etiqueta va a agregar protección y la clasificación automática o recomendada.

Haga lo siguiente para cambiar una etiqueta:

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e [inicie sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal). Después, vaya a la hoja **Azure Information Protection**. 
    
    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. En la opción de menú **CLASIFICACIONES** > **Etiquetas**: en la hoja **Azure Information Protection: etiquetas**, seleccione la etiqueta que desee cambiar.

    La excepción es si quiere volver a ordenar una etiqueta: en lugar de seleccionar la etiqueta, haga clic con el botón derecho en la etiqueta o seleccione el menú contextual de la etiqueta. Luego, seleccione las opciones **Subir** o **Bajar**.

3. Siempre que realice cambios en una nueva hoja, haga clic en **Guardar** en esa hoja si desea conservar los cambios.
    
    Al hacer clic en **Guardar**, los cambios están disponibles para los usuarios y servicios. Ya no hay una opción de publicación separada.

4. Si cambió el nombre para mostrar o la descripción de la etiqueta y los configuró para más idiomas: vuelva a exportar la directiva de Azure Information Protection, proporcione traducciones nuevas e importe los cambios. Para más información, consulte [Configuración de etiquetas para distintos idiomas](configure-policy-languages.md).

> [!TIP]
>Si quiere que alguna de las etiquetas vuelva a su valores predeterminados, use la información de [La directiva de Information Protection](configure-policy-default.md).

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre las opciones que puede cambiar para una etiqueta, así como otra configuración de la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


