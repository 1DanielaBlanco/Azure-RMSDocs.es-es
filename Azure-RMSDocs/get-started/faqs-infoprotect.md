---
title: "Preguntas más frecuentes sobre la clasificación y el etiquetado | Azure Information Protection"
description: "¿Tiene alguna pregunta sobre la versión preliminar de Azure Information Protection? Vea si se ha resuelto aquí."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/23/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d4338a1c89f2a94c744b8f5cc99bce1e54e7dec
ms.openlocfilehash: 028468e7f4bbcff53187a947038926fbf9af1498


---

# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Preguntas más frecuentes sobre la clasificación y el etiquetado en Azure Information Protection

>*Se aplica a: Azure Information Protection, Office 365*

¿Tiene alguna pregunta sobre Azure Information Protection que trate específicamente sobre clasificación y etiquetado?  Vea si se ha resuelto aquí. 

## <a name="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection"></a>¿Qué puedo hacer con las funcionalidades de clasificación en Azure Information Protection?

El cliente de Azure Information Protection agrega una barra de Information Protection a las aplicaciones de Microsoft Office que le permite ver y modificar las etiquetas de clasificación que se han asignado a los datos. La clasificación puede realizarse manualmente, recomendada para usted o se aplica automáticamente. Para las clasificaciones que especifique, los datos pueden protegerse mediante un servicio de Rights Management.  

El comportamiento y las etiquetas de clasificación se configuran en el Portal de Azure. Puede usar la directiva predeterminada integrada para evaluar rápidamente Azure Information Protection o personalizar completamente sus propias directivas. Puede cambiar los colores, los nombres y el orden de las etiquetas de clasificación que los usuarios ven. También puede configurar la información sobre herramientas y las marcas visuales de clasificación como el encabezado, el pie de página o una marca de agua.

Pruebe nuestro tutorial de inicio rápido para ver esto en funcionamiento en unos minutos: [Tutorial de inicio rápido de Azure Information Protection](infoprotect-quick-start-tutorial.md).

La versión actual tiene las limitaciones siguientes. Busque anuncios en el [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection) (Blog de seguridad y movilidad empresarial) y en nuestro [sitio de Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all) para saber cuándo estarán disponibles las funcionalidades y características adicionales:

- Solo puede aplicar etiquetas a los tipos de archivo de Office y a los mensajes de correo electrónico de Outlook.

- Las etiquetas en el complemento de Office son visibles para todos los usuarios que tienen instalado el cliente de Azure Information Protection.

- Los nombres de las etiquetas y la información sobre herramientas solo se admiten en un idioma.

- Los archivos no pueden clasificarse desde el Explorador de archivos de Windows.

- No existe un registro centralizado para la clasificación y el etiquetado.

- Las condiciones para la clasificación automática deben ser frases o patrones.

- Las aplicaciones de Office para los dispositivos móviles (iOS y Android) y los equipos Mac, y las aplicaciones web de Office (Office Online) todavía no se admiten.

- No existe una integración con Exchange Online o SharePoint Online.

- El SDK para partners y desarrolladores no está disponible.

## <a name="do-i-need-to-be-a-global-admin-to-try-azure-information-protection"></a>¿Necesito ser un administrador global para probar Azure Information Protection?

Para configurar la directiva de Azure Information Protection, debe iniciar sesión en Azure Portal como administrador global de Azure Active Directory.

En cambio, si selecciona la opción para instalar la directiva de demostración cuando instale el [cliente de Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018), no necesita iniciar sesión en el portal para ver y probar la funcionalidad de etiquetado. La directiva de demostración instala localmente la directiva predeterminada para Azure Information Protection, de forma que pueda probar el etiquetado de documentos y correos electrónicos, pero no podrá cambiar ni agregar etiquetas nuevas sin iniciar sesión en el Portal de Azure. 

## <a name="which-options-in-the-azure-portal-are-p1-or-p2"></a>¿Qué opciones en Azure Portal son P1 o P2?

Para comprobar qué características se incluyen en la suscripción **Azure Information Protection Premium 1** (P1) en comparación con la suscripción **Azure Information Protection Premium 2** (P2), consulte la [lista de características](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features) en el sitio de Azure Information Protection.

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>¿Azure Information Protection admite los escenarios híbridos y locales?

