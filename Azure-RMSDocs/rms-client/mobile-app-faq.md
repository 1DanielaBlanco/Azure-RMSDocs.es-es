---
title: "Preguntas más frecuentes sobre la aplicación de Azure Information Protection para iOS y Android | Azure Information Protection"
description: 
keywords: "Algunas preguntas frecuentes para ayudarle a usar la aplicación de Azure Information Protection para iOS y Android"
author: cabailey
manager: mbaldwin
ms.date: 11/03/2016
ms.topic: article
ms.prod: azure
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 539b4ff8-5d3b-4c4d-9c84-c14da83ff76d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2f1930f4657278d25ef6dd369866f16e4ba71644
ms.openlocfilehash: 1cafa88ded2bf951f8af93e4b27cc526735d19e8


---

# <a name="faqs-for-microsoft-azure-information-protection-app-for-ios-and-android"></a>Preguntas más frecuentes sobre la aplicación de Microsoft Azure Information Protection para iOS y Android

*Se aplica a: Active Directory Rights Management Services, Azure Information Protection*

En esta página se proporcionan respuestas a preguntas frecuentes sobre la aplicación de Azure Information Protection para iOS y Android.

## <a name="what-can-i-do-with-the-azure-information-protection-app"></a>¿Qué puedo hacer con la aplicación de Azure Information Protection?

Esta aplicación le permite ver mensajes de correo electrónico protegidos por derechos (archivos .rpmsg) si su aplicación de correo electrónico no admite de forma nativa la protección de datos de Rights Management. Esta aplicación también le permite ver archivos PDF protegidos por derechos, así como imágenes y archivos de texto protegidos por derechos. Actualmente, no puede usar esta aplicación para crear mensajes de correo electrónico protegidos, responder a ellos, o crear o editar archivos protegidos.

## <a name="can-i-open-pdf-files-that-are-in-sharepoint-protected-libraries-and-onedrive-for-business"></a>¿Puedo abrir archivos PDF que están en bibliotecas protegidas de SharePoint y en OneDrive para la Empresa?

Sí, puede abrir archivos PDF protegidos que otros usuarios han compartido con usted mediante SharePoint y OneDrive para la Empresa. Pulse el vínculo y elija esta aplicación para abrir el archivo automáticamente. 

## <a name="how-do-i-get-started-with-the-viewer-app"></a>¿Cómo puedo empezar a usar la aplicación de visor?

Debe acceder desde su dispositivo móvil a uno de los archivos que admite la aplicación para ver el visor en acción. Por ejemplo:

- **Un archivo .rpmsg**: se trata de un mensaje de correo electrónico protegido por derechos que se muestra como un archivo adjunto en un mensaje de correo electrónico cuando la aplicación de correo electrónico de su dispositivo móvil no admite de forma nativa la protección de datos de Rights Management. 
    
    Use otro dispositivo para enviarse a usted mismo un mensaje de correo electrónico protegido por derechos al que pueda acceder desde su dispositivo móvil. Por ejemplo, use Outlook en un equipo Windows. Para ver una lista de clientes de correo electrónico que admiten de forma nativa Rights Management, vea la columna CORREO ELECTRÓNICO de la página [Aplicaciones compatibles con la protección de datos de Azure Rights Management](../get-started/requirements-applications.md).

- **Un archivo PDF protegido por derechos**: use la aplicación para uso compartido de Rights Management en un equipo Windows o una aplicación de PDF que admita de forma nativa Rights Management para enviarse a usted mismo un archivo PDF protegido por derechos como un archivo adjunto en un correo electrónico. También puede cargar un archivo PDF en una biblioteca protegida de SharePoint y, después, compartirlo mediante su dirección de correo electrónico.

- **Un archivo .ptxt, .pjpg o .ppng**: use la aplicación para uso compartido de Rights Management en un equipo Windows y la opción [Uso compartido seguro](sharing-app-protect-by-email.md) para enviarse a usted mismo un archivo protegido como un archivo adjunto de correo electrónico. Para ver la lista completa de tipos de archivo que puede usar para realizar pruebas, consulte la primera tabla de la sección [Tipos de archivo y extensiones de nombre de archivo admitidos](sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions) de la guía del administrador de la aplicación para uso compartido de Rights Management. 

Para ver estos archivos en la aplicación de visor de Azure Information Protection, pulse el vínculo o el archivo adjunto del correo electrónico. Cuando se le pida que seleccione una aplicación para abrirlo, seleccione la aplicación **Visor AIP**. Se le pedirá que inicie sesión en su cuenta profesional o educativa. Una vez que se haya autenticado correctamente, la aplicación Azure Information Protection le muestra el correo electrónico o el archivo para que lo lea.

## <a name="what-credentials-should-i-use-to-sign-in-to-this-app"></a>¿Qué credenciales debo usar para iniciar sesión en esta aplicación?

Si su organización ya tiene AD RMS local (con la extensión de dispositivos móviles) o usa el servicio Azure Rights Management, puede usar sus credenciales para iniciar sesión. Si no, puede registrarse para obtener una nueva cuenta gratuita en la [página de Azure Information Protection](https://portal.office.com/signup?sku=rms&ru=https%3A%2F%2Fportal.azurerms.com%2F%23%2Fdownload).

## <a name="can-i-sign-up-for-the-free-account-with-my-personal-email-address-such-as-a-hotmail-or-gmail-account"></a>¿Puedo registrarme para obtener una cuenta gratuita con mi dirección de correo electrónico personal, como una cuenta de Hotmail o Gmail?

Todavía no. Actualmente, solo puede registrarse con su cuenta de correo electrónico empresarial (cuenta profesional o educativa). Estamos trabajando para ofrecer compatibilidad con las direcciones de correo electrónico personal y actualizaremos esta entrada cuando esa opción esté disponible.

## <a name="which-file-extensions-can-i-open-with-this-app"></a>¿Qué extensiones de archivo puedo abrir con esta aplicación?

Puede abrir .rpmsg, .pdf, .ppdf, .pjpg, .ptxt y varios formatos de archivo de imagen y texto.

##  <a name="how-do-i-provide-feedback-about-this-app"></a>¿Cómo puedo proporcionar comentarios sobre esta aplicación?

En la aplicación, vaya a **Configuración** > **Enviar comentarios**.


## <a name="my-question-has-not-been-answeredwhat-should-i-do"></a>Mi pregunta no se ha resuelto: ¿qué debo hacer?

Publique su pregunta en nuestro [sitio de Yammer](http://www.yammer.com/AskIPTeam) o [envíe un correo electrónico al equipo de Information Protection](mailto:askIPteam@microsoft.com?subject=Question%20about%20Azure%20Information%20Protection%20app).



<!--HONumber=Nov16_HO1-->


