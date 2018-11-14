---
title: 'Tutorial: Configuración de los parámetros de la directiva de Azure Information Protection para ayudar a clasificar documentos y correos electrónicos'
description: Un tutorial introductorio que le guiará en el proceso de configuración de las directivas de Azure Information Protection para ayudar a clasificar los documentos y los correos electrónicos de su organización.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/05/2018
ms.topic: tutorial
ms.service: information-protection
ms.openlocfilehash: ead65d9fef1b6c4f0087757e044caccee14805df
ms.sourcegitcommit: 80de8762953bdea2553c48b02259cd107d0c71dd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/05/2018
ms.locfileid: "51027077"
---
# <a name="tutorial-configure-azure-information-protection-policy-settings-that-work-together"></a>Tutorial: Configuración de los parámetros de la directiva de Azure Information Protection que funcionan en conjunto

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

En este tutorial, aprenderá a:
> [!div class="checklist"]
> * Configurar las opciones de directiva que funcionan conjuntamente
> * Ver la configuración en acción

En lugar de dejar que sean los usuarios quienes etiqueten manualmente sus documentos y correos electrónicos, puede usar la configuración de directiva para lo siguiente:

- Garantizar un nivel básico de clasificación del contenido nuevo y editado

- Formar a los usuarios acerca de las etiquetas y facilitarles la aplicación de la etiqueta correcta

Puede finalizar este tutorial en aproximadamente 15 minutos.

## <a name="prerequisites"></a>Requisitos previos 

Para completar este tutorial, necesita lo siguiente:

1. Una suscripción que incluya el plan 2 de Azure Information Protection.
    
    Si no tiene una suscripción que incluya este plan, puede crear una cuenta [gratuita](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) para su organización.

2. Ha agregado la hoja Azure Information Protection a Azure Portal y ha confirmado que el servicio de protección está activado.

    Si necesita ayuda con estas acciones, consulte este [Quickstart: Add Azure Information Protection to the Azure portal and view the policy](quickstart-viewpolicy.md) (Inicio rápido: Adición de Azure Information Protection a Azure Portal y visualización de la directiva).

3. El cliente de Azure Information Protection está instalado en su equipo. 
    
    Para instalar el cliente, vaya al [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) y descargue **AzInfoProtection.exe** en la página de Azure Information Protection.

4. Un equipo con Windows (como mínimo Windows 7 con Service Pack 1) y, en este equipo, haber iniciado sesión en aplicaciones de Office desde una de las siguientes categorías:
    
    - Office 365 con aplicaciones de Office 2016 (versión mínima 1805, compilación 9330.2078). Para usar esta opción, la cuenta debe tener asignada una licencia para Azure Rights Management. Esta licencia se incluye con la suscripción de Azure Information Protection.
    
    - Office 365 ProPlus con aplicaciones de 2016 o 2013 (instalación basada en Hacer clic y ejecutar o en Windows Installer).
    
    - Office Professional Plus 2016.
    
    - Office Professional Plus 2013 con Service Pack 1.
    
    - Office Professional Plus 2010 con Service Pack 2.

Para ver una lista completa de los requisitos previos para utilizar Azure Information Protection, consulte [Requisitos de Azure Information Protection](requirements.md).

Comencemos.

## <a name="edit-the-azure-information-protection-policy"></a>Edición de la directiva de Azure Information Protection

En lugar de dejar que sean los usuarios quienes etiqueten manualmente sus documentos y correos electrónicos, puede usar algunas de las opciones de configuración de la directiva para garantizar un nivel básico de clasificación. 

Mediante Azure Portal, editaremos la directiva global para cambiar la configuración de directiva para todos los usuarios.

