---
title: Eliminación o reordenación de una etiqueta de Azure Information Protection
description: Puede eliminar las etiquetas que ven los usuarios en la barra de Information Protection y, también, cambiarlas de orden; para ello, configúrelas en la directiva de Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/20/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ae0f603f-a632-4ac5-a3f7-6358d4255eff
ms.openlocfilehash: c24cd0bb9aae5b3a6b830151579d70561d56f7e0
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="how-to-delete-or-reorder-a-label-for-azure-information-protection"></a>Eliminación o cambio de orden de una etiqueta en Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Puede eliminar las etiquetas que los usuarios ven en la barra de Information Protection y, también, cambiarlas de orden; para ello, seleccione estas acciones en la directiva de Azure Information Protection.

![Eliminación o cambio de orden de las etiquetas en la directiva de Azure Information Protection](../media/info-protect-contextmenu.png)

Si elimina una etiqueta que se ha aplicado a documentos y mensajes de correo electrónico y, posteriormente, publica la directiva de Azure Information Protection, esa etiqueta se quitará automáticamente de esos documentos o mensajes de correo electrónico la próxima vez que los abra el cliente de Azure Information Protection.

Sin embargo, si la etiqueta aplicó la protección, dicha protección no se quita. La configuración de protección de la etiqueta permanece y se muestra en las **plantillas de protección**. Esta plantilla se puede convertir en una nueva etiqueta o vincularla a una etiqueta. Mientras permanezca esta plantilla, no se puede crear una nueva etiqueta con el mismo nombre que la etiqueta que ha eliminado. Si quiere hacerlo, tiene estas opciones:

- Convertir la plantilla en una etiqueta. 
    
    Se recomienda esta acción porque, si es necesario, puede cambiar el nombre de la plantilla y modificar la configuración de protección.

- Usar PowerShell para cambiar el nombre de la plantilla o eliminarla.
    
    Antes de realizar estas acciones, compruebe si otros administradores o servicios están usando la plantilla y la identifican por su nombre actual. Elimine una plantilla solamente si no es necesario abrir documentos o correos que estaban protegidos por la plantilla.

Para más información sobre la administración de plantillas de protección, vea [Configuración y administración de plantillas para Azure Information Protection](configure-policy-templates.md).

Antes de eliminar una etiqueta, considere la posibilidad de deshabilitarla. Cuando se deshabilita una etiqueta que se ha aplicado a documentos y correos electrónicos, la etiqueta aplicada no se quita de estos documentos y correos electrónicos, aunque ya no se mostrará como una etiqueta que los usuarios pueden seleccionar en la barra de Information Protection. La deshabilitación de una etiqueta también le permite mantener la configuración original para cuando desee que los usuarios seleccionen la etiqueta en otro momento, momento en el que solo tiene que volverla a habilitar.

Ordene las etiquetas para que los usuarios las vean en una progresión lógica en la barra de Information Protection. Por ejemplo, puede ordenarlas en sentido de confidencialidad ascendente para que los usuarios vean al principio la etiqueta menos confidencial y al final la más confidencial. La [directiva predeterminada](configure-policy-default.md) usa esta configuración y refleja la sensibilidad creciente en los nombres de etiqueta.

> [!IMPORTANT]
>Si configura [condiciones](configure-policy-classification.md) para las etiquetas que se pueden aplicar a más de una, deberá ordenar las etiquetas de la menos a la más confidencial. Este orden garantiza que cuando se evalúan las condiciones se aplica la etiqueta más confidencial.


Utilice las instrucciones siguientes para realizar estos cambios.

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e [inicie sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal). Después, vaya a la hoja **Azure Information Protection**. 
    
    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. Si la etiqueta que quiere configurar se va a aplicar a todos los usuarios, quédese en la hoja **Azure Information Protection - Global policy** (Azure Information Protection: directiva global).
    
    Si la etiqueta que quiere configurar se encuentra en una [directiva con ámbito](configure-policy-scope.md) para que se aplique únicamente a los usuarios seleccionados, en la selección del menú **DIRECTIVAS**, seleccione **Directivas con ámbito**. Después, seleccione la directiva con ámbito en la hoja **Azure Information Protection - Scoped policies** (Azure Information Protection: directivas con ámbito).

3. Realice una o varias de las acciones siguientes en la hoja **Azure Information Protection: directiva global** o en la hoja **Directiva:\<nombre>**: 

    - Para eliminar una etiqueta: haga clic con el botón derecho o seleccione el menú contextual (**...**) de la etiqueta que quiere eliminar, haga clic en **Delete this label** (Eliminar esta etiqueta) y haga clic en **Sí** para confirmar. A continuación, haga clic en **Guardar**. 

    - Para deshabilitar una etiqueta: seleccione la etiqueta que quiera deshabilitar. En la hoja **Etiqueta**, en **Habilitado**, haga clic en **Off** (Desactivado) y luego haga clic en **Guardar**.

    - Para cambiar el orden de una etiqueta: seleccione o haga clic con el botón derecho en el menú contextual (**...**) de la etiqueta cuyo orden quiera cambiar y haga clic en **Subir** o **Bajar** hasta que la etiqueta se sitúe en el orden deseado. A continuación, haga clic en **Guardar**. 

4. Para que los cambios estén disponibles para los usuarios, en la hoja **Azure Information Protection**, haga clic en **Publicar**.

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

