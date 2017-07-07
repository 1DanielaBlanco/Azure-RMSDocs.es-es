---
title: Cambio de los permisos en archivos protegidos por RMS - AIP
description: "Cuando un archivo está protegido por Rights Management, puede cambiar los permisos protegiéndolo de nuevo y especificando todos los usuarios que deben tener acceso a él y los permisos que quiere otorgarles."
keywords: 
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5ac121b3-d7a0-40e4-8fe7-90bf4cf796f1
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 3290b9436f75c2d0d37c401dd2e0be11bcf2d554
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2017
---
# <a name="change-permissions-on-files-that-have-been-protected-by-rights-management"></a>Change permissions on files that have been protected by Rights Management (Cambiar permisos de archivos protegidos por Rights Management)

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 7 con SP1, Windows 8 y Windows 8.1*

Cuando un archivo está protegido por Rights Management, puede cambiar los permisos protegiéndolo de nuevo y especificando todos los usuarios que deben tener acceso a él y los permisos que quiere otorgarles.

> [!IMPORTANT]
> No se trata de un cambio incremental, sino de un reemplazo completo. Está protegiendo de nuevo el archivo con el conjunto completo de permisos que quiera.
> 
>  Por ejemplo, si un archivo está protegido de forma que solo los usuarios del departamento de marketing pueden abrirlo y quiere que los usuarios del departamento de ventas también tengan acceso a él, debe volver a protegerlo para que ambos departamentos puedan abrirlo.
>
> De forma similar, si quiere agregar o quitar un permiso, no puede especificar solo ese permiso para agregarlo o quitarlo, sino que debe especificar todos los permisos que deben tener los usuarios especificados.

