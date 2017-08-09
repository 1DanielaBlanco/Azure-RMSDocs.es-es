---
title: "Paso 2 del tutorial de inicio rápido - AIP"
description: "Paso 2 de un tutorial de introducción para probar rápidamente Azure Information Protection: configuración de la directiva."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
ms.openlocfilehash: 86857d9fe744ee8b8949bdf247a360492ceb8165
ms.sourcegitcommit: 55a71f83947e7b178930aaa85a8716e993ffc063
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2017
---
# <a name="step-2-configure-and-publish-the-azure-information-protection-policy"></a>Paso 2: configurar y publicar la directiva de Azure Information Protection

>*Se aplica a: Azure Information Protection*

Aunque Azure Information Protection incluye una directiva predeterminada que se puede usar sin necesidad de configuración, echaremos un vistazo a esa directiva y haremos algunos cambios.

1. En una nueva ventana del explorador, inicie sesión en [Azure Portal](https://portal.azure.com) como administrador global o administrador de seguridad para su inquilino.

2. En el menú del concentrador, haga clic en **Nuevo** y, después, desde la lista **MARKETPLACE**, seleccione **Seguridad e identidad**. En la hoja **Seguridad e identidad**, de la lista **APLICACIONES DESTACADAS**, seleccione **Azure Information Protection**. En la hoja **Azure Information Protection**, haga clic en **Crear**.

    Esto activa el servicio para el inquilino y crea la hoja **Azure Information Protection** de modo que la próxima vez que inicie sesión en el portal pueda seleccionar el servicio desde la lista **Más servicios** del panel central. 

    > [!TIP] 
    > Seleccione **Anclar al panel** para crear un icono de **Azure Information Protection** en el panel, de modo que pueda omitir el examen del servicio la próxima vez que inicie sesión en el portal.

3. Observe la información que aparece en la página **Inicio rápido** que se abre automáticamente la primera vez que se conecta al servicio. Puede volver a esta información más adelante. Para este tutorial, haga clic en **Directiva global** para abrir la hoja **Policy: Global** (Directiva: Global). Esta hoja se abre automáticamente para las conexiones subsiguientes con el servicio y muestra la directiva de Information Protection predeterminada que se crea automáticamente para el inquilino:
    
    - Etiquetas de clasificación: **Personal**, **Público**, **General**, **Confidencial** y **Extremadamente confidencial**. Las dos últimas etiquetas se expanden para mostrar subetiquetas que incluyen **Todos los empleados** y **Cualquiera (sin protección)**, para proporcionar ejemplos de cómo una clasificación puede tener subcategorías.
    
       > [!NOTE]
       > Es posible que su directiva predeterminada sea ligeramente diferente a la de este tutorial. Por ejemplo, tiene una etiqueta denominada **Interno** en lugar de **General**, y **Secreto** en lugar de **Extremadamente confidencial**. O bien, tiene una subetiqueta adicional denominada **Solo destinatarios**. Esto se debe a que hay diferentes versiones de la directiva predeterminada, en función de cuándo se ha creado para el inquilino. O bien, es posible que la haya editado manualmente antes de iniciar el tutorial.
       > 
       > Si la directiva predeterminada tiene un aspecto diferente, puede seguir usando este tutorial, pero sea consciente de estos cambios al usar las instrucciones y las imágenes siguientes. Si quiere modificar la directiva predeterminada para que coincida con la directiva predeterminada actual, vea [Directiva predeterminada de Azure Information Protection](../deploy-use/configure-policy-default.md).

    - Con la configuración predeterminada, algunas etiquetas no tienen distintivos visuales configurados (por ejemplo, pie de página, encabezado, marca de agua). En función de la directiva predeterminada, algunas etiquetas podrían tener protección establecida o no. A continuación, se indica un ejemplo:
    
    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection - Directiva predeterminada](../media/info-protect-policy-default-labelsv2.png)
    
    Además, hay algunas configuraciones de directiva que no están definidas. No todos los documentos y correos electrónicos deben tener una etiqueta, no hay ninguna etiqueta predeterminada y los usuarios no tienen que dar ninguna justificación cuando cambian etiquetas:
    
    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection - Directiva predeterminada](../media/info-protect-policy-default-settings.png)

