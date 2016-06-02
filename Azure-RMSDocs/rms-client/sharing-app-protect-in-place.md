---
# required metadata

title: Protección de un archivo en un dispositivo (proteger en contexto) mediante la aplicación Rights Management sharing | Azure RM
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 33920329-5247-4f6c-8651-6227afb4a1fa

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Proteger un archivo en un dispositivo (proteger en contexto) mediante la aplicación para uso compartido de Rights Management.

*Se aplica a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*

Cuando se protege un archivo en contexto, se reemplaza el archivo sin protección original. A continuación, puede dejar el archivo donde se encuentra, copiarlo a otra carpeta o dispositivo, o compartir la carpeta en la que se encuentra, ya que el archivo seguirá estando protegido. También puede adjuntar el archivo protegido a un mensaje de correo electrónico, aunque la forma recomendada de compartir un archivo protegido por correo electrónico es hacerlo directamente desde el Explorador de archivos o desde una aplicación de Office (consulte [Protect a file that you share by email by using the Rights Management sharing application](sharing-app-protect-by-email.md) [Protección de un archivo que comparte por correo electrónico con la aplicación Rights Management sharing]).).

> [!TIP]
> Si ve errores al intentar proteger archivos, consulte las [FAQ for Microsoft Rights Management Sharing Application for Windows](http://go.microsoft.com/fwlink/?LinkId=303971) (Preguntas más frecuentes sobre la aplicación Microsoft Rights Management sharing para Windows)..

## Para proteger un archivo en un dispositivo (proteger en contexto)

1.  En el Explorador de archivos, seleccione el archivo que desea proteger. Haga clic con el botón derecho, seleccione **Proteger con RMS** y luego **Proteger en contexto**. Por ejemplo:

    ![Opción de menú Proteger en contexto](../media/ADRMS_MSRMSApp_SP_CompanyDefined.png)

    > [!NOTE]
    > Si no ve la opción **Proteger con RMS** , es probable que la aplicación de uso compartido de RMS no está instalada en el equipo o que deba reiniciar el equipo para completar la instalación. Para obtener más información sobre cómo instalar la aplicación RMS sharing, consulte [Download and install the Rights Management sharing application](install-sharing-app.md) (Descarga e instalación de la aplicación Rights Management sharing)..

2.  Realice una de las siguientes acciones:

    -   Seleccione una plantilla de directiva: se trata de permisos predefinidos que normalmente restringen el acceso y el uso a las personas de su organización. Por ejemplo, si el nombre de la organización es "Contoso, Ltd", es posible que vea **Contoso, Ltd - Solo vista confidencial**. Si es la primera vez que protege un archivo en este equipo, tiene que seleccionar antes **Protección definida por la compañía** para descargar las plantillas.

        La próxima vez que haga clic en la opción **Proteger en contexto**, verá hasta 10 plantillas entre las que elegir. Si hay más de 10 plantillas disponibles y la que desea no aparece, haga clic en **Protección definida por la compañía** para descargar y ver todas las plantillas.

        Al seleccionar una plantilla de directiva, también puede proteger varios archivos y una carpeta. Cuando se selecciona una carpeta, todos los archivos de esa carpeta se seleccionan automáticamente para protegerlos, pero los archivos nuevos que cree en esa carpeta no estará automáticamente protegidos.

    -   Seleccione **Permisos personalizados**: elija esta opción si las plantillas no proporcionan el nivel de protección que necesita o si desea establecer explícitamente las opciones de protección. Especifique las opciones que quiera para este archivo en el cuadro de diálogo [Agregar protección](sharing-app-dialog-box.md) y haga clic en **Aplicar**..

3.  Es probable que vea rápidamente un cuadro de diálogo que le indica que el archivo se está protegiendo y, a continuación, regrese al Explorador de archivos. El archivo o archivos seleccionados ahora están protegidos. En algunos casos (cuando al agregar la protección cambia la extensión de nombre de archivo), el archivo original del Explorador de archivos se reemplaza con un archivo nuevo que tiene el icono de bloqueo de protección de Rights Management. Por ejemplo:

    ![Proteger el archivo con el icono de bloqueo para la aplicación RMS sharing](../media/ADRMS_MSRMSApp_Pfile.png)

Si posteriormente tiene que quitar la protección de un archivo, consulte [Remove protection from a file by using the Rights Management sharing application](sharing-app-remove-protection.md) (Quitar la protección de un archivo mediante la aplicación Rights Management sharing)..

## Ejemplos y otras instrucciones
Para obtener ejemplos de cómo puede usar la aplicación para uso compartido de Rights Management e instrucciones de procedimientos, consulte las siguientes secciones de la guía de usuario de la aplicación para uso compartido de Rights Management:

-   [Ejemplos de uso de la aplicación RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [¿Qué desea hacer?](sharing-app-user-guide.md#what-do-you-want-to-do-)

## Véase también
[Guía de usuario de la aplicación de uso compartido Rights Management](sharing-app-user-guide.md)


<!--HONumber=May16_HO2-->


