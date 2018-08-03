---
title: Clasificación y protección de archivos y correos electrónicos mediante Azure Information Protection
description: Instrucciones de cómo clasificar y proteger sus documentos y correos electrónicos.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/12/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 75268245-6f14-4218-b904-202f63fb3ce6
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: baf3edc435672c8339c15ea74f5b5e14d6951f96
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39371550"
---
# <a name="user-guide-classify-and-protect-a-file-or-email-by-using-azure-information-protection"></a>Guía del usuario: Clasificación y protección de archivos y correos electrónicos mediante Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8 y Windows 7 con SP1*

> [!NOTE]
> Siga estas instrucciones para clasificar y proteger los documentos y correos electrónicos. Si solo necesita clasificar y no proteger los documentos y correos electrónicos, consulte las [instrucciones sobre solo clasificación](client-classify.md). Si no está seguro de qué conjunto de instrucciones debe usar, póngase en contacto con el administrador o el departamento de soporte técnico.

La manera más fácil de clasificar y proteger sus documentos y correos electrónicos es crearlos y editarlos con las aplicaciones de escritorio de Office: **Word**, **Excel**, **PowerPoint**, **Outlook**. 

Aun así, también puede clasificar y proteger archivos mediante el **Explorador de archivos**. Este método es compatible con tipos de archivo adicionales y es una manera cómoda de clasificar y proteger varios archivos a la vez. Este método admite la protección de documentos de Office, archivos PDF, archivos de texto e imagen y otros muchos archivos. 

Si la etiqueta aplica protección a un documento, no es adecuado guardar el documento protegido en SharePoint o OneDrive. Estas ubicaciones no admiten lo siguiente para los archivos protegidos: coautoría, Office Online, búsqueda, vista previa de documentos, miniaturas y exhibición de documentos electrónicos. 

### <a name="safely-share-a-file-with-people-outside-your-organization"></a>Uso compartido de un archivo de manera segura con personas ajenas a la organización

Los archivos protegidos se pueden compartir con otros de forma segura. Por ejemplo, se adjunta un documento protegido a un correo electrónico.

Antes de compartir archivos con personas fuera de su organización, póngase en contacto con el departamento de soporte técnico o el administrador sobre cómo proteger los archivos para los usuarios externos.

Por ejemplo, si su organización se comunica regularmente con personas de otra organización, el administrador podría haber configurado las etiquetas que establecen la protección de modo que estas personas puedan leer y usar documentos protegidos. Luego, seleccione estas etiquetas para clasificar y proteger los documentos que se van a compartir.

