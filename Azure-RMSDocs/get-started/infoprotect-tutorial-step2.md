---
title: "Paso 1 del tutorial de inicio rápido | Azure Information Protection"
description: "Paso 2 del tutorial introductorio para probar rápidamente Microsoft Azure Information Protection para su organización, que debería tardar unos 30 minutos."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 00d78bf12a7f400b3dfa7e35ada25177170e2d23


---

# <a name="step-2-configure-and-publish-the-azure-information-protection-policy"></a>Paso 2: configurar y publicar la directiva de Azure Information Protection

>*Se aplica a: Azure Information Protection*

Aunque Azure Information Protection incluye una directiva predeterminada que se puede usar sin necesidad de configuración, echaremos un vistazo a esa directiva y haremos algunos cambios.

1. En una nueva ventana del explorador, inicie sesión en [Azure Portal](https://portal.azure.com) como administrador global para su inquilino.

2. En el menú del concentrador, haga clic en **Nuevo** y, después, desde la lista **MARKETPLACE**, seleccione **Seguridad e identidad**. En la hoja **Seguridad e identidad**, de la lista **APLICACIONES DESTACADAS**, seleccione **Azure Information Protection**. En la hoja **Azure Information Protection**, haga clic en **Crear**.

    Esto crea la hoja **Azure Information Protection** de modo que la próxima vez que inicie sesión en el portal pueda seleccionar el servicio desde la lista **Más servicios** del panel central. 

    > [!TIP] 
    > Seleccione **Anclar al panel** para crear un icono de **Azure Information Protection** en el panel, de modo que pueda omitir el examen del servicio la próxima vez que inicie sesión en el portal.

3.  Explore la hoja **Policy: Global** (Directiva:Global) que aparece automáticamente, que muestra la directiva predeterminada de Information Protection que se crea automáticamente:
    
    - Etiquetas de clasificación: **Personal**, **Público**, **Interno**, **Confidencial** y **Secreto**. Lea la información sobre herramientas de cada etiqueta para saber cómo usarlas. Tenga en cuenta que **Secreto** tiene dos etiquetas secundarias: **Todos los empleados** y **Mi grupo**, que proporciona un ejemplo de cómo una clasificación puede tener subcategorías.

    - Con la configuración predeterminada, las etiquetas **Interno**, **Confidencial** y **Secreto** tienen distintivos visuales configurados (por ejemplo, pie de página, encabezado, marca de agua) y ninguna de las etiquetas tiene establecida la protección. 
    
    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection - Directiva predeterminada](../media/info-protect-policy-default-labels.png)
    
    Además, hay algunos valores globales que no están definidos de forma que no todos los documentos y correos electrónicos deban tener una etiqueta, no haya ninguna etiqueta predeterminada, los usuarios no tengan que dar ninguna justificación si cambian etiquetas y el cliente no esté configurado para un vínculo de ayuda personalizado.
    
    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection - Directiva predeterminada](../media/info-protect-policy-default-settings.png)

## <a name="changing-the-global-settings-for-a-default-template-and-prompt-for-justification"></a>Cambiar la configuración global de una plantilla predeterminada y solicitar la justificación

En nuestro tutorial, cambiaremos algunos valores de la directiva global para que pueda ver cómo funcionan:

1. En **Seleccionar la etiqueta predeterminada**, establezca esta opción en **Interno**.

2. En **Los usuarios deben proporcionar una justificación para establecer una etiqueta de clasificación inferior, quitar una etiqueta o quitar la protección**, establezca esta opción en **Activado**.

## <a name="configuring-a-label-for-protection-a-watermark-and-a-condition-to-prompt-for-classification"></a>Configurar una etiqueta para protección, una marca de agua y una condición para solicitar la clasificación

Ahora cambiaremos la configuración de una de las etiquetas, **Confidencial**:

1. Haga clic en la etiqueta **Confidencial**. 
    
    En la nueva hoja **Etiqueta: Confidencial**, verá la configuración disponible para cada etiqueta. 

