---
title: 'Tutorial: Edición de la directiva de Azure Information Protection y creación de una nueva etiqueta (AIP)'
description: Un tutorial introductorio para probar rápidamente Microsoft Azure Information Protection para su organización, que debería durar unos 15 minutos.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 01/29/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.openlocfilehash: e081da93ecc486de22746e4b19e2bb5334b44c66
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56254363"
---
# <a name="tutorial-edit-the-azure-information-protection-policy-and-create-a-new-label"></a>Tutorial: Edición de la directiva de Azure Information Protection y creación de una nueva etiqueta

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

En este tutorial, aprenderá a:
> [!div class="checklist"]
> * Configurar opciones de directiva
> * Creación de una nueva etiqueta 
> * Configurar la etiqueta en relación con los distintivos visuales, la clasificación recomendada y la protección
> * Ver la configuración y las etiquetas en acción

Como resultado de esta configuración, los usuarios ven una etiqueta predeterminada que se aplica cuando crea un nuevo documento o correo electrónico. Sin embargo, se les pide que apliquen la nueva etiqueta cuando se detecta información de tarjeta de crédito. Cuando se aplica la nueva etiqueta, el contenido se reclasifica y protege, con un pie de página y la marca de agua correspondientes. 

Puede finalizar este tutorial en aproximadamente 15 minutos.

## <a name="prerequisites"></a>Requisitos previos 

Para completar este tutorial, necesita lo siguiente:

1. Una suscripción que incluya el plan 2 de Azure Information Protection.
    
    Si no tiene una suscripción que incluya el plan 2 de Azure Information Protection, puede crear una cuenta [gratuita](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) para su organización.

2. Ha agregado la hoja Azure Information Protection a Azure Portal y ha confirmado que el servicio de protección está activado.

    Si necesita ayuda con estas acciones, consulte [Quickstart: Add Azure Information Protection to the Azure portal and view the policy](quickstart-viewpolicy.md) (Inicio rápido: Adición de Azure Information Protection a Azure Portal y visualización de la directiva).

3. El cliente de Azure Information Protection está instalado en su equipo. 
    
    Para instalar el cliente, vaya al [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) y descargue **AzInfoProtection.exe** en la página de Azure Information Protection.

4. Un equipo con Windows (como mínimo Windows 7 con Service Pack 1) y, en este equipo, haber iniciado sesión en aplicaciones de Office desde una de las siguientes categorías:
    
    - Aplicaciones de Office, versión mínima 1805, compilación 9330.2078 de Office 365 Empresa o Microsoft 365 Empresa cuando se le asigna una licencia de Azure Rights Management (también conocido como Azure Information Protection para Office 365).
    
    - Office 365 ProPlus.
    
    - Office Professional Plus 2019.
    
    - Office Professional Plus 2016.
    
    - Office Professional Plus 2013 con Service Pack 1.
    
    - Office Professional Plus 2010 con Service Pack 2.

Para ver una lista completa de los requisitos previos para utilizar Azure Information Protection, consulte [Requisitos de Azure Information Protection](requirements.md).

Comencemos.

## <a name="edit-the-azure-information-protection-policy"></a>Edición de la directiva de Azure Information Protection

Mediante Azure Portal, cambiaremos primero un par de configuraciones de la directiva y, a continuación, crearemos una nueva etiqueta.

### <a name="edit-the-policy-settings"></a>Edición de la configuración de directiva

