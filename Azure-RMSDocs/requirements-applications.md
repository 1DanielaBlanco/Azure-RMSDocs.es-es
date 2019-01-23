---
title: Compatibilidad con aplicaciones para la protección de datos de RMS - AIP
description: Identifique las aplicaciones que usarán las API de RMS para que sean compatibles de forma nativa con el servicio Azure Rights Management de Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/17/2019
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 0f83401b8cac96820f2628a501ca2f731d678126
ms.sourcegitcommit: 2daa75cda8475028a3dac83d70505fcfccef42a1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2019
ms.locfileid: "54361807"
---
# <a name="applications-that-support-azure-rights-management-data-protection"></a>Aplicaciones compatibles con la protección de datos de Azure Rights Management

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Use la tabla siguiente para identificar las aplicaciones y soluciones que son compatibles de forma nativa con el servicio Azure Rights Management (Azure RMS), que ofrece la protección de datos para Azure Information Protection.

Para estas aplicaciones y soluciones, la compatibilidad de Rights Management está integrada estrechamente con el uso de las API de Rights Management para permitir la compatibilidad con restricciones de uso. Estas aplicaciones y soluciones se conocen también como "habilitadas para RMS ".

A menos que se indique lo contrario, las funciones admitidas son válidas tanto para Azure RMS como para AD RMS. Además, la compatibilidad de AD RMS en iOS, Android, macOS y Windows Phone 8.1 requiere la [Extensión de dispositivos móviles para Active Directory Rights Management Services](https://technet.microsoft.com/library/dn673574.aspx).

## <a name="rms-enlightened-applications"></a>Aplicaciones habilitadas para RMS

En la siguiente tabla se muestran aplicaciones cliente de Microsoft y de proveedores de software habilitadas para RMS. 

Para obtener información sobre la visualización de documentos PDF protegidos, vea [Lectores PDF protegidos para Microsoft Information Protection](./rms-client/protected-pdf-readers.md).

Información acerca de las columnas de la tabla:

-   **Correo electrónico:** los clientes de correo electrónico enumerados pueden proteger el mensaje de correo en sí, lo que hace que también se protejan automáticamente los archivos adjuntos de Office que no lo están. En este escenario, la característica de vista previa del cliente puede mostrar el contenido protegido (mensaje y datos adjuntos) a destinatarios autorizados. Sin embargo, si un mensaje de correo electrónico no está protegido pero los datos adjuntos si lo están, la característica de vista previa no puede mostrar dichos datos a destinatarios autorizados. 
    
    Sugerencia: En el caso de los clientes de correo electrónico que no permitan proteger los correos electrónicos, le recomendamos que use las [reglas de flujo de correo electrónico de Exchange Online para aplicar dicha protección](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8).

-   **Otros tipos de archivo**: los archivos de texto e imagen incluyen archivos que tienen una extensión de nombre de archivo como .txt, .xml, .jpg y .jpeg. Estos archivos cambian su extensión de nombre de archivo después de protegerlos de forma nativa con Rights Management y se convierten en archivos de solo lectura. Los archivos que no se pueden proteger de forma nativa pasan a tener una extensión de nombre de archivo .pfile después de protegerlos de forma genérica con Rights Management. Para más información, vea [Tipos de archivos admitidos](./rms-client/client-admin-guide-file-types.md) en la guía para administradores del cliente de Azure Information Protection.


|**Sistema operativo del dispositivo**|Word, Excel, PowerPoint|Correo electrónico|Otros tipos de archivo|
|---------------------------|-----------------------|-----------------|---------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office 2016 <br /><br />Office Online (visualización de documentos protegidos) [[1]](#footnote-1)<br /><br />Explorador web [[2]](#footnote-2)|Outlook 2010<br /><br />Outlook 2013<br /><br />Office 2016 <br /><br />Explorador web [[3]](#footnote-3)<br /><br />Correo de Windows [[4]](#footnote-4) |Cliente de Azure Information Protection para Windows: Texto, imágenes, pfile<br /><br />Aplicaciones de uso compartido RMS para Windows: Texto, imágenes, pfile<br /><br />Complemento SealPath RMS para AutoCAD: .dwg|
|**iOS**|GigaTrust<br /><br /> Office Mobile (visualización y edición de documentos protegidos)<br /><br />Office Online [[1]](#footnote-1)<br /><br />Documentos TITUS<br /><br />Explorador web [[2]](#footnote-2)|Aplicación Azure Information Protection (visualización de correos protegidos)<br /><br />BlackBerry Work<br /><br />Citrix WorxMail <br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook para iPad y iPhone [[4]](#footnote-4)<br /><br />TITUS Mail <br /><br />Explorador web [[3]](#footnote-3)|Aplicación Azure Information Protection (visualización de texto e imágenes protegidos)<br /><br />Documentos TITUS: Pfile|
|**Android**|GigaTrust App para Android<br /><br />Office Online [[1]](#footnote-1)<br /><br />Office Mobile <br /><br />Explorador web [[2]](#footnote-2)|9Folders [[4]](#footnote-4)<br /><br />Aplicación Azure Information Protection (visualización de correos protegidos)<br /><br />BlackBerry Work <br /><br />GigaTrust App para Android [[4]](#footnote-4)<br /><br />Citrix WorxMail <br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook para Android [[4]](#footnote-4)<br /><br />Correo electrónico de Samsung (S3 y versiones posteriores) [[4]](#footnote-4)<br /><br />TITUS Classification for Mobile <br /><br />Explorador web [[3]](#footnote-3)|Aplicación Azure Information Protection (visualización de texto e imágenes protegidos)|
|**macOS**|Office 2016 para Mac<br /><br />Office Online [[1]](#footnote-1)<br /><br />Explorador web [[2]](#footnote-2)|Outlook 2016 para Mac<br /><br />Explorador web [[3]](#footnote-3)|Aplicación RMS sharing (visualización de texto e imágenes protegidos y archivos protegidos genéricamente)|
|**Windows 10 Mobile**|Aplicaciones de Office Mobile (visualización de documentos protegidos mediante Azure RMS) <br /><br />Explorador web [[2]](#footnote-2)|Citrix WorxMail <br /><br />Correo de Outlook (visualización de correos electrónicos protegidos) <br /><br />Explorador web [[3]](#footnote-3)|No compatible|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [[1]](#footnote-1)<br /><br />Explorador web [[2]](#footnote-2)|Outlook 2013 RT<br /><br />Aplicación de correo para Windows<br /><br />Explorador web [[3]](#footnote-3)<br /><br />Correo de Windows [[4]](#footnote-4)|Siemens JT2Go: Archivos JT|
|**Windows Phone 8.1**|Office Mobile (solo AD RMS)<br /><br />Explorador web [[2]](#footnote-2)|Outlook Mobile [[4]](#footnote-4) <br /><br />Explorador web [[3]](#footnote-3)|Aplicación RMS sharing (visualización de texto e imágenes protegidos y archivos protegidos genéricamente)|
|**Blackberry 10**|Explorador web [[2]](#footnote-2)|Correo electrónico de Blackberry [[4]](#footnote-4) <br /><br />Explorador web [[3]](#footnote-3)|No compatible|

###### <a name="footnote-1"></a>Nota al pie 1
Solo se admite con SharePoint Online y OneDrive para la Empresa, y los documentos se desprotegen antes de cargarse en una biblioteca protegida.

###### <a name="footnote-2"></a>Nota al pie 2
Para [datos adjuntos de Office](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM) que están protegidos mediante los pasos de [Announcing new capabilities available in Office 365 Message Encryption](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801) (Anuncio de nuevas capacidades disponibles en el cifrado de mensajes de Office 365).

###### <a name="footnote-3"></a>Nota al pie 3
Si el remitente y el destinatario forman parte de la misma organización. O cualquiera de las siguientes condiciones:

- El remitente o el destinatario usan Exchange Online.

- El remitente está usando Exchange local en una configuración híbrida. 

###### <a name="footnote-4"></a>Nota al pie 4
Usa Exchange ActiveSync IRM, que debe habilitar el administrador de Exchange. Los usuarios pueden usar las opciones de ver, responder y responder a todos para los mensajes de correo protegidos, pero no pueden proteger nuevos mensajes de correo.
 
Si la aplicación de correo no puede procesar el mensaje porque Exchange ActiveSync IRM no está habilitado, el destinatario puede ver el correo electrónico en un explorador web cuando el remitente usa Exchange Online o Exchange local en una configuración híbrida. 



### <a name="more-information-about-azure-rms-support-for-office"></a>Más información sobre la compatibilidad de Azure RMS con Office

Azure RMS se integra estrechamente en las aplicaciones de Word, Excel, PowerPoint y Outlook, donde esta funcionalidad se conoce a menudo como Information Rights Management (IRM). 

Consulte también: [Office Applications Service Description](https://technet.microsoft.com/library/office-applications-service-description.aspx) (Descripción del servicio de aplicaciones de Office)

#### <a name="windows-computers-for-information-rights-management-irm"></a>Equipos Windows para Information Rights Management (IRM)

Los siguientes conjuntos de aplicaciones cliente de Office admiten la protección de archivos y correos electrónicos en equipos Windows mediante el servicio Azure Rights Management:

- Office 365 con aplicaciones de Office 2016 (versión mínima 1805, compilación 9330.2078) cuando se asigna una licencia a un usuario para Azure Rights Management (también conocido como Azure Information Protection para Office 365)

- Office 365 ProPlus: Office 2016 y Office 2013
    
    Estas ediciones de Office se incluyen con la mayoría (aunque no todas) de las suscripciones de Office 365 que incluyen la protección de datos de Azure Information Protection. Consulte la información de su suscripción para comprobar si se incluye Office 365 ProPlus. También encontrará esta información en la [hoja de datos de Azure Information Protection](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

- Office Professional Plus 2016

- Office Professional Plus 2013

- Office Professional Plus 2010 con Service Pack 2

Todas las ediciones de Office (salvo Office 2007) pueden consumir contenido protegido.

Cuando usa el servicio Azure Rights Management con Office Professional Plus 2010 y Service Pack 2 u Office Professional 2010 con Service Pack 2:

- Requiere el cliente de Azure Information Protection para Windows o la aplicación Rights Management sharing para Windows.

- No se admite en Windows 10.

- No admite la autenticación basada en formularios para cuentas de usuario federadas. Estas cuentas deben usar la autenticación integrada de Windows.

- No se admite anular la protección de plantilla con permisos personalizados que el usuario selecciona con el cliente de Azure Information Protection. En este escenario, debe quitarse primero la protección original para poder aplicar permisos personalizados.

#### <a name="mac-computers-for-information-rights-management-irm"></a>Equipos Mac para Information Rights Management (IRM)

Los siguientes conjuntos de aplicaciones cliente de Office admiten la protección de archivos y correos electrónicos en macOS mediante Azure RMS:

- Office 365 ProPlus: Office 2016

- Office Standard 2016 para Mac

Todas las ediciones de Office para Mac 2016 pueden consumir contenido protegido.

Sugerencia: para empezar a proteger documentos mediante Office para Mac, puede que la siguiente página de preguntas frecuentes le resulte útil: [¿Cómo se configura un equipo Mac para proteger documentos y hacer un seguimiento de ellos?](faqs-rms.md#how-do-i-configure-a-mac-computer-to-protect-and-track-documents)

### <a name="more-information-about-the-azure-information-protection-app-for-ios-and-android"></a>Más información sobre la aplicación Azure Information Protection para iOS y Android

La aplicación de Azure Information Protection para iOS y Android proporciona un visor de mensajes de correo electrónico protegidos por derechos (archivos .rpmsg) cuando estos dispositivos móviles no tienen una aplicación de correo electrónico que pueda abrir los correos electrónicos protegidos. Esta aplicación también abre archivos PDF protegidos por derechos, así como imágenes y archivos de texto protegidos por derechos.

Si los dispositivos iOS y Android están inscritos por Microsoft Intune, los usuarios pueden instalar la aplicación desde el Portal de empresa y administrarla mediante el uso de [directivas de protección de aplicaciones de Intune](/intune/app-protection-policies).

Para más información sobre cómo usar la aplicación, vea las [Preguntas más frecuentes sobre la aplicación de Microsoft Azure Information Protection para iOS y Android](./rms-client/mobile-app-faq.md).


### <a name="more-information-about-the-azure-information-protection-client-for-windows"></a>Más información sobre el cliente de Azure Information Protection para Windows

Este cliente ahora reemplaza a la aplicación Rights Management sharing para Windows.

Para obtener más información, vea los recursos siguientes:

- [Guía de administrador de cliente de Azure Information Protection](./rms-client/client-admin-guide.md)

- [Guía del usuario de Azure Information Protection](./rms-client/client-user-guide.md)

- [Preguntas más frecuentes sobre la aplicación de Microsoft Azure Information Protection para iOS y Android](./rms-client/mobile-app-faq.md)

Descargue la aplicación correspondiente en los vínculos de la [página de Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970).

### <a name="more-information-about-the-rights-management-sharing-application"></a>Más información sobre la aplicación Rights Management sharing

Esta aplicación se va a reemplazar por el cliente de Azure Information Protection. Los dispositivos móviles con Windows Phone aún la necesitan para ver archivos protegidos. 

Para equipos Mac, ofrece un visor para archivos PDF protegidos (.ppdf), imágenes de texto protegidas y archivos protegidos genéricamente. La aplicación RMS sharing para Mac también puede proteger archivos de imagen, pero no los demás archivos. Para proteger archivos de Office, use Office para Mac. 

Para obtener más información, vea los recursos siguientes:

-   [Guía del administrador de la aplicación Rights Management sharing](./rms-client/sharing-app-admin-guide.md)

-   [Guía de usuario de la aplicación Rights Management sharing](./rms-client/sharing-app-user-guide.md)

-   [Preguntas frecuentes para la aplicación Microsoft Rights Management sharing para plataformas móviles](https://technet.microsoft.com/dn451248)

Descargue el visor para equipos Mac y para Windows Phone con los vínculos de la [página Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970).


### <a name="more-information-about-other-applications-that-support-azure-information-protection"></a>Más información sobre otras aplicaciones que admiten Azure Information Protection

Además de las aplicaciones de la tabla, cualquier aplicación que sea compatible con las API del servicio Azure Rights Management se puede integrar con Azure Information Protection. Aquí se incluyen:

- Aplicaciones de línea de negocio escritas internamente con RMS SDK.

- Aplicaciones de proveedores de software escritas con RMS SDK.

Para más información, consulte la [Guía del desarrollador de Azure Information Protection](./develop/developers-guide.md).

### <a name="applications-that-are-not-supported-by-azure-rms"></a>Aplicaciones no compatibles con Azure RMS

Las siguientes aplicaciones no son compatibles actualmente con Azure RMS:

-   Microsoft OneDrive para la Empresa para SharePoint Server 2013

-   Visor de XPS

Además, la aplicación RMS sharing y el cliente de Azure Information Protection tienen las restricciones siguientes:

-   Para equipos Windows: Precisa una versión mínima de Windows 7 Service Pack 1

## <a name="rms-enlightened-solutions"></a>Soluciones habilitadas para RMS

En la siguiente tabla se muestran soluciones de proveedores de software habilitadas para RMS.

Si es un proveedor de software y tiene una solución para esta tabla que no aparece, registre la aplicación con Azure AD. Para más información, consulte [Cómo registrar y habilitar para RMS la aplicación con Azure AD](./develop/authentication-integration.md).


|Product|Proveedor|Descripción|
|-------------------------------|---------------------------|-----------------|
|Absoluto|Absoluto|Prevención de pérdida de datos (DLP) para proteger el contenido.|
|Content Locker|VMware|Almacena, consume y crea contenido protegido.|
|Controle|TakeControle|eDiscovery mediante etiquetado y protección.|
|Forcepoint|DLP de Forcepoint|Solución de prevención de pérdida de datos (DLP) de puntos de conexión para aplicar las directivas de seguridad de datos de una organización.|
|Halocore|Secude|Protege archivos que se exportan desde entornos de SAP.|
|MaaS 360|IBM|Integración para consumir y proteger documentos.|
|Mobiliya|Mobiliya|Protege documentos de repositorios de Documentum de EMC.
|Ramessys|Ramessys|Integración para Chemcart y Documentum.
|Sealpath|Sealpath Technologies|Integración con herramientas de diseño CAD, como AutoCAD y Siemens Jt2GO.
|SecRMM|Sqaudra Technologies |Protección de documentos para medios extraíbles.
|Security Sheriff|CryptZone |Administración de acceso en SharePoint y protección de documentos, en función de su clasificación y permisos de acceso.
|DLP de Symantec|Symantec |Detección y supervisión para archivos protegidos.

## <a name="next-steps"></a>Pasos siguientes
Para comprobar otros requisitos, vea [Requisitos para Azure Information Protection](requirements.md).

Para más información sobre la compatibilidad de Azure RMS con las aplicaciones más usadas, vea [Compatibilidad de aplicaciones con el servicio Azure Rights Management](./applications-support.md).

Para más información sobre cómo configurar las aplicaciones de uso más común para Azure RMS, vea [Configuring applications for Azure Rights Management](configure-applications.md) (Configuración de aplicaciones para Azure Rights Management).

