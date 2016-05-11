---
# required metadata

title: Requisitos de Azure RMS&#58; aplicaciones | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Requisitos de Azure RMS: aplicaciones

Use la siguiente tabla para saber qué aplicaciones son compatibles de forma nativa con Azure RMS. Esto significa que RMS se integra estrechamente en estas aplicaciones mediante las API de RMS para admitir restricciones de uso. Estas aplicaciones se conocen también como habilitadas para RMS.

A menos que se indique lo contrario, las funciones admitidas son válidas tanto para Azure RMS como para AD RMS. Además, la compatibilidad de AD RMS en iOS, Android, OS X y Windows Phone 8.1 requiere la [Extensión de dispositivos móviles para Active Directory Rights Management Services](https://technet.microsoft.com/library/dn673574.aspx).

Información acerca de las columnas de la tabla:

-   **PDF protegido:** archivos que tienen una extensión de nombre de archivo .ppdf y que se crean automáticamente al usar la aplicación RMS sharing para compartir archivos de Office y archivos PDF por correo electrónico. La aplicación de uso compartido RMS incluye un lector para archivos PDF protegidos. Si ya creó archivos PDF y los protegió con Azure RMS o AD RMS, podrá seguir leyendo estos archivos en dispositivos Windows, iOS y Android usando Foxit Reader y Nitro Pro.

-   **Correo electrónico:** los clientes de correo electrónico enumerados pueden proteger el mensaje de correo en sí, lo que hará que también se protejan automáticamente los archivos adjuntos. En este escenario, la característica de vista previa del cliente puede mostrar el contenido protegido (mensaje y datos adjuntos) a destinatarios autorizados. Sin embargo, si un mensaje de correo electrónico no está protegido pero los datos adjuntos si lo están, la característica de vista previa no puede mostrar dichos datos a destinatarios autorizados.

-   **Otros tipos de archivo:** los archivos de texto e imagen incluyen archivos que tienen una extensión de nombre de archivo como .txt, .xml, .jpg y .jpeg. Estos archivos cambian su extensión de nombre de archivo después de que se protegen de forma nativa con RMS y se hacen de solo lectura. Los archivos que no se pueden proteger de forma nativa pasan a tener una extensión de nombre de archivo .pfile después de que RMS los proteja de forma genérica. Para más información, vea [Rights Management sharing application administrator guide](../rms-client/sharing-app-admin-guide.md) (Guía de administrador de la aplicación Rights Management sharing).


|**Sistema operativo de dispositivo**|Word, Excel, PowerPoint|PDF protegido|Correo electrónico|Otros tipos de archivo|
|-------------------------------|---------------------------|-----------------|---------|--------------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Aplicaciones de Office Mobile (solo Azure RMS) [[1]](#footnote-1)<br /><br />Office Online [[2]](#footnote-2)|Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br />Aplicación RMS sharing|Outlook 2010<br /><br />Outlook 2013<br /><br />Outlook Web App (OWA) [[3]](#footnote-3)<br /><br />Correo de Windows [[4]](#footnote-4)|Aplicación RMS sharing para Windows: texto, imágenes, pfile<br /><br />Siemens JT2Go: archivos JT (solo Windows 10)|
|**iOS**|Office para iPad y iPhone [[5]](#footnote-5)<br /><br />Office Online [[2]](#footnote-2)<br /><br />Documentos TITUS|Foxit Reader<br /><br />Aplicación RMS sharing [[1]](#footnote-1)<br /><br />Documentos TITUS|Citrix WorxMail<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook para iPad y iPhone [[4]](#footnote-4)<br /><br />OWA para iOS [[3]](#footnote-3)<br /><br />TITUS Mail|Aplicación RMS sharing [[1]](#footnote-1): texto, imágenes, pfile<br /><br />Documentos TITUS: pfile|
|**Android**|GigaTrust App para Android<br /><br />Office Online [[2]](#footnote-2)|GigaTrust App para Android<br /><br />Foxit Reader<br /><br />Aplicación RMS sharing [[1]](#footnote-1)|9Folders [[4]](#footnote-4)<br /><br />GigaTrust App para Android [[4]](#footnote-4)<br /><br />Citrix WorxMail<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />OWA para Android [[3]](#footnote-3) y [[6]](#footnote-6)<br /><br />Correo electrónico de Samsung (S3 y versiones posteriores) [[6]](#footnote-6)<br /><br />TITUS Classification for Mobile|Aplicación RMS sharing [[1]](#footnote-1): texto, imágenes, pfile|
|**OS X**|Office 2011 (solo AD RMS)<br /><br />Office 2016 para Mac<br /><br />Office Online [[2]](#footnote-2)|Foxit Reader<br /><br />Aplicación RMS sharing [[1]](#footnote-1)|Outlook 2011 (solo AD RMS)<br /><br />Outlook 2016 para Mac<br /><br />Outlook para Mac|Aplicación RMS sharing [[1]](#footnote-1): texto, imágenes, pfile|
|**Windows 10 Mobile**|Aplicaciones de Office Mobile (solo Azure RMS) [[1]](#footnote-1)|No compatible|Citrix WorxMail<br /><br />Correo de Outlook|No compatible|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [[2]](#footnote-2)|No compatible|Outlook 2013 RT<br /><br />Aplicación de correo para Windows<br /><br />Correo de Windows [[4]](#footnote-4)|Siemens JT2Go: archivos JT|
|**Windows Phone 8,1**|Office Mobile (solo AD RMS)|Aplicación RMS sharing [[1]](#footnote-1)|Outlook Mobile [[4]](#footnote-4)|Aplicación RMS sharing [[1]](#footnote-1): texto, imágenes, pfile|
|**Blackberry 10**|No compatible|No compatible|Correo electrónico de Blackberry [[4]](#footnote-4)|No compatible|


###### Nota al pie 1
Admite la visualización de contenido protegido.

###### Nota al pie 2 
Admite la visualización de contenido protegido en SharePoint Online, OneDrive para la Empresa y Outlook Web Access.

###### Nota al pie 3
Si un destinatario tiene un buzón de Exchange local y recibe un correo electrónico protegido, este contenido solo se puede abrir en un cliente de correo electrónico enriquecido, como Outlook.  Este contenido no se puede abrir desde Outlook Web Access.

###### Nota al pie 4
Usa Exchange ActiveSync IRM, que debe habilitar el administrador de Exchange. Los usuarios pueden usar la opción de ver, responder y responder a todos para los mensajes de correo electrónico protegidos, pero no pueden proteger por su cuenta los mensajes de correo electrónico nuevos.

Si un destinatario tiene un buzón de Exchange local y recibe un correo electrónico protegido de otra organización que usa Exchange, este contenido solo se puede abrir en un cliente de correo electrónico enriquecido, como Outlook.  Este contenido no se puede abrir desde un dispositivo que use Exchange Active Sync IRM.

###### Nota al pie 5
Admite la visualización y la edición de documentos protegidos. Para más información, vea la siguiente entrada en el blog de Office: [Azure Rights Management support comes to Office for iPad and iPhone](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/) (La compatibilidad de Azure Rights Management llega a Office para iPad y iPhone).

###### Nota al pie 6
Para más información, vea la siguiente entrada en el blog de Office: [OWA for Android now available on select devices](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/) (OWA para Android ahora disponible en algunos dispositivos).

## Más información sobre la compatibilidad de Azure RMS con Office

Todas las ediciones de Office (salvo Office 2007) pueden consumir contenido protegido.

Azure RMS con Office Professional Plus 2010 u Office Professional 2010:

- Requiere la aplicación de uso compartido Rights Management para Windows

- No se admite en Windows 10


## Más información sobre la aplicación Rights Management sharing

Para obtener más información acerca de la aplicación de uso compartido Rights Management para Windows, consulte los recursos siguientes:

-   [Guía de administrador de la aplicación de uso compartido Rights Management](../rms-client/sharing-app-admin-guide.md)

-   [Guía de usuario de la aplicación de uso compartido Rights Management](../rms-client/sharing-app-user-guide.md)

Para obtener más información acerca de la aplicación de uso compartido Rights Management para plataformas móviles, consulte los recursos siguientes:

-   Descargue la aplicación correspondiente mediante los vínculos de la [página de Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970).

-   Si tiene Microsoft Intune, puede implementar y administrar la aplicación mediante una aplicación administrada por directivas: 

    -   Si son dispositivos iOS y Android inscritos por Intune: [Configure and deploy mobile application management policies in the Microsoft Intune console](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console) (Configuración e implementación de directivas de administración de aplicaciones móviles en la consola de Microsoft Intune).

    -   Si son dispositivos iOS y Android no inscritos por Intune: [Create and deploy mobile app management policies with Microsoft Intune](/intune/deploy-use/create-and-deploy-mobile-app-management-policies-with-microsoft-intune) (Crear e implementar directivas de administración de aplicaciones móviles con Microsoft Intune).

-   [Preguntas frecuentes para la aplicación de uso compartido Rights Management de Microsoft para plataformas móviles](https://technet.microsoft.com/dn451248)



## Más información sobre otras aplicaciones que admiten Azure RMS

Aparte de las aplicaciones de la tabla, cualquier aplicación que permita integrar la API de RMS con Azure RMS, a saber:

- Aplicaciones de línea de negocio escritas internamente con RMS SDK.

- Aplicaciones de proveedores de software escritas con RMS SDK.

Para más información sobre el SDK, vea [Microsoft Rights Management SDK](../develop/developers-guide.md).

## Aplicaciones no compatibles con Azure RMS

Las siguientes aplicaciones no son compatibles actualmente con Azure RMS:

-   Microsoft Office para Mac 2011

-   Microsoft OneDrive para la Empresa para SharePoint Server 2013

-   Visor de XPS
 
Además, la aplicación de uso compartido de RMS presenta la restricciones siguientes:

-   En equipos con Windows: se necesita una versión mínima de Windows 7 Service Pack 1



## Pasos siguientes
Para buscar otros requisitos, vea [Requirements for Azure Rights Management](requirements-azure-rms.md) (Requisitos de Azure Rights Management).

Para más información sobre cómo  las aplicaciones de uso más común admiten Azure RMS, vea [How applications support Azure Rights Management](../understand-explore/applications-support.md) (Cómo admiten las aplicaciones Azure Rights Management).

Para más información sobre cómo configurar las aplicaciones de uso más común para Azure RMS, vea [Configuring applications for Azure Rights Management](../deploy-use/configure-applications.md) (Configuración de aplicaciones para Azure Rights Management).

<!--HONumber=Apr16_HO4-->


