---
title: "Ayuda a los usuarios para la protección de archivos con Azure RMS - AIP"
description: "Información para ayudarle a ofrecer instrucciones a los usuarios, administradores y al servicio de asistencia después de implementar y configurar el servicio Azure Rights Management de Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/02/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 58f9a6ff-4121-4c8c-9865-1bb290604ad2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 192f4ade987e9f9f88f5f30bb17c70e113569002
ms.sourcegitcommit: 8b6fc2201d99d72ee9bb43bb73356040893eceeb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2017
---
# <a name="helping-users-to-protect-files-by-using-the-azure-rights-management-service"></a>Ayuda a los usuarios para proteger archivos mediante el servicio Azure Rights Management

>*Se aplica a: Azure Information Protection, Office 365*

Después de implementar y configurar Azure Information Protection para su organización, ofrezca ayuda e instrucciones a los usuarios, administradores y al servicio de asistencia:

-   **Información del usuario final**
    
    Indique a los usuarios cómo y cuándo proteger documentos y mensajes de correo electrónico que contengan información confidencial. Siempre que sea posible, ofrezca esta información en sus flujos de trabajo existentes para que puedan incorporar los pasos adicionales a un proceso ya conocido, en lugar de introducir procesos que sean nuevos. Asegúrese de informarle de los beneficios (y de los riesgos) específicos para su negocios, así como de proporcionar orientación para cuándo deben proteger archivos y mensajes de correo electrónico. Si ha configurado [plantillas](configure-policy-templates.md), proporcione instrucciones sobre cuál seleccionar si el nombre de la plantilla y la descripción no son suficientes para elegir la correcta.
    
    > [!TIP]
    > Vídeos de ejemplo para usuarios finales:
    > -   [Azure RMS user experience](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-user-experience) (Experiencia del usuario con Azure RMS)
    > -   [Azure RMS Document Tracking and Revocation](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation) (Revocación y seguimiento de documentos de Azure RMS)

-   **Información del administrador**
    
    Algunas aplicaciones aplican automáticamente protección de la información, mediante directivas y configuración que los administradores establecen. Para estas aplicaciones, puede que tenga que proporcionar instrucciones para otros administradores que administran estas aplicaciones y servicios. 
    
    Para más información, vea [Compatibilidad de aplicaciones con el servicio Azure Rights Management](../understand-explore/applications-support.md) y [Configuración de aplicaciones para el servicio Azure Rights Management](configure-applications.md).
    