2. En la hoja **Etiqueta: Confidencial**, ubique la sección **Configuración de la plantilla de RMS para proteger documentos y correos electrónicos que contienen esta etiqueta**:
    
    Para la opción **Seleccionar plantilla RMS**, mantenga la opción predeterminada de **Azure RMS**. A continuación, en **Select RMS template** (Seleccionar plantilla de RMS), haga clic en el cuadro desplegable y seleccione la plantilla predeterminada **\<nombre de su organización > - Confidencial**. 
    
    Por ejemplo, si el nombre de la organización es VanArsdel, Ltd, verá y seleccionará **VanArsdel, Ltd - Confidencial**: 
    
    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection: establecer protección Azure RMS](../media/step2-select-rms-template.png)
    
    Si ha desactivado esta plantilla predeterminada de Azure Rights Management, seleccione una plantilla alternativa. Pero si selecciona una plantilla de departamento, asegúrese de que su cuenta esté incluida en el ámbito.
    
3. Busque la sección **Establecer distintivo visual**:
    
    Para la opción **Los documentos que tienen esta etiqueta tienen una marca de agua**, haga clic en **Activado** y, en el cuadro **Texto**, escriba el nombre de la organización. Por ejemplo, **VanArsdel, Ltd**: 
    
    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection: establecer protección Azure RMS](../media/step2-configure-watermark.png)
    
    Aunque puede cambiar el tamaño, el color y el diseño de las marcas de agua, dejaremos estas opciones como predeterminadas por ahora.
    
4. Busque la sección **Configurar condiciones para aplicar automáticamente esta etiqueta**:
    
    Haga clic en **Agregar una nueva condición** y, después, en la hoja **Condición**, seleccione lo siguiente:
    
    a. **Elegir el tipo de condición**: mantener el valor predeterminado de **Integrado**.
    
    b. **Seleccionar estilo integrado**: desde el menú desplegable, seleccione **Número de tarjeta de crédito**.
    
    c. **Número mínimo de repeticiones**: mantenga el valor predeterminado de **1**.
    
    d. **Contar solo las repeticiones con valores únicos**: mantenga el valor predeterminado en **Desactivado**.
    
    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection: configurar la condición de la tarjeta de crédito](../media/step2-configure-condition.png)
    
    Haga clic en **Guardar** para volver a la hoja **Etiqueta: Confidencial**.

5. En la hoja **Etiqueta: Confidencial**, verá que aparece **Número de tarjeta de crédito** como **NOMBRE DE CONDICIÓN** con **1** **REPETICIONES**:
    
    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection: configurar la condición de la tarjeta de crédito](../media/step2-see-condition.png)

6. Para **Seleccionar cómo se aplica esta etiqueta**: mantenga el valor predeterminado de **Recomendado** y no cambie la sugerencia de la directiva predeterminada:
    
    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection: clasificación recomendada](../media/step2-keep-recommended.png)

7. En el cuadro **Escribir notas para mantenimiento interno**, escriba **Solo con fines de prueba**:
    
    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection: escribir notas](../media/step2-type-notes.png)

8. Haga clic en **Guardar** en esta hoja **Etiqueta: confidencial**. A continuación, en la hoja **Policy: Global** (Directiva:Global), haga clic de nuevo en **Guardar**.

    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection - Directiva predeterminada configurada](../media/info-protect-policy-configured.png)

9. Ahora que hemos realizado nuestros cambios y los hemos guardado, queremos que estén disponibles para los usuarios, así que en la hoja inicial de **Azure Information Protection**, haga clic en **Publicar** y luego en **Sí** para confirmar.

Puede cerrar el portal de Azure o dejarlo abierto para probar opciones de configuración adicionales cuando haya terminado este tutorial.

Ahora que ya ha dado un vistazo a la directiva predeterminada y ha hecho algunos cambios, el siguiente paso consiste en instalar el cliente de Azure Information Protection y la aplicación de Rights Management sharing.

|Si desea obtener más información|Información adicional|
|--------------------------------|--------------------------|
|Acerca de las opciones de configuración de la directiva|[Configuración de la directiva de Azure Information Protection](../deploy-use/configure-policy.md)|


>[!div class="step-by-step"]
[&#171; Paso 1](infoprotect-tutorial-step1.md)
[Paso 3 &#187;](infoprotect-tutorial-step3.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


