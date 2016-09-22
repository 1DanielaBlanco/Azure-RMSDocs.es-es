---
title: "Tutorial de inicio rápido de Azure Information Protection, paso 2 | Azure Information Protection"
description: "Paso 2 del tutorial introductorio rápido para probar Microsoft Azure Information Protection para su organización, que contiene solo 4 pasos que deberían tardar menos de 15 minutos."
author: cabailey
manager: mbaldwin
ms.date: 09/14/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
translationtype: Human Translation
ms.sourcegitcommit: ba0f05619e1d13e16b8d4f6d86231b89e9326726
ms.openlocfilehash: 9dfbeb4c887c619d07b11be0da304ac4f4e7d4a9


---

# Paso 2: configurar y publicar la directiva de Azure Information Protection

>*Se aplica a: Azure Information Protection (versión preliminar)*

**[Esta información es preliminar y está sujeta a cambios. ]**

Aunque Azure Information Protection incluye una directiva predeterminada que se puede usar sin necesidad de configuración, echaremos un vistazo a esa directiva y haremos algunos cambios.

1. En una nueva ventana del explorador, inicie sesión en [Azure Portal](https://portal.azure.com). Si quiere probar la protección, así como la clasificación y etiquetado, inicie sesión como administrador global para que pueda recuperar las plantillas de Azure Rights Management.
 
2. En el menú del concentrador: haga clic en **Nuevo** > **Seguridad e identidad** > **Azure Information Protection (versión preliminar)** > **Crear**.

    Esto crea la hoja **Azure Information Protection** de modo que la próxima vez que inicie sesión en el portal pueda seleccionar el servicio desde la lista **Más servicios** del panel central. 

    > [!TIP] 
    > Seleccione **Anclar al panel** para crear un icono de **Azure Information Protection** en el panel, de modo que pueda omitir el examen del servicio la próxima vez que inicie sesión en el portal.

3.  Explore la hoja principal **Azure Information Protection**, en la que se muestra la directiva predeterminada de Information Protection que se ha creado automáticamente:
    
    - Etiquetas de clasificación: **Personal**, **Público**, **Interno**, **Confidencial** y **Secreto**. Lea la información sobre herramientas de cada etiqueta para saber cómo usarlas. Tenga en cuenta que **Secreto** tiene dos etiquetas secundarias: **Todos los empleados** y **Mi grupo**, que proporciona un ejemplo de cómo una clasificación puede tener subcategorías.

    - Con la configuración predeterminada, las etiquetas **Interno**, **Confidencial** y **Secreto** tienen distintivos visuales configurados (por ejemplo, pie de página, encabezado, marca de agua) y ninguna de las etiquetas tienen establecida la protección. Además, los tres valores globales no están establecidos para que ningún documento ni ningún correo electrónico deba tener una etiqueta; no hay ninguna etiqueta predeterminada y los usuarios no tienen que dar ninguna justificación si bajan el nivel de confidencialidad.

    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection - Directiva predeterminada](../media/info-protect-policy.png)

En nuestro tutorial, cambiaremos algunos de estos valores globales para que pueda ver cómo funcionan:

-  **Select the default label** (Seleccionar la etiqueta predeterminada): establezca esta opción en **Interno**.

- **Users must provide justification to set a lower classification label, remove a label, or remove protection** (Los usuarios deben proporcionar una justificación para establecer una etiqueta de clasificación inferior, quitar una etiqueta o quitar la protección): **active** esta opción.

Ahora cambiaremos la configuración de una de las etiquetas, **Confidencial**:

1. Haga clic en la etiqueta **Confidencial**.

2. En la hoja **Etiqueta: Confidencial**, verá la configuración disponible para cada etiqueta. Haga los siguientes cambios:

    a. Si ha activado Azure Rights Management: en la sección **Set RMS template for protecting documents and emails containing this label** (Configuración de la plantilla de RMS para proteger documentos y correos electrónicos que contienen esta etiqueta), en **Select RMS template from** (Seleccionar plantilla de RMS de), mantenga el valor predeterminado de **Azure RMS**. A continuación, en **Select RMS template** (Seleccionar plantilla de RMS), haga clic en el cuadro desplegable y seleccione la plantilla predeterminada **\<nombre de su organización > - Confidencial**. Por ejemplo, si el nombre de la organización es VanArsdel, Ltd, verá **VanArsdel, Ltd - Confidencial**, opción que debe seleccionar. Si ha desactivado esta plantilla predeterminada de Azure Rights Management, seleccione una plantilla alternativa. Pero si selecciona una plantilla de departamento, asegúrese de que su cuenta esté incluida en el ámbito.
    
    Si no ha activado Azure Rights Management, no puede usar esta opción.
    
    b. **Documents with this label have a watermark** (Los documentos que tienen esta etiqueta tienen una marca de agua): haga clic en **Activado** y, en el cuadro **Texto**, escriba el nombre de la organización. Por ejemplo, **VanArsdel, Ltd**. 
    
    c. Haga clic en **Agregar una nueva condición** y, después, en la hoja **Condición**, seleccione lo siguiente:
    
    - **Elija el tipo de condición**: **Integrada**
    
    - **Seleccionar estilo integrado**: **número de tarjeta de crédito**
    
    - **Número mínimo de repeticiones**: **1**
    
    - **Count occurrences with unique values only** (Contar solo las repeticiones con valores únicos): **On** (Activado)
    
    - Haga clic en **Guardar** para volver a la hoja **Etiqueta: Confidencial**.

3. En la hoja **Etiqueta: Confidencial**, verá que aparece **Número de tarjeta de crédito** como **NOMBRE DE CONDICIÓN** con **1** **REPETICIONES**.

4. Deje **Select how this label is applied** (Seleccionar cómo se aplica esta etiqueta) en **Recomendado**

5. En el cuadro **Enter notes for internal housekeeping**(Escribir notas para mantenimiento interno), escriba **Solo con fines de prueba**.

6. Haga clic en **Guardar** en la hoja **Etiqueta: Confidencial** y, en la hoja principal de **Azure Information Protection**, vuelva a hacer clic en **Guardar**.

7. Ahora que hemos hecho los cambios y los hemos guardado, queremos que estén disponibles para los usuarios. Para ello, haga clic en **Publicar** y en **Sí** para confirmar.

![Paso 3 del tutorial de inicio rápido de Azure Information Protection - Directiva predeterminada configurada](../media/info-protect-policy-configured.png)

Puede cerrar el portal de Azure o dejarlo abierto para probar opciones de configuración adicionales cuando haya terminado este tutorial.

Ahora que ya ha dado un vistazo a la directiva predeterminada y ha hecho algunos cambios, el siguiente paso consiste en instalar el cliente de Azure Information Protection.

|Si desea obtener más información|Información adicional|
|--------------------------------|--------------------------|
|Acerca de las opciones de configuración de la directiva|[Configuración de la directiva de Azure Information Protection](configure-policy.md)|


>[!div class="step-by-step"]
[&#171; Paso 1](infoprotect-tutorial-step1.md)
[Paso 3 &#187;](infoprotect-tutorial-step3.md)


<!--HONumber=Sep16_HO3-->


