---
title: Cómo los servicios y las aplicaciones de Office son compatibles con Azure RMS desde AIP
description: Cómo las aplicaciones de Office de usuario final (como Word y Outlook) y los servicios de Office (como Exchange y SharePoint) pueden usar el servicio Azure Rights Management desde AIP para ayudar a proteger los datos de una organización.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/17/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 388e67cd-c16f-4fa0-a7bb-ffe0def2be81
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 0a9dacaee902d802311c8b7ca76f3f8ed538b667
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39373367"
---
# <a name="how-office-applications-and-services-support-azure-rights-management"></a>Cómo las aplicaciones y los servicios de Office admiten Azure Rights Management 

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Las aplicaciones de Office de usuario final y los servicios de Office pueden usar el servicio Azure Rights Management desde Azure Information Protection con el objetivo de proteger los datos de la organización. Estas aplicaciones de Office son Word, Excel, PowerPoint y Outlook. Los servicios de Office son Exchange y SharePoint. Las configuraciones de Office que admiten el servicio Azure Rights Management suelen usar el término **Information Rights Management (IRM)**.

## <a name="office-applications-word-excel-powerpoint-outlook"></a>Aplicaciones de Office: Word, Excel, PowerPoint, Outlook
Estas aplicaciones admiten de forma nativa Azure Rights Management y permiten a los usuarios aplicar protección a un documento guardado o a un mensaje de correo electrónico que se enviará. Los usuarios pueden usar plantillas para aplicar la protección. En el caso de Word, Excel y PowerPoint, los usuarios pueden elegir configuraciones personalizadas para restricciones de uso, derechos y acceso. 

Por ejemplo, los usuarios pueden configurar un documento de Word para que solamente tengan acceso a él las personas de la organización, o controlar si se puede editar una hoja de cálculo de Excel, si se restringe a solo lectura o si se impide que se pueda imprimir. En el caso de los archivos sujetos a limitación temporal, se puede configurar una fecha de expiración en la que ya no se podrá tener acceso al archivo. Esta configuración pueden aplicarla directamente los usuarios o bien puede aplicarse mediante una plantilla. Para Outlook, los usuarios también pueden elegir la opción **No reenviar** con el fin de evitar la fuga de datos.

Además de la compatibilidad nativa de Office con Azure Rights Management, estas aplicaciones admiten la barra de Azure Information Protection que se instala con el [cliente de Azure Information Protection](../rms-client/aip-client.md). En esta barra se muestran etiquetas que facilitan a los usuarios aplicar automáticamente la protección a documentos y correos electrónicos que contienen información confidencial.

Si está listo para configurar aplicaciones de Office y el cliente de Azure Information Protection:

- Para configurar aplicaciones de Office, vea [Aplicaciones de Office: configuración para clientes](../deploy-use/configure-office-apps.md).

- Para instalar y configurar el cliente de Azure Information Protection, vea [Cliente de Azure Information Protection: instalación y configuración de clientes](../deploy-use/configure-client.md).

## <a name="exchange-online-and-exchange-server"></a>Exchange Online y Exchange Server
Cuando se usa Exchange Online o Exchange Server, es posible configurar opciones de Information Rights Management (IRM) compatibles con Azure Rights Management. Esta configuración permite a Exchange proporcionar las siguientes soluciones de protección:

-   **Exchange ActiveSync IRM** para que los dispositivos móviles puedan proteger y consumir mensajes de correo electrónico protegidos.

-   Compatibilidad con protección de correo electrónico para **Outlook en la Web**, que se implementa de forma similar en el cliente de Outlook. Esta configuración permite a los usuarios proteger mensajes de correo electrónico mediante plantillas o el establecimiento de opciones individuales. Los usuarios podrán leer y usar los mensajes de correo electrónico protegidos que se les envíen.

