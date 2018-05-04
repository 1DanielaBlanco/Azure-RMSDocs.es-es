---
title: Agregar o quitar una etiqueta a o desde una directiva de Azure Information Protection
description: Agregar o quitar una etiqueta de Azure Information Protection a o desde la directiva global para todos los usuarios, o hacia o desde una directiva de ámbito para un subconjunto de usuarios.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/22/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0546cc11-67a5-4194-8c54-f3ac8ce9ebe1
ms.openlocfilehash: 73152d2202096775d315f874b30269c89213f8e1
ms.sourcegitcommit: 94d1c7c795e305444e9fde17ad73e46f242bcfa9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2018
---
# <a name="add-or-remove-a-label-to-or-from-an-azure-information-protection-policy"></a>Agregar o quitar una etiqueta a o desde una directiva de Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

>[!NOTE]
> En este artículo se reflejan las actualizaciones más recientes para Azure Portal, que le permiten crear una etiqueta de forma independiente de la directiva global o de una directiva de ámbito. También se quita la opción para publicar las directivas. Si el inquilino aún no está actualizado para estos cambios, por ejemplo, todavía se ve una opción **Publicar** para Azure Information Protection y no ve la opción de menú **CLASIFICACIONES**, espere unos días y luego vuelva a estas instrucciones.  

Después de crear una etiqueta de Azure Information Protection, puede agregarla a una directiva para que esté disponible para los usuarios. Si la etiqueta es para todos los usuarios, agregue la etiqueta a la directiva global. Si la etiqueta es para un subconjunto de usuarios, agregue la etiqueta a una directiva de ámbito. Actualmente, se puede agregar una etiqueta solo con una directiva. Para agregar una subetiqueta, la etiqueta principal debe estar en la misma directiva o en la directiva global.

Para las etiquetas que ya están en una directiva, puede quitarlas de la directiva. Esta acción no elimina la etiqueta. Sigue estando disponible para su uso en otra directiva.

Si aún no ha creado la etiqueta, consulte [Creación de una nueva etiqueta para Azure Information Protection](configure-policy-new-label.md).

Si tiene que crear una directiva de ámbito para que la etiqueta se aplique a un subconjunto de usuarios, consulte [Configuración de la directiva de Azure Information Protection para usuarios específicos mediante directivas de ámbito](configure-policy-scope.md).

## <a name="to-add-or-remove-a-label-to-or-from-a-policy"></a>Para agregar o quitar una etiqueta a o desde una directiva

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e [inicie sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal). Después, vaya a la hoja **Azure Information Protection**.
    
    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. En la opción de menú **CLASIFICACIONES** > **Directivas**: en la hoja **Azure Information Protection** - **Directivas**, seleccione **Global** si la etiqueta que desea agregar o quitar se aplica a todos los usuarios.

    Si la etiqueta que desea agregar o quitar se aplica a un subconjunto de usuarios, seleccione en su lugar la directiva de ámbito.

3. En la hoja **Directiva**, seleccione **Agregar o quitar etiquetas**.

4. En la hoja **Directiva: Agregar o quitar etiquetas**, verá todas las etiquetas con una casilla activada si ya están en una directiva, y el nombre de la directiva correspondiente en la columna **DIRECTIVA**.
     
    Las subetiquetas se muestran con sangría aplicada. En una directiva de ámbito, las etiquetas que se heredan de la directiva global se muestran como no disponibles.
    
    Realice una de las siguientes acciones y haga clic en **Aceptar**:
    
    - Para agregar una etiqueta, selecciónela, lo que agrega una casilla activada.
    
    - Para quitar una etiqueta, desactive la casilla.
  
5. Para guardar los cambios, haga clic en **Guardar**.
   
    Los cambios están disponibles para los usuarios y servicios. Ya no hay una opción de publicación separada.


## <a name="next-steps"></a>Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
