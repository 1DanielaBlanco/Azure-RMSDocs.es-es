---
title: "Preguntas más frecuentes de Azure Information Protection (versión preliminar) | Azure Information Protection"
description: "¿Tiene alguna pregunta sobre la versión preliminar de Azure Information Protection? Vea si se ha resuelto aquí."
author: cabailey
manager: mbaldwin
ms.date: 08/22/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: c9f9211e7c1dcf293caf81475515114b5433d6a7
ms.openlocfilehash: 55d56786150d38b36ae8185c4a7ac4c8a5c51ba4


---

# Preguntas más frecuentes de Azure Information Protection (versión preliminar)

>*Se aplica a: Azure Information Protection (versión preliminar)*

**[Esta información es preliminar y está sujeta a cambios. ]**

¿Tiene alguna pregunta sobre la versión preliminar de Azure Information Protection?  Vea si se ha resuelto aquí. 

Esperamos que esta lista se actualice frecuentemente ya que parte de la información se mueve a la documentación principal e incluiremos preguntas nuevas que nos llegan de nuestros clientes. 

## ¿Qué puedo hacer con la versión preliminar de Azure Information Protection y cuáles son las limitaciones actuales?

Esta versión preliminar agrega una barra de Information Protection a las aplicaciones de Microsoft Office que le permite ver y modificar las etiquetas de clasificación que se han asignado a los datos. La clasificación puede realizarse manualmente, recomendada para usted o se aplica automáticamente. Para las clasificaciones que especifique, los datos pueden protegerse mediante una plantilla de Azure Rights Management.  

El comportamiento y las etiquetas de clasificación se configuran en el Portal de Azure. Puede usar las directivas predeterminadas integradas para evaluar rápidamente a Azure Information Protection o personalizar completamente sus propias directivas. Puede cambiar los colores, los nombres y el orden de las etiquetas de clasificación que los usuarios ven. También puede configurar la información sobre herramientas y las marcas visuales de clasificación como el encabezado, el pie de página o una marca de agua.

Pruebe nuestro tutorial de inicio rápido para ver esto en funcionamiento en unos minutos: [Tutorial de inicio rápido de Azure Information Protection](infoprotect-quick-start-tutorial.md).

Tenga en cuenta que la versión preliminar le permite probar el nuevo **plan de servicio Premium P2** y que algunas características avanzadas, como el etiquetado recomendado y automático, puede que no estén disponibles en su plan actual con disponibilidad general. Para obtener información sobre los diferentes planes de servicio (Azure Information Protection Premium P1 y Azure Information Protection Premium P2), vea la siguiente publicación del blog: [Introducing Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/2016/07/07/introducing-enterprise-mobility-security/)(Introducción a Enterprise Mobility + Security).

Esta versión preliminar tiene las limitaciones siguientes: Busque anuncios en el [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection) (Blog de seguridad y movilidad empresarial) y en nuestro [sitio de Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all) para saber cuándo estarán disponibles las funcionalidades y características adicionales:

- No existe un registro centralizado para la clasificación y el etiquetado.

- Los nombres de las etiquetas y la información sobre herramientas solo se admiten en un idioma.

- Las condiciones para la clasificación automática deben ser frases o patrones.

- Los archivos no pueden clasificarse desde el Explorador de archivos de Windows.

- Las aplicaciones de Office para los dispositivos móviles (iOS y Android) y los equipos Mac, y las aplicaciones web de Office (Office Online) todavía no se admiten.

- No existe una integración con Exchange Online o SharePoint Online.

- El SDK para partners y desarrolladores no está disponible.

## ¿Qué suscripción necesito para probar Azure Information Protection?