1. Abra una nueva ventana del explorador e inicie sesión en [Azure Portal](https://portal.azure.com). Después, vaya a **Azure Information Protection**. 
    
    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. Seleccione **Clasificaciones** > **Directivas** > **Global** para abrir la hoja **Policy: Global** (Directiva:global). 

3. Busque la configuración de la directiva después de las etiquetas, en la sección **Configure settings to display and apply on Information Protection end users** (Configuración de valores para mostrar y aplicar en los usuarios finales de Information Protection). La configuración podría tener valores diferentes a los que se muestran aquí:
    
    ![Tutorial de Azure Information Protection: configuración predeterminada](./media/defaultsettings-aip.png)

4. Cambie la configuración para que coincida con el valor de la tabla siguiente. Tome nota de los valores que cambian por si quisiera volver a cambiarlos cuando haya terminado este tutorial. 

    |Setting|Valor|Información de|
    |-------|-----|-----|
    |**Select the default label** (Seleccionar la etiqueta predeterminada)|**General**|Si no tiene una etiqueta denominada **General**, seleccione otra etiqueta en la lista desplegable. Se aplicará automáticamente esta etiqueta a los documentos y correos electrónicos sin etiquetar como clasificación de base. Sin embargo, los usuarios pueden cambiar la etiqueta seleccionada por otra distinta.|
    |**All documents and emails must have a label** (Todos los documentos y correos electrónicos deben tener una etiqueta)|**Activado**|Esta opción se conoce a menudo como "etiquetado obligatorio" porque evita que los usuarios guarden documentos o envíen correos electrónicos que estén sin etiquetar. Junto con la etiqueta predeterminada, los documentos y correos electrónicos tendrán la etiqueta predeterminada que establezca o una etiqueta que elija.
    |**Para los mensajes de correo electrónico con datos adjuntos, aplicar una etiqueta que coincida con la clasificación más alta de los datos adjuntos**|**Recomendado**|Esta opción pide a los usuarios que seleccionen una etiqueta de clasificación superior para sus mensajes de correo electrónico cuando adjuntan documentos que tienen una clasificación más alta que la etiqueta predeterminada seleccionada.
    |**Mostrar la barra de Information Protection en las aplicaciones de Office**|**Activado**|El hecho de mostrar la barra de Information Protection facilita a los usuarios el proceso de ver y cambiar la etiqueta predeterminada.
    
    La configuración debería ser ahora similar a la siguiente:
    
    ![Tutorial de Azure Information Protection: configuración predeterminada cambiada](./media/defaultsettings-aip-changed.png)

5. Seleccione **Guardar** en la hoja **Policy: Global** (Directiva: Global) y, si se le pide que confirme la acción, seleccione **Aceptar**. 

## <a name="see-your-policy-settings-in-action"></a>Visualización de la configuración de directiva en acción 

Para este tutorial, vamos a usar Word y Outlook para ver los cambios de la directiva en acción. Si estas aplicaciones ya estaban cargadas antes de cambiar la configuración de directiva, debe reiniciarlas para descargar los cambios.

### <a name="default-label-and-the-information-protection-bar"></a>Etiqueta predeterminada y barra de Information Protection

Abra un nuevo documento en Word. Verá que el documento se ha etiquetado automáticamente como **General** en lugar de esperar a que sean los usuarios quienes seleccionen una etiqueta. 

Una vez que la barra de Information Protection aparece y muestra las etiquetas disponibles, para los usuarios es fácil ver la etiqueta seleccionada actualmente y cambiarla en caso de que no sea adecuada:

![Tutorial de Azure Information Protection: nuevo documento con la etiqueta predeterminada](./media/defaultlabel-word.png)

En lugar de cambiar la etiqueta, cierre la barra de Information Protection para ver cómo es la experiencia de no mostrar la barra:

![Tutorial de Azure Information Protection: nuevo documento con la etiqueta predeterminada](./media/infoprotect-bar-close.png)

La etiqueta **General** sigue seleccionada, pero es mucho menos evidente. También resulta menos intuitivo el hecho de seleccionar una etiqueta diferente. Para ello, los usuarios deben seleccionar el botón **Proteger**:

![Tutorial de Azure Information Protection: botón Proteger seleccionado](./media/infoprotect-protectbutton-pulldown.png)

Ahora, en el menú desplegable, verá que la etiqueta **General** está seleccionada porque presenta una marca de verificación a su lado. Para cambiar la etiqueta seleccionada actualmente, los usuarios pueden seleccionar otra en la lista. Si los usuarios no están familiarizados con el etiquetado, es posible que no recuerden la activación del botón **Proteger** botón cada vez. También es posible que no sepan que se puede seleccionar otra etiqueta.

Para mostrar de nuevo la barra de Information Protection, seleccione **Mostrar barra** en el menú desplegable.

> [!TIP]
> Puede seleccionar otra etiqueta predeterminada para Outlook por medio de la [configuración de cliente avanzada](./rms-client/client-admin-guide-customizations.md#set-a-different-default-label-for-outlook).

### <a name="mandatory-labeling"></a>Etiquetado obligatorio

Puede cambiar la etiqueta **General** seleccionada actualmente a una etiqueta diferente, pero no puede quitarla. Dado que hemos cambiado el valor de **All documents and emails must have a label** (Todos los documentos y correos electrónicos deben tener una etiqueta) a **Activado**, el icono **Eliminar etiqueta** no está disponible en la barra de Information Protection. 

Si no hubiésemos cambiado ese valor, este icono aparecería en la barra de Information Protection:

![Tutorial de Azure Information Protection: botón Proteger seleccionado](./media/infoprotect-deletelabel-icon.png)

Junto con la etiqueta predeterminada, el etiquetado obligatorio garantiza que los documentos (y correos electrónicos) nuevos y editados tienen la clasificación de base que elija. 

Si no se hubiera configurado una etiqueta predeterminada con el parámetro de etiquetado obligatorio, los usuarios siempre tendrían que seleccionar una etiqueta al guardar un documento sin etiqueta o enviar un correo electrónico sin etiqueta. Para muchos usuarios, estas solicitudes continuas pueden resultar frustrantes, y además generan un etiquetado menos preciso. El hecho de que se les pida que seleccionen una etiqueta cuando han terminado de trabajar en un documento o correo electrónico supone una interrupción en el proceso de trabajo, así que existe la tentación se seleccionar una etiqueta cualquiera para poder avanzar.

### <a name="recommendations-for-emails-with-attachments"></a>Recomendaciones para correos electrónicos con datos adjuntos

Para el documento de Word abierto, elija una etiqueta con una clasificación más alta que **General**. Por ejemplo, una de las subetiquetas del grupo **Confidencial**, tales como **Confidencial \ Cualquiera (sin protección)**. Guarde el documento de forma local y póngale cualquier nombre. 

Inicie Outlook y cree un nuevo mensaje de correo electrónico. Tal como hemos visto con Word, el nuevo mensaje de correo electrónico se etiqueta automáticamente como **General** y se muestra la barra de Information Protection.

Agregue el documento de Word que acaba de etiquetar como adjunto al mensaje de correo electrónico. Verá una solicitud para que cambie la etiqueta del correo electrónico a la etiqueta **Confidencial** que coincide con el adjunto de Word. Puede aceptar la recomendación o descartarla.

![Tutorial de Information Protection Azure: solicitud para cambiar la etiqueta del correo electrónico para que coincida con el adjunto etiquetado](./media/infoprotect-matchemail-label.png)

Si hace clic en **Descartar**, no se aplica la nueva etiqueta, pero verá que el correo electrónico sigue etiquetado con la etiqueta predeterminada que hemos configurado: **General**. Las etiquetas disponibles todavía están visibles para seleccionarlas como alternativa.

Si selecciona **Cambiar ahora**, el correo electrónico se vuelve a etiquetar con la subetiqueta **Confidencial**. Sin embargo, los usuarios todavía pueden cambiar la etiqueta antes de enviar el correo electrónico mediante la selección de Editar etiqueta:

![Tutorial de Information Protection Azure: solicitud para cambiar la etiqueta del correo electrónico para que coincida con el adjunto etiquetado](./media/infoprotect-editlabel-icon.png)

La barra de Information Protection se muestra entonces de nuevo para que los usuarios seleccionen una etiqueta alternativa.

Dado que la etiqueta se activa antes de enviar el correo electrónico, no hay necesidad de enviar realmente el correo electrónico para ver cómo funciona esta configuración de directiva. Puede cerrar el correo electrónico sin enviarlo ni guardarlo.

Sin embargo, puede intentar repetir este ejercicio adjuntando también otro documento que tenga una clasificación más alta (una subetiqueta de grupo **Extremadamente confidencial**). A continuación, podrá ver cómo cambia la solicitud para aplicar la etiqueta de clasificación superior.

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no desea conservar los cambios realizados en este tutorial, haga lo siguiente:

1. Seleccione **Clasificaciones** > **Directivas** > **Global** para abrir la hoja **Policy: Global** (Directiva:global).

2. Devuelva las opciones de la configuración de directiva que anotó a sus valores originales y, a continuación, seleccione **Guardar**.

Reinicie las aplicaciones de Word y Outlook para descargar estos cambios.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre la edición de los parámetros de directiva de Azure Information Protection, vea [Configuración directivas para Azure Information Protection](configure-policy-settings.md).

La configuración de directiva que hemos cambiado ha ayudado a garantizar un nivel básico de clasificación, así como a animar a los usuarios a seleccionar una etiqueta adecuada. El siguiente paso es aumentar esta estrategia mediante la inspección del contenido de documentos y correos electrónicos y, a continuación, la recomendación o aplicación automática de una etiqueta adecuada. Para ello, puede configurar condiciones en las etiquetas. Para obtener más información, consulte [Configuración de las condiciones para la clasificación automática y recomendada en Azure Information Protection](configure-policy-classification.md).
