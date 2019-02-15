---
title: Cómo los servicios y las aplicaciones de Office son compatibles con Azure RMS desde AIP
description: Cómo las aplicaciones de Office de usuario final (como Word y Outlook) y los servicios de Office (como Exchange y SharePoint) pueden usar el servicio Azure Rights Management desde AIP para ayudar a proteger los datos de una organización.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/13/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 388e67cd-c16f-4fa0-a7bb-ffe0def2be81
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 71f5afc3f65713f62607717d5459080aa11bedf2
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56256760"
---
# <a name="how-office-applications-and-services-support-azure-rights-management"></a>Cómo las aplicaciones y los servicios de Office admiten Azure Rights Management 

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Las aplicaciones de Office de usuario final y los servicios de Office pueden usar el servicio Azure Rights Management desde Azure Information Protection con el objetivo de proteger los datos de la organización. Estas aplicaciones de Office son Word, Excel, PowerPoint y Outlook. Los servicios de Office son Exchange y SharePoint. Las configuraciones de Office que admiten el servicio Azure Rights Management suelen usar el término **Information Rights Management (IRM)**.

## <a name="office-applications-word-excel-powerpoint-outlook"></a>Aplicaciones de Office: Word, Excel, PowerPoint, Outlook
Estas aplicaciones admiten de forma nativa Azure Rights Management y permiten a los usuarios aplicar protección a un documento guardado o a un mensaje de correo electrónico que se enviará. Los usuarios pueden aplicar [plantillas](configure-policy-templates.md) para aplicar la protección. En el caso de Word, Excel y PowerPoint, los usuarios pueden elegir configuraciones personalizadas para restricciones de uso, derechos y acceso.

Por ejemplo, los usuarios pueden configurar un documento de Word para que solamente tengan acceso a él las personas de la organización, o controlar si se puede editar una hoja de cálculo de Excel, si se restringe a solo lectura o si se impide que se pueda imprimir. En el caso de los archivos sujetos a limitación temporal, se puede configurar una fecha de expiración en la que ya no se podrá tener acceso al archivo. Los usuarios pueden aplicar directamente esta configuración, o bien se puede aplicar mediante una plantilla. Para Outlook, los usuarios también pueden elegir la opción **No reenviar** con el fin de evitar la fuga de datos.

Además de la compatibilidad nativa de Office con Azure Rights Management, estas aplicaciones admiten la barra de Azure Information Protection que se instala con el [cliente de Azure Information Protection](./rms-client/aip-client.md). En esta barra se muestran etiquetas que facilitan a los usuarios aplicar automáticamente la protección a documentos y correos electrónicos que contienen información confidencial.

Si está listo para configurar aplicaciones de Office y el cliente de Azure Information Protection:

- Para configurar aplicaciones de Office, vea [Aplicaciones de Office: configuración para los clientes que usan el servicio Azure Rights Management](configure-office-apps.md).

- Para instalar y configurar el cliente de Azure Information Protection, vea [Cliente de Azure Information Protection: instalación y configuración de clientes](configure-client.md).

## <a name="exchange-online-and-exchange-server"></a>Exchange Online y Exchange Server
Cuando se usa Exchange Online o Exchange Server, se pueden configurar opciones para Azure Information Protection. Esta configuración permite a Exchange proporcionar las siguientes soluciones de protección:

-   **Exchange ActiveSync IRM** para que los dispositivos móviles puedan proteger y consumir mensajes de correo electrónico protegidos.

-   Compatibilidad con protección de correo electrónico para **Outlook en la Web**, que se implementa de forma similar en el cliente de Outlook. Esta configuración permite a los usuarios proteger los mensajes de correo electrónico mediante plantillas u opciones de protección. Los usuarios podrán leer y usar los mensajes de correo electrónico protegidos que se les envíen.

