---
title: "Clasificación y protección mediante Azure Information Protection"
description: "Instrucciones de cómo clasificar y proteger sus documentos y correos electrónicos."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/06/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 75268245-6f14-4218-b904-202f63fb3ce6
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 960fe1abf2fa4f5b8976f190454d31849736298a
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2017
---
<a id="classify-and-protect-a-file-or-email-by-using-azure-information-protection" class="xliff"></a>

# Clasificación y protección de archivos o correos electrónicos mediante Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8 y Windows 7 con SP1*

La manera más fácil de clasificar y proteger sus documentos y correos electrónicos es crearlos y editarlos con las aplicaciones de escritorio de Office: **Word**, **Excel**, **PowerPoint**, **Outlook**. 

Sin embargo, también puede clasificar y proteger archivos mediante el **Explorador de archivos**, que admite tipos de archivo adicionales y es una forma cómoda de clasificar y proteger varios archivos a la vez. Este método admite la protección de documentos de Office, archivos PDF, archivos de texto e imagen y otros muchos archivos. 

<a id="safely-share-a-file-with-people-outside-your-organization" class="xliff"></a>

### Uso compartido de un archivo de manera segura con personas ajenas a la organización

Los archivos protegidos se pueden compartir con otros de forma segura. Por ejemplo, puede adjuntar el archivo a un correo electrónico o enviar una invitación desde el sitio de SharePoint.

