---
title: "Paso 5 del tutorial de inicio rápido | Azure Information Protection"
description: "Paso 5 del tutorial introductorio para probar rápidamente Microsoft Azure Information Protection para su organización, que debería tardar unos 30 minutos."
keywords: 
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4e59a3b3-f0f4-4535-8b96-cac68303d855
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: 5844ddd3f675cdc5a88de3abc3170d7e8a89aee9


---


# <a name="step-5-see-sharing-of-protected-files-in-action-and-track-your-document"></a>Paso 5: ver el funcionamiento del uso compartido de archivos protegidos y realizar un seguimiento del documento 

>*Se aplica a: Azure Information Protection*

Para este paso final del tutorial, busque un documento de Word que ya haya creado y envíelo a un partner o compañero de trabajo. Para este tutorial, lo que importa no es el texto en concreto, si no el hecho de que haya texto para confirmar más fácilmente si el recipiente autorizado puede leerlo.

A continuación, estará listo para compartir de forma segura este documento por correo electrónico. 

## <a name="to-safely-share-your-document-by-email"></a>Para compartir de forma segura el documento por correo electrónico

1.  En Word, abra el documento. Verá que la etiqueta predeterminada de **Interno** se aplica de nuevo automáticamente. 

2.  En la pestaña **Inicio** , en el grupo **RMS** , haga clic en **Uso compartido protegido** y de nuevo en **Uso compartido protegido** del menú:

    ![Paso 5 del tutorial de inicio rápido de Azure Information Protection: uso compartido protegido](../media/share-protected-callout.png)

    Verá el cuadro de diálogo **Uso compartido protegido**, similar a esta imagen:

    ![Paso 5 del tutorial de inicio rápido de Azure Information Protection: cuadro de diálogo uso compartido protegido](../media/example-share-protected-dialog.png)

3. En el cuadro **Usuarios**, escriba una o más direcciones de correo electrónico empresarial, como lo haría cuando envía un documento a alguien con el que su organización trabaja. O, puede especificar una dirección de correo electrónico de un compañero de trabajo. Asegúrese de especificar una dirección de correo electrónico empresarial, como **janetm@contoso.com** o **p.dover@fabrikam.com** porque, actualmente, Azure Information Protection no es compatible con las direcciones de correo electrónico personales. 

    No se preocupe por saber si la persona a la que envía el archivo también tiene Azure Information Protection o no.

4. Seleccione **Visor – Solo ver**.

    Esto significa que los destinatarios podrán ver el documento pero no editarlo ni imprimirlo.

