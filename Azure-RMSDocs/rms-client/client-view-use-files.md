---
title: "Visualización y uso de documentos protegidos con el cliente AIP"
description: Instrucciones para ver y usar un documento protegido que requiere tener instalado el cliente de Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ce1c7d4c-b5ff-4672-8b9a-a72129bac992
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: a2eb82d81945793eb0b29d05ff8c6bd995481faf
ms.sourcegitcommit: 832d3ef5f9c41d6adb18a8cf5304f6048cc7252e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/24/2017
---
# <a name="user-guide-view-and-use-files-that-have-been-protected-by-rights-management"></a>Guía del usuario: Visualización y uso de archivos protegidos con Rights Management

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8 y Windows 7 con SP1*

A menudo, puede ver un documento protegido con tan solo abrirlo. Por ejemplo, podría hacer doble clic en los datos adjuntos de un mensaje de correo electrónico o en un archivo del Explorador de archivos, o podría hacer clic en un vínculo a un archivo.

Si los archivos no se abren automáticamente, es posible que el **Visor de Azure Information Protection** pueda abrirlo. Este visor puede abrir archivos de texto protegidos, archivos de imagen protegidos, archivos PDF protegidos y todos los archivos con una extensión de nombre de archivo **.pfile**.

El visor se instala automáticamente como parte del cliente de Azure Information Protection o puede instalarlo por separado. Puede instalar el cliente y el visor desde la página [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) en el sitio web de Microsoft. Para más información sobre cómo instalar el cliente, vea [Descarga e instalación del cliente de Azure Information Protection](install-client-app.md).

> [!NOTE]
> Aunque la instalación del cliente proporciona más funcionalidad, requiere permisos de administrador local y la funcionalidad completa requiere un servicio correspondiente para la organización:
> 
> - Azure Information Protection
> 
> - Azure Rights Management
> 
> - Active Directory Rights Management Services 
> 
> Instale el visor si alguien de otra organización le ha enviado un documento protegido o si no tiene permisos de administrador local para el equipo.

Para poder abrir un documento protegido, la aplicación debe estar "habilitada para RMS". Las aplicaciones de Office y el visor de Azure Information Protection son ejemplos de aplicaciones habilitadas para RMS. Para ver una lista de aplicaciones por tipo y dispositivos compatibles, consulte la tabla de [aplicaciones habilitadas para RMS](../get-started/requirements-applications.md#rms-enlightened-applications).  
## <a name="messagerpmsg-as-an-email-attachment"></a>Message.rpmsg como datos adjuntos de correo electrónico

Si ve **message.rpmsg** como un archivo adjunto en un correo electrónico, no se trata de un documento protegido sino un mensaje de correo electrónico protegido que se muestra como archivo adjunto. No puede usar el visor de Azure Information Protection para Windows para ver este mensaje de correo electrónico protegido en el equipo Windows. En su lugar, necesitará una aplicación de correo electrónico para Windows compatible con la protección de Rights Management, como Office Outlook. También puede usar Outlook en la Web.

Sin embargo, si tiene un dispositivo iOS o Android, puede usar la aplicación Azure Information Protection para abrir estos mensajes de correo electrónico protegidos. Puede descargar esta aplicación para estos dispositivos móviles desde la página [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) en el sitio web de Microsoft.

## <a name="prompts-for-authentication"></a>Solicitudes de autenticación

Para poder ver el archivo protegido, el servicio Rights Management utilizado para proteger el archivo primero debe confirmar que está autorizado para ver el archivo. Para ello, el servicio comprueba el nombre de usuario y la contraseña. En algunos casos, esto se puede almacenar en caché y no verá un mensaje que le solicite sus credenciales. En otros casos, se le pedirá que proporcione sus credenciales.

Si la organización no tiene una cuenta en la nube para que pueda usarla (para Office 365 o Azure) y no usa una versión local equivalente (AD RMS), tiene dos opciones:

- Si recibe un correo protegido, siga las instrucciones para iniciar sesión con su proveedor de identidades sociales (como Google para una cuenta de Gmail) o solicitar un código de acceso de un solo uso.

- Puede solicitar una cuenta gratuita que aceptará las credenciales para que pueda abrir documentos que estén protegidos por Rights Management. Para solicitar esta cuenta, haga clic en el vínculo para solicitar [RMS para usuarios](http://go.microsoft.com/fwlink/?LinkId=309469) y use la dirección de correo de su empresa en lugar de una dirección de correo personal. 

## <a name="to-view-and-use-a-protected-document"></a>Para ver y usar un documento protegido

1. Abra el archivo protegido (por ejemplo, al haciendo doble clic en el archivo o los datos adjuntos o haciendo clic en el vínculo al archivo). Si se le pide que seleccione una aplicación, seleccione **Visor de Azure Information Protection**. 

2. Si ve una página para **iniciar sesión** o **registrarse**: haga clic en **Iniciar sesión** y escriba sus credenciales. Si el archivo protegido se le envió como datos adjuntos, asegúrese de especificar la misma dirección de correo electrónico que la usada para enviar el archivo.
    
    Si no tiene una cuenta aceptable, vea la sección [Solicitudes de autenticación](#prompts-for-authentication) de esta página.

3. Se abre una versión de solo lectura del archivo en **Azure Information Protection Viewer**. Si tiene permisos suficientes, puede imprimir el archivo y modificarlo. 

    Puede comprobar los permisos del archivo haciendo clic en **Permisos**. En el cuadro de diálogo **Permisos**, también puede identificar el propietario del archivo al que acudir si quiere solicitar una nueva versión del archivo con permisos adicionales.
    
    Para más información sobre los permisos y los derechos de uso que contiene cada uno, consulte los [derechos incluidos en niveles de permisos](../deploy-use/configure-usage-rights.md#rights-included-in-permissions-levels).

4. Para editar el archivo, haga clic en **Guardar como**, que permite guardar el archivo sin protección con su extensión de nombre de archivo original. Luego puede editar el archivo mediante la aplicación que está asociada a ese tipo de archivo.

5. Si tiene archivos protegidos adicionales para abrir, puede ir directamente a ellos desde el visor, mediante la opción **Abrir**. El archivo seleccionado reemplaza al archivo original en el visor. 

> [!TIP]
> Si el archivo protegido no se abre, puede usar la opción **Ejecutar diagnósticos** desde **Proteger** > **Ayuda y comentarios** para comprobar si en el cliente de Azure Information Protection hay problemas que impidan abrir un documento protegido.

## <a name="other-instructions"></a>Otras instrucciones
Puede encontrar más instrucciones sobre procedimientos en la guía del usuario de Azure Information Protection:

-   [¿Qué desea hacer?](client-user-guide.md#what-do-you-want-to-do)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]