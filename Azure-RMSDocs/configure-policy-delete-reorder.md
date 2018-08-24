---
title: Eliminación o reordenación de una etiqueta de Azure Information Protection
description: Puede eliminar o cambiar de orden las etiquetas de Azure Information Protection que ven los usuarios.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/30/2018
ms.topic: article
ms.service: information-protection
ms.assetid: ae0f603f-a632-4ac5-a3f7-6358d4255eff
ms.openlocfilehash: 25048d3a6b876b461df229d84fc8c8a188d42e09
ms.sourcegitcommit: 7ba9850e5bb07b14741bb90ebbe98f1ebe057b10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2018
ms.locfileid: "42807033"
---
# <a name="how-to-delete-or-reorder-a-label-for-azure-information-protection"></a>Eliminación o cambio de orden de una etiqueta en Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Para eliminar o cambiar de orden las etiquetas de Azure Information Protection que ven los usuarios en las aplicaciones de Office, seleccione estas acciones para las etiquetas.

![Eliminación o cambio de orden de las etiquetas en la directiva de Azure Information Protection](./media/info-protect-contextmenu.png)

Cuando elimina una etiqueta que se ha aplicado a documentos y correos electrónicos, los usuarios ven **No establecido** en el estado de la etiqueta cuando estos documentos y correos electrónicos se abren de nuevo por el cliente Azure Information Protection. Sin embargo, la información de la etiqueta permanece en los metadatos y todavía se puede leer por los servicios que buscan esta información de la etiqueta.

Además, si la etiqueta eliminada aplicó la protección, dicha protección no se quita. La configuración de protección de la etiqueta permanece y se muestra en la sección de **plantillas de protección**. Esta plantilla se puede convertir en una nueva etiqueta o vincularla a una etiqueta. Mientras permanezca esta plantilla, no se puede crear una nueva etiqueta con el mismo nombre que la etiqueta que ha eliminado. Si quiere hacerlo, tiene estas opciones:

- Convertir la plantilla en una etiqueta. 
    
    Se recomienda esta acción porque, si es necesario, puede cambiar el nombre de la plantilla y modificar la configuración de protección.

- Usar PowerShell para cambiar el nombre de la plantilla o eliminarla.
    
    Antes de realizar estas acciones, compruebe si otros administradores o servicios están usando la plantilla y la identifican por su nombre actual. Elimine una plantilla solamente si no es necesario abrir documentos o correos que estaban protegidos por la plantilla.

Para más información sobre la administración de plantillas de protección, vea [Configuración y administración de plantillas para Azure Information Protection](configure-policy-templates.md).

Antes de eliminar una etiqueta, en su lugar, considere la posibilidad de deshabilitarla o de quitarla de la directiva:
    
- Cuando deshabilita una etiqueta que se ha aplicado a documentos y correos electrónicos, la etiqueta aplicada no se quita de estos documentos y correos electrónicos. La etiqueta permanece en la directiva pero ya no se muestra como una etiqueta que los usuarios pueden seleccionar en la barra de Information Protection. La deshabilitación de una etiqueta le permite mantener la configuración original para cuando desee que los usuarios de la misma directiva seleccionen la etiqueta en otro momento, cuando solo tiene que volver a habilitar la etiqueta.

- Cuando se quita una etiqueta de una directiva, la etiqueta aplicada tampoco se quita de estos documentos y correos electrónicos. Pero cuando quite la etiqueta de la directiva, estará disponible para que agregue esta etiqueta a otra directiva. Para más información, consulte [Agregar o quitar una etiqueta a o desde una directiva de Azure Information Protection](configure-policy-add-remove-label.md).

Ordene las etiquetas para que los usuarios las vean en una progresión lógica en la barra de Information Protection. Por ejemplo, puede ordenarlas en sentido de confidencialidad ascendente para que los usuarios vean al principio la etiqueta menos confidencial y al final la más confidencial. La [directiva predeterminada](configure-policy-default.md) usa esta configuración y refleja la sensibilidad creciente en los nombres de etiqueta.

> [!IMPORTANT]
>Si configura [condiciones](configure-policy-classification.md) para las etiquetas que se pueden aplicar a más de una, deberá ordenar las etiquetas de la menos a la más confidencial. Este orden garantiza que cuando se evalúan las condiciones se aplica la etiqueta más confidencial.


Utilice las instrucciones siguientes para realizar estos cambios.

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e [inicie sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal). Después, vaya a la hoja **Azure Information Protection**. 
    
    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. En la opción de menú **CLASIFICACIONES** > **Etiquetas**: en la hoja **Azure Information Protection: etiquetas**, realice una o varias de las acciones siguientes: 

    - Para eliminar una etiqueta: haga clic con el botón derecho o seleccione el menú contextual (**...**) de la etiqueta que quiere eliminar, haga clic en **Eliminar esta etiqueta** y haga clic en **Aceptar** para confirmar. 

    - Para deshabilitar una etiqueta: seleccione la etiqueta que quiera deshabilitar. En la hoja **Etiqueta**, en **Habilitado**, haga clic en **Desactivado** y luego haga clic en **Guardar**.

    - Para cambiar el orden de una etiqueta: seleccione o haga clic con el botón derecho en el menú contextual (**...**) de la etiqueta cuyo orden quiera cambiar y haga clic en **Subir** o **Bajar** hasta que la etiqueta se sitúe en el orden deseado.  

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).  