5. Seleccione **Enviarme un correo electrónico cuando alguien trate de abrir estos documentos**.

    Recibirá una notificación por correo electrónico cada vez que los destinatarios intenten abrir el archivo adjunto, y también si alguien más intenta abrirlo (por ejemplo, cuando el destinatario reenvía el correo electrónico a un compañero de trabajo. Si el documento se reenvía, verá que se deniega el acceso y, a partir de los detalles del usuario, podrá decidir si enviar a esa persona una copia del documento que puede abrir.

6. Seleccione **Permítame revocar el acceso a estos documentos de forma instantánea**.

    Esta opción requiere que los destinatarios tengan una conexión a Internet cada vez que abran el archivo adjunto, pero con el beneficio de que si más adelante se revoca el documento, la próxima vez que intenten abrirlo, no podrán hacerlo. 

4.  Haga clic en **Enviar** para ver un mensaje de correo electrónico que esté listo para enviarse a los destinatarios que ha especificado y con el texto predeterminado para obtener instrucciones. Por ejemplo:

    ![Ejemplo de mensaje de correo electrónico cuando realiza un uso compartido protegido](../media/example-email-share-protected.png)
    
    **NOTA**: Si Outlook estaba abierto cuando ha instalado el cliente de protección de Azure Information Protection, no verá la barra de Information Protection que aparece en la imagen anterior: no se usa concretamente en este paso que muestra el uso compartido protegido de documentos, por lo que no es necesario cerrar y volver a abrir Outlook para completar el tutorial. Si ha abierto Outlook después de instalar el cliente de Azure Information Protection, verá que este mensaje de correo electrónico, como nuestro documento de Word la primera vez que se ha abierto, tiene la etiqueta **Interno** aplicada de manera predeterminada como resultado de configurar esta opción global en la directiva de Azure Information Protection.
    
    Puede que observe que tiene dos adjuntos; el documento de Word original y un archivo que tiene el mismo nombre pero con una extensión de nombre de archivo **.ppdf**. La versión .ppdf es un archivo PDF protegido que se crea automáticamente mediante la aplicación Rights Management sharing, en caso de que el destinatario no tenga una versión de Office que admita los documentos protegidos. Este archivo adicional permite que el destinatario lea el documento protegido al usar el visor que está instalado en la aplicación Rights Management sharing.

    Haga clic en **Enviar** en su mensaje de correo electrónico.

Ahora que ha enviado el documento protegido, está listo para pedir a los destinatarios que esperen a que llegue para luego abrirlo. Pero no debe cerrar Word porque lo volveremos a usar en el último procedimiento para realizar un seguimiento del documento compartido.

## <a name="ask-your-recipients-to-open-the-emailed-document"></a>Pedir a los destinatarios que abran el documento por correo electrónico

Los destinatarios pueden usar muchos dispositivos para leer el documento protegido que envía como datos adjuntos por correo electrónico. Entre los dispositivos, se encuentran el iPad, el iPhone, tabletas y teléfonos Android, y equipos Mac, así como los equipos Windows.

Pídales que lean el mensaje de correo electrónico que ha enviado. Teniendo en cuenta que esta es la primera vez que han recibido datos adjuntos que están protegidos por Rights Management, solicíteles que hagan clic en el vínculo de las instrucciones. Después, verán la página [Bienvenido a Microsoft RMS](https://portal.azurerms.com/#/rmshelp) con instrucciones para instalar la aplicación RMS sharing y, si es necesario, suscribirse a una cuenta gratuita. Después, están listos para leer el documento adjunto protegido.

### <a name="instructions-for-recipient-to-view-the-protected-document-attachment"></a>Instrucciones para los destinatarios: para ver los datos adjuntos del documento protegido

1. Abra uno de los documentos adjuntos para leer el documento:
    
    - Si tiene una versión de Office en su dispositivo que admita Rights Management:
    
        -  Abra el documento que tiene la extensión del nombre de archivo **.docx**.
        
    - Si no tiene una versión de Office que admita Rights Management, o si no está seguro, o simplemente quiere probar el visor de la aplicación de Rights Management sharing: 
    
        - Abra el documento que tiene la extensión del nombre de archivo **.ppdf**.

2.  Si se le pide su nombre de usuario y contraseña, escriba su nombre de usuario en el mismo formato que la dirección de correo electrónico que se usó para enviarle el correo electrónico y los datos adjuntos. Por ejemplo, **janetm@contoso.com** o **p.dover@fabrikam.com**. Para la contraseña, escriba la contraseña que proporcionó al suscribirse a RMS para usuarios. O, si su organización tiene un servicio en la nube como Office 365 o usa Azure, escriba su contraseña de trabajo habitual.

3. Lea el contenido del documento cuando se abra. Debido a que es de solo lectura, no puede cambiar el contenido.

Como paso opcional, el destinatario puede reenviar el correo electrónico a otras personas que no ha especificado en el correo electrónico original. Estas personas no podrán abrir el documento adjunto. Cuando se les pide el nombre de usuario, se deniega el acceso al documento.

Ahora que el destinatario ha abierto el archivo adjunto y lo ha enviado de forma opcional a alguien más, espere la notificación por correo electrónico que informa de esta actividad. En cambio, los mensajes de correo electrónico son fáciles de perder con el tiempo, así que una mejor manera de realizar un seguimiento de quién tuvo acceso al documento es usar el sitio de seguimiento de documentos, que se explica en el procedimiento final.

## <a name="to-track-your-protected-document"></a>Para hacer un seguimiento de un documento protegido

1.  De nuevo en Word, en la pestaña **Inicio** del grupo **RMS**, haga clic en **Uso compartido protegido** y luego haga clic en **Hacer seguimiento de uso** del menú:

    ![Opción realizar seguimiento](../media/track-usage-callout.png)

    Esto le lleva al sitio de seguimiento de documentos.

2.  Si ve la página **Proteger y compartir en sus términos**, haga clic en **Iniciar sesión** y proporcione su nombre de usuario y contraseña nuevamente.

3.  En la página **Sus documentos compartidos**, verá el nombre del documento que ha compartido. En este punto, es el único archivo que aparece, pero a medida que comparta más documentos protegidos, la lista aumentará.

    En esta página, verá la fecha en la que compartió el documento (cuándo envió el correo electrónico con el archivo adjunto protegido), la fecha de la última actividad y el nombre del destinatario al que envía el correo electrónico. Haga clic en el nombre del documento para obtener detalles adicionales.

4.  En la página nueva, que tiene el nombre del archivo en el que hizo clic, verá los detalles de resumen solo para ese documento y una lista de otras opciones que están disponibles para el documento (**Lista**, **Escala de tiempo**, **Mapa**, **Configuración**).

    Haga clic en cada opción para explorar maneras diferentes para hacer un seguimiento de un documento protegido. O bien, también en la página **Resumen** , haga clic en **Abrir en Excel** para exportar la información a una hoja de cálculo o en **Revocar acceso** para dejar de compartir el documento.

Puede volver a este sitio para realizar un seguimiento de más actividad relacionada con su documento protegido o revocar el acceso si es necesario. Incluso puede acceder al sitio desde su dispositivo móvil o tableta mediante un explorador con este vínculo: [seguimiento de documentos](http://go.microsoft.com/fwlink/?LinkId=529562)



|Si desea obtener más información|Información adicional|
|--------------------------------|--------------------------|
|Todas las instrucciones y los métodos alternativos para proteger los archivos que comparte por correo electrónico|[Protección de un archivo que comparte por correo electrónico con la aplicación Rights Management sharing](../rms-client/sharing-app-protect-by-email.md)|
|Acerca de las opciones del cuadro de diálogo **Uso compartido seguro**|[Opciones del cuadro de diálogo para la aplicación Rights Management sharing](../rms-client/sharing-app-dialog-box.md)|
|Sobre la cuenta gratuita para que se registren otros usuarios|[RMS para individuos y Azure Rights Management](../understand-explore/rms-for-individuals.md)|
|Sobre usar el sitio de seguimiento de documentos|[Realizar un seguimiento de los documentos y revocarlos](../rms-client/sharing-app-track-revoke.md)


## <a name="next-steps"></a>Pasos siguientes

Ahora que ha visto la directiva predeterminada de Azure Information Protection, cómo personalizarla y cómo funciona el etiquetado en un documento de Word, pruebe algunas de las otras opciones y vea cómo funcionan en otras aplicaciones de Office que son compatibles con Azure Information Protection: Excel, PowerPoint u Outlook. Si estas aplicaciones estaban abiertas al instalar el cliente de Azure Information Protection, ciérrelas y vuelva a abrirlas antes de intentar usarlas con Azure Information Protection.

Intente compartir más documentos y realice un seguimiento de cómo se usan y confirme cómo funciona la revocación de documentos.

Después, puede encontrar útil leer algunas de las [preguntas más frecuentes](faqs.md) de Azure Information Protection, y explorar algunos de los demás artículos de documentación. Pero si no está listo para empezar a implementar Azure Information Protection en su organización, el siguiente paso será el [mapa de ruta de implementación de Azure Information Protection](../plan-design/deployment-roadmap.md). 


<!--HONumber=Nov16_HO2-->


