---
title: "Paso 2 del tutorial de inicio rápido de Azure Information Protection | Azure Rights Management"
description: "Paso 2 del tutorial introductorio rápido para probar Microsoft Azure Information Protection para su organización, que contiene solo 4 pasos que deberían tardar menos de 15 minutos."
author: cabailey
manager: mbaldwin
ms.date: 07/20/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
translationtype: Human Translation
ms.sourcegitcommit: 463c0bc1fa86f73e2623faf5a624afeabcadeedb
ms.openlocfilehash: c6ecf22b72d862c605f8be2ab1f75fd2126f8575


---

# Paso 2: configurar y publicar la directiva de Azure Information Protection

*Se aplica a: Azure Information Protection (versión preliminar)*

Aunque Azure Information Protection incluye una directiva predeterminada que se puede usar sin necesidad de configuración, echaremos un vistazo a esa directiva y haremos algunos cambios.

1. Inicie sesión en el portal de Azure mediante este vínculo especial de Azure Information Protection: https://portal.azure.com/?microsoft_azure_informationprotection=true
 
2. En el menú del concentrador, haga clic en **Examinar** y comience a escribir **Información** en el cuadro Filtro. Seleccione **Azure Information Protection**.

- Verá la hoja principal **Azure Information Protection**, en la que se muestra la directiva predeterminada de Information Protection que se ha creado automáticamente. Esta directiva predeterminada contiene las siguientes etiquetas de clasificación: **Personal**, **Público**, **Interno**, **Confidencial** y **Secreto**. Lea la información sobre herramientas de cada etiqueta para saber cómo usarlas. Tenga en cuenta que **Secreto** tiene dos etiquetas secundarias: **Todos los empleados** y **Mi grupo**, que proporciona un ejemplo de cómo una clasificación puede tener subcategorías.

- Con sus valores predeterminados, **Interno**, **Confidencial** y **Secreto** tienen distintivos visuales configurados (por ejemplo, pie de página, encabezado, marca de agua...) y ninguna de las etiquetas tienen establecida la protección. Además, los tres valores globales no están establecidos para que ningún documento ni ningún correo electrónico deba tener una etiqueta; no hay ninguna etiqueta predeterminada y los usuarios no tienen que dar ninguna justificación si bajan el nivel de confidencialidad.

    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection - Directiva predeterminada](../media/info-protect-policy.png)

En nuestro tutorial, cambiaremos algunos de estos valores globales para que pueda ver cómo funcionan:

-  **Select the default label** (Seleccionar la etiqueta predeterminada): establezca esta opción en **Interno**.

- **Users must provide justification when lowering the sensitivity level** (Los usuarios deben proporcionar justificación al reducir el nivel de confidencialidad): establezca esta opción en **Activado**.

Ahora cambiaremos la configuración de una de las etiquetas, **Confidencial**:

1. Haga clic en la entrada de la etiqueta **Confidencial**.

2. En la hoja **Etiqueta: Confidencial**, verá la configuración disponible para cada etiqueta. Haga los siguientes cambios:

    a. Si ha activado Azure Rights Management, para la opción **Seleccionar plantilla RMS**, haga clic en el cuadro desplegable y seleccione la plantilla predeterminada **\<nombre de la organización > - Confidencial**. Por ejemplo, si el nombre de la organización es VanArsdel, Ltd, verá **VanArsdel, Ltd - Confidencial**, opción que debe seleccionar. Si ha desactivado esta plantilla predeterminada de Azure Rights Management, seleccione una plantilla alternativa. Pero si selecciona una plantilla de departamento, asegúrese de que su cuenta esté incluida en el ámbito.

    Si no ha activado Azure Rights Management, no puede usar esta opción.

    b. **Documents with this label have a watermark** (Los documentos que tienen esta etiqueta tienen una marca de agua): haga clic en **Activado** y, en el cuadro **Texto**, escriba el nombre de la organización. Por ejemplo, **VanArsdel, Ltd**. 

    c. Haga clic en **Agregar una nueva condición** y, después, en la hoja **Condición**, seleccione lo siguiente:

    - **Elija el tipo de condición**: **Integrada**

    - **Seleccionar estilo integrado**: **número de tarjeta de crédito**

    - **Número mínimo de repeticiones**: **1**

    - Haga clic en **Guardar** para volver a la hoja **Etiqueta: Confidencial**.

3. En la hoja **Etiqueta: Confidencial**, verá que aparece **Número de tarjeta de crédito** como **NOMBRE DE CONDICIÓN** con **1** **REPETICIONES**.

4. Deje **Select how this label is applied** (Seleccionar cómo se aplica esta etiqueta) en **Recomendado**

5. En el cuadro **Enter notes for internal housekeeping**(Escribir notas para mantenimiento interno), escriba **Solo con fines de prueba**.

6. Haga clic en **Guardar** en la hoja **Etiqueta: Confidencial** y, en la hoja principal de **Azure Information Protection**, vuelva a hacer clic en **Guardar**.

7. Ahora que hemos hecho los cambios y los hemos guardado, queremos que estén disponibles para los usuarios. Para ello, haga clic en **Publicar** y en **Sí** para confirmar.

![Paso 3 del tutorial de inicio rápido de Azure Information Protection - Directiva predeterminada configurada](../media/info-protect-policy-configured.png)

Puede cerrar el portal de Azure o dejarlo abierto para probar opciones de configuración adicionales cuando haya terminado este tutorial.

Ahora que ya ha dado un vistazo a la directiva predeterminada y ha hecho algunos cambios, el siguiente paso consiste en instalar el cliente de Azure Information Protection.


>[!div class="step-by-step"]
[&#171; Paso 1](infoprotect-tutorial-step1.md)
[Paso 3 &#187;](infoprotect-tutorial-step3.md)


<!--HONumber=Jul16_HO3-->