Azure Information Protection es una solución basada en la nube. Si está interesado en implementar Azure Information Protection para un escenario híbrido, póngase en contacto con el equipo de Information Protection; para ello, envíe un correo electrónico a askipteam@microsoft.com.

## <a name="how-do-computers-get-the-policy-information-from-azure-information-protection-and-how-often-is-it-refreshed"></a>¿Cómo obtienen los equipos la información de la directiva de Azure Information Protection y con qué frecuencia se actualiza?

Cada vez que un usuario abre una aplicación de Office, el cliente de Azure Information Protection comprueba si existe una versión posterior de la directiva de Azure Information Protection. Además, las aplicaciones de Office se comprueban cada 24 horas. Si existe una versión posterior, el cliente la puede descargar mediante un vínculo HTTPS para proteger los datos. 

Si se cargan varias instancias de la aplicación de Office cuando se publica una nueva directiva de Azure Information Protection, debe cerrar todas las instancias para obtener la última versión de la directiva. Por ejemplo, tiene abiertos dos documentos de Word y quiere probar la directiva de Azure Information Protection actualizada solo en uno de ellos: cierre ambos documentos de Word y vuelva a abrir aquel que quiera usar con la directiva más reciente.

## <a name="where-can-files-be-stored-to-use-azure-information-protection"></a>¿Dónde pueden almacenarse los archivos para usar Azure Information Protection? 

Como Azure Information Protection aplica etiquetas persistentes y protección a los archivos y correos electrónicos, no importa dónde se almacenen.

## <a name="can-i-classify-only-new-data-or-can-i-also-classify-existing-data"></a>¿Puedo clasificar solo los datos nuevos o también los existentes?

Las acciones de la directiva de Azure Information Protection entran en vigor cuando los documentos se guardan y los correos electrónicos se envían, tanto para el contenido nuevo como para los cambios en el contenido existente. 

Si ha guardado los archivos que quiere clasificar, simplemente abra y guárdelos en su aplicación de Office. 

Actualmente, no puede analizar y aplicar una clasificación en masa, y debe abrir y guardar cada documento en la aplicación de Office. 

## <a name="can-i-use-azure-information-protection-for-classification-only-without-enforcing-encryption-and-restricting-usage-rights"></a>¿Puedo usar Azure Information Protection solo para la clasificación, sin forzar el cifrado y sin restringir los derechos de uso?

Sí. Puede configurar una directiva de Azure Information Protection que solo aplique una etiqueta. De hecho, esperamos que este sea el caso principal para implementar redes donde necesita proteger solo un subconjunto de documentos o correos electrónicos que requieran una administración especial de datos.

## <a name="how-does-automatic-classification-work"></a>¿Cómo funciona la clasificación automática?

En el Portal de Azure, puede usar patrones predefinidos, como "números de tarjeta de crédito" o el "número del seguro social de EE. UU.". O puede definir un patrón o una cadena personalizada como condición de una clasificación automática.

Verá un ejemplo de esto en el [Tutorial de inicio rápido de Azure Information Protection](infoprotect-quick-start-tutorial.md). 

La precisión de la clasificación depende de cómo configure la regla de clasificación, que se basa en condiciones. En estos momentos, las condiciones admiten patrones de texto y expresiones regulares. Para obtener una explicación de cada una de las opciones disponibles durante la versión preliminar, junto con algunos ejemplos sugeridos para que pruebe, consulte [Configuración de las condiciones para la clasificación automática y recomendada de Azure Information Protection](../deploy-use/configure-policy-classification.md). La detección se ejecuta cuando el documento se guarda o cuando un correo electrónico se envía.

Para obtener la mejor experiencia de usuario y para garantizar la continuidad empresarial, le recomendamos que comience con acciones de recomendación del usuario, en lugar de acciones completamente automáticas. Esto proporciona a sus usuarios la capacidad de aceptar la acción de protección o etiquetado, o de reemplazar estas sugerencias.   

## <a name="can-azure-information-protection-prompt-users-to-classify-files-themselves-rather-than-use-automatic-classification"></a>¿Puede Azure Information Protection solicitar a los usuarios que clasifiquen los archivos ellos mismos en lugar de usar la clasificación automática? 

