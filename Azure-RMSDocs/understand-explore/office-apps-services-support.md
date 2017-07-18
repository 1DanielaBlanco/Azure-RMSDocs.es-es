---
title: Aplicaciones y servicios de Office con Azure Information Protection
description: "Cómo las aplicaciones de Office de usuario final (como Word, Excel, PowerPoint y Outlook) y los servicios de Office (como Exchange y SharePoint) pueden usar el servicio Azure Rights Management para ayudar a proteger los datos de una organización."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/11/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 388e67cd-c16f-4fa0-a7bb-ffe0def2be81
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 7fe044ab9b8e253e3095af5828a33926271bc42b
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2017
---
# <a name="office-applications-and-services"></a>Aplicaciones y servicios de Office

>*Se aplica a: Azure Information Protection, Office 365*

Las aplicaciones de Office de usuario final (como Word, Excel, PowerPoint y Outlook) y los servicios de Office (como Exchange y SharePoint) pueden usar el servicio Azure Rights Management de Azure Information Protection con la idea de proteger los datos de su organización.

## <a name="office-applications-word-excel-powerpoint-outlook"></a>Aplicaciones de Office: Word, Excel, PowerPoint, Outlook
Estas aplicaciones admiten de forma nativa Rights Management mediante Information Rights Management (IRM) y permiten a los usuarios aplicar protección a un documento guardado o a un mensaje de correo electrónico que se enviará. Los usuarios pueden aplicar plantillas o, para Word, Excel y PowerPoint, pueden elegir configuraciones muy personalizadas para restricciones de acceso, derechos y uso. 

Por ejemplo, los usuarios pueden configurar un documento de Word para que solamente pueda acceder a él gente de la organización, o controlar si se puede editar una hoja de cálculo de Excel, si se restringe a solo lectura o si se impide que se pueda imprimir. Para archivos sujetos a limitación temporal, se puede configurar una fecha de caducidad (directamente por parte de los usuarios o aplicando una plantilla) en la que ya no se podrá acceder al archivo. Para Outlook, los usuarios pueden elegir la opción **No reenviar** con el fin de evitar la fuga de datos, además de elegir una plantilla.

Además de la compatibilidad nativa con IRM, estas aplicaciones admiten la barra de Azure Information Protection que se instala con el [cliente de Azure Information Protection](../rms-client/aip-client.md). Esta barra muestra etiquetas que facilitan a los usuarios aplicar automáticamente la protección de Rights Management a documentos y correos electrónicos que contienen datos confidenciales.

Si está listo para configurar aplicaciones de Office y el cliente de Azure Information Protection:

- Para configurar aplicaciones de Office, vea [Aplicaciones de Office: configuración para clientes](../deploy-use/configure-office-apps.md).

- Para instalar y configurar el cliente de Azure Information Protection, vea [Cliente de Azure Information Protection: instalación y configuración de clientes](../deploy-use/configure-client.md).

## <a name="exchange-online-and-exchange-server"></a>Exchange Online y Exchange Server
Cuando usas Exchange Online o Exchange Server, puedes utilizar la integración de Information Rights Management (IRM), que proporciona más soluciones de protección de la información:

-   **Exchange ActiveSync IRM** para que los dispositivos móviles puedan proteger y consumir mensajes de correo electrónico protegidos.

-   Compatibilidad de RMS con **Outlook Web App**, que se implementa de forma similar al cliente de Outlook, para que los usuarios puedan proteger mensajes de correo electrónico mediante plantillas o especificando opciones individuales. Y los usuarios pueden leer y usar los mensajes de correo electrónico protegidos que se les hayan enviado.

