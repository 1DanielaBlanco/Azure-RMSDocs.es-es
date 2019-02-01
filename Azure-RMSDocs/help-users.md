---
title: Ayuda a los usuarios para la protección de archivos con Azure RMS - AIP
description: Información para ayudarle a ofrecer instrucciones a los usuarios, administradores y al servicio de asistencia después de implementar y configurar el servicio Azure Rights Management de Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/24/2019
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 58f9a6ff-4121-4c8c-9865-1bb290604ad2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: b023eaa514fc22dcb3d595495c724d7d19e58c08
ms.sourcegitcommit: 1c1d7067ae7aa8b822bb4ecd23cd7a644989e38c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2019
ms.locfileid: "55067676"
---
# <a name="helping-users-to-protect-files-by-using-the-azure-rights-management-service"></a>Ayuda a los usuarios para proteger archivos mediante el servicio Azure Rights Management

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Después de implementar y configurar Azure Information Protection para su organización, ofrezca ayuda e instrucciones a los usuarios, administradores y al servicio de asistencia:

-   **Información del usuario final**
    
    Indique a los usuarios cómo y cuándo proteger documentos y mensajes de correo electrónico que contengan información confidencial. Siempre que sea posible, ofrezca esta información en sus flujos de trabajo existentes para que puedan incorporar los pasos adicionales a un proceso ya conocido, en lugar de introducir procesos que sean nuevos. Asegúrese de informarle de los beneficios (y de los riesgos) específicos para su negocios, así como de proporcionar orientación para cuándo deben proteger archivos y mensajes de correo electrónico. Si ha configurado [plantillas](configure-policy-templates.md), proporcione instrucciones sobre cuál seleccionar si el nombre de la plantilla y la descripción no son suficientes para elegir la correcta.
    
    > [!TIP]
    > Vídeos de ejemplo para usuarios finales:
    > -   [Microsoft Azure Information Protection](https://youtu.be/ToShAUdlrPo?list=PL8nfc9haGeb6qSm1kLU8n3Zqg398764h5)
    > -   [Azure RMS Document Tracking and Revocation](https://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation) (Revocación y seguimiento de documentos de Azure RMS)

-   **Información del administrador**
    
    Algunas aplicaciones aplican automáticamente protección de la información, mediante directivas y configuración que los administradores establecen. Para estas aplicaciones, puede que tenga que proporcionar instrucciones para otros administradores que administran estas aplicaciones y servicios. 
    
    Para más información, vea [Compatibilidad de aplicaciones con el servicio Azure Rights Management](applications-support.md) y [Configuración de aplicaciones para el servicio Azure Rights Management](configure-applications.md).
    
-   **Información del departamento de soporte técnico**
    
    Si los usuarios tienen el cliente de Azure Information Protection, los operadores del departamento de soporte técnico pueden pedirles que usen la opción **Ayuda y comentarios** para obtener información como, por ejemplo, si la edición de Office no puede admitir la protección, y la cuenta de usuario que tiene iniciada la sesión en ese momento. También puede usar esta opción para recopilar archivos de registro y restablecer el cliente. Para más información, vea la guía del administrador: [Comprobaciones de instalación y solución de problemas](./rms-client/client-admin-guide.md#installation-checks-and-troubleshooting).
    
    Si hay solicitudes legítimas para tener derechos completos de acceso a documentos protegidos, asegúrese de que el servicio de asistencia tenga procesos para solicitar este acceso con la [característica de superusuario](configure-super-users.md) de Azure Rights Management. Por ejemplo, estas solicitudes podrían provenir del departamento legal o de un administrador después de que un empleado haya dejado la organización.
    
    Además, algunos de los problemas típicos que podrían notificar los usuarios incluyen las categorías siguientes:
    
    - **Ayuda de inicio de sesión**
        
        A los usuarios se les pedirán las credenciales cuando el servicio Azure Rights Management necesite autenticar a un usuario y no pueda usar credenciales en caché. Las credenciales necesarias son normalmente las de la cuenta profesional o educativa del usuario y la contraseña que está asociada a su inquilino de Office 365 o de Azure Active Directory. Aunque el servicio de Azure Rights Management puede autenticar cuentas de Azure AD, algunas aplicaciones también pueden abrir contenido protegido cuando se usa una cuenta Microsoft para la autenticación. [Más información](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents) 
        
        Proporcione a los usuarios y al departamento de soporte técnico instrucciones sobre la cuenta que se usará cuando a los usuarios se les pidan credenciales en caso de que tengan aplicaciones que usan el servicio Azure Rights Management.
        
    - **Problemas de protección o consumo de contenido**
        
        Asegúrese de que los usuarios tengan las instrucciones apropiadas para las aplicaciones que usan y que usen aplicaciones y dispositivos compatibles con el servicio Azure Rights Management. Para más información sobre dispositivos y aplicaciones compatibles, consulte [Requirements for Azure Rights Management](requirements.md) (Requisitos para Azure Rights Management).
        
        Para confirmar que un usuario o grupo específico está autorizado por Azure Active Directory para proteger o consumir contenido protegido, utilice las comprobaciones indicadas en el artículo [Preparación de usuarios y grupos para Azure Information Protection](prepare.md).
        
        Si los usuarios informan de que pueden abrir contenido protegido, pero no tienen los derechos que necesitan, el problema podría ser que el usuario no está en el grupo correcto configurado para una plantilla de Rights Management. O bien, el problema podría ser que [la plantilla debe volver a configurarse ](configure-policy-templates.md) para el usuario o grupo. 
        
        Si los derechos que tienen los usuarios no son los previstos, compruebe su descripción y cualquier implementación específica de la aplicación en la [tabla de derechos de uso](configure-usage-rights.md#usage-rights-and-descriptions).

Use las secciones siguientes para obtener información específica de la aplicación a fin de ayudar a los usuarios a proteger documentos y mensajes de correo electrónico.

## <a name="using-information-protection-with-the-azure-information-protection-client"></a>Uso de la protección de la información con el cliente de Azure Information Protection

Si los usuarios tienen Office 2010, es necesario el cliente de Azure Information Protection (o la aplicación anterior, la aplicación Microsoft Rights Management sharing) para proteger y consumir mensajes de correo electrónico y documentos protegidos. Aun así, también se recomienda el cliente de Azure Information Protection para todos los equipos y dispositivos móviles compatibles con este servicio.

Además de facilitar a los usuarios la protección de documentos y correos electrónicos, el cliente de Azure Information Protection permite a los usuarios realizar el seguimiento de los documentos que han protegido. También se pueden revocar los documentos con seguimiento si los usuarios autorizados previamente ya no tienen acceso a ellos.

Para obtener instrucciones para usar este cliente para equipos con Windows, vea la [Guía del usuario de Azure Information Protection](./rms-client/client-user-guide.md).


## <a name="using-information-protection-with-office365-office-2019-office-2016-or-office2013"></a>Uso de protección de la información con Office 365, Office 2019, Office 2016 u Office 2013
Si usa el servicio Azure Rights Management y no ha instalado el cliente de Azure Information Protection, los usuarios no verán la barra de Azure Information Protection en sus aplicaciones de escritorio de Office. Tampoco verán el botón **Proteger** en la cinta o **Clasificar y proteger** en el Explorador de archivos. Estas adiciones facilitan a los usuarios la protección de documentos y correos electrónicos. Para estos usuarios, deben seguir instrucciones similares a los pasos siguientes.

> [!TIP]
> Para buscar ayuda específica de la aplicación e instrucciones para usar protección de la información con estas aplicaciones, busque **IRM** y el nombre y la versión de la aplicación.

#### <a name="to-protect-a-document-in-wordfrom-office-365-proplus"></a>Para proteger un documento de Word de Office 365 ProPlus

1.  En Microsoft Word, cree un documento.

2.  En el menú **Archivo**: **Información** > **Proteger documento** >  **Restringir acceso**.

3. Después elija una plantilla para aplicar de inmediato los permisos de uso correspondientes o elija **Restringir acceso** y seleccione usted mismo los permisos de uso.

    > [!NOTE]
    > Si anteriormente no ha usado Rights Management en el equipo, la opción **Restringir acceso** se conecta al servicio Azure Rights Management y se le pedirán las credenciales para configurar el cliente de IRM de Office. Después, puede elegir una plantilla o unos derechos de uso.

3.  Guarde el documento.

Cuando otros usuarios abran el documento, se les autenticará primero. Si no está autenticados para abrir el documento, el documento no se abrirá. Si están autorizados para abrir el documento, se abre con los [derechos de uso](configure-usage-rights.md) restringidos que se especificaron para ese usuario. 

Por ejemplo, un derecho de uso de Solo vista no permite al usuario editar o guardar el documento, aunque se copie primero a otra ubicación. 

Los derechos de uso se muestran en la parte superior del documento mediante una pancarta de restricción. La pancarta puede mostrar los permisos que se aplican al documento o puede proporcionar un vínculo para mostrarlos.

#### <a name="to-protect-an-email-message-using-outlookfrom-office-365-proplus-connecting-to-exchange-online"></a>Para proteger un mensaje de correo electrónico con Outlook de Office 365 ProPlus conectando a Exchange Online

1.  Dentro de Outlook, cree un mensaje de correo electrónico para un destinatario dentro de la organización.

2.  En la pestaña **OPCIONES**: **Permiso** > Seleccione una opción. Por ejemplo: **No reenviar**, **\<Nombre de la compañía> - Confidencial** o **\<Nombre de la compañía> - Confidencial. Ver solo**.

3.  Envíe el mensaje.

De manera similar a la visualización de un documento protegido, cuando los destinatarios abren el mensaje de correo electrónico protegido, se autentican en primer lugar. Si están autorizados a ver el mensaje de correo electrónico, se abrirá con los [derechos de uso](configure-usage-rights.md) restringidos que se especificaron para ese usuario. 

Por ejemplo, si el mensaje de correo electrónico está protegido mediante la opción **No reenviar**, el botón Reenviar de la cinta de opciones no estará disponible.

#### <a name="to-protect-an-email-message-using-outlook-on-the-web"></a>Para proteger un mensaje de correo electrónico con Outlook en la Web

1. Con Outlook en la Web, cree un mensaje de correo electrónico para un destinatario dentro de la organización.

2. Seleccione **Proteger**. A menos que un administrador haya cambiado el valor predeterminado, la opción **No reenviar** se selecciona automáticamente. Si desea cambiar el valor predeterminado, seleccione **Cambiar permisos** y, a continuación, seleccione una opción en la lista desplegable. Por ejemplo: **Cifrar** o **\<Nombre de la empresa > - Confidencial**.

3. Envíe el mensaje.

De manera similar a visualizar un documento protegido, cuando los destinatarios abren el mensaje de correo electrónico, lo primero es autenticarse. Si están autorizados a ver el mensaje de correo electrónico, se abrirá con los [derechos de uso](configure-usage-rights.md) restringidos que se especificaron para ese usuario. 

Por ejemplo, con la opción predeterminada **No reenviar**, la opción **Reenviar** en la ventana de mensajes no está disponible.