1. Abra una nueva ventana del explorador e inicie sesión en [Azure Portal](https://portal.azure.com) como administrador global. Después, vaya a **Azure Information Protection**. 
    
    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.
    
    Si no es el administrador global, utilice el siguiente vínculo para roles alternativos: [Inicio de sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal)

2. Seleccione **Clasificaciones** > **Directivas** > **Global** para abrir la hoja **Policy: Global** (Directiva:global). 

3. Busque la configuración de la directiva después de las etiquetas, en la sección **Configure settings to display and apply on Information Protection end users** (Configuración de valores para mostrar y aplicar en los usuarios finales de Information Protection). 
    
    Tome nota de la configuración actual de los valores. En concreto, la configuración de **Seleccione la etiqueta predeterminada** y **Para establecer una etiqueta de clasificación menor, eliminar una etiqueta o quitar la protección, los usuarios deben dar una justificación al respecto**. Por ejemplo:
    
    ![Tutorial de Azure Information Protection: configuración de directiva para cambiar](./media/info-protect-policy-default-settings.png)
    
    Vamos a usar esta configuración de directiva más adelante, al ponerla en práctica.

4. Para la opción **Seleccione la etiqueta predeterminada**, elija **General**. 

    Si no tiene esta etiqueta porque tiene una versión anterior de la directiva, elija **Interno** como etiqueta equivalente.

5. En **Para establecer una etiqueta de clasificación menor, eliminar una etiqueta o quitar la protección, los usuarios deben dar una justificación al respecto**, establezca esta opción en **Activado** si no lo está todavía.

6. Además, asegúrese de que **Mostrar la barra de Information Protection en las aplicaciones de Office** está establecido en **Activado**.

7. Seleccione **Guardar** en esta hoja **Policy: Global** (Directiva: Global) y, si se le pide que confirme la acción, seleccione **Aceptar**. Cierre esta página.

### <a name="create-a-new-label-for-protection-visual-markers-and-a-condition-to-prompt-for-classification"></a>Creación de una etiqueta para protección, marcadores visuales y una condición para solicitar la clasificación

Ahora vamos a crear una subetiqueta para **Confidencial**.

1. Desde la opción de menú **Clasificaciones** > **Etiquetas**: Haga clic con el botón derecho en la etiqueta **Confidencial** y elija **Agregar una subetiqueta**.
    
    Si no tiene una etiqueta denominada **Confidencial**, puede seleccionar otra etiqueta o crear una etiqueta y seguir el tutorial con pequeñas diferencias.

2. En la hoja **Subetiqueta**, especifique el nombre de etiqueta **Finanzas** y agregue la siguiente descripción: **Datos confidenciales que contienen información financiera restringida únicamente a los empleados**.
    
    Este texto describe cómo se piensa usar la etiqueta seleccionada y es visible para los usuarios como una información sobre herramientas, para ayudarles a decidir la etiqueta que se va a seleccionar.

3. En **Establecer permisos para documentos y correos electrónicos que contengan esta etiqueta**, seleccione **Proteger** y, luego, **Protección**:
    
    ![Configuración de una etiqueta de Azure Information Protection para protección](./media/info-protect-protection-bar-configured.png) 
    
4. En la hoja **Protección**, asegúrese de que **Azure (clave en la nube)** esté seleccionado. Esta opción usa el servicio Azure Rights Management para proteger documentos y mensajes de correo electrónico. Además, asegúrese de que la opción **Establecer permisos** esté seleccionada. Después, seleccione **Agregar permisos**.

5. En la hoja **Agregar permisos**, seleccione **Agregar \<nombre de organización> -Todos los miembros**. Por ejemplo, si el nombre de la organización es VanArsdel Ltd, verá la siguiente opción:
    
    ![Conceder a todos los miembros permisos de protección para una etiqueta de Azure Information Protection](./media/info-protect-protection-all-members.png) 
    
    Esta opción selecciona automáticamente todos los usuarios de la organización a los que se pueden conceder permisos. Pero puede ver en las otras opciones que ya podía examinar y buscar grupos o usuarios del inquilino. O bien, al seleccionar la opción **Escriba los detalles**, puede especificar direcciones de correo electrónico individuales o incluso todos los usuarios de otra organización.

6. Para los permisos, seleccione **Revisor** entre las opciones preestablecidas. Verá que este nivel de permiso concede automáticamente algunos de los permisos que se muestran, pero no todos:
    
    ![Conceder permisos de protección de coautor para una etiqueta de Azure Information Protection](./media/info-protect-protection-reviewer.png)
    
    Puede seleccionar distintos niveles de permisos o especificar derechos de uso individuales mediante la opción **Personalizado**. Pero para este tutorial, use la opción **Revisor**. Puede experimentar con distintos permisos más adelante y leer cómo restringen lo que los usuarios especificados pueden hacer con el documento o correo electrónico protegido.

7. Haga clic en **Aceptar** para cerrar la hoja **Agregar permisos** y ver cómo se actualiza la hoja **Protección** para reflejar la configuración. Por ejemplo:
    
     ![Hoja Protección en la que se muestra la configuración de permisos para una etiqueta de Azure Information Protection](./media/info-protect-protection-configured.png)
    
    Si selecciona **Agregar permisos**, se volverá a abrir la hoja **Agregar permisos** para que pueda agregar más usuarios y concederles permisos diferentes. Por ejemplo, puede conceder únicamente acceso de vista a un grupo específico. Pero para este tutorial, usaremos un conjunto de permisos para todos los usuarios.

8. Revise y mantenga los valores predeterminados para la expiración del contenido y el acceso sin conexión y, después, haga clic en **Aceptar** para guardar y cerrar la hoja **Protección**.

8. De nuevo en la hoja **Subetiqueta**, busque la sección **Establecer un distintivo visual**:
    
    Para la opción **Los documentos con esta etiqueta tienen un pie de página**, haga clic en **Activado** y, en el cuadro **Texto**, escriba **Clasificado como confidencial**. 
    
    Para la opción **Los documentos que tienen esta etiqueta tienen una marca de agua**, haga clic en **Activado** y, en el cuadro **Texto**, escriba el nombre de la organización. Por ejemplo, **VanArsdel, Ltd**. 
    
    Aunque es posible cambiar el aspecto de estos marcadores visuales, dejaremos estas opciones en sus valores predeterminados por ahora.
    
9. Busque la sección **Configurar condiciones para aplicar automáticamente esta etiqueta**:
    
    Haga clic en **Agregar una nueva condición** y, después, en la hoja **Condición**, seleccione lo siguiente:
    
    a. **Elija el tipo de condición**: Mantenga el valor predeterminado de **Tipos de información**.
    
    b. Para **Elegir un sector**: mantenga el valor predeterminado de **Todo**.
    
    c. En el cuadro de búsqueda **Seleccione los tipos de información**: escriba **número de la tarjeta de crédito**. Después, en los resultados de la búsqueda, seleccione **Número de la tarjeta de crédito**.
    
    d. **Número mínimo de repeticiones**: mantenga el valor predeterminado de **1**.
    
    e. **Contar solo las repeticiones con valores únicos	**: mantenga el valor predeterminado de **Desactivado**.
    
    ![Tutorial de Azure Information Protection: configurar la condición de la tarjeta de crédito](./media/step2-configure-condition.png)
    
    Haga clic en **Guardar** para volver a la hoja **Subetiqueta**.

10. En la hoja **Subetiqueta**, puede ver que aparece **Número de la tarjeta de crédito** como **NOMBRE DE CONDICIÓN** con **1** **REPETICIONES**:
    
    ![Tutorial de Azure Information Protection: configurar la condición de la tarjeta de crédito](./media/step2-see-condition.png)

11. Para **Select how this label is applied** (Seleccionar cómo se aplica esta etiqueta): mantenga el valor predeterminado de **Recomendado** y no cambie la sugerencia de la directiva predeterminada. 

12. En el cuadro **Agregue notas para el uso del administrador**, escriba **Solo con fines de prueba**.

13. Haga clic en **Guardar** en la hoja **Subetiqueta**. Si se le pide que confirme, haga clic en **Aceptar**. La nueva etiqueta se crea y se guarda, pero no se agrega aún a una directiva.

14. En la opción de menú **Clasificaciones** > **Directivas**: vuelva a seleccionar **Global** y luego seleccione el vínculo **Agregar o quitar etiquetas** después de las etiquetas.

15. En la hoja **Directiva: agregar o quitar etiquetas**, seleccione la etiqueta que acaba de crear y la etiqueta denominada **Finanzas** y haga clic en **Aceptar**.

16. En la hoja **Directiva: Global** (Directiva:global), ahora verá la nueva subetiqueta en la directiva global, que está configurada para distintivos visuales y protección. Por ejemplo:

    ![Tutorial de Azure Information Protection: nueva subetiqueta](./media/info-protect-policy-configuredv2.png)
    
    También verá que los valores se configuran para la etiqueta y la justificación predeterminadas:
    
    ![Tutorial de Azure Information Protection: configuración establecida](./media/info-protect-settings-configuredv2.png)
    

17. Seleccione **Guardar** en esta hoja **Policy: Global** (Directiva:global). Si se le pide que confirme esta acción, haga clic en **Aceptar**.

Puede cerrar Azure Portal o dejarlo abierto para probar opciones de configuración adicionales cuando haya terminado este tutorial.

Está listo para probar los resultados de los cambios.

## <a name="see-classification-labeling-and-protection-in-action"></a>Visualización de la clasificación, el etiquetado y la protección en funcionamiento 

Los cambios de directiva realizados y la nueva etiqueta creada se aplican a Word, Excel, PowerPoint y Outlook. En este tutorial, vamos a usar Word para verlos en acción. 

Abra un nuevo documento en Word. Dado que el cliente de Azure Information Protection está instalado, verá lo siguiente:

![Tutorial de Azure Information Protection - cliente instalado](./media/word2016-calloutsv2.png)

- En la pestaña **Inicio**, un grupo **Protección**, con un botón denominado **Proteger**.
    
    Haga clic en **Proteger** > **Ayuda y comentarios** y, en el cuadro de diálogo **Microsoft Azure Information Protection**, confirme el estado del cliente. Debe aparecer **Connected as** (Conectado como) y su nombre de usuario. Asimismo, debe ver también una hora y fecha recientes de la última conexión y cuándo se descargó la directiva de Information Protection. Compruebe que el nombre de usuario que se muestra es correcto para su inquilino.

- Un nueva barra se muestra debajo de la cinta de opciones; la barra de Information Protection. Muestra el título **Sensibilidad** y las etiquetas que hemos visto en Azure Portal.

### <a name="to-manually-change-our-default-label"></a>Para cambiar de manera manual nuestra etiqueta predeterminada

1. En la barra de Information Protection, seleccione la última etiqueta y verá cómo se muestran las subetiquetas:
    
    ![Tutorial de Azure Information Protection: ver subetiquetas](./media/info-protect-sub-labelsv2.png)

2. Seleccione una de estas subetiquetas y verá cómo las otras etiquetas ya no aparecen en la barra ahora que ha seleccionado una etiqueta para este documento. El valor **Sensibilidad** cambia para mostrar el nombre de la etiqueta y la subetiqueta, con un cambio de color de la etiqueta correspondiente. Por ejemplo:
    
    ![Tutorial de Azure Information Protection: subetiqueta seleccionada](./media/info-protect-sub-label-selectedv2.png)

3. En la barra de Information Protection, haga clic en el icono **Editar etiqueta** junto al valor de etiqueta seleccionado actualmente:
    
    ![Tutorial de Azure Information Protection: icono Editar etiqueta](./media/info-protect-edit-label-selectedv2.png)
    
    Con esta acción se vuelven a mostrar las etiquetas disponibles.

4. Ahora seleccione la primera etiqueta, **Personal**. Puesto que seleccionó una etiqueta de una clasificación inferior a la etiqueta seleccionada anteriormente en este documento, deberá justificar por qué se reduce el nivel de clasificación:
    
    ![Tutorial de Information Protection Azure: solicitud para confirmar el motivo de la reducción](./media/info-protect-lower-justification.png)
    
    Seleccione **Ya no se aplica la etiqueta anterior** y haga clic en **Confirmar**. El valor **Sensibilidad** cambia a **Personal** y las demás etiquetas se vuelven a ocultar.

### <a name="to-remove-the-classification-completely"></a>Para quitar la clasificación completamente

1. En la barra de Information Protection, haga clic en el icono **Editar etiqueta**. En lugar de elegir una de las etiquetas, haga clic en el icono **Eliminar etiqueta**:
    
    ![Tutorial de Azure Information Protection: eliminar icono](./media/delete-icon-from-personalv2.png)
    
2. Esta vez, cuando se le solicite, escriba "Este documento no necesita clasificación" y haga clic en **Confirmar**.  
    
    Ve que el valor **Confidencialidad** muestra **No establecido**, que es lo que los usuarios ven inicialmente para los nuevos documentos si no establece una etiqueta predeterminada como configuración de directiva.

### <a name="to-see-a-recommendation-prompt-for-labeling-and-automatic-protection"></a>Para ver un aviso de recomendación para el etiquetado y la protección automática

1. En el documento de Word, escriba un número de tarjeta de crédito válido, por ejemplo: **4242-4242-4242-4242**. 

2. Guarde el documento de forma local, con cualquier nombre de archivo. 

3. Ahora verá un aviso para aplicar la etiqueta que ha configurado para la protección cuando se detectan los números de tarjeta de crédito. Si no estamos de acuerdo con la recomendación, nuestra configuración de directiva nos permite rechazarla, seleccionando **Descartar**. Proporcionar una recomendación pero permitir que un usuario la invalide facilita reducir los falsos positivos cuando se usa la clasificación automática. Para este tutorial, haga clic en **Cambiar ahora**.

    ![Tutorial de Azure Information Protection: solicitud de recomendación](./media/change-nowv2.png)

    Además del documento que ahora muestra que se aplica nuestra etiqueta configurada (por ejemplo, **Confidencial \ Finanzas**), ve inmediatamente la marca de agua del nombre de su organización en la página, y también se aplica el pie de página **Clasificado como confidencial**. 

    El documento también está protegido con los permisos que ha especificado para esta etiqueta. Para confirmar que el documento está protegido, haga clic en la pestaña **Archivo** y vea la información de **Proteger documento**. Verá que el documento está protegido como **Confidencial \ Finanzas** y la descripción de la etiqueta. 
    
    Debido a la configuración de protección de la etiqueta, solo los empleados pueden abrir el documento y algunas acciones están restringidas para ellos. Por ejemplo, como no tienen permisos para imprimir, copiar y extraer contenido, no pueden imprimir el documento ni copiar datos de él. Estas restricciones ayudan a evitar la pérdida de datos. Como propietario del documento, puede imprimirlo y copiar contenido de él. Sin embargo, si envía el documento por correo electrónico a otro usuario de la organización, este no puede realizar estas acciones.

4. Ya puede cerrar este documento.

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no desea conservar los cambios realizados en este tutorial, haga lo siguiente:

1. Seleccione **Clasificaciones** > **Directivas** > **Global** para abrir la hoja **Policy: Global** (Directiva:global).

2. Devuelva las opciones de la configuración de directiva que anotó a sus valores originales y, a continuación, seleccione **Guardar**. 

3. Desde la opción de menú **Clasificaciones** > **Etiqueta**: En la hoja **Azure Information Protection: etiqueta**, seleccione el menú contextual (**...**) para la etiqueta**Finanzas** creada.

4. Seleccione **Eliminar esta etiqueta** y, si se le pide que confirme, seleccione **Aceptar**.

Reinicie Word para descargar estos cambios.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre cómo editar la directiva de Azure Information Protection, vea [Configuración de la directiva de Azure Information Protection](configure-policy.md).

Para obtener más información acerca de dónde se registra la actividad de etiquetado, consulte [Registro de uso del cliente de Azure Information Protection](./rms-client/client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client).