O bien, si los usuarios externos tienen [cuentas de negocio a negocio (B2B)](/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b) creadas para ellos, puede usar la [aplicación de Office para establecer permisos personalizados](#set-custom-permissions-for-a-document) o el [Explorador de archivos para establecer permisos personalizados](#using-file-explorer-to-classify-and-protect-files) para un documento antes de compartirlo. Si establece sus propios permisos personalizados y el documento ya está protegido para uso interno, primero haga una copia de dicho archivo para conservar los permisos originales. Después, utilice la copia para establecer los permisos personalizados.


## <a name="using-office-apps-to-classify-and-protect-your-documents-and-emails"></a>Uso de aplicaciones de Office para clasificar y proteger los documentos y correos electrónicos

Use la barra de Azure Information Protection o el botón **Proteger** de la cinta para seleccionar una de las etiquetas que se han configurado para usted. 

Por ejemplo, en la imagen siguiente se muestra que el documento aún no se ha etiquetado, porque en **Confidencialidad** aparece **Sin establecer** en la barra de Azure Information Protection. Para establecer una etiqueta, como "General", haga clic en **General**. Si no está seguro de qué etiqueta aplicar en el documento o correo electrónico actual, utilice la información sobre herramientas de etiquetas para obtener más detalles sobre cada etiqueta y cuándo aplicarla. 

![Ejemplo de barra de Azure Information Protection](../media/info-protect-bar-not-set-callout.png)

Si ya se ha aplicado la etiqueta al documento y desea cambiarla, puede seleccionar una etiqueta diferente. Si las etiquetas no se muestran en la barra, primero haga clic en el icono **Editar etiqueta**, junto al valor de la etiqueta actual.

Además de seleccionar manualmente las etiquetas, estas también pueden aplicarse como sigue:

- El administrador ha configurado una etiqueta predeterminada, que puede mantener o cambiar.

- El administrador ha configurado avisos recomendados para seleccionar una etiqueta específica cuando se detecta información confidencial. Puede aceptar la recomendación (y se aplica la etiqueta), o rechazarla (no se aplica la etiqueta recomendada).

### <a name="exceptions-for-the-azure-information-protection-bar"></a>Excepciones de la barra de Azure Information Protection 

##### <a name="dont-see-this-information-protection-bar-in-your-office-apps"></a>¿No aparece la barra de Information Protection en las aplicaciones de Office?

Posibles razones:

- El cliente de Azure Information Protection no está [instalado](install-client-app.md).

- Tiene instalado el cliente, pero el administrador ha establecido una configuración que no muestra la barra. En su lugar, seleccione las etiquetas desde el botón **Proteger**, en la pestaña **Archivo** de la cinta de Office. 

- El cliente se está ejecutando en [modo de solo protección](client-protection-only-mode.md).
 
##### <a name="is-the-label-that-you-expect-to-see-not-displayed"></a>¿No se muestra la etiqueta que esperaba ver? 

Posibles razones:

- Si el administrador ha configurado recientemente una etiqueta nueva, intente cerrar todas las instancias de la aplicación de Office y vuelva a abrirla. Esta acción comprueba si las etiquetas han experimentado algún cambio.

- Si la etiqueta que falta aplica protección, es posible que tenga una edición de Office que no admite la aplicación de protección de Rights Management. Para comprobarlo, haga clic en **Proteger** > **Ayuda y comentarios**. En el cuadro de diálogo, compruebe si en la sección **Estado del cliente** aparece el mensaje **Este cliente no tiene licencia de Office Profesional Plus**. 

- La etiqueta debe estar en una directiva de ámbito que no incluye su cuenta. Póngase en contacto con el Servicio de asistencia o con el administrador.

### <a name="set-custom-permissions-for-a-document"></a>Establecimiento de permisos personalizados para un documento

Si el administrador lo permite, puede especificar su propia configuración de protección para los documentos en lugar de usar la configuración de protección que es posible que el administrador haya incluido con la etiqueta seleccionada. Esta opción es específica de documentos y no está disponible con Outlook.

1. En la pestaña **Inicio**, en el grupo **Protección**, haga clic en **Proteger** > **Permisos personalizados**:

    ![Opción Permisisons personalizados](../media/custom-permissions-callout.png)
    
    Si no ve **Permisos personalizados**, significa que el administrador no permite usar esta opción.
    
    Tenga en cuenta que cualquier permiso personalizado que especifique reemplaza, en lugar de complementar, la configuración de protección que el administrador podría haber definido para la etiqueta elegida.  

2. En el cuadro de diálogo **Microsoft Azure Information Protection**, especifique lo siguiente:

    - **Proteger con permisos personalizados**: Asegúrese de que esta opción está seleccionada para que pueda especificar y aplicar los permisos personalizados. Desactive esta opción para quitar todos los permisos personalizados.
    
    - **Seleccionar permisos**: Si desea proteger el archivo para que solo usted pueda acceder a él, seleccione **Solo para mí**. De lo contrario, seleccione el nivel de acceso que desea que tengan las personas.
    
    - **Seleccionar usuarios, grupos u organizaciones**: Especifique las personas que deben tener los permisos seleccionados para los archivos. Escriba sus direcciones de correo electrónico completas, una dirección de correo electrónico de grupo o un nombre de dominio de la organización para todos los usuarios de esa organización. 
        
        También puede usar el icono de la libreta de direcciones para seleccionar usuarios o grupos de la libreta de direcciones de Outlook.
    
    - **Expire access** (Acceso con expiración): seleccione esta opción solo para archivos sujetos a limitación temporal, de modo que las personas que ha especificado no puedan abrir los archivos seleccionados después de una fecha especificada. Aún podrá abrir el archivo original, pero el día seleccionado después de medianoche (su zona horaria actual), las personas que haya especificado no podrán abrir el archivo.

5. Haga clic en **Aplicar** y espere a que aparezca el mensaje **Se han aplicado permisos personalizados**. A continuación, haga clic en **Cerrar**.

### <a name="safely-sharing-by-email"></a>Uso compartido seguro por correo electrónico

Cuando comparte documentos de Office por correo electrónico, puede adjuntar el documento a un correo protegido, de modo que el documento queda protegido automáticamente con las mismas restricciones que se aplican al correo. 

Para hacerlo, le recomendamos que proteja primero el documento y luego lo adjunte al correo. Proteja también el correo si el mensaje de correo contiene información confidencial. Dos ventajas de proteger el documento antes de adjuntarlo a un correo:

- Puede realizar un seguimiento y, si es necesario, revocar el documento después de haberlo enviado por correo.

- Puede aplicar permisos diferentes al documento y al mensaje de correo.

## <a name="using-file-explorer-to-classify-and-protect-files"></a>Uso del Explorador de archivos para clasificar y proteger archivos

Con el Explorador de archivos, puede clasificar y proteger rápidamente un solo archivo, varios archivos o una carpeta. 

Cuando seleccione una carpeta, todos los archivos que contiene y sus subcarpetas se seleccionan automáticamente para las opciones de clasificación y protección establecidas. Sin embargo, los nuevos archivos que se crean en esa carpeta o en las subcarpetas no se configuran automáticamente con esas opciones.

Cuando utilice el Explorador de archivos para clasificar y proteger los archivos, si una o varias de las etiquetas aparecen atenuadas, significa que los archivos que ha seleccionado no admiten la clasificación. Para estos archivos, solo puede seleccionar una etiqueta si el administrador la ha configurado para aplicar protección. O bien, puede especificar su propia configuración de protección. 

Algunos archivos se excluyen automáticamente de la clasificación y la protección, porque cambiarlos podría detener la ejecución del equipo. Aunque puede seleccionar estos archivos, se omiten como un archivo o carpeta excluidos. Se incluyen como ejemplo los archivos ejecutables y la carpeta Windows.

La guía para administradores contiene una lista completa de los tipos de archivos admitidos y los archivos y carpetas que se excluyen automáticamente: [Tipos de archivos compatibles con el cliente de Azure Information Protection](client-admin-guide-file-types.md).


### <a name="to-classify-and-protect-a-file-by-using-file-explorer"></a>Para clasificar y proteger un archivo mediante el Explorador de archivos

1. En el Explorador de archivos, seleccione un archivo, varios archivos o una carpeta. Haga clic con el botón derecho y seleccione **Clasificar y proteger**. Por ejemplo:
    
    ![Explorador de archivos Menú contextual Clasificar y proteger con Azure Information Protection](../media/right-click-classify-protect-folder.png)

2. En el cuadro de diálogo **Classify and protect - Azure Information Protection** (Clasificar y proteger: Azure Information Protection), use las etiquetas del mismo modo que en una aplicación de Office, que establece la clasificación y protección definidas por el administrador. 

    - Si no se puede seleccionar ninguna etiqueta (aparecen atenuadas): el archivo seleccionado no admite la clasificación, pero puede protegerlo con permisos personalizados (paso 3). Por ejemplo:

    ![Ninguna etiqueta disponible en el cuadro de diálogo Clasificar y proteger: Azure Information Protection**](../media/info-protect-dialog-labels-dimmed.png)
    
    - Si no ve las etiquetas en este cuadro de diálogo, pero sí la opción para la **protección predefinida por la empresa**: el cliente se ejecuta en [modo de solo protección](client-protection-only-mode.md). Seleccione una plantilla para aplicar la protección que el administrador ha configurado, o bien seleccione **Permisos personalizados** para especificar su propia configuración de protección y vaya al paso 4.
    
    ![Ninguna etiqueta en el cuadro de diálogo Clasificar y proteger: Azure Information Protection**](../media/info-protect-dialog-labels-protection-only.png)
    
3. Si el administrador lo permite, puede especificar su propia configuración de protección en lugar de usar la configuración de protección que es posible que el administrador haya incluido con la etiqueta seleccionada. Para ello, seleccione **Proteger con permisos personalizados**.
    
    Si no ve **Proteger con permisos personalizados**, significa que el administrador no permite usar esta opción.
    
    Cualquier permiso personalizado que especifique reemplaza, en lugar de complementar, la configuración de protección que el administrador podría haber definido para la etiqueta elegida.  

4. Si ha seleccionado la opción de permisos personalizados, especifique ahora lo siguiente:

    - **Seleccionar permisos**: seleccione el nivel de acceso que quiere que tengan las personas al proteger los archivos seleccionados.
    
    - **Seleccionar usuarios, grupos u organizaciones**: Especifique las personas que deben tener los permisos seleccionados para los archivos. Escriba sus direcciones de correo electrónico completas, una dirección de correo electrónico de grupo o un nombre de dominio de la organización para todos los usuarios de esa organización. 
    
    Como alternativa, puede usar el icono de la libreta de direcciones para seleccionar usuarios o grupos de la libreta de direcciones de Outlook.
        
    - **Expire access** (Expirar acceso): seleccione esta opción solo para archivos dependientes del tiempo, de modo que las personas que ha especificado no puedan abrir los archivos seleccionados después de una fecha determinada. Usted todavía podrá abrir el archivo original, pero después de la medianoche (de su zona horaria actual) del día que establezca. Las personas que especifique no podrán abrir el archivo.
    
    Tenga en cuenta que si esta configuración se estableció previamente mediante permisos personalizados desde una aplicación de Office 2010, la fecha de expiración especificada no aparece en este cuadro de diálogo, pero de todos modos está establecida. Este problema de visualización solo se genera cuando la fecha de expiración se configuró en Office 2010.

5. Haga clic en **Aplicar** y espere a que aparezca el mensaje **Trabajo finalizado** para ver los resultados. A continuación, haga clic en **Cerrar**.

Los archivos seleccionados están ahora clasificados y protegidos, de acuerdo con sus selecciones. En algunos casos (al agregar protección cambia la extensión de nombre de archivo), el archivo original del Explorador de archivos se reemplaza por un nuevo archivo que tiene el icono de bloqueo de Azure Information Protection. Por ejemplo:

![Archivo protegido con icono de bloqueo para Azure Information Protection](../media/Pfile.png)

Si cambia de opinión sobre la clasificación y la protección o más tarde necesita modificar la configuración, solo tiene que repetir este proceso con su nueva configuración.

La clasificación y la protección que especificó permanece con el archivo, incluso si lo envía por correo electrónico o lo guarda en otra ubicación. Si ha protegido el archivo, puede realizar un seguimiento de cómo las personas lo usan y, si es necesario, revocar el acceso a él. Para más información, consulte [Seguimiento y revocación de los documentos protegidos al usar Azure Information Protection](client-track-revoke.md). 


## <a name="other-instructions"></a>Otras instrucciones
Puede encontrar más instrucciones sobre procedimientos en la guía del usuario de Azure Information Protection:

-   [¿Qué desea hacer?](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Información adicional para los administradores    
Para obtener instrucciones de configuración para habilitar la configuración de directivas **Configuración de la opción de permisos personalizados para que esté disponible para los usuarios**, vea [Configuración de la directiva de Azure Information Protection](../deploy-use/configure-policy-settings.md).

Otras instrucciones de configuración: [Configuración de la directiva de Azure Information Protection](../deploy-use/configure-policy.md).