-   **Reglas de protección** para clientes de Outlook que un administrador configura para aplicar automáticamente plantillas de Rights Management a mensajes de correo electrónico para destinatarios concretos. Por ejemplo, cuando se envían correos electrónicos internos a tu departamento legal, solo los miembros del departamento legal pueden leerlos y no se pueden reenviar. Los usuarios consultan la protección que se aplicará al mensaje de correo electrónico antes de enviarlo y, de forma predeterminada, pueden quitarla si deciden que no es necesaria. Los correos electrónicos se cifran antes de enviarlos. Para más información, consulte [Reglas de protección de Outlook](https://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx) y [Creación de una regla de protección de Outlook](https://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx) en la biblioteca de Exchange.

-   **Reglas de transporte** que un administrador configura para aplicar automáticamente plantillas de Rights Management a mensajes de correo electrónico en función de propiedades como el remitente, el destinatario, el asunto del mensaje y el contenido. Dichas reglas son similares en concepto a las reglas de protección, pero no permiten a los usuarios quitar la protección. Se pueden aplicar a Outlook Web Access y a correos electrónicos enviados mediante dispositivos móviles, y no cifra mensajes de correo electrónico antes de que el cliente los envíe. Para más información, consulte [Creación de una regla de protección de transporte](https://technet.microsoft.com/library/dd302432.aspx) en la biblioteca de Exchange.

-   **Directivas de prevención de la pérdida de datos (DLP)** que contienen conjuntos de condiciones para filtrar mensajes de correo electrónico y tomar medidas para tratar de evitar la pérdida de contenido confidencial (por ejemplo, información personal o de tarjetas de crédito). Las sugerencias de las directivas se pueden usar cuando se detectan datos sensibles, para alertar a los usuarios de que es posible que sea necesario aplicar protección de la información, en función de la información del mensaje de correo electrónico. Para más información, consulte [Prevención de pérdida de datos](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx) en la biblioteca de Exchange.

-   **Cifrado de mensajes de Office 365** que usa reglas de transporte para enviar correos electrónicos cifrados a personas que están fuera de su compañía y que leen el correo en un explorador con una interfaz similar a la de Outlook Web App. Puedes personalizar el texto de aviso y el texto de cabecera en los correos electrónicos cifrados de tu compañía e, incluso, agregar el logotipo de la compañía. Para más información, consulte [Cifrado de mensajes de Office 365](https://office.microsoft.com/o365-message-encryption-FX104179182.aspx) en el sitio web de Office.

Si usa Exchange Server, puede usar las funciones de protección de la información con el servicio Azure Rights Management implementando el conector RMS, que actúa como un transmisor entre tus servidores locales y el servicio Azure Rights Management.

Si está listo para configurar Exchange para IRM:

- Para Exchange Online, vea [Exchange Online: Configuración de IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration).

- Para Exchange local: [Implementación del conector de Azure Rights Management](../deploy-use/deploy-rms-connector.md).


## <a name="sharepoint-online-and-sharepoint-server"></a>SharePoint Online y SharePoint Server

Cuando se usa SharePoint Online o SharePoint Server, se pueden proteger los documentos mediante Information Rights Management (IRM). Esta configuración permite a los administradores proteger listas o bibliotecas para que cuando un usuario consulte un documento, el archivo descargado esté protegido para que solo personas autorizadas puedan verlo y usarlo según las directivas de protección de la información que se hayan especificado. Por ejemplo, el archivo podría ser de solo lectura, deshabilitar el copiado del texto, evitar que se guarde una copia local e impedir que se pueda imprimir.

De manera predeterminada, la protección está restringida a la persona que descarga el documento. Pero puede cambiar esto con una opción de configuración que extiende la protección a todos los usuarios que tienen acceso al documento en SharePoint o a un grupo que especifique.

Para listas y bibliotecas de SharePoint, la protección de la información siempre la configura un administrador, nunca un usuario final. Los permisos se establecen en el nivel de sitio, y estos permisos, de forma predeterminada, se heredan por cualquier lista o biblioteca de ese sitio. Si usa SharePoint Online, los usuarios también pueden configurar la protección IRM para su biblioteca de OneDrive para la Empresa.

Para un control más específico, puede configurar una lista o biblioteca en el sitio para que deje de heredar permisos de su elemento primario. Después, puede configurar los permisos de IRM en ese nivel (lista o biblioteca) y luego se denominarán "permisos exclusivos". Pero los permisos siempre se establecen en el nivel de contenedor, no se pueden establecer permisos en archivos individuales. 

En primer lugar, el servicio IRM se debe habilitar para SharePoint. Después, especifique los permisos IRM para una biblioteca. En el caso de SharePoint Online y OneDrive para la Empresa, los usuarios también pueden especificar permisos IRM para su biblioteca de OneDrive para la Empresa. SharePoint no usa plantillas de directiva de derechos, aunque hay valores de configuración de SharePoint que se pueden seleccionar que coinciden con la configuración que se puede especificar en las plantillas.

Si usa SharePoint Server, puede usar la protección IRM implementando el conector Azure Rights Management. Este conector actúa como un relé entre los servidores locales y el servicio en la nube de Rights Management. Para más información, consulte [Implementación del conector de Azure Rights Management](../deploy-use/deploy-rms-connector.md).

> [!NOTE]
> Actualmente, hay algunas limitaciones al usar IRM de SharePoint:
> 
> - No puede usar las plantillas predeterminadas o personalizadas que se administran en el Portal de Azure clásico. 
> 
> - Los archivos que tienen una extensión de nombre de archivo .PPDF para archivos PDF protegidos no se admiten. Los archivos que tienen una extensión de nombre de archivo .PDF y que han sido protegidos forma nativa por Rights Management se admiten cuando se usa un lector PDF que admita Rights Management de forma nativa.


Cuando se usa la protección IRM, el servicio Azure Rights Management aplica restricciones de uso y cifrado de datos para documentos cuando se descargan de SharePoint y no cuando el documento se crea primero en SharePoint o se carga en la biblioteca. Para obtener información sobre cómo se protegen los documentos antes de descargarse, consulte [Cifrado de datos en OneDrive para la Empresa y SharePoint Online](https://technet.microsoft.com/library/dn905447.aspx) en la documentación de SharePoint.

Aunque ya no sea una novedad, la siguiente entrada del blog de Office contiene información adicional que podría ser útil: [What’s New with Information Rights Management in SharePoint and SharePoint Online](https://blogs.office.com/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/) (Novedades de Information Rights Management en SharePoint y SharePoint Online)

Si está listo para configurar SharePoint para IRM:

- Para SharePoint Online, vea [SharePoint Online y OneDrive para la Empresa: Configuración de IRM](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration).

- Para Sharepoint Server, vea [Implementación del conector de Azure Rights Management](../deploy-use/deploy-rms-connector.md).


## <a name="next-steps"></a>Pasos siguientes

Para conocer otras aplicaciones y servicios compatibles con el servicio Azure Rights Management de Azure Information Protection, vea [Compatibilidad de aplicaciones con el servicio Azure Rights Management](applications-support.md).

Si está listo para comenzar la implementación, que incluye la configuración de estas aplicaciones y servicios, vea el [Mapa de ruta de implementación de Azure Information Protection](/plan-design/deployment-roadmap.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]