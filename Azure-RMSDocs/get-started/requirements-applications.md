---
title: "Compatibilidad de aplicaciones con la protección de datos | Azure Information Protection"
description: "Identifique las aplicaciones que usarán las API de RMS para que sean compatibles de forma nativa con el servicio Azure Rights Management de Azure Information Protection."
author: cabailey
manager: mbaldwin
ms.date: 10/17/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b6dbbfacd072d5badd69cc6ea452a86baa99cc46
ms.openlocfilehash: 0649b4300c1bd10ddcfc0c1432144f5eaa0b7797


---


# Aplicaciones compatibles con la protección de datos de Azure Rights Management

>*Se aplica a: Azure Information Protection, Office 365*


Use la tabla siguiente para identificar las aplicaciones que son compatibles de forma nativa con el servicio Azure Rights Management (Azure RMS), que ofrece la protección de datos para Azure Information Protection. 

Para estas aplicaciones, la compatibilidad de Rights Management está integrada estrechamente con el uso de las API de Rights Management para permitir la compatibilidad con restricciones de uso. Estas aplicaciones se conocen también como habilitadas para RMS.

A menos que se indique lo contrario, las funciones admitidas son válidas tanto para Azure RMS como para AD RMS. Además, la compatibilidad de AD RMS en iOS, Android, OS X y Windows Phone 8.1 requiere la [Extensión de dispositivos móviles para Active Directory Rights Management Services](https://technet.microsoft.com/library/dn673574.aspx).

Información acerca de las columnas de la tabla:

-   **PDF protegido:** archivos que tienen una extensión de nombre de archivo .ppdf y que se crean automáticamente al usar la aplicación RMS sharing para compartir archivos de Office y archivos PDF por correo electrónico. En la aplicación RMS sharing y la aplicación Azure Information Protection para iOS y Android se incluye un lector de archivos PDF protegidos. Si ya creó archivos PDF y los protegió con Azure RMS o AD RMS, podrá seguir leyendo estos archivos en dispositivos Windows, iOS y Android usando Foxit Reader y Nitro Pro.

-   **Correo electrónico:** los clientes de correo electrónico enumerados pueden proteger el mensaje de correo en sí, lo que hará que también se protejan automáticamente los archivos adjuntos. En este escenario, la característica de vista previa del cliente puede mostrar el contenido protegido (mensaje y datos adjuntos) a destinatarios autorizados. Sin embargo, si un mensaje de correo electrónico no está protegido pero los datos adjuntos si lo están, la característica de vista previa no puede mostrar dichos datos a destinatarios autorizados.

-   **Otros tipos de archivo:** los archivos de texto e imagen incluyen archivos que tienen una extensión de nombre de archivo como .txt, .xml, .jpg y .jpeg. Estos archivos cambian su extensión de nombre de archivo después de protegerlos de forma nativa con Rights Management y se convierten en archivos de solo lectura. Los archivos que no se pueden proteger de forma nativa pasan a tener una extensión de nombre de archivo .pfile después de protegerlos de forma genérica con Rights Management. Para más información, vea [Rights Management sharing application administrator guide](../rms-client/sharing-app-admin-guide.md) (Guía de administrador de la aplicación Rights Management sharing).


|**Sistema operativo de dispositivo**|Word, Excel, PowerPoint|PDF protegido|Correo electrónico|Otros tipos de archivo|
|-------------------------------|---------------------------|-----------------|---------|--------------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office 2016 <br /><br />Aplicaciones de Office Mobile (solo Azure RMS) [[1]](#footnote-1)<br /><br />Office Online [[2]](#footnote-2)|Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br />Aplicación RMS sharing|Outlook 2010<br /><br />Outlook 2013<br /><br />Office 2016 <br /><br />Outlook Web App (OWA) [[3]](#footnote-3)<br /><br />Correo de Windows [[4]](#footnote-4)|Aplicación RMS sharing para Windows: texto, imágenes, pfile<br /><br />Siemens JT2Go: archivos JT (solo Windows 10)|
|**iOS**|Office para iPad y iPhone [[5]](#footnote-5)<br /><br />Office Online [[2]](#footnote-2)<br /><br />Documentos TITUS|Aplicación Azure Information Protection [[1]](#footnote-1)<br /><br /> Foxit Reader<br /><br />Documentos TITUS|Aplicación Azure Information Protection [[1]](#footnote-1)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook para iPad y iPhone [[4]](#footnote-4)<br /><br />OWA para iOS [[3]](#footnote-3)<br /><br />TITUS Mail|Aplicación Azure Information Protection [[1]](#footnote-1): texto, imágenes<br /><br />Documentos TITUS: pfile|
|**Android**|GigaTrust App para Android<br /><br />Office Online [[2]](#footnote-2)<br /><br />Office Mobile (solo Azure RMS) [[1]](#footnote-1)|Aplicación Azure Information Protection [[1]](#footnote-1)<br /><br />GigaTrust App para Android<br /><br />Foxit Reader<br /><br />Aplicación RMS sharing [[1]](#footnote-1)|9Folders [[4]](#footnote-4)<br /><br />Aplicación Azure Information Protection [[1]](#footnote-1)<br /><br />GigaTrust App para Android [[4]](#footnote-4)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook para Android [[4]](#footnote-4)<br /><br />OWA para Android [[3]](#footnote-3) y [[7]](#footnote-7)<br /><br />Correo electrónico de Samsung (S3 y versiones posteriores) [[7]](#footnote-7)<br /><br />TITUS Classification for Mobile|Aplicación Azure Information Protection [[1]](#footnote-1): texto, imágenes|
|**OS X**|Office 2011 (solo AD RMS)<br /><br />Office 2016 para Mac<br /><br />Office Online [[2]](#footnote-2)|Foxit Reader<br /><br />Aplicación RMS sharing [[1]](#footnote-1)|Outlook 2011 (solo AD RMS)<br /><br />Outlook 2016 para Mac<br /><br />Outlook para Mac|Aplicación RMS sharing [[1]](#footnote-1): texto, imágenes, pfile|
|**Windows 10 Mobile**|Aplicaciones de Office Mobile (solo Azure RMS) [[1]](#footnote-1)|No compatible|Citrix WorxMail [[6]](#footnote-6)<br /><br />Correo de Outlook|No compatible|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [[2]](#footnote-2)|No compatible|Outlook 2013 RT<br /><br />Aplicación de correo para Windows<br /><br />Correo de Windows [[4]](#footnote-4)|Siemens JT2Go: archivos JT|
|**Windows Phone 8,1**|Office Mobile (solo AD RMS)|Aplicación RMS sharing [[1]](#footnote-1)|Outlook Mobile [[4]](#footnote-4)|Aplicación RMS sharing [[1]](#footnote-1): texto, imágenes, pfile|
|**Blackberry 10**|No compatible|No compatible|Correo electrónico de Blackberry [[4]](#footnote-4)|No compatible|


##### Nota al pie 1
Admite la visualización de contenido protegido.

##### Nota al pie 2 
Admite la visualización de contenido protegido en SharePoint Online, OneDrive para la Empresa y Outlook Web Access.

##### Nota al pie 3
Si un destinatario recibe un correo electrónico protegido y no usa Exchange como servidor de correo o si el remitente pertenece a otra organización, este contenido solo se puede abrir en un cliente de correo electrónico enriquecido, como Outlook. Este contenido no se puede abrir desde Outlook Web Access.

##### Nota al pie 4
Usa Exchange ActiveSync IRM, que debe habilitar el administrador de Exchange. Los usuarios pueden usar la opción de ver, responder y responder a todos para los mensajes de correo electrónico protegidos, pero no pueden proteger por su cuenta los mensajes de correo electrónico nuevos.

Si un destinatario recibe un correo electrónico protegido y no usa Exchange como servidor de correo o si el remitente pertenece a otra organización, este contenido solo se puede abrir en un cliente de correo electrónico enriquecido, como Outlook. Este contenido no se puede abrir desde Outlook Web Access o desde clientes de correo electrónico móvil que usan IRM de Exchange Active Sync.

##### Nota al pie 5
Admite la visualización y la edición de documentos protegidos. Para más información, vea la siguiente entrada en el blog de Office: [Azure Rights Management support comes to Office for iPad and iPhone](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/) (La compatibilidad de Azure Rights Management llega a Office para iPad y iPhone).

##### Nota al pie 6
Para obtener más información, vea la [documentación del producto para WorxMail](http://docs.citrix.com/en-us/worx-mobile-apps/10/xmob-worx-mail.html) de Citrix.

##### Nota al pie 7
Para más información, vea la siguiente entrada en el blog de Office: [OWA for Android now available on select devices](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/) (OWA para Android ahora disponible en algunos dispositivos).

## Más información sobre la compatibilidad de Azure RMS con Office

Azure RMS se integra estrechamente en las aplicaciones de Word, Excel, PowerPoint y Outlook, donde esta funcionalidad se conoce a menudo como Information Rights Management (IRM). Las siguientes ediciones del cliente de Office admiten la protección de archivos y correos electrónicos con Azure RMS:

- Office Professional Plus 2016

- Office Professional Plus 2013

- Office Professional Plus 2010

Todas las ediciones de Office (salvo Office 2007) pueden consumir contenido protegido.

Azure RMS con Office Professional Plus 2010 u Office Professional 2010:

- Requiere la aplicación de uso compartido Rights Management para Windows

- No se admite en Windows 10

## Más información sobre la aplicación Azure Information Protection para iOS y Android

La aplicación Azure Information Protection para iOS y Android reemplaza a la aplicación RMS sharing para esos dispositivos. Ofrece las mismas funciones y, además, es compatible con mensajes de correo electrónico con protección de derechos y archivos PDF con protección de derechos en SharePoint Online.

Si los dispositivos iOS y Android están inscritos en Microsoft Intune, puede implementar y administrar esta aplicación con una aplicación administrada por directivas. Para más información, consulte [Configure and deploy mobile application management policies in the Microsoft Intune console](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console) (Configuración e implementación de directivas de administración de aplicaciones móviles en la consola de Microsoft Intune). Para completar el paso 2 de esta documentación de Intune, siga las instrucciones para publicar una aplicación administrada por directiva.

Para más información, vea las [Preguntas más frecuentes para la aplicación Microsoft Azure Information Protection para iOS y Android](../rms-client/mobile-app-faq.md).


## Más información sobre la aplicación Rights Management sharing

Para obtener más información acerca de la aplicación de uso compartido Rights Management para Windows, consulte los recursos siguientes:

-   [Guía de administrador de la aplicación de uso compartido Rights Management](../rms-client/sharing-app-admin-guide.md)

-   [Guía de usuario de la aplicación de uso compartido Rights Management](../rms-client/sharing-app-user-guide.md)

Para obtener más información acerca de la aplicación de uso compartido Rights Management para plataformas móviles, consulte los recursos siguientes:

-   Descargue la aplicación correspondiente en los vínculos de la [página de Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970)

-   [Preguntas frecuentes para la aplicación de uso compartido Rights Management de Microsoft para plataformas móviles](https://technet.microsoft.com/dn451248)

> [!NOTE]
> La aplicación RMS sharing para iOS y Android se ha reemplazado por la aplicación Azure Information Protection.

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
Para comprobar otros requisitos, vea [Requisitos para Azure Information Protection](requirements-azure-rms.md).

Para más información sobre la compatibilidad de Azure RMS con las aplicaciones más usadas, vea [Compatibilidad de aplicaciones con el servicio Azure Rights Management](../understand-explore/applications-support.md).

Para más información sobre cómo configurar las aplicaciones de uso más común para Azure RMS, vea [Configuring applications for Azure Rights Management](../deploy-use/configure-applications.md) (Configuración de aplicaciones para Azure Rights Management).


<!--HONumber=Oct16_HO3-->