Sí. Use el Portal de Azure para configurar el uso de la clasificación automática o realizar una recomendación a los usuarios al establecer la opción **Select how this label is applied: automatically or recommended to user (Seleccionar cómo se aplica esta etiqueta: automáticamente o recomendado para el usuario)** en **Recomendado**.

Verá un ejemplo de esto en el [Tutorial de inicio rápido de Azure Information Protection](infoprotect-quick-start-tutorial.md).  

## <a name="can-i-force-all-documents-to-be-classified"></a>¿Puedo forzar que todos los documentos se clasifiquen?

Sí. Si necesita que los usuarios clasifiquen todos los archivos que guarden, en el Portal de Azure, establezca la opción **All documents and emails must have a label (Todos los documentos y correos electrónicos deben tener una etiqueta)** en **Activado**. 

## <a name="can-i-remove-classification-from-a-file"></a>¿Puedo quitar una clasificación de un archivo?

Sí. Para quitar la clasificación de un archivo, abra el archivo en la aplicación de Office, haga clic en el icono **Editar etiqueta** en la barra de Information Protection, haga clic en el icono **Quitar etiqueta** y, después, haga clic en **Aceptar** para confirmar su acción. 


## <a name="can-i-prompt-users-to-justify-why-they-are-changing-the-classification-level"></a>¿Puedo solicitar a los usuarios que justifiquen por qué están cambiando el nivel de clasificación?

Sí. Para asegurarse de que los usuarios justifiquen su cambio de clasificación, en el Portal de Azure, **active** la opción **Users must provide justification to set a lower classification label, remove a label, or remove protection** (Los usuarios deben proporcionar una justificación para establecer una etiqueta de clasificación inferior, quitar una etiqueta o quitar la protección). Cuando hagan esto, su motivo de justificación y la acción se registran en su registro de eventos de Windows local: **Aplicación** > **Microsoft Azure Information Protection**.

## <a name="how-can-i-automatically-protect-the-content-after-its-been-classified"></a>¿Cómo puedo proteger automáticamente el contenido después de que se haya clasificado?

En Azure Portal, puede seleccionar una plantilla de Rights Management para proteger automáticamente el contenido, según el nivel de clasificación que especifique.

Verá un ejemplo de esto en el [Tutorial de inicio rápido de Azure Information Protection](infoprotect-quick-start-tutorial.md). Para más información, consulte [Configuración de una etiqueta para aplicar protección de Rights Management](../deploy-use/configure-policy-protection.md).

## <a name="can-a-file-be-classified-with-two-different-classifications"></a>¿Puede clasificarse un archivo con dos clasificaciones diferentes?

Si fuera necesario, puede crear subetiquetas para describir mejor las subcategorías de una etiqueta de confidencialidad específica. Por ejemplo, la etiqueta principal **Secreto** podría contener subetiquetas como **Secreto: legal** y **Secreto: finanzas**. Por consiguiente, puede aplicar diferentes marcas visuales de clasificación y diferentes plantillas de Rights Management en diferentes subetiquetas.

Aunque en estos momentos puede establecer marcas visuales, protección y condiciones en ambos niveles, cuando use los subniveles, configure estas opciones solo en el subnivel. Si configura las mismas opciones en la etiqueta principal y en su subnivel, la configuración del subnivel tiene prioridad.

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>Cuando se etiqueta un correo electrónico, ¿los datos adjuntos reciben automáticamente el mismo etiquetado?

No. Al etiquetar un mensaje de correo electrónico que tiene datos adjuntos, dichos datos adjuntos no heredan la misma etiqueta. Los datos adjuntos siguen sin etiqueta o conservarán una etiqueta aplicada por separado. Sin embargo, si la etiqueta para el correo electrónico aplica protección, dicha protección se aplica a los datos adjuntos.

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>¿Cómo pueden las soluciones DLP y otras aplicaciones integrarse con Azure Information Protection?

Como Azure Information Protection usa metadatos persistentes para la clasificación, que incluyen una etiqueta no cifrada, esta información puede leerse mediante soluciones DLP y otras aplicaciones. En los archivos, estos metadatos se almacenan en propiedades personalizadas; en los correos electrónicos, esta información se encuentra en los encabezados del correo.

## <a name="how-does-document-tracking-and-revocation-work-for-azure-information-protection"></a>¿Cómo funciona la revocación y el seguimiento de documentos en Azure Information Protection?