-   **Información del departamento de soporte técnico**
    
    Si los usuarios tienen el cliente de Azure Information Protection, los operadores del departamento de soporte técnico pueden pedirles que usen la opción **Ejecutar diagnósticos** de **Ayuda y comentarios** y que restablezcan el cliente. Sin embargo, el restablecimiento no cierra la sesión del usuario ni reinicia el cliente y no hay ninguna corrección automática.
    
    Si hay solicitudes legítimas para tener derechos completos de acceso a documentos protegidos, asegúrese de que el servicio de asistencia tenga procesos para solicitar este acceso con la [característica de superusuario](configure-super-users.md) de Azure Rights Management. Por ejemplo, estas solicitudes podrían provenir del departamento legal o de un administrador después de que un empleado haya dejado la organización. 
    
    Además, algunos de los problemas típicos que podrían notificar los usuarios incluyen las categorías siguientes:
    
    - **Ayuda de inicio de sesión**
        
        A los usuarios se les pedirán las credenciales cuando el servicio Azure Rights Management necesite autenticar a un usuario y no pueda usar credenciales en caché. Las credenciales necesarias son para la cuenta profesional o educativa del usuario y la contraseña que está asociada a su inquilino de Office 365 o de Azure Active Directory. Las credenciales necesarias no serán para una cuenta Microsoft (anteriormente, Microsoft Live ID) o su cuenta de correo personal, ya que actualmente estas cuentas no son compatibles con el servicio Azure Rights Management. 
        
        Proporcione a los usuarios y al departamento de soporte técnico instrucciones sobre la cuenta que se usará cuando a los usuarios se les pidan credenciales en caso de que tengan aplicaciones que usan el servicio Azure Rights Management.
        
    - **Problemas de protección o consumo de contenido**
        
        Asegúrese de que los usuarios tengan las instrucciones apropiadas para las aplicaciones que usan y que usen aplicaciones y dispositivos compatibles con el servicio Azure Rights Management. Para más información sobre dispositivos y aplicaciones compatibles, consulte [Requirements for Azure Rights Management](../get-started/requirements-azure-rms.md) (Requisitos para Azure Rights Management).
        
        La autenticación y autorización se basan en cuentas y grupos de Azure Active Directory. Para confirmar que un usuario o grupo específico está autorizado para consumir contenido protegido, utilice las comprobaciones indicadas en el artículo [Preparación de usuarios y grupos para Azure Information Protection](../plan-design/prepare.md).
        
        Si los usuarios informan de que pueden abrir contenido protegido, pero no tienen los derechos que necesitan, el problema podría ser que el usuario no está en el grupo correcto configurado para una plantilla de Rights Management. O bien, el problema podría ser que [la plantilla debe volver a configurarse ](configure-policy-templates.md) para el usuario o grupo. 
        
        Si los derechos que tienen los usuarios no son los previstos, compruebe su descripción y cualquier implementación específica de la aplicación en la [tabla de derechos de uso](../deploy-use/configure-usage-rights.md#usage-rights-and-descriptions).

Use las secciones siguientes para obtener información específica de la aplicación a fin de ayudar a los usuarios a proteger documentos y mensajes de correo electrónico.

## <a name="using-information-protection-with-the-azure-information-protection-client"></a>Uso de la protección de la información con el cliente de Azure Information Protection

Si los usuarios tienen Office 2010, es necesario el cliente de Azure Information Protection (o la aplicación anterior, la aplicación Microsoft Rights Management sharing) para proteger y consumir mensajes de correo electrónico y documentos protegidos. Aun así, también se recomienda el cliente de Azure Information Protection para todos los equipos y dispositivos móviles compatibles con este servicio.

Además de facilitar a los usuarios la protección de documentos y correos electrónicos, el cliente de Azure Information Protection permite a los usuarios realizar el seguimiento de los documentos que han protegido. También se pueden revocar los documentos con seguimiento si los usuarios autorizados previamente ya no tienen acceso a ellos.

Para obtener instrucciones para usar este cliente para equipos con Windows, vea la [Guía del usuario de Azure Information Protection](../rms-client/client-user-guide.md).


## <a name="using-information-protection-with-office-365-office-2016-or-office-2013"></a>Uso de protección de la información con Office 365, Office 2016 u Office 2013
Si usa el servicio Azure Rights Management y no ha instalado el cliente de Azure Information Protection, los usuarios no verán la barra de Azure Information Protection en sus aplicaciones de escritorio de Office. Tampoco verán el botón **Proteger** en la cinta o **Clasificar y proteger** en el Explorador de archivos. Estas adiciones facilitan a los usuarios la protección de documentos y correos electrónicos. Para estos usuarios, deben seguir instrucciones similares a los pasos siguientes.

> [!TIP]
> Para buscar ayuda específica de la aplicación e instrucciones para usar protección de la información con estas aplicaciones, busque **IRM** y el nombre y la versión de la aplicación.

#### <a name="to-protect-a-document-in-word-2013"></a>Para proteger un documento en Word 2013

1.  En Microsoft Word, cree un documento.

2.  En el menú **Archivo**, haga clic sucesivamente en **Información**, **Proteger documento** y, finalmente, en **Restringir acceso**.

3. Después elija una plantilla para aplicar de inmediato los permisos de uso correspondientes o elija **Restringir acceso** y seleccione usted mismo los permisos de uso.

    > [!NOTE]
    > Si anteriormente no ha usado Rights Management en el equipo, la opción **Restringir acceso** conecta al servicio [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] y se le pedirán las credenciales para configurar el cliente de Office IRM. Después, puede elegir una plantilla o unos derechos de uso.

3.  Guarde el documento.

Cuando otros usuarios abran el documento, se les autenticará primero. Si no está autenticados para abrir el documento, el documento no se abrirá. Si están autorizados para abrir el documento, se abre con los [derechos de uso](../deploy-use/configure-usage-rights.md) restringidos que se especificaron para ese usuario. 

Por ejemplo, un derecho de uso de Solo vista no permite al usuario editar o guardar el documento, aunque se copie primero a otra ubicación. 

Los derechos de uso se muestran en la parte superior del documento mediante una pancarta de restricción. La pancarta puede mostrar los permisos que se aplican al documento o puede proporcionar un vínculo para mostrarlos.

#### <a name="to-protect-an-email-message-using-outlook-2013-and-exchange-online"></a>Para proteger un mensaje de correo electrónico con Outlook 2013 y Exchange Online

1.  Dentro de Outlook, cree un mensaje de correo electrónico para un destinatario dentro de la organización.

2.  En la pestaña **OPCIONES** , haga clic en **Permiso**y seleccione una opción. Por ejemplo: **No reenviar**, **\<Nombre de empresa> - Confidencial** o **\<Nombre de empresa> - Confidencial. Ver solo**.

3.  Envíe el mensaje.

De manera similar a la visualización de un documento protegido, cuando los destinatarios abren el mensaje de correo electrónico protegido, se autentican en primer lugar. Si están autorizados a ver el mensaje de correo electrónico, se abrirá con los [derechos de uso](../deploy-use/configure-usage-rights.md) restringidos que se especificaron para ese usuario. 

Por ejemplo, si el mensaje de correo electrónico está protegido mediante la opción **No reenviar**, el botón Reenviar de la cinta de opciones no estará disponible.

#### <a name="to-protect-an-email-message-using-outlook-on-the-web"></a>Para proteger un mensaje de correo electrónico con Outlook en la Web

1.  Con Outlook en la Web, cree un mensaje de correo electrónico para un destinatario dentro de la organización.

2.  Haga clic en  **...**, elija **Establecer permisos**y seleccione una opción. Por ejemplo: **No reenviar** o **No responder a todos**. O bien, **\<Nombre de empresa> - Confidencial** o **\<Nombre de empresa> - Confidencial. Ver solo**.

3.  Envíe el mensaje.

De manera similar a visualizar un documento protegido, cuando los destinatarios abren el mensaje de correo electrónico, lo primero es autenticarse. Si están autorizados a ver el mensaje de correo electrónico, se abrirá con los [derechos de uso](../deploy-use/configure-usage-rights.md) restringidos que se especificaron para ese usuario. 

Por ejemplo, si seleccionó **No responder a todos**, la opción **RESPONDER A TODOS** no está disponible en la ventana del mensaje.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

