---
title: 'Configuración de directivas de ámbito para Azure Information Protection: AIP'
description: Para configurar valores y etiquetas diferentes para usuarios específicos, debe configurar una directiva de ámbito para Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/05/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4b134785-0353-4109-8fa7-096d1caa2242
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 505e02c48a0090551cfb57ffb57605af5b27470c
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56255155"
---
# <a name="how-to-configure-the-azure-information-protection-policy-for-specific-users-by-using-scoped-policies"></a>Configuración de la directiva de Azure Information Protection para usuarios específicos mediante directivas de ámbito

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Cuando se descarga la directiva de Azure Information Protection en equipos que tienen instalado el [cliente de Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018), todos los usuarios obtienen las configuraciones y las etiquetas de la directiva predeterminada o los cambios que se han configurado para la directiva global. Si quiere complementarlas para usuarios específicos, teniendo configuraciones y etiquetas diferentes, debe crear una **directiva de ámbito** que esté configurada para esos usuarios.

En las aplicaciones que admiten el cliente de Azure Information Protection, todos los usuarios reciben la directiva global, que contiene el título y la información sobre herramientas de Information Protection, la configuración global y las etiquetas globales. Si ha configurado directivas de ámbito para usuarios específicos, esos usuarios reciben entonces esas configuraciones y etiquetas adicionales. 

Tenga en cuenta que, además de las aplicaciones de escritorio de Office que son compatibles con el cliente de Azure Information Protection, las etiquetas también son compatibles con PowerShell y el analizador de Azure Information Protection. Esto significa que puede crear y configurar directivas con ámbito para las cuentas que ejecutan comandos de PowerShell o el analizador. 

Las directivas de ámbito, al igual que las etiquetas, se ordenan en el portal de Azure. Si un usuario está configurado para varios ámbitos, se calcula una directiva efectiva para ese usuario antes de descargarla. Según el orden de las directivas, se aplica la última configuración de directiva. Las etiquetas que ve el usuario son de la directiva global y las etiquetas adicionales de directivas de ámbito a las que pertenece el usuario.

La excepción es cuando un usuario del inquilino abre un documento o un correo electrónico etiquetados y ese usuario no está en el ámbito de la etiqueta. En este escenario, el usuario ve el nombre de la etiqueta establecida, pero esta no se muestra como disponible para seleccionarla.  

Dado que una directiva de ámbito siempre hereda la configuración y las etiquetas de la directiva global, al crear o editar una directiva de ámbito se muestran las etiquetas de la directiva global. Sin embargo, no puede editar las etiquetas de la directiva global cuando edita una directiva de ámbito. No obstante, puede agregar subetiquetas a esas etiquetas heredadas.

Por ejemplo, si tiene una etiqueta denominada **Confidencial** en la directiva global, todos los usuarios ven esta etiqueta. No puede quitarla ni cambiarla de orden con una directiva de ámbito. En cambio, puede que quiera crear una directiva de ámbito para el departamento de Marketing que agregue una nueva subetiqueta a Confidencial, por lo que estos usuarios verían **Confidencial/Promociones**. Luego, crea otra directiva de ámbito para el departamento de Ventas que agrega una nueva subetiqueta a Confidencial, de modo que estos usuarios ven **Confidencial/Asociados**. Cada subetiqueta se puede configurar después para distintas configuraciones y esta es solo visible para los usuarios de los respectivos departamentos.

Para configurar una directiva de ámbito de Azure Information Protection:

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e [inicie sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal). Después, vaya a la hoja **Azure Information Protection**.

    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. En la opción de menú **Clasificaciones** > **Directivas**: En la hoja **Azure Information Protection - Directivas**, seleccione **Agregar una directiva**. Verá la hoja **Directiva** en la que se muestra la directiva global existente, donde puede configurar la nueva directiva con ámbito.

3. Especifique un nombre de directiva y una descripción que solo los administradores vean en el portal de Azure. El nombre debe ser único en el inquilino. Después, seleccione **Specify which users/groups get this policy** (Especificar qué usuarios o grupos obtienen esta directiva) y, en las hojas siguientes, busque y seleccione los usuarios y los grupos a los que se aplica esta directiva. Las etiquetas y valores de configuración que defina en esta directiva de ámbito se aplican solo a estos usuarios.
    
    Por motivos de rendimiento, la pertenencia a grupos de las directivas con ámbito se almacena [en caché](prepare.md#group-membership-caching-by-azure-information-protection).

4. Ahora agregue nuevas etiquetas o configure los valores de la directiva de ámbito. La directiva global siempre se aplica primero, así que puede complementarla con nuevas etiquetas e invalidar los valores de configuración globales. Por ejemplo, si la directiva global no tiene especificada una etiqueta predeterminada, podría configurar una etiqueta predeterminada diferente en diferentes directivas de ámbito para departamentos específicos.

    Si necesita ayuda para configurar las etiquetas o los valores, use el vínculo de la sección [Configuración de la directiva de la organización](configure-policy.md#configuring-your-organizations-policy).

6. Lo mismo que cuando edita la directiva global, cuando realiza cambios en una hoja de Azure Information Protection, haga clic en **Guardar** para guardar los cambios o en **Descartar** para volver a la última configuración guardada. 

7. Cuando haya terminado de realizar los cambios deseados para esta directiva de ámbito, en la hoja inicial **Azure Information Protection: directivas**, asegúrese de que esta directiva de ámbito esté en el orden en que quiere que se aplique. Esto es importante cuando ha seleccionado el mismo usuario para varias directivas de ámbito. Para cambiar el orden, seleccione el menú contextual (**…**) y **Subir** o **Bajar**. 

El cliente de Azure Information Protection comprueba si hay cambios cada vez que se inicia una aplicación de Office compatible o se abre el Explorador de archivos. El cliente descarga los cambios en la directiva global o las directivas de ámbito que se apliquen a ese usuario.

## <a name="next-steps"></a>Pasos siguientes

Para ver un ejemplo de cómo personalizar la directiva predeterminada y ver el comportamiento resultante en una aplicación de Office, pruebe el tutorial [Edit the policy and create a new label](infoprotect-quick-start-tutorial.md) (Edición de la directiva y creación de una etiqueta nueva).
