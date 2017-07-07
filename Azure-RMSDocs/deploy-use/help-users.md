---
title: "Ayuda a los usuarios para la protección de archivos con Azure RMS - AIP"
description: "Información para ayudarle a ofrecer instrucciones a los usuarios, administradores y al servicio de asistencia después de implementar y configurar el servicio Azure Rights Management de Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/02/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 58f9a6ff-4121-4c8c-9865-1bb290604ad2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: f1d2db08951c1d017ea4f011855d99423fa9d577
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2017
---
# <a name="helping-users-to-protect-files-by-using-the-azure-rights-management-service"></a>Ayuda a los usuarios para proteger archivos mediante el servicio Azure Rights Management

>*Se aplica a: Azure Information Protection, Office 365*

Después de implementar y configurar Azure Information Protection para su organización, ofrezca ayuda e instrucciones a los usuarios, administradores y al servicio de asistencia:

-   **Información del usuario final:**

    Indique a los usuarios cómo y cuándo proteger documentos y mensajes de correo electrónico que contengan información confidencial. Siempre que sea posible, ofrezca esta información en sus flujos de trabajo existentes para que puedan incorporar los pasos adicionales a un proceso ya conocido, en lugar de introducir procesos que sean completamente nuevos. Asegúrese de informarle de los beneficios (y de los riesgos) específicos para su negocios, así como de proporcionar orientación para cuándo deben proteger archivos y mensajes de correo electrónico. Si ha configurado [plantillas personalizadas](configure-custom-templates.md), ofrezca instrucciones sobre cuál elegir si el nombre de la plantilla y la descripción no es suficiente para que elijan la correcta.

    > [!TIP]
    > Vídeos de ejemplo para usuarios finales:
    >
    > -   [Azure RMS user experience](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-user-experience) (Experiencia del usuario con Azure RMS)
    > -   [Azure RMS Document Tracking and Revocation](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation) (Revocación y seguimiento de documentos de Azure RMS)

-   **Información del administrador:**

    Algunas aplicaciones aplican automáticamente protección de la información, mediante directivas y configuración que los administradores establecen. Para estas aplicaciones, puede que tenga que proporcionar instrucciones para otros administradores que administran estas aplicaciones y servicios. Para más información, vea [Compatibilidad de aplicaciones con el servicio Azure Rights Management](../understand-explore/applications-support.md) y [Configuración de aplicaciones para el servicio Azure Rights Management](configure-applications.md).

-   **Información del departamento de soporte técnico:**

    Una de las herramientas más útiles para el servicio de asistencia es [RMSAnalyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437). Los operadores del servicio de asistencia pueden ejecutarlo con la opción de administrador de Azure RMS, y pueden pedir a los usuarios que lo ejecuten con la opción de usuario de Azure RMS. Esta herramienta no solo puede ayudar a identificar problemas, sino también a corregir los problemas que encuentre y, si todavía no se han solucionado, anotar los registros de seguimiento.
    
    Si los usuarios ejecutan el cliente de Azure Information Protection, los operadores del help desk pueden pedirles que utilicen l**Ayuda y comentarios**, opción **Ejecutar diagnósticos** y, a continuación, restablezca el cliente. Sin embargo, a diferencia del analizador de RMS, el restablecimiento no cierra la sesión del usuario ni reinicia el cliente y no hay ninguna corrección automática.

    Si hay solicitudes legítimas para tener derechos completos de acceso a documentos protegidos (por ejemplo, una solicitud del departamento jurídico o de un administrador después de que un empleado ha dejado la organización), asegúrese de que el servicio de asistencia tenga procesos para solicitar esto con la [característica de superusuario](configure-super-users.md) de Azure Rights Management.

    Además, estos son algunos de los problemas típicos que podrían notificar los usuarios:

    -   **Ayuda de inicio de sesión:**

        A los usuarios se les pedirán las credenciales cuando el servicio Azure Rights Management necesite autenticar a un usuario y no pueda usar credenciales en caché. Serán la cuenta profesional o educativa del usuario y la contraseña que están asociadas con su inquilino de Office 365 o de Azure Active Directory. No será una cuenta Microsoft (anteriormente, Microsoft Live ID) o su cuenta de correo personal, ya que actualmente no son compatibles con el servicio Azure Rights Management. Ofrezca a los usuarios y al servicio de asistencia instrucciones sobre la cuenta que se usará cuando a los usuarios se les pidan credenciales al usar estas aplicaciones con el servicio Azure Rights Management.

    -   **Problemas de protección o consumo de contenido:**

        Asegúrese de que los usuarios tengan las instrucciones apropiadas para las aplicaciones que usan y que usen aplicaciones y dispositivos compatibles con el servicio Azure Rights Management. Para más información sobre dispositivos y aplicaciones compatibles, consulte [Requirements for Azure Rights Management](../get-started/requirements-azure-rms.md) (Requisitos para Azure Rights Management).

        Si los usuarios ven un error al intentar proteger o consumir contenido, pídales que ejecuten [RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437) como usuarios de Azure RMS.

        Si los usuarios informan de que pueden abrir contenido protegido, pero no tiene los derechos que necesitan, pedirles que ejecuten [RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437) como usuarios de Azure RMS y que descarguen y vean las plantillas. De este modo se confirmará que han descargado correctamente las plantillas y qué derechos proporcionan las plantillas. El problema puede ser que el usuario no está en el grupo correcto que se configura para la plantilla, o que es necesario volver a configurar la plantilla para el usuario.

