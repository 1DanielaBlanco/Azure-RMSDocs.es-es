---
title: "Escenario: Compartir un archivo de Office con usuarios de otra organización | Azure Information Protection"
description: "En este escenario y en la documentación de usuario correspondiente se usa la protección de Azure Rights Management para que los usuarios puedan enviar por correo electrónico de forma segura un archivo de Office a usuarios de otra organización."
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: c10a4d7b-f57a-4a43-b66e-477777be59cc
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 03bd68b03d423908e7fbe89efb6aac6773283f2f
ms.openlocfilehash: 1e8ba22c5fdcf3f17b3cec0a99444975c03ec008


---

# Escenario: Compartir un archivo de Office con usuarios de otra organización

>*Se aplica a: Azure Information Protection, Office 365*

En este escenario y en la documentación de usuario correspondiente se usa la tecnología Azure Rights Management de Azure Information Protection para que los usuarios puedan enviar de forma segura por correo electrónico un archivo de Office a usuarios de otra organización. Por ejemplo, el archivo de Office puede ser un documento de Word, una hoja de cálculo de Excel o una presentación de PowerPoint que contenga información de lista de precios para un asociado, una lista de productos para un distribuidor o una lista de escalas de tiempo de entrega con clientes potenciales. Cuando los usuarios siguen las instrucciones, el archivo adjuntado al mensaje de correo electrónico lo protegerá Azure Rights Management.

Este escenario es adecuado para el conjunto de circunstancias siguiente:

-   El empleado debe enviar la información fuera de la organización, por correo electrónico, en forma de datos adjuntos de un documento de Office.

-   El documento contiene información que no es pública, pero tampoco es exclusivamente para uso interno.

-   Los usuarios destinatarios no tienen ningún requisito para compartir esta información con otras personas, imprimirla o utilizarla como parte de su propia documentación. Si este no es el caso, puede cambiar las instrucciones de usuario de seleccionar permisos de solo vista a otra opción que permita al destinatario cambiar los datos adjuntos.

-   Puede que el empleado esté interesado en saber cuándo el usuario externo abre este documento.

## Instrucciones de implementación
![Instrucciones para el administrador para la implementación rápida de Azure RMS](../media/AzRMS_AdminBanner.png)

Asegúrese de que se cumplen los siguientes requisitos antes de pasar a la documentación del usuario.

## Requisitos para este escenario
Para que funcionen las instrucciones de usuario para este escenario, debe disponer de lo siguiente:

