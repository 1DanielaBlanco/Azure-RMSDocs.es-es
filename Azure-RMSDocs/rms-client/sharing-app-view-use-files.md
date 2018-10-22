---
title: Apertura de archivos protegidos con RMS con la aplicación RMS sharing - AIP
description: Instrucciones para ver y usar un archivo protegido, que requiere que tenga la aplicación Rights Management (RMS) sharing instalada.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/18/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: e5fa4666-6906-405a-9e0c-2c52d4cd27c8
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 27de9df7062f6072e7e15b66759f540d5ce81dba
ms.sourcegitcommit: 26a2c1becdf3e3145dc1168f5ea8492f2e1ff2f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2018
ms.locfileid: "44148059"
---
# <a name="view-and-use-files-that-have-been-protected-by-rights-management"></a>Ver y usar los archivos protegidos por Rights Management

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 7 con SP1, Windows 8 y Windows 8.1*

Cuando la [aplicación Rights Management sharing (RMS) está instalada en el equipo](install-sharing-app.md), puede ver un archivo protegido simplemente haciendo doble clic en él. El archivo puede ser un archivo adjunto en un mensaje de correo electrónico, o podría verlo al usar el Explorador de archivos.

> [!NOTE]
> Para ver el archivo protegido, el servicio Rights Management necesita confirmar primero que está autorizado para ver el archivo (para hacerlo, comprobará su nombre de usuario y contraseña). En algunos casos, esto se puede almacenar en caché y no verá un mensaje que le solicite sus credenciales. En otros casos, se le pedirá que proporcione sus credenciales.
>
> Si su organización no usa Azure Information Protection o AD RMS, puede pedir una cuenta gratuita que acepte sus credenciales para poder abrir los archivos protegidos con RMS:
>
> -   Para solicitar esta cuenta, haga clic en el vínculo para solicitar [RMS para usuarios](http://go.microsoft.com/fwlink/?LinkId=309469).
>
>     Al suscribirse, use la dirección de correo electrónico de su empresa en lugar de una dirección de correo electrónico personal. Si va a suscribirse porque le enviaron un archivo adjunto protegido por correo electrónico, use la misma dirección de correo electrónico que se usó para enviarle el mensaje de correo electrónico.
> -   Para obtener más información, consulte [RMS for individuals and Azure Rights Management](../rms-for-individuals.md) (RMS para usuarios y Azure Rights Management).

## <a name="to-view-a-protected-file"></a>Para ver un archivo protegido
Usando el Explorador de archivos o el mensaje de correo electrónico que contiene el archivo adjunto, haga doble clic en el archivo protegido y escriba sus credenciales si se le solicita que lo haga.

Si ve dos versiones del archivo pero con extensiones de nombre de archivo diferentes, abra el archivo que tiene una extensión de archivo .ppdf únicamente si el otro archivo no se abre. Si tampoco puede abrir la versión .ppdf, instale primero la [aplicación RMS sharing](install-sharing-app.md), que sabe cómo abrir los archivos que tienen una extensión de nombre de archivo .ppdf.

> [!NOTE]
> Para obtener más información, consulte [¿Qué es el archivo .ppdf que se crea automáticamente?](sharing-app-dialog-box.md#whats-the-ppdf-file-thats-automatically-created)

La manera en que se abre el archivo depende de cómo se protegió, lo que se puede saber por la extensión de nombre de archivo. En cualquier caso, el proceso de abrir el archivo podría auditarse, y sigue auditándose mientras esté protegido. Además, si el archivo se envió como un archivo adjunto por correo electrónico, es posible que el remitente reciba una notificación por correo electrónico cada vez que abra el archivo.

- **El archivo tiene una *.pfile* extensión de nombre de archivo**

    El archivo se protegió de forma genérica.

    Al abrir el archivo, verá el cuadro de diálogo **archivo protegido** de la aplicación de uso compartido que indica la persona que protegió el archivo y que se espera que respete los permisos de copropietario. Haga clic en **Abrir** para leer el archivo.

    ![Cuadro de diálogo de un archivo pfile compartido por correo electrónico cuando se usa la aplicación RMS sharing](../media/ADRMS_MSRMSApp_PfilePermission.png)

- **El archivo tiene una extensión de nombre de archivo *.ppdf* o es un archivo de imagen o texto protegido (como *.ptxt* o *.pjpg*)**

    El archivo se protegió de forma nativa como una copia de solo lectura.

    El archivo se abre mediante el visor que se instala con la aplicación para uso compartido de RMS. Este archivo es de solo lectura, aunque lo guarde en otra ubicación o le cambie el nombre.

- **Otras extensiones de nombre de archivo**

    El archivo se protegió de forma nativa.

    El archivo se abre con la aplicación que está asociada con la extensión de nombre de archivo original y se muestra una pancarta de restricción en la parte superior del archivo. La pancarta puede mostrar los permisos que se aplican al archivo o puede proporcionar un vínculo para mostrarlos. Por ejemplo, podría ver lo siguiente, donde debe hacer clic en **El permiso está restringido actualmente** para ver los permisos reales que se aplican al archivo y a las personas que pueden tener acceso a él:

    ![Banner de acceso restringido cuando el archivo está protegido](../media/ADRMS_MSRMSApp_RestrictedAccess.png)



Para obtener la lista completa de extensiones de nombres de archivo que admiten los servicios de Rights Management, vea las secciones [Tipos de archivo y extensiones de nombre de archivo admitidos](sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions) de la [Guía del administrador de la aplicación Rights Management sharing](sharing-app-admin-guide.md). Si su extensión de nombre de archivo no se incluye, realice una búsqueda web para ver si es una extensión de nombre de archivo admitida por otra aplicación.

## <a name="to-use-files-that-have-been-protected-for-example-edit-and-print-the-file"></a>Para usar archivos que están protegidos (por ejemplo, editar e imprimir el archivo)
Si, tras abrir el archivo protegido, desea hacer algo más que simplemente leerlo (como editarlo, copiarlo e imprimirlo), siga las instrucciones correspondientes a la extensión de nombre de archivo :

- **El archivo tiene una extensión de nombre de archivo *.pfile*** 

    Guarde el archivo abierto y asígnele una nueva extensión de nombre de archivo que esté asociada a la aplicación que desea usar.

    Por ejemplo, si un archivo se protegió con el nombre de archivo document.vsdx.pfile, visualice el archivo y, en el Explorador de archivos, guárdelo como document.vsdx.

    El nuevo archivo ya no está protegido. Si desea protegerlo, debe hacerlo manualmente. Para obtener instrucciones, consulte [Protección de un archivo en un dispositivo (proteger en contexto) mediante la aplicación Rights Management sharing](sharing-app-protect-in-place.md).

- **El archivo tiene una extensión de nombre de archivo *.ppdf* o es un archivo de imagen o texto protegido (como *.ptxt* o *.pjpg*)**

    Solo puede ver el archivo, y si le cambia el nombre o si lo mueve, el archivo sigue estando protegido.

- **Otras extensiones de nombre de archivo**

    Para poder usar estos archivos, el dispositivo necesita usar una aplicación que entienda la protección de Rights Management. Estas aplicaciones se denominan aplicaciones habilitadas para RMS. Las aplicaciones de Office 2016, Office 2013 y Office 2010 (como Word, Excel, PowerPoint y Outlook) son ejemplos de aplicaciones que están habilitadas para Rights Management. Sin embargo, las aplicaciones que no proceden de Microsoft, como las de otras empresas de software y sus propias aplicaciones de línea de negocio, también podrían estar habilitadas para Rights Management.

    Las aplicaciones que están habilitadas para Rights Management saben cómo abrir los archivos que se protegieron mediante otras aplicaciones habilitadas para Rights Management. Además, conservan la protección que tenían aplicada, aun cuando modifique el archivo o lo guarde con otro nombre de archivo o en otra ubicación. Estas aplicaciones permiten usar el archivo según los permisos que tenga aplicados actualmente, por lo que si tiene permisos para usar el archivo, puede hacerlo. Por ejemplo, es posible que pueda editar el archivo pero no imprimirlo.


## <a name="examples-and-other-instructions"></a>Ejemplos y otras instrucciones
Para obtener ejemplos de cómo puede usar la aplicación para uso compartido de Rights Management e instrucciones de procedimientos, consulte las siguientes secciones de la guía de usuario de la aplicación para uso compartido de Rights Management:

-   [Ejemplos de uso de la aplicación RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [¿Qué desea hacer?](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>Consulte también
[Guía de usuario de la aplicación Rights Management sharing](sharing-app-user-guide.md)