## <a name="changing-the-settings-for-a-default-label-and-prompt-for-justification"></a>Cambiar la configuración de una etiqueta predeterminada y solicitar la justificación

En este tutorial, se cambiarán algunas de esas configuraciones de directiva para que pueda ver cómo funcionan:

1. Para **Seleccione la etiqueta predeterminada**, establezca esta opción en **General**. 

    Si no tiene esta etiqueta porque tiene una versión anterior de la directiva, elija **Interno** como etiqueta equivalente.

2. En **Los usuarios deben proporcionar una justificación para establecer una etiqueta de clasificación inferior, quitar una etiqueta o quitar la protección**, establezca esta opción en **Activado**.

## <a name="configuring-a-label-for-protection-a-watermark-and-a-condition-to-prompt-for-classification"></a>Configurar una etiqueta para protección, una marca de agua y una condición para solicitar la clasificación

Ahora cambiaremos la configuración de una de las subetiquetas, **Todos los empleados**, desde la etiqueta principal **Confidencial**. 

Si la etiqueta **Confidencial** no tiene subetiquetas porque tiene una versión anterior de la directiva, puede usar la etiqueta **Confidencial** en su lugar. Los pasos de configuración son los mismos, pero el nombre de la hoja de la etiqueta es **Confidencial** en lugar de **Todos los empleados**.

1. Asegúrese de que la etiqueta **Confidencial** está expandida para mostrar las subetiquetas y, en la etiqueta **Todos los empleados**, observe si se muestra **Azure RMS** para la columna **PROTECCIÓN**. Si es así, tiene la directiva predeterminada más reciente y la protección de esta etiqueta está configurada automáticamente. Si esta columna está en blanco, deberá configurar la protección en un paso posterior.

    Seleccione la subetiqueta **Todos los empleados** y, en la nueva hoja **Etiqueta: Todos los empleados**, verá la configuración disponible para cada etiqueta. 

2. Lea el texto **Descripción** de esta etiqueta. Describe cómo se piensa usar la etiqueta seleccionada y es visible para los usuarios como una información sobre herramientas, para ayudarles a decidir la etiqueta que se va a seleccionar.

3. Si la protección ya está configurada para la etiqueta, vaya al paso 5.
    
    Si la protección no está configurada para la etiqueta, localice la sección **Establecer permisos para documentos y correos electrónicos que contengan esta etiqueta**. Seleccione **Proteger** y, después, la barra **Protección**:
    
    ![Protección configurada para una etiqueta de Azure Information Protection](../media/info-protect-protection-bar-configured.png) 
    
4. En la hoja **Protección**, asegúrese de que **Azure RMS** está seleccionado y elija **Seleccionar una plantilla predefinida**. Haga clic en el cuadro desplegable y elija la plantilla predeterminada que permite a todos los usuarios de la organización ver y editar contenido protegido. 
    
    Si hace poco que ha obtenido su suscripción, esta plantilla se denomina **Confidencial\Todos los empleados**. 
    
    Si ya hace tiempo que la tiene, la plantilla predeterminada puede denominarse **\<nombre de su organización> - Confidencial**. Por ejemplo, si el nombre de la organización es VanArsdel, Ltd, verá y seleccionará **VanArsdel, Ltd - Confidencial**: 
    
    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection: establecer protección Azure RMS](../media/step2-select-rms-template.png)
    
    Si ha desactivado esta plantilla predeterminada de Azure Rights Management, seleccione una plantilla alternativa. Pero si selecciona una plantilla de departamento, asegúrese de que su cuenta esté incluida en el ámbito.
    
4. Haga clic en **Aceptar** para guardar los cambios y cerrar la hoja **Protección**. Verá que la barra Protección se actualiza en la hoja **Etiqueta: Todos los empleados**. Por ejemplo:
    
    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection: protección de Azure RMS configurada](../media/protection-bar-configured.png)
    
