---
title: Agregar o quitar una etiqueta a o desde una directiva de Azure Information Protection
description: Agregar o quitar una etiqueta de Azure Information Protection a o desde la directiva global para todos los usuarios, o hacia o desde una directiva de ámbito para un subconjunto de usuarios.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/30/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 0546cc11-67a5-4194-8c54-f3ac8ce9ebe1
ms.openlocfilehash: a5e5e50f5271476c3690280cbe026be9ada7ceb2
ms.sourcegitcommit: 1e6394044d646278ae582c7713cac8ffb9bf4c1e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2018
ms.locfileid: "49170279"
---
# <a name="add-or-remove-a-label-to-or-from-an-azure-information-protection-policy"></a>Agregar o quitar una etiqueta a o desde una directiva de Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Después de crear una etiqueta de Azure Information Protection, puede agregarla a una directiva para que esté disponible para los usuarios. Si la etiqueta es para todos los usuarios, agregue la etiqueta a la directiva global. Si la etiqueta es para un subconjunto de usuarios, agregue la etiqueta a una directiva de ámbito. Actualmente, se puede agregar una etiqueta solo con una directiva. Para agregar una subetiqueta, la etiqueta principal debe estar en la misma directiva o en la directiva global.

Para las etiquetas que ya están en una directiva, puede quitarlas de la directiva. Esta acción no elimina la etiqueta. Sigue estando disponible para su uso en otra directiva.

Si aún no ha creado la etiqueta, consulte [Creación de una nueva etiqueta para Azure Information Protection](configure-policy-new-label.md).

Si tiene que crear una directiva de ámbito para que la etiqueta se aplique a un subconjunto de usuarios, consulte [Configuración de la directiva de Azure Information Protection para usuarios específicos mediante directivas de ámbito](configure-policy-scope.md).

## <a name="to-add-or-remove-a-label-to-or-from-a-policy"></a>Para agregar o quitar una etiqueta a o desde una directiva

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e [inicie sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal). Después, vaya a la hoja **Azure Information Protection**.
    
    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. En la opción de menú **Clasificaciones** > **Directivas**: en la hoja **Azure Information Protection** - **Directivas**, seleccione **Global** si la etiqueta que se va a agregar o quitar se aplica a todos los usuarios.

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