-   **Reglas de protección** para clientes de Outlook que un administrador configura para aplicar automáticamente plantillas de protección a mensajes de correo electrónico para destinatarios concretos. Por ejemplo, cuando se envían correos electrónicos internos a tu departamento legal, solo los miembros del departamento legal pueden leerlos y no se pueden reenviar. Los usuarios consultan la protección que se aplicará al mensaje de correo electrónico antes de enviarlo y, de forma predeterminada, pueden quitarla si deciden que no es necesaria. Los correos electrónicos se cifran antes de enviarlos. Para más información, consulte [Reglas de protección de Outlook](https://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx) y [Creación de una regla de protección de Outlook](https://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx) en la biblioteca de Exchange.

-   **Reglas de flujo de correo** que un administrador configura para aplicar automáticamente plantillas de protección a mensajes de correo electrónico. Estas reglas se basan en propiedades como el remitente, el destinatario, el asunto del mensaje y el contenido. Como concepto, estas reglas son similares a las reglas de protección, pero no permiten que los usuarios quiten la protección. Las reglas pueden aplicarse a Outlook en la Web y a mensajes de correo electrónico enviados desde un dispositivo móvil. Además, estas reglas no cifran los mensajes de correo electrónico antes de enviarlos desde el cliente. Para más información, consulte [Creación de una regla de protección de transporte](https://technet.microsoft.com/library/dd302432.aspx) en la biblioteca de Exchange.

-   **Directivas de prevención de pérdida de datos (DLP)** que contienen conjuntos de condiciones para filtrar mensajes de correo electrónico y tomar medidas para tratar de evitar la pérdida de contenido confidencial, por ejemplo, información personal o de tarjetas de crédito. Las sugerencias de las directivas se pueden usar cuando se detecta información confidencial, para alertar a los usuarios de que es posible que sea necesario aplicar protección. Para más información, consulte [Prevención de pérdida de datos] (https://technet.microsoft.com/library/jj150527(v=exchg.160\).aspx) en la biblioteca de Exchange.

-   **Cifrado de mensajes de Office 365**, que admite enviar un mensaje de correo protegido y documentos de Office protegidos como datos adjuntos a cualquier dirección en cualquier dispositivo. Las cuentas de usuario que no usan Azure AD pueden usar la experiencia web, compatible con el uso de proveedores de identidades sociales o de un código de acceso de un solo uso. Para más información, vea [Set up new Office 365 Message Encryption capabilities built on top of Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e) (Configuración de nuevas capacidades del cifrado de mensajes de Office 365 sobre Azure Information Protection) desde el sitio web de Office.

Si usa Exchange local, puede usar las características de IRM con el servicio Azure Rights Management. Para ello, implemente el conector de Azure Rights Management. Este conector actúa como un punto de retransmisión entre los servidores locales y el servicio Azure Rights Management.

Si está listo para configurar Exchange para IRM:

- Para Exchange Online, vea [Exchange Online: Configuración de IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration).

- Para Exchange local: [Implementación del conector de Azure Rights Management](../deploy-use/deploy-rms-connector.md).


## <a name="sharepoint-online-and-sharepoint-server"></a>SharePoint Online y SharePoint Server

Cuando se usa SharePoint Online o SharePoint Server, se pueden proteger los documentos mediante la característica Information Rights Management (IRM) de SharePoint. Esta característica permite a los administradores proteger listas o bibliotecas de modo que cuando un usuario consulte un documento, el archivo descargado esté protegido para que solo personas autorizadas puedan verlo y usarlo según las directivas de protección de la información que se hayan especificado. Por ejemplo, el archivo podría ser de solo lectura, deshabilitar el copiado del texto, evitar que se guarde una copia local e impedir que se pueda imprimir.

Los documentos de Word, PowerPoint, Excel y PDF admiten esta protección IRM de SharePoint. De manera predeterminada, la protección está restringida a la persona que descarga el documento. Puede cambiar este valor predeterminado con una opción de configuración que extiende la protección a todos los usuarios que tienen acceso al documento en SharePoint o a un grupo que especifique.

Para listas y bibliotecas de SharePoint, esta protección siempre la configura un administrador, nunca un usuario final. Los permisos se establecen en el nivel de sitio, y estos permisos, de forma predeterminada, se heredan por cualquier lista o biblioteca de ese sitio. Si usa SharePoint Online, los usuarios también pueden configurar la protección IRM para su biblioteca de OneDrive para la Empresa.

Para un control más específico, puede configurar una lista o biblioteca en el sitio para que deje de heredar permisos de su elemento primario. Después, puede configurar los permisos de IRM en ese nivel (lista o biblioteca) y luego se denominarán "permisos exclusivos". Pero los permisos siempre se establecen en el nivel de contenedor, no se pueden establecer permisos en archivos individuales. 

En primer lugar, el servicio IRM se debe habilitar para SharePoint. Después, especifique los permisos IRM para una biblioteca. En el caso de SharePoint Online y OneDrive para la Empresa, los usuarios también pueden especificar permisos IRM para su biblioteca de OneDrive para la Empresa. SharePoint no usa plantillas de directiva de derechos, aunque hay valores de configuración de SharePoint que se pueden seleccionar que coinciden con la configuración que se puede especificar en las plantillas.

Si usa SharePoint Server, puede usar la protección IRM implementando el conector Azure Rights Management. Este conector actúa como un relé entre los servidores locales y el servicio en la nube de Rights Management. Para más información, consulte [Implementación del conector de Azure Rights Management](../deploy-use/deploy-rms-connector.md).

> [!NOTE]
> Actualmente, hay algunas limitaciones al usar IRM de SharePoint:
> 
> - No pueden utilizar las plantillas de protección predeterminadas o personalizadas que se administran en Azure Portal. 
> 
> - No se admiten los archivos que tienen una extensión de nombre de archivo .ppdf para archivos PDF protegidos. Se admiten los archivos que tienen la extensión de nombre de archivo .pdf y, cuando se descargan, se pueden abrir con una aplicación PDF que admita de forma nativa Rights Management. Por ejemplo, el cliente de Azure Information Protection para Windows incluye un visor para estos archivos PDF protegidos. Se recogen otros visores PDF alternativos en la [tabla de aplicaciones habilitadas para RMS](../get-started/requirements-applications.md#rms-enlightened-applications).
> 
> - No se admite la generación conjunta, cuando más de una persona edita un documento al mismo tiempo. Para editar un documento en una biblioteca protegida mediante IRM, debe activar primero el documento y descargarlo y, a continuación, modificarlo en la aplicación de Office. Por lo tanto, solo una persona puede editar el documento a la vez.

En el caso de las bibliotecas que no estén protegidas mediante IRM, al proteger un archivo y cargarlo en SharePoint u OneDrive, las características siguientes no son compatibles con el archivo: coautoría, Office Online, búsqueda, vista previa de documentos, miniaturas, eDiscovery y prevención de pérdida de datos (DLP).

Al usar la protección IRM de SharePoint, el servicio Azure Rights Management aplica restricciones de uso y cifrado de datos a los documentos. Concretamente, se aplican al descargar los documentos de SharePoint y no al crearlos allí ni al cargarlos en la biblioteca. Para obtener información sobre cómo se protegen los documentos antes de descargarse, consulte [Cifrado de datos en OneDrive para la Empresa y SharePoint Online](https://technet.microsoft.com/library/dn905447.aspx) en la documentación de SharePoint.

Aunque ya no sea una novedad, la siguiente entrada del blog de Office 365 contiene información adicional que podría ser útil: [What’s New with Information Rights Management in SharePoint and SharePoint Online](https://www.microsoft.com/en-us/microsoft-365/blog/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/) (Novedades de Information Rights Management en SharePoint y SharePoint Online.)

Si está listo para configurar SharePoint para IRM:

- Para SharePoint Online, vea [SharePoint Online y OneDrive para la Empresa: Configuración de IRM](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration).

- Para Sharepoint Server, vea [Implementación del conector de Azure Rights Management](../deploy-use/deploy-rms-connector.md).


## <a name="next-steps"></a>Pasos siguientes

Si tiene Office 365, es posible que le interese revisar [Soluciones de protección de archivos en Office 365](/office365/enterprise/microsoft-cloud-it-architecture-resources#BKMK_O365fileprotect), que ofrece funcionalidades recomendadas para proteger archivos en Office 365.

Para conocer otras aplicaciones y servicios compatibles con el servicio Azure Rights Management de Azure Information Protection, vea [Compatibilidad de aplicaciones con el servicio Azure Rights Management](applications-support.md).

Si está listo para comenzar la implementación, que incluye la configuración de estas aplicaciones y servicios, vea el [Mapa de ruta de implementación de Azure Information Protection](../plan-design/deployment-roadmap.md).