Use las secciones siguientes para información específica de aplicación a fin de ayudar a los usuarios a proteger documentos y mensajes de correo electrónico confidenciales.

## <a name="using-information-protection-with-the-azure-information-protection-client"></a>Uso de la protección de la información con el cliente de Azure Information Protection
El cliente de Azure Information Protection puede ser necesario para que los usuarios protejan y consuman correos electrónicos y documentos protegidos si usan Office 2010, pero también se recomienda para equipos y dispositivos móviles.

Además de facilitar a los usuarios la protección de documentos importantes, el cliente de Azure Information Protection permite a los usuarios realizar el seguimiento de los documentos que han protegido y, si es necesario, revocar el acceso a ellos.

Para obtener instrucciones para usar este cliente para equipos con Windows, vea la [Guía del usuario de Azure Information Protection](../rms-client/client-user-guide.md).


## <a name="using-information-protection-with-office-365-office-2016-or-office-2013"></a>Uso de protección de la información con Office 365, Office 2016 u Office 2013
Si usa el servicio Azure Rights Management y no se ha instalado el cliente de Azure Information Protection, los usuarios no verán la barra de Azure Information Protection en sus aplicaciones de escritorio de Office, el botón **Proteger** en la cinta o **Clasificar y proteger** en el Explorador de archivos, que facilita la protección de archivos. Para estos usuarios, deben seguir instrucciones similares a los pasos siguientes.

> [!TIP]
> Para buscar ayuda específica de la aplicación e instrucciones para usar protección de la información con estas aplicaciones, busque **IRM** y el nombre y la versión de la aplicación.

#### <a name="to-protect-a-document-in-word-2013"></a>Para proteger un documento en Word 2013

1.  Dentro de Microsoft Word, cree un nuevo documento.

2.  En el menú **Archivo** , haga clic en **Información**, elija **Proteger documento**y haga clic en **Restringir el acceso**. Después elija una plantilla para aplicar de inmediato los permisos de uso correspondientes o elija **Restringir el acceso** y seleccione usted mismo los permisos de uso.

    > [!NOTE]
    > Si esta es la primera vez que ha usado Rights Management, se pondrá en contacto con el servicio de [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] y se le solicitarán las credenciales para configurar el cliente de Office IRM.

3.  Guarde el documento.

Cuando otros usuarios abran el documento, se les autenticará primero. Si no está autenticados para abrir el documento, el documento no se abrirá. Si están autorizados para abrir el documento, se abrirá con los derechos de uso restringidos que se especificaron para ese usuario. Por ejemplo, un derecho de uso de Solo vista no permite al usuario editar o guardar el documento, aunque se copie primero a otra ubicación. Los derechos de uso se muestran en la parte superior del documento mediante una pancarta de restricción. La pancarta puede mostrar los permisos que se aplican al documento o puede proporcionar un vínculo para mostrarlos.

#### <a name="to-protect-an-email-message-using-outlook-2013-and-exchange-online"></a>Para proteger un mensaje de correo electrónico con Outlook 2013 y Exchange Online

1.  Dentro de Outlook, cree un nuevo mensaje de correo electrónico para un destinatario dentro de la organización.

2.  En la pestaña **OPCIONES** , haga clic en **Permiso**y seleccione una opción. Por ejemplo: **No reenviar**, **&lt;Nombre de empresa&gt; - Confidencial** o **&lt;Nombre de empresa&gt; - Solo vista confidencial**.

3.  Envíe el mensaje.

De manera similar a la visualización de un documento protegido, cuando los destinatarios reciben el mensaje de correo electrónico, se autentican en primer lugar. Si están autorizados para ver el mensaje de correo electrónico, se abrirá con los derechos de uso restringidos que se especificaron para ese usuario. Por ejemplo, si seleccionó **No reenviar**, el botón Reenviar no está disponible en la cinta de opciones.

#### <a name="to-protect-an-email-message-using-the-outlook-web-app"></a>Para proteger un mensaje de correo electrónico con Outlook Web App

1.  Dentro de Outlook Web Ap, cree un nuevo mensaje de correo electrónico para un destinatario dentro de la organización.

2.  Haga clic en  **...**, elija **Establecer permisos**y seleccione una opción. Por ejemplo: **No reenviar**, **No responder a todos**, **&lt;Nombre de empresa&gt; - Confidencial** o **&lt;Nombre de empresa&gt; - Solo vista confidencial**.

3.  Envíe el mensaje.

De manera similar a la visualización de un documento protegido, cuando los destinatarios reciben el mensaje de correo electrónico, se autentican en primer lugar. Si están autorizados para ver el mensaje de correo electrónico, se abrirá con los derechos de uso restringidos que se especificaron para ese usuario. Por ejemplo, si seleccionó **No responder a todos**, la opción **RESPONDER A TODOS** no está disponible en la ventana del mensaje.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

