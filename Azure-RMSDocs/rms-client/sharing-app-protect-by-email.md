---
title: "Protección de un archivo que comparte por correo electrónico con la aplicación Rights Management sharing | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4c1cd1d3-78dd-4f90-8b37-dcc9205a6736
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: c611fa8a846612fed238e59e5077be67f6f9531a
ms.openlocfilehash: ea7f186e01606ca5e487bdfaab87d1eb0f2f41d3


---

# Protección de un archivo que comparte por correo electrónico con la aplicación Rights Management sharing

*Se aplica a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*

Cuando protege un archivo que comparte por correo electrónico, se crea una nueva versión del archivo original. El archivo original permanece sin protección y la nueva versión, que está protegida, se adjunta automáticamente a un correo electrónico que después envía.

En algunos casos (para los archivos creados con Microsoft Word, Excel y PowerPoint), la aplicación RMS sharing crea dos versiones del archivo que se adjunta al mensaje de correo electrónico. La segunda versión del archivo tiene la extensión de nombre de archivo **.ppdf** y es una instantánea en formato PDF del archivo. Esta versión del archivo garantiza que los destinatarios siempre puedan leer el archivo, incluso si no tienen instalada la misma aplicación que utilizó para crearlo. Esto suele ocurrir cuando las personas leen su correo electrónico en dispositivos móviles y quieren ver datos adjuntos del correo electrónico. Todo lo que necesitan para abrir el archivo es la aplicación RMS sharing. Así pueden leer el archivo adjunto, pero no podrán cambiarlo hasta que abran la otra versión del archivo con una aplicación que admita RMS.

Si su organización usa Azure RMS, puede hacer un seguimiento de los archivos que se protegen con la aplicación RMS sharing:

-   Seleccione una opción para recibir mensajes de correo electrónico cuando alguien intente abrir estos archivos adjuntos protegidos. Cada vez que se tenga acceso al archivo, se le notificará qué usuarios intentaron abrir el archivo, cuándo y si se autenticaron correctamente o no.

-   Utilice el sitio de seguimiento de documentos. Incluso puede dejar de compartir el archivo. Para ello, revoque el acceso a él en el sitio de seguimiento de documentos. Para más información, consulte [Seguimiento y revocación de documentos cuando se usa la aplicación RMS sharing](sharing-app-track-revoke.md).

## Con Outlook: Para proteger un archivo que comparte por correo electrónico

1.  Cree su mensaje de correo electrónico y adjunte el archivo. A continuación, en la pestaña **Mensaje** , en el grupo **RMS** , haga clic en **Compartir protegido** y después otra vez en **Compartir protegido** :

    ![Complemento de Outlook para la aplicación de uso compartido de RMS](../media/ADRMS_MSRMSApp_SP_OutlookToolbar.png)

    Si no ve este botón, es probable que la aplicación RMS sharing no esté instalada en el equipo, que no esté instalada la versión más reciente o que el equipo deba reiniciarse para completar la instalación. Para más información sobre cómo instalar la aplicación de uso compartido, consulte [Descarga e instalación de la aplicación Rights Management sharing](install-sharing-app.md).

2.  Especifique las opciones que desee para este archivo en el cuadro de diálogo [Uso compartido seguro](sharing-app-dialog-box.md) y haga clic en **Enviar ahora**.

### Otras formas de proteger un archivo que comparte por correo electrónico
Además de compartir un archivo protegido con Outlook, también puede utilizar estas alternativas:

-   Desde el Explorador de archivos: Este método funciona para todos los archivos.

-   Desde una aplicación de Office: Este método funciona para las aplicaciones compatibles con la aplicación RMS sharing mediante el complemento de Office, para que se vea el grupo **RMS** en la cinta.

#### Con el Explorador de archivos o una aplicación de Office: Para proteger un archivo que comparte por correo electrónico

1.  Utilice una de las siguientes opciones:

    -   En el Explorador de archivos: Haga clic con el botón derecho en el archivo, seleccione **Proteger con RMS** y, luego, **Uso compartido seguro**.

        ![Opción de menú Uso compartido seguro](../media/ADRMS_MSRMSApp_ShareProtectedMenu.png)

    -   Para las aplicaciones de Office, Word, Excel y PowerPoint: Asegúrese de que ha guardado antes el archivo. A continuación, en la pestaña **Inicio** , en el grupo **RMS** , haga clic en **Compartir protegido** y de nuevo en **Compartir protegido** :

        ![Complemento de barra de herramientas de Office](../media/ADRMS_MSRMSApp_SP_OfficeToolbar.png)

    Si no ve estas opciones para la protección, es probable que la aplicación RMS sharing no esté instalada en el equipo, que no esté instalada la versión más reciente o que el equipo deba reiniciarse para completar la instalación. Para más información sobre cómo instalar la aplicación de uso compartido, consulte [Descarga e instalación de la aplicación Rights Management sharing](install-sharing-app.md).

2.  Especifique las opciones que desee para este archivo en el cuadro de diálogo [Uso compartido seguro](sharing-app-dialog-box.md) y haga clic en **Enviar**.

3.  Quizá vea un cuadro de dialogo rápido donde se indica que se está protegiendo el archivo y, a continuación, verá un mensaje de correo electrónico creado para usted que indica a los destinatarios que los datos adjuntos están protegidos con Microsoft RMS y que deben iniciar sesión. Cuando hagan clic en el vínculo para iniciar sesión, verán instrucciones y vínculos para garantizar que puedan abrir los datos adjuntos protegidos.

    Ejemplo:

    ![Mensaje de correo electrónico para Azure RMS](../media/ADRMS_MSRMSApp_EmailMessage.PNG)

    Probablemente se esté preguntando: [¿Qué es el archivo .ppdf que se crea automáticamente?](sharing-app-dialog-box.md#what-s-the-ppdf-file-that-s-automatically-created-)

4.  Opcional: Puede cambiar cualquier cosa que desee en este mensaje de correo electrónico. Por ejemplo, puede agregar o cambiar el asunto o el texto del mensaje.

    > [!WARNING]
    > Aunque puede agregar o quitar usuarios de este mensaje de correo electrónico, esto no cambia los permisos para los datos adjuntos que especificó en el cuadro de diálogo **Agregar protegido** . Si desea cambiar los permisos (por ejemplo, conceder permisos para abrir el archivo), cierre el mensaje de correo electrónico sin guardarlo ni enviarlo y vuelva al paso 1.

5.  Envíe el mensaje de correo electrónico.

## Ejemplos y otras instrucciones
Para obtener ejemplos de cómo puede usar la aplicación para uso compartido de Rights Management e instrucciones de procedimientos, consulte las siguientes secciones de la guía de usuario de la aplicación para uso compartido de Rights Management:

-   [Ejemplos de uso de la aplicación RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [¿Qué desea hacer?](sharing-app-user-guide.md#what-do-you-want-to-do-)

## Véase también
[Guía de usuario de la aplicación de uso compartido Rights Management](sharing-app-user-guide.md)



<!--HONumber=Jun16_HO4-->