-   **Reglas de protección** para clientes de Outlook que un administrador configura para aplicar automáticamente plantillas de protección y opciones a los mensajes de correo electrónico para destinatarios concretos. Por ejemplo, cuando se envían correos electrónicos internos a tu departamento legal, solo los miembros del departamento legal pueden leerlos y no se pueden reenviar. Los usuarios consultan la protección que se aplicará al mensaje de correo electrónico antes de enviarlo y, de forma predeterminada, pueden quitarla si deciden que no es necesaria. Los correos electrónicos se cifran antes de enviarlos. Para más información, consulte [Reglas de protección de Outlook](https://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx) y [Creación de una regla de protección de Outlook](https://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx) en la biblioteca de Exchange.

-   **Reglas de flujo de correo** que un administrador configura para aplicar automáticamente plantillas u opciones de protección a los mensajes de correo electrónico. Estas reglas se basan en propiedades como el remitente, el destinatario, el asunto del mensaje y el contenido. Conceptualmente estas reglas son similares a las reglas de protección pero no permiten a los usuarios quitar la protección, ya que está establecida por el servicio de Exchange y no por el cliente. Como el servicio establece la protección, es irrelevante el dispositivo o el sistema operativo que tengan los usuarios. Para obtener más información, vea [Reglas de flujo de correo (reglas de transporte) en Exchange Online](/exchange/security-and-compliance/mail-flow-rules/mail-flow-rules) y [Crear una regla de protección de transporte](https://technet.microsoft.com/library/dd302432.aspx) para Exchange local.

-   **Directivas de prevención de pérdida de datos (DLP)** que contienen conjuntos de condiciones para filtrar mensajes de correo electrónico y tomar medidas para tratar de evitar la pérdida de contenido confidencial. Una de las acciones que puede especificar es aplicar el cifrado como protección, mediante la especificación de una de las opciones o plantillas de protección. Las sugerencias de las directivas se pueden usar cuando se detecta información confidencial, para alertar a los usuarios de que es posible que sea necesario aplicar protección. Para obtener más información, vea [Prevención de pérdida de datos](/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention) en la documentación de Exchange Online.

-   **Cifrado de mensajes de Office 365**, que admite el envío de un mensaje de correo protegido y documentos de Office protegidos como datos adjuntos a cualquier dirección de correo electrónico en cualquier dispositivo. Las cuentas de usuario que no usan Azure AD pueden usar la experiencia web, compatible con el uso de proveedores de identidades sociales o de un código de acceso de un solo uso. Para obtener más información, vea [Set up new Office 365 Message Encryption capabilities built on top of Azure Information Protection](/office365/securitycompliance/set-up-new-message-encryption-capabilities) (Configuración de las nuevas funciones de cifrado de mensajes de Office 365 sobre Azure Information Protection) en la documentación de Office 365. Para ayudarle a buscar información adicional relacionada con esta configuración, vea [Cifrado de mensajes de Office 365](https://docs.microsoft.com/office365/securitycompliance/ome).

Si usa Exchange local, puede usar las características de IRM con el servicio Azure Rights Management. Para ello, implemente el conector de Azure Rights Management. Este conector actúa como un punto de retransmisión entre los servidores locales y el servicio Azure Rights Management.

Para obtener más información sobre las plantillas de protección, vea [Configuración y administración de plantillas para Azure Information Protection](configure-policy-templates.md).

Para más información sobre las opciones de correo electrónico que se pueden usar para proteger los mensajes de correo, vea [Opción No reenviar para correos electrónicos](configure-usage-rights.md#do-not-forward-option-for-emails) y [Opción Solo cifrar para los correos electrónicos](configure-usage-rights.md#encrypt-only-option-for-emails).

Si ya está listo para configurar Exchange para proteger el correo electrónico:

- Para Exchange Online, vea [Configuración de IRM de Exchange Online](configure-office365.md#exchangeonline-irm-configuration)

- Para Exchange local: [Implementación del conector de Azure Rights Management](deploy-rms-connector.md).


## <a name="sharepoint-online-and-sharepoint-server"></a>SharePoint Online y SharePoint Server

Cuando se usa SharePoint Online o SharePoint Server, se pueden proteger los documentos mediante la característica Information Rights Management (IRM) de SharePoint. Esta característica permite a los administradores proteger listas o bibliotecas de modo que cuando un usuario consulte un documento, el archivo descargado esté protegido para que solo personas autorizadas puedan verlo y usarlo según las directivas de protección de la información que se hayan especificado. Por ejemplo, el archivo podría ser de solo lectura, deshabilitar el copiado del texto, evitar que se guarde una copia local e impedir que se pueda imprimir.

Los documentos de Word, PowerPoint, Excel y PDF admiten esta protección IRM de SharePoint. De manera predeterminada, la protección está restringida a la persona que descarga el documento. Puede cambiar este ajuste predeterminado por una opción de configuración denominada **Permitir la protección de grupos**, que amplía la protección a un grupo que se debe especificar. Por ejemplo, podría especificar un grupo que tenga permiso para editar documentos en la biblioteca para que el mismo grupo de usuarios pueda editar el documento fuera de SharePoint, independientemente de que el usuario descargue el documento. También podría especificar un grupo al que no se le hayan concedido permisos en SharePoint, pero los usuarios de este grupo deben acceder al documento fuera de SharePoint. 

Para listas y bibliotecas de SharePoint, esta protección siempre la configura un administrador, nunca un usuario final. Los permisos se establecen en el nivel de sitio, y estos permisos, de forma predeterminada, se heredan por cualquier lista o biblioteca de ese sitio. Si usa SharePoint Online, los usuarios también pueden configurar la protección IRM para su biblioteca de OneDrive para la Empresa.

Para un control más específico, puede configurar una lista o biblioteca en el sitio para que deje de heredar permisos de su elemento primario. Después, puede configurar los permisos de IRM en ese nivel (lista o biblioteca) y luego se denominarán "permisos exclusivos". Pero los permisos siempre se establecen en el nivel de contenedor, no se pueden establecer permisos en archivos individuales. 

En primer lugar, el servicio IRM se debe habilitar para SharePoint. Después, especifique los permisos IRM para una biblioteca. En el caso de SharePoint Online y OneDrive para la Empresa, los usuarios también pueden especificar permisos IRM para su biblioteca de OneDrive para la Empresa. SharePoint no usa plantillas de directiva de derechos, aunque hay valores de configuración de SharePoint que se pueden seleccionar que coinciden con la configuración que se puede especificar en las plantillas.

Si usa SharePoint Server, puede usar la protección IRM implementando el conector Azure Rights Management. Este conector actúa como un relé entre los servidores locales y el servicio en la nube de Rights Management. Para más información, consulte [Implementación del conector de Azure Rights Management](deploy-rms-connector.md).

> [!NOTE]
> Actualmente, hay algunas limitaciones al usar IRM de SharePoint:
> 
> - No pueden utilizar las plantillas de protección predeterminadas o personalizadas que se administran en Azure Portal. 
> 
> - No se admiten los archivos que tienen una extensión de nombre de archivo .ppdf para archivos PDF protegidos. Para más información sobre la visualización de documentos PDF protegidos, consulte [Lectores PDF protegidos para Microsoft Information Protection](./rms-client/protected-pdf-readers.md).
> 
> - Cuando más de un usuario edita un documento al mismo tiempo, la co-autoría no se admite. Para editar un documento en una biblioteca protegida mediante IRM, debe activar primero el documento y descargarlo y, a continuación, modificarlo en la aplicación de Office. Por lo tanto, solo una persona puede editar el documento a la vez.

Para las bibliotecas que no están protegidas mediante IRM, si protege un archivo que después carga en SharePoint o OneDrive, los siguientes no funcionan con este archivo: Coautoría, Office Online, búsqueda, vista previa de documentos, miniaturas, eDiscovery y prevención de pérdida de datos.

Al usar la protección IRM de SharePoint, el servicio Azure Rights Management aplica restricciones de uso y cifrado de datos a los documentos. Concretamente, se aplican al descargar los documentos de SharePoint y no al crearlos allí ni al cargarlos en la biblioteca. Para obtener información sobre cómo se protegen los documentos antes de descargarse, consulte [Cifrado de datos en OneDrive para la Empresa y SharePoint Online](https://technet.microsoft.com/library/dn905447.aspx) en la documentación de SharePoint.

Aunque ya no es nueva, la siguiente entrada del blog de Office 365 tiene información adicional que puede resultarle útil: [What’s New with Information Rights Management in SharePoint and SharePoint Online](https://www.microsoft.com/en-us/microsoft-365/blog/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/) (Novedades de Information Rights Management en SharePoint y SharePoint Online)

Si está listo para configurar SharePoint para IRM:

- Para SharePoint Online, vea [SharePoint Online y OneDrive para la Empresa: Configuración de IRM](configure-office365.md#sharepointonline-and-onedrive-for-business-irm-configuration).

- Para Sharepoint Server, vea [Implementación del conector de Azure Rights Management](deploy-rms-connector.md).


## <a name="next-steps"></a>Pasos siguientes

Si tiene Office 365, es posible que le interese revisar [Soluciones de protección de archivos en Office 365](/office365/enterprise/microsoft-cloud-it-architecture-resources#BKMK_O365fileprotect), que ofrece funcionalidades recomendadas para proteger archivos en Office 365.

Para conocer otras aplicaciones y servicios compatibles con el servicio Azure Rights Management de Azure Information Protection, vea [Compatibilidad de aplicaciones con el servicio Azure Rights Management](applications-support.md).

Si está listo para comenzar la implementación, que incluye la configuración de estas aplicaciones y servicios, vea el [Mapa de ruta de implementación de Azure Information Protection](deployment-roadmap.md).