|Requisito|Si necesita más información|
|---------------|--------------------------------|
|Ha preparado cuantas y grupos para Office 365 o Azure Active Directory|[Preparación de Azure Information Protection](https://technet.microsoft.com/library/jj585029.aspx)|
|Azure Rights Management no está activado|[Activar Rights Management de Azure](https://technet.microsoft.com/library/jj658941.aspx)|
|La aplicación Rights Management sharing se implementa en los equipos de los usuarios que ejecutan Windows|[Implementación automática de la aplicación Microsoft Rights Management sharing](../rms-client/sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application)|
|Los usuarios tienen Outlook de Office 2013|Si los usuarios tienen Office 2016 u Office 2010, reemplace la captura de pantalla por una versión equivalente para que la imagen coincida con lo que ven los usuarios.|
|En la suscripción a Azure Information Protection se incluye el seguimiento de documentos|Si en la suscripción a Azure RMS no se incluye la revocación y el seguimiento de documentos, los usuarios no podrán completar todos los pasos de las instrucciones de usuario. En este caso, compre una suscripción que admita estas características o modifique las instrucciones de usuario para quitar los pasos que utilizan estas características.<br /><br />Vea la información sobre la suscripción en la [página de precios](https://go.microsoft.com/fwlink/?LinkId=827589) de Azure Information Protection.|

## Instrucciones de la documentación del usuario
Con la siguiente plantilla, copie y pegue las instrucciones de usuario en una comunicación dirigida a sus usuarios finales y realice estas modificaciones para reflejar su entorno:

1.  Reemplace *&lt;nombre de tipo de documento de Office&gt;* por el tipo de documento que van a enviar los usuarios. Use nombres que sean específicos y familiares a sus flujos de trabajo, por ejemplo, "lista de precios", "tiempos de entrega" y "propuesta de puja" en lugar de "Documento de Word" y "Hoja de cálculo de Excel". Estas palabras más específicas ayudan a aumentar la posibilidad de que sigan las instrucciones al trabajar con esos documentos.

2.  Reemplace *&lt;detalles de contacto&gt;* por instrucciones sobre cómo los usuarios pueden ponerse en contacto con el departamento de soporte técnico, por ejemplo, un vínculo de sitio web, una dirección de correo electrónico o un número de teléfono.

3.  **Otras modificaciones que pueden interesarle:**

    -   En el paso 2, le sugerimos **Visor - Solo ver** para los permisos, de tal forma que el documento adjunto (pero no el original) sea de solo lectura para los destinatarios. Si esta restricción no es adecuada para sus necesidades de negocio, cambie esta opción por otro conjunto de permisos, como **Revisor - Ver y editar**.

    -   En el paso 3, sugerimos la opción **Permítame revocar el acceso a estos documentos de forma instantánea** para que no hay ningún retraso si los usuarios revocan el documento más adelante, pero esta opción requiere que el destinatario siempre tenga una conexión a Internet para abrir el archivo adjunto. Este paso también requiere una suscripción que admita el seguimiento y la revocación de documentos. Elimine este paso si no es adecuado para los usuarios.

    -   En el paso 4, se recomienda la opción **Enviarme un correo electrónico cuando alguien intente abrir estos documentos**. Si los usuarios realizan el seguimiento de sus documentos mediante el portal de seguimiento de documentos, puede decidir que la notificación de correo electrónico no es necesaria y eliminar este paso.

    -   Los pasos no incluyen el establecimiento de una fecha de expiración. Si no debe usarse la información después de una fecha concreta, agregue otro paso para establecer un tiempo de expiración adecuado, como 90 días desde el envío del mensaje de correo electrónico.

    > [!NOTE]
    > Para obtener más información sobre las opciones que pueden seleccionar los usuarios, consulte [Opciones del cuadro de diálogo para la aplicación Rights Management sharing](https://technet.microsoft.com/library/dn574738.aspx)

4.  Realice cualquier otro cambio que desee en este conjunto de instrucciones y, después, envíelo a estos usuarios.

En la documentación de ejemplo se muestra el aspecto de estas instrucciones para los usuarios tras sus personalizaciones.

![Documentación de usuario de la plantilla para la implementación rápida de Azure RMS](../media/AzRMS_UsersBanner.png)

### Cómo compartir un &lt;nombre de tipo de documento de Office&gt;

1.  Cree el mensaje de correo electrónico especificando la dirección o direcciones de correo electrónico, escriba el mensaje y adjunte el *&lt;nombre de tipo de documento de Office&gt;* al mensaje de correo electrónico. A continuación, en la pestaña **MENSAJE** , en el grupo **RMS** , haga clic en **Compartir protegido** y después otra vez en **Compartir protegido** :

    ![Captura de pantalla sobre cómo compartir un documento de Office mediante Outlook](../media/AzRMSUserInstructions_ShareProtectedRibbon2013.png)

2.  En el cuadro de diálogo **compartir protegido** , seleccione **Visor: solo ver**:

    ![cuadro de diálogo uso compartido seguro, Visor: solo ver](../media/AzRMS_SharedProtected_ViewerOnly.PNG)

3.  Seleccione **Permítame revocar el acceso a estos documentos de forma instantánea**:

    ![cuadro de diálogo uso compartido seguro, revocar de forma instantánea](../media/AzRMS_SharedProtected_InstantRevoke.PNG)

4.  Seleccione **Enviarme un correo electrónico cuando alguien intente abrir estos documentos**:

    ![cuadro de diálogo uso compartido seguro, enviarme un correo electrónico](../media/AzRMS_SharedProtected_EmailMe.PNG)

5.  Haga clic en **Enviar ahora**.

Cuando alguien en las líneas **Para**, **CC** o **CCO** recibe este correo electrónico, ve un mensaje que le da las instrucciones de cómo leer el archivo adjunto *&lt;nombre de tipo de documento de Office&gt;*. Se puede leer el documento en varios dispositivos, como tabletas y teléfonos iPad, iPhone y Android, equipos Mac y equipos Windows.

Use el [portal de seguimiento de documentos](https://track.azurerms.com/) para realizar el seguimiento cuando abran el &lt;nombre de tipo de documento de Office&gt; adjunto. Considere la posibilidad de ponerse en contacto por teléfono poco después de ver que han abierto el &lt;nombre de tipo de documento de Office&gt;.

**¿Necesita ayuda?**

-   Para obtener información adicional:

    -   [Proteger un archivo que comparte por correo electrónico](../rms-client/sharing-app-protect-by-email.md)

    -   [Realizar el seguimiento y revocar los documentos](../rms-client/sharing-app-track-revoke.md)

-   Póngase en contacto con el departamento de soporte técnico:

    -   *&lt;detalles de contacto&gt;*

### Documentación de usuario personalizada de ejemplo
![Documentación de usuario de ejemplo para la implementación rápida de Azure RMS](../media/AzRMS_ExampleBanner.png)

#### Cómo compartir una lista de precios con el cliente

1.  Cree el mensaje de correo electrónico especificando la dirección o direcciones de correo electrónico, escriba el mensaje y adjunte la lista de precios más reciente al mensaje de correo electrónico. A continuación, en la pestaña **MENSAJE** , en el grupo **RMS** , haga clic en **Compartir protegido** y después otra vez en **Compartir protegido** :

    ![Captura de pantalla sobre cómo compartir un documento de Office mediante Outlook](../media/AzRMSUserInstructions_ShareProtectedRibbon2013.png)

2.  En el cuadro de diálogo **compartir protegido** , seleccione **Visor: solo ver**:

    ![cuadro de diálogo uso compartido seguro, Visor: solo ver](../media/AzRMS_SharedProtected_ViewerOnly.PNG)

3.  Seleccione **Permítame revocar el acceso a estos documentos de forma instantánea**:

    ![cuadro de diálogo uso compartido seguro, revocar de forma instantánea](../media/AzRMS_SharedProtected_InstantRevoke.PNG)

4.  Seleccione **Enviarme un correo electrónico cuando alguien intente abrir estos documentos**:

    ![cuadro de diálogo uso compartido seguro, enviarme un correo electrónico](../media/AzRMS_SharedProtected_EmailMe.PNG)

5.  Haga clic en **Enviar ahora**.

Cuando alguien en las líneas **Para**, **CC**o **CCO** recibe este correo electrónico, ve un mensaje que le da las instrucciones de cómo leer la lista de precios adjunta. Se puede leer el documento en varios dispositivos, como tabletas y teléfonos iPad, iPhone y Android, equipos Mac y equipos Windows.

Utilice el [portal de seguimiento de documentos](https://track.azurerms.com/) para realizar el seguimiento cuando abran la lista de precios adjunta. Considere la posibilidad de ponerse en contacto por teléfono poco después de ver que ha abierto la lista de precios.

**¿Necesita ayuda?**

-   Para obtener información adicional:

    -   [Proteger un archivo que comparte por correo electrónico](../rms-client/sharing-app-protect-by-email.md)

    -   [Realizar el seguimiento y revocar los documentos](../rms-client/sharing-app-track-revoke.md)

-   Póngase en contacto con el departamento de soporte técnico:

    -   Correo electrónico: helpdesk@vanarsdelltd.com




<!--HONumber=Sep16_HO4-->