El seguimiento de documentos para los archivos que clasifica y protege mediante Azure Information Protection funciona con la protección de Azure Rights Management y la aplicación RMS sharing. También puede acceder al sitio de seguimiento de documentos mediante el cliente de Azure Information Protection (versión 1.0.233 o posterior): 

- En una aplicación de Office, en la pestaña **Inicio**, en el grupo **Protección**, haga clic en **Proteger** > **Hacer seguimiento de uso**. 

Para obtener más información, vea [Seguimiento y revocación de documentos cuando se usa la aplicación RMS sharing](../rms-client/sharing-app-track-revoke.md).

## <a name="can-i-control-which-users-can-use-azure-information-protection-to-classify-and-protect-content"></a>¿Puedo controlar qué usuarios pueden usar Azure Information Protection para clasificar y proteger el contenido?

Puede restringir qué usuarios clasifican y protegen los datos mediante el control de la distribución del cliente de Azure Information Protection. 

Los archivos y los correos electrónicos que Azure Information Protection clasifica pueden consumirse o editarse por cualquier usuario, con o sin el cliente de Azure Information Protection instalado. 

## <a name="how-do-i-sign-in-as-a-different-user"></a>¿Cómo se inicia sesión como un usuario diferente?

En un entorno de producción, normalmente no necesitará iniciar sesión como un usuario diferente cuando esté utilizando el cliente de Azure Information Protection. Sin embargo, tendrá que hacerlo si tiene varios inquilinos. Por ejemplo, en caso de que tenga un inquilino de prueba además del inquilino de Office 365 o Azure que usa la organización.

Puede comprobar con qué cuenta ha iniciado sesión en el cuadro de diálogo **Microsoft Azure Information Protection**: abra una aplicación de Office y, en la pestaña **Inicio** del grupo **Protección**, haga clic en **Proteger** y finalmente en **Ayuda y comentarios**. El nombre de cuenta se muestra en la sección **Estado del cliente**.

Especialmente si está usando una cuenta de administrador, asegúrese de comprobar el nombre de dominio de la cuenta con la sesión iniciada que aparece. Por ejemplo, si tiene una cuenta de "administrador" en dos inquilinos diferentes, puede ser fácil pasar por alto que se ha iniciado sesión con el nombre de cuenta correcto pero con el dominio incorrecto. Esto se traduciría en que no se podría descargar la directiva de Azure Information Protection o no se verían las etiquetas de comportamiento esperadas.

Para iniciar sesión como un usuario diferente, actualmente debe modificar el registro:

1. Mediante un editor del Registro, vaya a **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP** y elimine la clave **TokenCache**.

2. Reinicie todas las aplicaciones de Office abiertas e inicie sesión con su cuenta de usuario diferente. Si no ve un mensaje en la aplicación de Office para iniciar sesión en el servicio Azure Information Protection, vuelva al cuadro de diálogo **Microsoft Azure Information Protection** y haga clic en **Iniciar sesión** desde la sección **Estado del cliente** actualizada.

Además:

- Si desea reinicializar el entorno para el servicio de Azure Rights Management (también conocido como arranque), puede hacerlo mediante la opción **Restablecer** de la [herramienta RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437).

- Si desea eliminar la directiva actualmente descargada de Azure Information Protection, puede hacerlo eliminando el archivo **Policy.msip** de la carpeta %localappdata%\Microsoft\MSIP.

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>¿Cómo puedo informar de un problema o enviar comentarios de Azure Information Protection?

Si tiene un problema con Azure Information Protection y está usando la versión actual del cliente: vaya a la aplicación de Office, seleccione la pestaña **Inicio** y, en el grupo **Protección**, haga clic en **Proteger** y luego en **Ayuda y comentarios**. En el cuadro de diálogo **Microsoft Azure Information Protection**, haga clic en **Enviar comentarios**. Esto se envía por correo electrónico al equipo de Information Protection y, automáticamente, adjunta los archivos de registro de su equipo PC para ayudar en el diagnóstico del problema. 

Si tiene alguna pregunta o comentario, use el [sitio de Yammer de Azure Information Protection](https://www.yammer.com/askipteam/). 


<!--HONumber=Nov16_HO4-->


