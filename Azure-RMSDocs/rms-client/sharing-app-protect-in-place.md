---
title: Protección en contexto mediante la aplicación RMS sharing - AIP
description: Instrucciones sobre cómo almacenar un archivo de forma segura en un equipo, un servidor u otro dispositivo de almacenamiento.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 33920329-5247-4f6c-8651-6227afb4a1fa
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 9156f7af9cb7915595f911b6d0ff8fa70332d8d7
ms.sourcegitcommit: d06594550e7ff94b4098a2aa379ef2b19bc6123d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/07/2018
ms.locfileid: "53023454"
---
# <a name="protect-a-file-on-a-device-protect-in-place-by-using-the-rights-management-sharing-application"></a>Proteger un archivo en un dispositivo (proteger en contexto) mediante la aplicación para uso compartido de Rights Management.

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 7 con SP1, Windows 8 y Windows 8.1*

Cuando se protege un archivo en contexto, se reemplaza el archivo sin protección original. A continuación, puede dejar el archivo donde se encuentra, copiarlo a otra carpeta o dispositivo, o compartir la carpeta en la que se encuentra, ya que el archivo seguirá estando protegido. También puede adjuntar el archivo protegido a un mensaje de correo electrónico, aunque la forma recomendada de compartir un archivo protegido por correo electrónico es hacerlo directamente desde el Explorador de archivos o desde una aplicación de Office (consulte [Protección de un archivo que comparte por correo electrónico con la aplicación Rights Management sharing](sharing-app-protect-by-email.md)).

> [!TIP]
> Si ve errores al intentar proteger archivos, consulte las [Preguntas más frecuentes sobre la aplicación para uso compartido de Microsoft Rights Management para Windows](https://go.microsoft.com/fwlink/?LinkId=303971).

## <a name="to-protect-a-file-on-a-device-protect-in-place"></a>Para proteger un archivo en un dispositivo (proteger en contexto)

1.  En el Explorador de archivos, seleccione el archivo que desea proteger. Haga clic con el botón derecho, seleccione **Proteger con RMS** y luego **Proteger en contexto**. Por ejemplo:

    ![Opción de menú Proteger en contexto](../media/ADRMS_MSRMSApp_SP_CompanyDefined.png)

    > [!NOTE]
    > Si no ve la opción **Proteger con RMS** , es probable que la aplicación de uso compartido de RMS no está instalada en el equipo o que deba reiniciar el equipo para completar la instalación. Para más información sobre cómo instalar la aplicación RMS sharing, consulte [Descarga e instalación de la aplicación Rights Management sharing](install-sharing-app.md).

2.  Realice una de las siguientes acciones:

    -   Seleccione una plantilla de directiva: se trata de permisos predefinidos que normalmente restringen el acceso y el uso a las personas de su organización. Por ejemplo, si el nombre de la organización es "Contoso, Ltd", es posible que vea **Contoso, Ltd - Solo vista confidencial**. Si es la primera vez que protege un archivo en este equipo, tiene que seleccionar antes **Protección definida por la compañía** para descargar las plantillas.

        La próxima vez que haga clic en la opción **Proteger en contexto**, verá hasta 10 plantillas entre las que elegir. Si hay más de 10 plantillas disponibles y la que desea no aparece, haga clic en **Protección definida por la compañía** para descargar y ver todas las plantillas.

        Al seleccionar una plantilla de directiva, también puede proteger varios archivos y una carpeta. Cuando se selecciona una carpeta, todos los archivos de esa carpeta se seleccionan automáticamente para protegerlos, pero los archivos nuevos que cree en esa carpeta no estará automáticamente protegidos.

    -   Seleccione **Permisos personalizados**: elija esta opción si las plantillas no proporcionan el nivel de protección que necesita o si desea establecer explícitamente las opciones de protección. Especifique las opciones que quiera para este archivo en el cuadro de diálogo [Agregar protección](sharing-app-dialog-box.md) y haga clic en **Aplicar**.

3.  Es probable que vea rápidamente un cuadro de diálogo que le indica que el archivo se está protegiendo y, a continuación, regrese al Explorador de archivos. El archivo o archivos seleccionados ahora están protegidos. En algunos casos (cuando al agregar la protección cambia la extensión de nombre de archivo), el archivo original del Explorador de archivos se reemplaza con un archivo nuevo que tiene el icono de bloqueo de protección de Rights Management. Por ejemplo:

    ![Proteger el archivo con el icono de bloqueo para la aplicación RMS sharing](../media/ADRMS_MSRMSApp_Pfile.png)

Si cambia de opinión en cuanto a los permisos o necesita modificarlos más adelante, lo único que tiene que hacer es volver a proteger el archivo.

Si posteriormente tiene que quitar la protección de un archivo, consulte [Quitar la protección de un archivo mediante la aplicación Rights Management sharing](sharing-app-remove-protection.md).

## <a name="examples-and-other-instructions"></a>Ejemplos y otras instrucciones
Para obtener ejemplos de cómo puede usar la aplicación para uso compartido de Rights Management e instrucciones de procedimientos, consulte las siguientes secciones de la guía de usuario de la aplicación para uso compartido de Rights Management:

-   [Ejemplos de uso de la aplicación RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [¿Qué desea hacer?](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>Consulte también
[Guía de usuario de la aplicación Rights Management sharing](sharing-app-user-guide.md)
