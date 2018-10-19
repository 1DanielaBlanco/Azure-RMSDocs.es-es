---
title: Nueva etiqueta de Azure Information Protection
description: Aunque Azure Information Protection incluye etiquetas predeterminadas que se pueden personalizar, también puede crear sus propias etiquetas que los usuarios verán en la barra de Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/30/2018
ms.topic: article
ms.service: information-protection
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
ms.openlocfilehash: 2825a2b794512364fda5cfdea7a0084e99e2db89
ms.sourcegitcommit: 7ba9850e5bb07b14741bb90ebbe98f1ebe057b10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2018
ms.locfileid: "42805564"
---
# <a name="how-to-create-a-new-label-for-azure-information-protection"></a>Creación de una nueva etiqueta para Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Aunque Azure Information Protection incluye etiquetas predeterminadas que se pueden personalizar, también puede crear sus propias etiquetas.

Cuando necesite un nivel de clasificación extra, puede agregar nuevas etiquetas o subetiquetas a una etiqueta existente. Por ejemplo, la última etiqueta de la [directiva predeterminada](configure-policy-default.md) contiene subetiquetas.

Al crear la primera subetiqueta de una etiqueta, los usuarios ya no pueden seleccionar la etiqueta original principal. En caso necesario, cree otra subetiqueta para recrear la configuración de la etiqueta principal a fin de que los usuarios puedan aplicar la misma configuración.

Utilice las instrucciones siguientes para agregar una nueva etiqueta que después se puede agregar a una directiva de Azure Information Protection.

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e [inicie sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal). Después, vaya a la hoja **Azure Information Protection**.
    
    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. En la opción de menú **CLASIFICACIONES** > **Etiquetas**: en la hoja **Azure Information Protection: etiquetas**, realice una de las acciones siguientes:
    
    - Para crear una nueva etiqueta: haga clic en **Add a new label** (Agregar una nueva etiqueta).
    
    - Para crear una subetiqueta: seleccione o haga clic con el botón derecho en el menú contextual (**...**) correspondiente a la etiqueta para la que quiera crear una subetiqueta y, luego, haga clic en **Agregar una subetiqueta**.

4. En la hoja **Etiqueta** o **Sub-label** (Etiqueta secundaria), seleccione las opciones que quiere para esta etiqueta y luego haga clic en **Guardar**.
    
    Al especificar un nombre para mostrar, se le impide especificar algunos caracteres (como una barra invertida y un Y comercial) porque no todos los servicios y aplicaciones que usan Azure Information Protection admiten estos caracteres. Además de los caracteres que están bloqueados, no se especifica el carácter **#**.    
    
    Tenga en cuenta que a las etiquetas nuevas se les asigna automáticamente el color negro. Elija un color distintivo de la lista de colores, o especifique un código hexadecimal triple para los componentes de rojo, verde y azul (RGB) del color. Por ejemplo, **#DAA520**. Si necesita una referencia de estos códigos, [Colors by Name](https://msdn.microsoft.com/library/aa358802\(v=vs.85).aspx) (Colores por nombre), que encontrará en la documentación de MSDN, es un muy buen lugar para empezar. También podrá encontrar estos códigos en muchos programas de edición de imágenes, como Microsoft Paint, que le permite elegir un color personalizado a partir de una paleta y le muestra automáticamente sus valores RGB.

5. Para que la etiqueta esté disponible para los usuarios: En la opción del menú **CLASIFICACIONES** > **Directivas**, seleccione la directiva que contiene la nueva etiqueta. Seleccione **Agregar o quitar etiquetas**. Seleccione la etiqueta en la hoja **Directiva: agregar o quitar etiquetas**, seleccione **Aceptar** y, a continuación, seleccione **Guardar**.
    
    >[!TIP]
    >En el caso de etiquetas nuevas, considere agregarlas primero a una directiva de ámbito que utilice para las pruebas. Cuando esté satisfecho con los resultados, quite la etiqueta de este ámbito de pruebas y, después, agregue la etiqueta a una directiva que se utilice en producción.     
    
    Para más información acerca de cómo agregar etiquetas, consulte [Cómo agregar o quitar una etiqueta](configure-policy-add-remove-label.md).
    
    Los cambios están disponibles para los usuarios y servicios. Ya no hay una opción de publicación separada.

6. Si desea que el nombre y la descripción de esta nueva etiqueta se muestren en distintos idiomas para los usuarios, siga los procedimientos que se encuentran en [Configuración de etiquetas para distintos idiomas](configure-policy-languages.md). 

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).  