Si es el propietario del archivo que quiere volver a proteger (por ejemplo, lo ha protegido con la aplicación RMS sharing), obtendrá permisos de forma automática para volver a proteger el archivo. Si no es el propietario, puede que tenga permisos o no para volver a proteger el archivo, en función de los permisos que tenga actualmente el archivo protegido. Para volver a proteger un archivo, se necesita el [derecho de uso de Control total](../deploy-use/configure-usage-rights.md#usage-rights-and-descriptions) .

Por ejemplo, si otro usuario protegió el archivo mediante la aplicación Rights Management sharing y especificó un grupo al que usted pertenece y **Copropietario** como permiso personalizado, podrá volver a proteger el archivo. Pero si dicho usuario no especificó su nombre o un grupo al que usted pertenece, o bien si seleccionó **Revisor – Ver y editar** o una plantilla que no le permite quitar los permisos, no podrá volver a proteger el archivo. La manera más sencilla de averiguarlo es intentando proteger el archivo de nuevo.

Si quiere quitar todos los permisos para que el archivo ya no está protegido, vea [Quitar la protección de un archivo](sharing-app-remove-protection.md).

## <a name="to-re-protect-a-file-in-place"></a>Para volver a proteger un archivo local

1.  En el Explorador de archivos, seleccione el archivo que desea proteger. Haga clic con el botón derecho, seleccione **Proteger con RMS** y luego **Proteger en contexto**. Por ejemplo:

    ![Opción de menú Proteger en contexto](../media/ADRMS_MSRMSApp_SP_CompanyDefined.png)

    > [!NOTE]
    > Si no ve la opción **Proteger con RMS** , es probable que la aplicación de uso compartido de RMS no está instalada en el equipo o que deba reiniciar el equipo para completar la instalación. Para más información sobre cómo instalar la aplicación RMS sharing, consulte [Descarga e instalación de la aplicación Rights Management sharing](install-sharing-app.md).

2.  Realice una de las siguientes acciones:

    -   Seleccione una plantilla de directiva: se trata de permisos predefinidos que normalmente restringen el acceso y el uso a las personas de su organización. Por ejemplo, si el nombre de la organización es "Contoso, Ltd", es posible que vea **Contoso, Ltd - Solo vista confidencial**. Si es la primera vez que protege un archivo en este equipo, tiene que seleccionar antes **Protección definida por la compañía** para descargar las plantillas.

        La próxima vez que haga clic en la opción **Proteger en contexto**, verá hasta 10 plantillas entre las que elegir. Si hay más de 10 plantillas disponibles y la que desea no aparece, haga clic en **Protección definida por la compañía** para descargar y ver todas las plantillas.

        Al seleccionar una plantilla de directiva, también puede proteger varios archivos y una carpeta. Cuando se selecciona una carpeta, todos los archivos de esa carpeta se seleccionan automáticamente para protegerlos, pero los archivos nuevos que cree en esa carpeta no estará automáticamente protegidos.

    -   Seleccione **Permisos personalizados**: elija esta opción si las plantillas no proporcionan el nivel de protección que necesita o si desea establecer explícitamente las opciones de protección. Especifique las opciones que quiera para este archivo en el cuadro de diálogo [Agregar protección](sharing-app-dialog-box.md) y haga clic en **Aplicar**.

3. Si no tiene permisos para volver a proteger el archivo, verá el mensaje **Unable to protect content** (No se puede proteger el contenido) con la dirección de correo electrónico de la persona de contacto (el propietario del documento) para que le cambie los permisos.

    En caso de tener permisos para volver a proteger el archivo, es probable que vea un cuadro de diálogo en el que se le indica que el archivo se está protegiendo y, después, regrese al Explorador de archivos. El archivo o archivos seleccionados ahora están protegidos con sus cambios. 

> [!NOTE]
> Para poder volver a proteger el archivo, el servicio Rights Management debe confirmar primero que está autorizado para llevar a cabo esta acción sobre este archivo. Para ello, comprobará su nombre de usuario y contraseña. En algunos casos, esto se puede almacenar en caché y no verá un mensaje que le solicite sus credenciales. En otros casos, se le pedirá que proporcione sus credenciales.
>
> Si su organización no usa Azure Information Protection ni AD RMS, puede solicitar una cuenta gratuita que acepte sus credenciales para que pueda usar los archivos protegidos mediante RMS:
>
> -   Para solicitar esta cuenta, haga clic en el vínculo para solicitar [RMS para usuarios](http://go.microsoft.com/fwlink/?LinkId=309469).
>
>     Al suscribirse, use la dirección de correo electrónico de su empresa en lugar de una dirección de correo electrónico personal. Si va a suscribirse porque le enviaron un archivo adjunto protegido por correo electrónico, use la misma dirección de correo electrónico que se usó para enviarle el mensaje de correo electrónico.
> -   Para obtener más información, consulte [RMS for individuals and Azure Rights Management](../understand-explore/rms-for-individuals.md) (RMS para usuarios y Azure Rights Management).

## <a name="to-re-protect-a-file-that-you-have-emailed"></a>Para volver a proteger un archivo que ha enviado por correo electrónico

Si quiere cambiar los permisos de un archivo que ha enviado por correo electrónico:

- **Para que más usuarios puedan leer el archivo**: envíeles el archivo por correo electrónico siguiendo las instrucciones de [Protección de un archivo que comparte por correo electrónico](sharing-app-protect-by-email.md).

- **Para cambiar los permisos del archivo**: vuelva a enviar el archivo por correo electrónico siguiendo las instrucciones de [Protección de un archivo que comparte por correo electrónico](sharing-app-protect-by-email.md) y elija los nuevos permisos que quiera. 

    Dado que no se pueden quitar los permisos anteriores del archivo enviado por correo electrónico, solo reemplazarlos por una versión nueva, considere la posibilidad de revocar el archivo enviado anteriormente para que los destinatarios ya no puedan abrir dicha versión del documento. La revocación es idónea si tiene que restringir los permisos (por ejemplo, quitar usuarios que no deben tener acceso al archivo o que ya no deberían poder editarlo).

    Para revocar un archivo enviado por correo electrónico, vea [Seguimiento y revocación de documentos cuando se utiliza la aplicación RMS sharing](sharing-app-track-revoke.md).


## <a name="examples-and-other-instructions"></a>Ejemplos y otras instrucciones
Para obtener ejemplos de cómo puede usar la aplicación para uso compartido de Rights Management e instrucciones de procedimientos, consulte las siguientes secciones de la guía de usuario de la aplicación para uso compartido de Rights Management:

-   [Ejemplos de uso de la aplicación RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [¿Qué desea hacer?](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>Véase también
[Guía de usuario de la aplicación Rights Management sharing](sharing-app-user-guide.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]