Si regularmente comparte archivos con personas ajenas a la organización, puede que el administrador haya configurado una etiqueta que establece la protección de tal forma que dichas personas puedan leerla. Como alternativa, puede usar la [aplicación de Office](#set-custom-permissions-for-a-document) o el [Explorador de archivos](#using-file-explorer-to-classify-and-protect-files) para establecer permisos personalizados para un archivo antes de compartirlo. 

Si establece sus propios permisos personalizados y el archivo ya está protegido para uso interno, primero haga una copia de dicho archivo para conservar los permisos originales. Después, utilice la copia para establecer los permisos personalizados.  

Si el archivo está protegido con los permisos personalizados, use el mecanismo de uso compartido estándar para compartir el archivo. Si es la primera vez que estas personas con las que comparte el archivo han recibido un archivo protegido, es posible que necesiten instrucciones para verlo. Para estas personas, puede copiar y pegar el siguiente mensaje: **Este archivo está protegido con Microsoft Azure Information Protection. Para el primer uso, vea estas [instrucciones](https://aka.ms/rms-signup).**


<a id="using-office-apps-to-classify-and-protect-your-documents-and-emails" class="xliff"></a>

## Uso de aplicaciones de Office para clasificar y proteger los documentos y correos electrónicos

Use la barra de Azure Information Protection y seleccione una de las etiquetas configuradas para usted. 

Por ejemplo, en la siguiente imagen se muestra que el documento aún no se ha etiquetado, porque en **Confidencialidad** aparece **Sin establecer**. Para establecer una etiqueta, como "Interna", haga clic en **Interno**. Si no está seguro de qué etiqueta aplicar en el documento o correo electrónico actual, utilice la información sobre herramientas de etiquetas para obtener más detalles sobre cada etiqueta y cuándo aplicarla.

![Ejemplo de barra de Azure Information Protection](../media/info-protect-bar-not-set-callout.png)

Si ya se ha aplicado la etiqueta al documento y desea cambiarla, puede seleccionar una etiqueta diferente. Si las etiquetas no se muestran en la barra, primero haga clic en el icono **Editar etiqueta**, junto al valor de la etiqueta actual.

Además de seleccionar manualmente las etiquetas, estas también pueden aplicarse como sigue:

- El administrador ha configurado una etiqueta predeterminada, que puede mantener o cambiar.

- El administrador ha configurado avisos recomendados para seleccionar una etiqueta específica cuando se detecta información confidencial. Puede aceptar la recomendación (y se aplica la etiqueta), o rechazarla (no se aplica la etiqueta recomendada).

<a id="exceptions-for-the-azure-information-protection-bar" class="xliff"></a>

### Excepciones de la barra de Azure Information Protection 

<a id="dont-see-this-information-protection-bar-in-your-office-apps" class="xliff"></a>

##### ¿No aparece la barra de Information Protection en las aplicaciones de Office?

- Puede que no tenga [instalado](install-client-app.md) el cliente de Azure Information Protection, o que este se encuentre en ejecución en el [modo de solo protección](client-protection-only-mode.md).
 
<a id="is-the-label-that-you-expect-to-see-not-displayed-on-the-bar" class="xliff"></a>

##### ¿La etiqueta que esperaba ver no aparece en la barra? 

- Si el administrador ha configurado recientemente una etiqueta nueva, intente cerrar todas las instancias de la aplicación de Office y vuelva a abrirla. Esta acción comprueba si las etiquetas han experimentado algún cambio.

- Si la etiqueta que falta aplica protección, es posible que tenga una edición de Office que no admite la aplicación de protección de Rights Management. Para verificarlo, haga clic en **Proteger** > **Ayuda y comentarios** y compruebe si en la sección **Estado del cliente** aparece el mensaje **Este cliente no tiene licencia de Office Professional Plus**. 

- La etiqueta debe estar en una directiva de ámbito que no incluye su cuenta. Póngase en contacto con el Servicio de asistencia o con el administrador.

<a id="set-custom-permissions-for-a-document" class="xliff"></a>

### Establecimiento de permisos personalizados para un documento

Puede especificar su propia configuración de protección para documentos en lugar de usar la configuración de protección que el administrador podría haber incluido con la etiqueta seleccionada.

1. En la pestaña **Inicio**, en el grupo **Protección**, haga clic en **Proteger** > **Permisos personalizados**:

    ![Opción Permisisons personalizados](../media/custom-permissions-callout.png)
    
    Tenga en cuenta que cualquier permiso personalizado que especifique reemplaza, en lugar de complementar, la configuración de protección que el administrador podría haber definido para la etiqueta elegida.  

2. En el cuadro de diálogo **Microsoft Azure Information Protection**, especifique lo siguiente:

    - **Proteger con permisos personalizados**: Asegúrese de que esta opción está seleccionada para que pueda especificar y aplicar los permisos personalizados. Desactive esta opción para quitar todos los permisos personalizados.
    
    - **Seleccionar permisos**: Si desea proteger el archivo para que solo usted pueda acceder a él, seleccione **Solo para mí**. De lo contrario, seleccione el nivel de acceso que desea que tengan las personas.

    - **Seleccionar usuarios, grupos u organizaciones**: Especifique las personas que deben tener los permisos seleccionados para los archivos. Escriba sus direcciones de correo electrónico completas, una dirección de correo electrónico de grupo o un nombre de dominio de la organización para todos los usuarios de esa organización. Tenga en cuenta que actualmente no se admiten direcciones de correo electrónico personales.
        
    - **Expire access** (Expirar acceso): seleccione esta opción solo para archivos dependientes del tiempo, de modo que las personas que ha especificado no puedan abrir los archivos seleccionados después de una fecha determinada. Usted todavía podrá abrir el archivo original, pero después de la medianoche (de su zona horaria actual) del día que establezca. Las personas que especifique no podrán abrir el archivo.

5. Haga clic en **Aplicar** y espere a que aparezca el mensaje **Se han aplicado permisos personalizados**. A continuación, haga clic en **Cerrar**.


<a id="keyboard-shortcuts-for-the-azure-information-protection-bar" class="xliff"></a>

### Métodos abreviados de teclado para la barra Azure Information Protection

Para acceder a la barra Azure Information Protection mediante el uso de métodos abreviados de teclado, utilice la combinación de teclas siguiente:

- Presione **Ctrl** + **Mayús** + **~** 

A continuación, utilice la tecla de tabulación para seleccionar las etiquetas y otros controles en la barra (el icono **Ocultar etiquetas** y el icono **Eliminar etiqueta**) y la tecla ENTRAR para seleccionarlos.

<a id="using-file-explorer-to-classify-and-protect-files" class="xliff"></a>

## Uso del Explorador de archivos para clasificar y proteger archivos

Con el Explorador de archivos, puede clasificar y proteger rápidamente un solo archivo, varios archivos o una carpeta. 

Cuando seleccione una carpeta, todos los archivos que contiene y sus subcarpetas se seleccionan automáticamente para las opciones de clasificación y protección establecidas. Sin embargo, los nuevos archivos que se crean en esa carpeta o en las subcarpetas no se configuran automáticamente con esas opciones.

Cuando utilice el Explorador de archivos para clasificar y proteger los archivos, si una o varias de las etiquetas aparecen atenuadas, significa que los archivos que ha seleccionado no admiten la clasificación. Para estos archivos, solo puede seleccionar una etiqueta si el administrador la ha configurado para aplicar protección. O bien, puede especificar su propia configuración de protección. 

Algunos archivos se excluyen automáticamente de la clasificación y la protección, porque cambiarlos podría detener la ejecución del equipo. Aunque puede seleccionar estos archivos, se omiten como un archivo o carpeta excluidos. Se incluyen como ejemplo los archivos ejecutables y la carpeta Windows.

La guía para administradores contiene una lista completa de los tipos de archivos admitidos y los archivos y carpetas que se excluyen automáticamente: [Tipos de archivos compatibles con el cliente de Azure Information Protection](client-admin-guide-file-types.md).


<a id="to-classify-and-protect-a-file-by-using-file-explorer" class="xliff"></a>

### Para clasificar y proteger un archivo mediante el Explorador de archivos

1. En el Explorador de archivos, seleccione un archivo, varios archivos o una carpeta. Haga clic con el botón derecho y seleccione **Clasificar y proteger**. Por ejemplo:
    
    ![Explorador de archivos Menú contextual Clasificar y proteger con Azure Information Protection](../media/right-click-classify-protect-folder.png)

2. En el cuadro de diálogo **Classify and protect - Azure Information Protection** (Clasificar y proteger: Azure Information Protection), use las etiquetas del mismo modo que en una aplicación de Office, que establece la clasificación y protección definidas por el administrador. 

    - Si no se puede seleccionar ninguna etiqueta (aparecen atenuadas): el archivo seleccionado no admite la clasificación, pero puede protegerlo con permisos personalizados (paso 3). Por ejemplo:

    ![Ninguna etiqueta disponible en el cuadro de diálogo Clasificar y proteger: Azure Information Protection**](../media/info-protect-dialog-labels-dimmed.png)
    
    - Si no ve las etiquetas en este cuadro de diálogo, pero sí la opción para la **protección predefinida por la empresa**: el cliente se ejecuta en [modo de solo protección](client-protection-only-mode.md). Seleccione una plantilla para aplicar la protección que el administrador ha configurado, o bien seleccione **Permisos personalizados** para especificar su propia configuración de protección y vaya al paso 4.
    
    ![Ninguna etiqueta en el cuadro de diálogo Clasificar y proteger: Azure Information Protection**](../media/info-protect-dialog-labels-protection-only.png)
    
3. Si desea especificar su propia configuración de protección en lugar de usar la configuración de protección que el administrador podría haber incluido con la etiqueta seleccionada, seleccione **Protect with custom permissions** (Proteger con permisos personalizados).
    
    Cualquier permiso personalizado que especifique reemplaza, en lugar de complementar, la configuración de protección que el administrador podría haber definido para la etiqueta elegida.  

4. Si ha seleccionado la opción de permisos personalizados, especifique ahora lo siguiente:

    - **Seleccionar permisos**: seleccione el nivel de acceso que quiere que tengan las personas al proteger los archivos seleccionados.
    
    - **Seleccionar usuarios**: especifique las personas que deben tener los permisos seleccionados para los archivos. Es posible que pueda seleccionarlas en la libreta de direcciones (por ejemplo, personas de su organización y contactos de otras organizaciones). En el caso de otras personas, escriba sus direcciones de correo electrónico completas, una dirección de correo electrónico de grupo o un nombre de dominio de la organización para todos los usuarios de esa organización. Tenga en cuenta que actualmente no se admiten direcciones de correo electrónico personales.
        
    - **Expire access** (Expirar acceso): seleccione esta opción solo para archivos dependientes del tiempo, de modo que las personas que ha especificado no puedan abrir los archivos seleccionados después de una fecha determinada. Usted todavía podrá abrir el archivo original, pero después de la medianoche (de su zona horaria actual) del día que establezca. Las personas que especifique no podrán abrir el archivo.
    
    Tenga en cuenta que si esta configuración se estableció previamente mediante permisos personalizados desde una aplicación de Office 2010, la fecha de expiración especificada no aparece en este cuadro de diálogo, pero de todos modos está establecida. Este problema de visualización solo se genera cuando la fecha de expiración se configuró en Office 2010.

5. Haga clic en **Aplicar** y espere a que aparezca el mensaje **Trabajo finalizado** para ver los resultados. A continuación, haga clic en **Cerrar**.

Los archivos seleccionados están ahora clasificados y protegidos, de acuerdo con sus selecciones. En algunos casos (al agregar protección cambia la extensión de nombre de archivo), el archivo original del Explorador de archivos se reemplaza por un nuevo archivo que tiene el icono de bloqueo de Azure Information Protection. Por ejemplo:

![Archivo protegido con icono de bloqueo para Azure Information Protection](../media/Pfile.png)

Si cambia de opinión sobre la clasificación y la protección o más tarde necesita modificar la configuración, solo tiene que repetir este proceso con su nueva configuración.

La clasificación y la protección que especificó permanece con el archivo, incluso si lo envía por correo electrónico o lo guarda en otra ubicación. Si ha protegido el archivo, puede realizar un seguimiento de cómo las personas lo usan y, si es necesario, revocar el acceso a él. Para más información, consulte [Seguimiento y revocación de los documentos protegidos al usar Azure Information Protection](client-track-revoke.md). 


<a id="other-instructions" class="xliff"></a>

## Otras instrucciones
Puede encontrar más instrucciones sobre procedimientos en la guía del usuario de Azure Information Protection:

-   [¿Qué desea hacer?](client-user-guide.md#what-do-you-want-to-do)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
