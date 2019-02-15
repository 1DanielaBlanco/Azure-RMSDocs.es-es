---
title: 'Adición o eliminación de una etiqueta a o desde una directiva de Azure Information Protection: AIP'
description: Agregar o quitar una etiqueta de Azure Information Protection a o desde la directiva global para todos los usuarios, o hacia o desde una directiva de ámbito para un subconjunto de usuarios.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 12/27/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0546cc11-67a5-4194-8c54-f3ac8ce9ebe1
ms.openlocfilehash: 825161b85dd1999374eab61fa640ddb5a2a05953
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259208"
---
# <a name="add-or-remove-a-label-to-or-from-an-azure-information-protection-policy"></a>Agregar o quitar una etiqueta a o desde una directiva de Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Después de crear una etiqueta de Azure Information Protection, puede agregarla a una directiva para que esté disponible para los usuarios. Si la etiqueta es para todos los usuarios, agregue la etiqueta a la directiva global. Si la etiqueta es para un subconjunto de usuarios, agregue la etiqueta a una directiva de ámbito. Se puede agregar una etiqueta solo a una directiva. 

Para agregar una subetiqueta, la etiqueta principal debe estar en la misma directiva o en la directiva global. Al agregar una subetiqueta, no se hereda la configuración de la etiqueta principal. Para los usuarios a los que se les asigna la subetiqueta en su directiva, se admite la etiqueta principal solo como un contenedor para mostrar el nombre y el color. En este escenario, no se admiten otras opciones de configuración en la etiqueta principal para marcas visuales, protección y condiciones. Aunque todavía puede configurarlos, esos valores en la etiqueta principal solo son compatibles con los usuarios que tienen la etiqueta principal en su directiva sin la subetiqueta.

Para las etiquetas que ya están en una directiva, puede quitarlas de la directiva. Esta acción no elimina la etiqueta. Sigue estando disponible para su uso en otra directiva.

Si aún no ha creado la etiqueta, consulte [Creación de una nueva etiqueta para Azure Information Protection](configure-policy-new-label.md).

Si tiene que crear una directiva de ámbito para que la etiqueta se aplique a un subconjunto de usuarios, consulte [Configuración de la directiva de Azure Information Protection para usuarios específicos mediante directivas de ámbito](configure-policy-scope.md).

## <a name="to-add-or-remove-a-label-to-or-from-a-policy"></a>Para agregar o quitar una etiqueta a o desde una directiva

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e [inicie sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal). Después, vaya a la hoja **Azure Information Protection**.
    
    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. En la opción de menú **Clasificaciones** > **Directivas**: en la hoja **Azure Information Protection** - **Directivas**, seleccione **Global** si la etiqueta que se va a agregar o quitar se aplica a todos los usuarios.

    Si la etiqueta que desea agregar o quitar se aplica a un subconjunto de usuarios, seleccione en su lugar la directiva de ámbito.

3. En la hoja **Directiva**, seleccione **Agregar o quitar etiquetas**.

4. En la hoja **Directiva: Agregar o quitar etiquetas**, verá todas las etiquetas con una casilla activada si ya están en una directiva y el nombre de la directiva correspondiente en la columna **DIRECTIVA**.
     
    Las subetiquetas se muestran con sangría aplicada. En una directiva de ámbito, las etiquetas que se heredan de la directiva global se muestran como no disponibles.
    
    Realice una de las siguientes acciones y haga clic en **Aceptar**:
    
    - Para agregar una etiqueta, selecciónela, lo que agrega una casilla activada.
    
    - Para quitar una etiqueta, desactive la casilla.
  
5. Para guardar los cambios, haga clic en **Guardar**.
   
    Los cambios están disponibles para los usuarios y servicios. Ya no hay una opción de publicación separada.


## <a name="next-steps"></a>Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).