Para la vista previa, puede usar cualquier suscripción de Office 365 que incluya la protección de correos electrónicos y documentos de Office mediante Azure Rights Management. Azure Information Protection está disponible en todas las regiones. Para obtener más información sobre las suscripciones y los vínculos disponibles para las pruebas gratuitas, vea la sección [Suscripción de Office 365](../get-started/requirements-subscriptions.md#office-365-subscription) de la documentación de requisitos de Azure RMS.

Para configurar las directivas de Azure Information Protection en el Portal de Azure, debe tener una suscripción de Azure. Si no dispone aún de una suscripción de Azure para su organización, puede obtener una si se registra para una prueba gratuita: vaya a la página [Introducción a Azure](https://account.windowsazure.com/organization) y siga las instrucciones.

Cualquier cambio que se produzca en los requisitos de la suscripción se anunciará en el [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection)(Blog de seguridad y movilidad empresarial).

## ¿Necesito ser un administrador global para probar la versión preliminar de Azure Information Protection?

Solo para la versión preliminar, cualquier usuario que se autentique mediante Azure puede ver y configurar la directiva de Azure Information Protection de su inquilino para clasificación y etiquetado en el Portal de Azure. En cambio, para configurar una etiqueta para aplicar una plantilla de Azure Rights Management, debe iniciar sesión como administrador global de Azure Active Directory.

Si selecciona la opción para instalar la directiva de demostración cuando instale el [cliente de Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018), no necesita iniciar sesión en el portal para probar la versión preliminar. La directiva de demostración instala localmente la directiva predeterminada para Azure Information Protection, de forma que pueda probar el etiquetado de documentos y correos electrónicos, pero no podrá cambiar ni agregar etiquetas nuevas sin iniciar sesión en el Portal de Azure. 

Si quiere proteger los documentos y los correos electrónicos que clasifica y etiqueta, y no ha activado todavía Azure Rights Management, el proceso de activación requiere permisos especiales de administrador. Para obtener más información, vea [¿Debe ser un administrador global para configurar Azure RMS o puedo delegar a otros administradores?](../get-started/faqs.md#do-you-need-to-be-a-global-admin-to-configure-azure-rms-or-can-i-delegate-to-other-administrators)


## ¿Azure Information Protection admite los escenarios híbridos y locales?

Azure Information Protection es una solución basada en la nube. Si está interesado en implementar Azure Information Protection para un escenario híbrido, póngase en contacto con el equipo de Information Protection; para ello, envíe un correo electrónico a askipteam@microsoft.com.

## ¿Qué aplicaciones y plataformas de clientes son compatibles con Azure Information Protection?

Esto aparece documentado y se actualizará en [Requisitos de Azure Information Protection](requirements-azure-infoprotect.md).


## ¿Cómo obtienen los equipos la información de la directiva de Azure Information Protection y con qué frecuencia se actualiza?

Cada vez que un usuario abre una aplicación de Office, el cliente de Azure Information Protection comprueba si existe una versión posterior de la directiva de Azure Information Protection. Si existe una versión posterior, el cliente la puede descargar mediante un vínculo HTTPS para proteger los datos. 

Si se cargan varias instancias de la aplicación de Office cuando se publica una nueva directiva de Azure Information Protection, debe cerrar todas las instancias para obtener la última versión de la directiva. Por ejemplo, tiene abiertos dos documentos de Word y quiere probar la directiva de Azure Information Protection actualizada solo en uno de ellos: cierre ambos documentos de Word y vuelva a abrir aquel que quiera usar con la directiva más reciente.

## ¿Dónde pueden almacenarse los archivos para usar Azure Information Protection? 

Como Azure Information Protection aplica etiquetas persistentes y protección a los archivos y correos electrónicos, no importa dónde se almacenen.

## ¿Puedo clasificar solo los datos nuevos o también los existentes?

Las acciones de la directiva de Azure Information Protection entran en vigor cuando los documentos se guardan y los correos electrónicos se envían, tanto para el contenido nuevo como para los cambios en el contenido existente. 

Si ha guardado los archivos que quiere clasificar, simplemente abra y guárdelos en su aplicación de Office. 

Actualmente, no puede analizar y aplicar una clasificación en masa, y debe abrir y guardar cada documento en la aplicación de Office. 

## ¿Puedo usar Azure Information Protection solo para la clasificación, sin forzar el cifrado y sin restringir los derechos de uso?

Sí. Puede configurar una directiva de Azure Information Protection que solo aplique una etiqueta. De hecho, esperamos que este sea el caso principal para implementar redes donde necesita proteger solo un subconjunto de documentos o correos electrónicos que requieran una administración especial de datos.

## ¿Cómo funciona la clasificación automática?

En el Portal de Azure, puede usar patrones predefinidos, como "números de tarjeta de crédito" o el "número del seguro social de EE. UU.". O puede definir un patrón o una cadena personalizada como condición de una clasificación automática.

Verá un ejemplo de esto en el [Tutorial de inicio rápido de Azure Information Protection](infoprotect-quick-start-tutorial.md). 

La precisión de la clasificación depende de cómo configure la regla de clasificación, que se basa en condiciones. En estos momentos, las condiciones admiten patrones de texto y expresiones regulares. Para obtener una explicación de cada una de las opciones disponibles durante la versión preliminar, junto con algunos ejemplos sugeridos para que pruebe, consulte [Configuración de las condiciones para la clasificación automática y recomendada de Azure Information Protection](configure-policy-classification.md). La detección se ejecuta cuando el documento se guarda o cuando un correo electrónico se envía.

Para obtener la mejor experiencia de usuario y para garantizar la continuidad empresarial, le recomendamos que comience con acciones de recomendación del usuario, en lugar de acciones completamente automáticas. Esto proporciona a sus usuarios la capacidad de aceptar la acción de protección o etiquetado, o de reemplazar estas sugerencias.   

## ¿Puede Azure Information Protection solicitar a los usuarios que clasifiquen los archivos ellos mismos en lugar de usar la clasificación automática? 

Sí. Use el Portal de Azure para configurar el uso de la clasificación automática o realizar una recomendación a los usuarios al establecer la opción **Select how this label is applied: automatically or recommended to user (Seleccionar cómo se aplica esta etiqueta: automáticamente o recomendado para el usuario)** en **Recomendado**.

Verá un ejemplo de esto en el [Tutorial de inicio rápido de Azure Information Protection](infoprotect-quick-start-tutorial.md).  

## ¿Puedo forzar que todos los documentos se clasifiquen?

Sí. Si necesita que los usuarios clasifiquen todos los archivos que guarden, en el Portal de Azure, establezca la opción **All documents and emails must have a label (Todos los documentos y correos electrónicos deben tener una etiqueta)** en **Activado**. 

## ¿Puedo quitar una clasificación de un archivo?

Sí. Para quitar la clasificación de un archivo, abra el archivo en la aplicación de Office, haga clic en el icono **Editar etiqueta** en la barra de Information Protection, haga clic en el icono **Quitar etiqueta** y, después, haga clic en **Aceptar** para confirmar su acción. 


## ¿Puedo solicitar a los usuarios que justifiquen por qué están cambiando el nivel de clasificación?

Sí. Para asegurarse de que los usuarios justifican su cambio de clasificación, en el Portal de Azure, establezca la opción **Users must provide justification when lowering the sensitivity level (Los usuarios deben proporcionar justificación al reducir el nivel de confidencialidad)** en **Activado**. Cuando hagan esto, su motivo de justificación y la acción se registran en su registro de eventos de Windows local: **Aplicación** > **Microsoft Azure Information Protection**.

## ¿Cómo puedo proteger automáticamente el contenido después de que se haya clasificado?

En el Portal de Azure, puede seleccionar una plantilla de Azure Rights Management para proteger automáticamente el contenido, según el nivel de clasificación que especifique.

Verá un ejemplo de esto en el [Tutorial de inicio rápido de Azure Information Protection](infoprotect-quick-start-tutorial.md). Para más información, consulte [Configuración de una etiqueta para aplicar protección de Rights Management](configure-policy-protection.md).

## ¿Puede clasificarse un archivo con dos clasificaciones diferentes?

Si fuera necesario, puede crear subetiquetas para describir mejor las subcategorías de una etiqueta de confidencialidad específica. Por ejemplo, la etiqueta principal **Secreto** podría contener subetiquetas como **Secreto: legal** y **Secreto: finanzas**. Por consiguiente, puede aplicar diferentes marcas visuales de clasificación y diferentes plantillas de Rights Management en diferentes subetiquetas.

Aunque en estos momentos puede establecer marcas visuales, protección y condiciones en ambos niveles, cuando use los subniveles, configure estas opciones solo en el subnivel. Si configura las mismas opciones en la etiqueta principal y en su subnivel, la configuración del subnivel tiene prioridad.

## ¿Cómo pueden las soluciones DLP y otras aplicaciones integrarse con Azure Information Protection?

Como Azure Information Protection usa metadatos persistentes para la clasificación, que incluyen una etiqueta no cifrada, esta información puede leerse mediante soluciones DLP y otras aplicaciones. En los archivos, estos metadatos se almacenan en propiedades personalizadas; en los correos electrónicos, esta información se encuentra en los encabezados del correo.

## ¿Cómo funciona la revocación y el seguimiento de documentos en Azure Information Protection?

El seguimiento de documentos para los archivos que clasifica y protege mediante Azure Information Protection funciona de la misma forma que en la actualidad para Azure Rights Management y la aplicación RMS sharing. También puede acceder al sitio de seguimiento de documentos mediante el cliente de Azure Information Protection (versión 1.0.233 o posterior): 

- En una aplicación de Office, en la pestaña **Inicio**, en el grupo **Protección**, haga clic en **Proteger** > **Hacer seguimiento de uso**. 

Para obtener más información, vea [Seguimiento y revocación de documentos cuando se usa la aplicación RMS sharing](../rms-client/sharing-app-track-revoke.md).

## ¿Cómo aplica Azure Information Protection las directivas que configuro?

Cuando un documento está protegido mediante una plantilla de Azure Rights Management, el usuario se autentica primero para asegurarse de que tiene derechos en el documento y, después, la aplicación ejecuta la directiva de derechos de uso. 

## ¿Cómo Azure Information Protection usa Azure Active Directory?

Azure Information Protection usa Azure Active Directory para la autenticación de usuarios.

## ¿Puedo controlar qué usuarios pueden usar Azure Information Protection para clasificar y proteger el contenido?

Puede restringir qué usuarios clasifican y protegen los datos mediante el control de la distribución del cliente de Azure Information Protection. 

Los archivos y los correos electrónicos que Azure Information Protection clasifica pueden consumirse o editarse por cualquier usuario, con o sin el cliente de Azure Information Protection instalado. 

## ¿Cómo puedo informar de un problema o enviar comentarios de esta versión preliminar?

Si encuentra algún problema al usar esta versión preliminar, en su aplicación de Office, en la pestaña **Inicio**, en el grupo **Protección**, haga clic en **Proteger** y, después, haga clic en **Ayuda y comentarios**. En el cuadro de diálogo **Microsoft Azure Information Protection**, haga clic en **Enviar comentarios**. Esto se envía por correo electrónico al equipo de Information Protection y, automáticamente, adjunta los archivos de registro de su equipo PC para ayudar en el diagnóstico del problema. 

Si tiene alguna pregunta o comentario, use el [sitio de Yammer de Azure Information Protection](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all). 

## ¿Qué debo hacer si mi pregunta no aparece aquí?

Primero, compruebe que su pregunta no se incluye en el [anuncio de versión preliminar de Azure Information Protection](https://blogs.technet.microsoft.com/enterprisemobility/2016/07/12/azure-information-protection-public-preview-available-now/), en el Enterprise Mobility and Security Blog (Blog de seguridad y movilidad empresarial).

Después, visite nuestro [sitio de Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all) para ver si alguien ha realizado la misma pregunta. Si no, publique su pregunta ahí.







<!--HONumber=Aug16_HO4-->