5. Ahora en la hoja **Etiqueta: Todos los empleados**, busque la sección **Establecer un distintivo visual**:
    
    Para la opción **Los documentos que tienen esta etiqueta tienen una marca de agua**, haga clic en **Activado** y, en el cuadro **Texto**, escriba el nombre de la organización. Por ejemplo, **VanArsdel, Ltd**: 
    
    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection: establecer protección Azure RMS](../media/step2-configure-watermark.png)
    
    Aunque puede cambiar el tamaño, el color y el diseño de las marcas de agua, dejaremos estas opciones en sus valores predeterminados por ahora.
    
6. Busque la sección **Configurar condiciones para aplicar automáticamente esta etiqueta**:
    
    Haga clic en **Agregar una nueva condición** y, después, en la hoja **Condición**, seleccione lo siguiente:
    
    a. **Elegir el tipo de condición**: mantener el valor predeterminado de **Integrado**.
    
    b. **Seleccionar estilo integrado**: en el menú desplegable, seleccione **Número de tarjeta de crédito**.
    
    c. **Número mínimo de repeticiones**: mantenga el valor predeterminado de **1**.
    
    d. **Contar solo las repeticiones con valores únicos**: mantenga el valor predeterminado en **Desactivado**.
    
    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection: configurar la condición de la tarjeta de crédito](../media/step2-configure-condition.png)
    
    Haga clic en **Guardar** para volver a la hoja **Etiqueta: Todos los empleados**.

7. En la hoja **Etiqueta: Todos los empleados**, puede ver que aparece **Número de tarjeta de crédito** como **NOMBRE DE CONDICIÓN** con **1** **REPETICIONES**:
    
    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection: configurar la condición de la tarjeta de crédito](../media/step2-see-condition.png)

8. Para **Seleccionar cómo se aplica esta etiqueta**: mantenga el valor predeterminado de **Recomendado** y no cambie la sugerencia de la directiva predeterminada:
    
    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection: clasificación recomendada](../media/step2-keep-recommendedv2.png)

9. En el cuadro **Escribir notas para mantenimiento interno**, escriba **Solo con fines de prueba**:
    
    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection: escribir notas](../media/step2-type-notes.png)

10. Haga clic en **Guardar** en la hoja **Etiqueta: Todos los empleados**. A continuación, en la hoja **Policy: Global** (Directiva:Global), haga clic de nuevo en **Guardar**.
    
    Si ha configurado la etiqueta para la protección, se actualiza ahora para mostrar la protección de Azure RMS:

    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection - Directiva predeterminada configurada](../media/info-protect-policy-configuredv2.png)
    
    También verá que los valores se configuran con los cambios correspondientes a la etiqueta y la justificación predeterminadas:
    
    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection: valores configurados](../media/info-protect-settings-configuredv2.png)
    
11. Ahora que hemos realizado nuestros cambios y los hemos guardado, queremos que estén disponibles para los usuarios, así que en la hoja inicial de **Azure Information Protection**, haga clic en **Publicar** y luego en **Sí** para confirmar.

    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection: publicar la directiva configurada](../media/info-protect-publish.png)

Puede cerrar el portal de Azure o dejarlo abierto para probar opciones de configuración adicionales cuando haya terminado este tutorial.

Ahora que ya ha dado un vistazo a la directiva predeterminada y ha hecho algunos cambios, el siguiente paso consiste en instalar el cliente de Azure Information Protection.

|Si desea obtener más información|Información adicional|
|--------------------------------|--------------------------|
|Acerca de las opciones de configuración de la directiva|[Configuración de la directiva de Azure Information Protection](../deploy-use/configure-policy.md)|
|Opciones de configuración de la directiva predeterminada|[Directiva predeterminada de Azure Information Protection](../deploy-use/configure-policy-default.md)|


>[!div class="step-by-step"]
[&#171; Paso 1](infoprotect-tutorial-step1.md)
[Paso 3 &#187;](infoprotect-tutorial-step3.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]