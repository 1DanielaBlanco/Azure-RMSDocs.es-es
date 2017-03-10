---
title: "Configuración de directivas de ámbito para Azure Information Protection"
description: "Para configurar valores y etiquetas diferentes para usuarios específicos, debe configurar una directiva de ámbito para Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b134785-0353-4109-8fa7-096d1caa2242
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 4f64a0f29beb11e132dbabde099902e296f2e513
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="how-to-configure-the-azure-information-protection-policy-for-specific-users-by-using-scoped-policies"></a>Configuración de la directiva de Azure Information Protection para usuarios específicos mediante directivas de ámbito

>*Se aplica a: Azure Information Protection*

Cuando se descarga la directiva de Azure Information Protection en equipos que tienen instalado el [cliente de Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018), todos los usuarios obtienen las configuraciones y las etiquetas de la directiva predeterminada o los cambios que se han configurado para la directiva global. Si quiere complementarlas para usuarios específicos, teniendo configuraciones y etiquetas diferentes, debe crear una **directiva de ámbito** que esté configurada para esos usuarios.

Todos los usuarios reciben la directiva global, que contiene el título y la información sobre herramientas de Information Protection, la configuración global y las etiquetas globales. Si ha configurado directivas de ámbito para usuarios específicos, esos usuarios reciben entonces esas configuraciones y etiquetas adicionales. 

Las directivas de ámbito, al igual que las etiquetas, se ordenan en el portal de Azure. Si un usuario está configurado para varios ámbitos, se calcula una directiva efectiva para ese usuario antes de descargarla. Según el orden de las directivas, se aplica la última configuración de directiva. Las etiquetas que ve el usuario son de la directiva global y las etiquetas adicionales de directivas de ámbito a las que pertenece el usuario. 

Dado que una directiva de ámbito siempre hereda la configuración y las etiquetas de la directiva global, al crear o editar una directiva de ámbito se muestran las etiquetas de la directiva global. Sin embargo, no puede editar las etiquetas de la directiva global cuando edita una directiva de ámbito. No obstante, puede agregar subetiquetas a esas etiquetas heredadas.

Por ejemplo, si tiene una etiqueta denominada **Confidencial** en la directiva global, todos los usuarios ven esta etiqueta. No puede quitarla ni cambiar su orden con una directiva de ámbito. Sin embargo, puede que quiera crear una directiva de ámbito para el departamento de Marketing que agrega una nueva subetiqueta a Confidencial, por lo que estos usuarios verían **Confidencial\Promociones**. Luego crea otra directiva de ámbito para el departamento de Ventas que agrega una nueva subetiqueta a Confidencial, de modo que estos usuarios ven **Confidencial/Asociados**. Cada subetiqueta se puede configurar luego para distintas configuraciones y esta es solo visible para los usuarios de los departamentos respectivos.


Para configurar una directiva de ámbito de Azure Information Protection:

1. En una nueva ventana del explorador, inicie sesión en [Azure Portal](https://portal.azure.com) como administrador global.

2. Vaya a la hoja **Azure Information Protection**: por ejemplo, en el menú del centro, haga clic en **Más servicios** y comience a escribir **Information Protection** en el cuadro Filtro. De los resultados, seleccione **Azure Information Protection**. 

    En la hoja inicial de **Azure Information Protection**, seleccione **Agregar una directiva**. Verá entonces la segunda hoja que se usa para mostrar la actualización de la directiva global, por lo que ahora puede configurar la nueva directiva de ámbito.

3. Especifique un nombre de directiva y una descripción que solo los administradores vean en el portal de Azure. El nombre debe ser único en el inquilino. A continuación, haga clic en **Specify which users/groups get this policy** (Especificar qué usuarios o grupos obtienen esta directiva) y, en las siguientes hojas, busque y seleccione los usuarios y grupos a los que se aplica esta directiva. Las etiquetas y valores de configuración que defina en esta directiva de ámbito se aplican solo a estos usuarios. 

4. Ahora cree nuevas etiquetas o configure los valores de la directiva de ámbito. La directiva global siempre se aplica primero, así que puede complementarla con nuevas etiquetas e invalidar los valores de configuración globales. Por ejemplo, si la directiva global no tiene especificada una etiqueta predeterminada, podría configurar una etiqueta predeterminada diferente en diferentes directivas de ámbito para departamentos específicos.

    Si necesita ayuda para configurar las etiquetas o los valores, use el vínculo de la sección [Configuración de la directiva de la organización](configure-policy.md#configuring-your-organizations-policy).

5. Lo mismo que cuando edita la directiva global, cuando realiza cambios en una hoja de Azure Information Protection, haga clic en **Guardar** para guardar los cambios o en **Descartar** para volver a la última configuración guardada. 

6. Cuando haya terminado de realizar los cambios deseados para esta directiva de ámbito, en la hoja inicial de **Azure Information Protection**, asegúrese de que esta directiva de ámbito esté en el orden en que quiere que se aplique. Esto es importante cuando ha seleccionado el mismo usuario para varias directivas de ámbito. A continuación, haga clic en **Publicar**. 

El cliente de Azure Information Protection comprueba si hay cambios cada vez que se inicia una aplicación de Office compatible o se abre el Explorador de archivos. El cliente descarga los cambios en la directiva global o las directivas de ámbito que se apliquen a ese usuario.

> [!TIP]
> Después de guardar la directiva de ámbito, puede utilizar el **Editor de directivas cruzadas** de la hoja **Azure Information Protection** inicial, para ver y volver a configurar todas las etiquetas de la directiva de Azure Information Protection. Este método proporciona una manera fácil de comparar etiquetas de varias directivas (su directiva global y todas las directivas de ámbito). Sin embargo, este editor no permite agregar o reordenar etiquetas, o ver o definir la configuración de directivas.

## <a name="next-steps"></a>Pasos siguientes

Para ver un ejemplo de cómo personalizar la directiva predeterminada y ver el comportamiento resultante en una aplicación de Office, pruebe el [tutorial de inicio rápido de Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
