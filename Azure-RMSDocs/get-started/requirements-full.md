---
title: "Requisitos de Azure Information Protection - Artículo completo | Azure Information Protection"
description: "Identifique los requisitos previos para implementar Azure Information Protection en su organización."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 10cf9371-a61b-495f-9d42-898448806994
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 68b3d74d32b98f44cfdf9cf78b7a9151f16124ce
ms.openlocfilehash: b4afd639439f0549ce38de1e63a1798d30680066


---


# <a name="requirements-for-azure-information-protection"></a>Requirements for Azure Information Protection (Requisitos de Azure Information Protection)

>*Se aplica a: Azure Information Protection, Office 365*


Antes de implementar Azure Information Protection para su organización, asegúrese de que tiene los siguientes requisitos previos. 

|Requisito|Más información|
|---------------|--------------------|
|Una suscripción a Azure Information Protection|Revise la [información sobre la suscripción](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing) y la [lista de características](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features) en el sitio de Azure Information Protection para asegurarse de que la suscripción de la organización incluye las características de Azure Information Protection que quiere usar.|
|Azure Active Directory|Su organización debe tener un directorio de Azure Active Directory (Azure AD) para admitir la autenticación de usuario para Azure Information Protection. Además, si desea usar sus cuentas de usuario desde su directorio local (AD DS), también deberá configurar la integración de directorios.<br /><br />Si las cuentas están federadas (por ejemplo, usa AD FS), deben usar la autenticación integrada de Windows. No se admite la autenticación basada en formularios en Azure Information Protection.<br /><br />Multi-Factor Authentication (MFA) es compatible con Azure Information Protection si tiene el software cliente necesario y la infraestructura de MFA configurada correctamente.<br /><br />Para obtener más información, vea [Requisitos de Azure Active Directory para Azure Information Protection](requirements-azure-ad.md).|
|Dispositivos cliente|Los usuarios deben tener dispositivos cliente (equipo o dispositivo móvil) que ejecuten un sistema operativo compatible con Azure Information Protection.<br /><br />Los siguientes dispositivos admiten el cliente de Azure Information Protection, que permite a los usuarios clasificar y etiquetar los correos electrónicos y documentos de Office:<br /><br />- Windows 10 (x86 y x64)<br /><br />- Windows 8.1 (x86 y x64)<br /><br />- Windows 8 (x86 y x64)<br /><br />- Windows 7 Service Pack 1 (x86 y x64)<br /><br />Cuando este cliente protege los datos mediante el servicio Azure Rights Management, puede consumirse por los mismos dispositivos (Windows, Mac, iOS, Android), que admiten el servicio Azure Rights Management. <br /><br />Para obtener información sobre los dispositivos que admiten el servicio Azure Rights Management, vea [Requisitos de Azure RMS: Dispositivos cliente que son compatibles con Azure RMS](../get-started/requirements-client-devices.md).|
|Aplicaciones|El cliente de Azure Information Protection admite el etiquetado y la protección de archivos y correos electrónicos creados con las siguientes aplicaciones de Office: **Word**, **Excel**, **PowerPoint** y **Outlook** desde los siguientes paquetes de Office:<br /><br />- Office Professional Plus 2016<br /><br />- Office Professional Plus 2013 con Service Pack 1<br /><br />- Office Professional Plus 2010<br /><br />Para obtener información sobre las aplicaciones que son compatibles con el servicio Azure Rights Management, vea [Aplicaciones compatibles con la protección de datos de Azure Rights Management](requirements-applications.md).|
|Infraestructura compatible con la conectividad a Internet y dependiente de los servicios en la nube|Si tiene un firewall o dispositivos de red de intervención similares que deban configurarse para permitir conexiones específicas, vea la información de **Azure Rights Management (RMS)** en la sección [Portal de Office 365 e infraestructura compartida](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#BKMK_Portal-identity) del siguiente artículo de Office: [URL de Office 365 e intervalos de direcciones IP](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).<br /><br />Siga las instrucciones de este artículo de Office para suscribirse a una fuente RSS y mantenerse así al día de los cambios que se hagan en esta información.<br /><br />Además de la información del artículo de Office específica de Azure Information Protection:<br /><br />- Permita tráfico HTTPS en TCP 443 a **api.informationprotection.azure.com**.<br /><br />- No termine la conexión TLS de cliente a servicio (por ejemplo, para realizar una inspección de los paquetes). Al hacerlo, se interrumpe la asignación de certificados que los clientes de RMS utilizan con las entidades de certificación administradas por Microsoft para ayudar a proteger su comunicación con Azure RMS.<br /><br />- Si usa un proxy web que precisa de autenticación, debe configurarlo para usar autenticación integrada de Windows con las credenciales de inicio de sesión de Active Directory del usuario.|

Si quiere usar el servicio Azure Rights Management de Azure Information Protection con servidores locales, los siguientes productos son compatibles:

-   Exchange Server

-   Servidor de SharePoint

-   Servidores de archivos de Windows Server que son compatibles con la Infraestructura de la clasificación de archivos

Para más información sobre los requisitos adicionales para este escenario, vea [Requisitos de Azure RMS: Servidores locales que son compatibles con Azure RMS](requirements-servers.md).

> [!IMPORTANT]
> El siguiente escenario de implementación no se admite a no ser que esté usando la protección de AD RMS con Azure Information Protection (la configuración “conserve su propia clave” o HYOK):
> 
> -   Ejecución de AD RMS y Azure RMS en paralelo en la misma organización, salvo durante la migración, tal como se describe en [Migración desde AD RMS a Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).
> 
> Existe una ruta de acceso de migración que se admite [desde AD RMS a Azure Information Protection](http://technet.microsoft.com/library/Dn858447.aspx) y desde [Azure Information Protection a AD RMS](http://msdn.microsoft.com/library/azure/dn629429.aspx). Si implementa Azure Information Protection y después decide que ya no quiere usar este servicio en la nube, vea [Retirada y desactivación de Azure Information Protection](../deploy-use/decommission-deactivate.md).

## <a name="azure-active-directory-requirements-for-azure-information-protection"></a>Requisitos de Azure Active Directory para Azure Information Protection

Para poder usar Azure Information Protection se necesita un directorio de Azure AD. Use la cuenta de la organización para este directorio para poder iniciar sesión en el Portal de Azure clásico, en donde, por ejemplo, podrá configurar y administrar las plantillas de Rights Management.

Si no dispone aún de suscripción de Azure para su organización, puede obtener una si se registra para una prueba gratuita: vaya a la página [Introducción a Azure](https://account.windowsazure.com/organization) y siga las instrucciones.

Para más información, consulte los recursos siguientes en la documentación de Azure Active Directory:

-   [¿Qué es el directorio de Azure AD?](/active-directory/active-directory-whatis)

-   [Asociación de las suscripciones a Azure con Azure Active Directory](/active-directory/active-directory-how-subscriptions-associated-directory)

Si desea integrar el directorio de Azure AD con los bosques de AD locales, consulte [Integración de las identidades locales con Azure Active Directory](/active-directory/active-directory-aadconnect).

> [!NOTE]
> Si tiene dispositivos móviles o equipos que realizan la autenticación localmente utilizando AD FS o un proveedor de autenticación equivalente:
> 
> -   Debe usar AD FS en la versión mínima de servidor de **Windows Server 2012 R2** o un proveedor de autenticación alternativo que admita el protocolo OAuth 2.0.

### <a name="multifactor-authentication-mfa-and-azure-information-protection"></a>Multi-Factor Authentication (MFA) y Azure Information Protection
Para usar Multi-Factor Authentication (MFA) con Azure Information Protection se necesita como mínimo uno de los dos requisitos siguientes:

-   Office 2013 (versión mínima):

    -   Si tiene Office 2013, también debe instalar la [actualización del 9 de junio de 2015 para Office 2013 (KB3054853)](https://support.microsoft.com/kb/3054853). Para más información sobre esta actualización y sobre la manera en que la autenticación moderna proporciona el inicio de sesión basado en la Biblioteca de autenticación de Active Directory (ADAL) para Office 2013, consulte [Anuncio de la versión preliminar pública de la autenticación moderna de Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/) en el blog de Office.

-   Aplicación para uso compartido de Rights Management para Windows:

    -   Debe tener instalada la versión mínima de 1.0.1908.0, lo que puede confirmar mediante el Panel de control, Programas y características. Para más información sobre la aplicación de uso compartido, consulte [Aplicación de uso compartido Rights Management para Windows](../rms-client/sharing-app-windows.md).

-   Aplicación para uso compartido de Rights Management para dispositivos móviles y equipos Mac:

    -   Asegúrese de que tiene la última versión instalada. La compatibilidad con MFA se incluyó en la versión de septiembre de 2015 de la aplicación para uso compartido de RMS.

A continuación, configure la solución MFA:

-   Para inquilinos administrados por Microsoft (dispone de Azure Active Directory u Office 365):

    -   Configure Azure MFA para aplicar MFA en los usuarios. Para obtener instrucciones, consulte [Introducción a Azure Multi-Factor Authentication en la nube](/multi-factor-authentication/multi-factor-authentication-get-started-cloud) en la documentación de Multi-factor Authentication.

        Para más información sobre Azure MFA, consulte [¿Qué es Azure Multi-Factor Authentication?](/multi-factor-authentication/multi-factor-authentication)

-   Para inquilinos federados (los servidores de federación funcionan localmente):

    -   Configure los servidores de federación para Azure Active Directory u Office 365. Por ejemplo, si usa AD FS, consulte [Configurar métodos de autenticación adicionales para AD FS](https://technet.microsoft.com/library/dn758113.aspx) en TechNet.

        Para más información sobre este escenario, consulte [Programa Works with Office 365 – Identity ahora simplificado](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/) en el blog de Office.

## <a name="client-devices-that-support-azure-rights-management-data-protection"></a>Dispositivos cliente que son compatibles con la protección de datos de Azure Rights Management

Vea las secciones siguientes para identificar los dispositivos que son compatibles con el servicio Azure Rights Management, que ofrece protección de datos para Azure Information Protection.

### <a name="computers"></a>Equipos
Los siguientes sistemas operativos de equipos son compatibles con el servicio Azure Rights Management:

-   **Windows 7** (x86, x64)

-   **Windows 8** (x86, x64)

-   **Windows 8.1** (x86, x64)

-   **Windows 10** (x86, x64)

-   **Mac OS X**: versión mínima de Mac OS X 10.8 (Mountain Lion)

### <a name="mobile-devices"></a>Dispositivos móviles
Los siguientes sistemas operativos de dispositivos móviles son compatibles con el servicio Azure Rights Management:

-   **Windows Phone**: Windows Phone 8.1

-   **Teléfonos y tabletas Android**: versión mínima de Android 4.0.3

-   **iPhone y iPad**: versión mínima de iOS 7.0

-   **Tabletas de Windows**: Windows 10 Mobile y Windows 8.1 RT

## <a name="applications-that-support-azure-rights-management-data-protection"></a>Aplicaciones compatibles con la protección de datos de Azure Rights Management

Use la tabla siguiente para identificar las aplicaciones que son compatibles de forma nativa con el servicio Azure Rights Management (Azure RMS), que ofrece la protección de datos para Azure Information Protection. 

Para estas aplicaciones, la compatibilidad de Rights Management está integrada estrechamente con el uso de las API de Rights Management para permitir la compatibilidad con restricciones de uso. Estas aplicaciones se conocen también como habilitadas para RMS.

A menos que se indique lo contrario, las funciones admitidas son válidas tanto para Azure RMS como para AD RMS. Además, la compatibilidad de AD RMS en iOS, Android, OS X y Windows Phone 8.1 requiere la [Extensión de dispositivos móviles para Active Directory Rights Management Services](https://technet.microsoft.com/library/dn673574.aspx).

Información acerca de las columnas de la tabla:

-   **PDF protegido:** archivos que tienen una extensión de nombre de archivo .ppdf y que se crean automáticamente al usar la aplicación RMS sharing para compartir archivos de Office y archivos PDF por correo electrónico. En la aplicación RMS sharing y la aplicación Azure Information Protection para iOS y Android se incluye un lector de archivos PDF protegidos. Si ya creó archivos PDF y los protegió con Azure RMS o AD RMS, podrá seguir leyendo estos archivos en dispositivos Windows, iOS y Android usando Foxit Reader y Nitro Pro.

-   **Correo electrónico:** los clientes de correo electrónico enumerados pueden proteger el mensaje de correo en sí, lo que hará que también se protejan automáticamente los archivos adjuntos. En este escenario, la característica de vista previa del cliente puede mostrar el contenido protegido (mensaje y datos adjuntos) a destinatarios autorizados. Sin embargo, si un mensaje de correo electrónico no está protegido, pero los datos adjuntos sí lo están, la característica de vista previa no puede mostrar dichos datos a destinatarios autorizados.

-   **Otros tipos de archivo:** los archivos de texto e imagen incluyen archivos que tienen una extensión de nombre de archivo como .txt, .xml, .jpg y .jpeg. Estos archivos cambian su extensión de nombre de archivo después de protegerlos de forma nativa con Rights Management y se convierten en archivos de solo lectura. Los archivos que no se pueden proteger de forma nativa pasan a tener una extensión de nombre de archivo .pfile después de protegerlos de forma genérica con Rights Management. Para más información, vea [Rights Management sharing application administrator guide](../rms-client/sharing-app-admin-guide.md) (Guía de administrador de la aplicación Rights Management sharing).


|**Sistema operativo del dispositivo**|Word, Excel, PowerPoint|PDF protegido|Correo electrónico|Otros tipos de archivo|
|-------------------------------|---------------------------|-----------------|---------|--------------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office 2016 <br /><br />Aplicaciones de Office Mobile (solo Azure RMS) [[1]](#footnote-1)<br /><br />Office Online [[2]](#footnote-2)|Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br />Aplicación RMS sharing|Outlook 2010<br /><br />Outlook 2013<br /><br />Office 2016 <br /><br />Outlook Web App (OWA) [[3]](#footnote-3)<br /><br />Correo de Windows [[4]](#footnote-4)|Aplicación RMS sharing para Windows: texto, imágenes, pfile<br /><br />Siemens JT2Go: archivos JT (solo Windows 10)|
|**iOS**|Office para iPad y iPhone [[5]](#footnote-5)<br /><br />Office Online [[2]](#footnote-2)<br /><br />Documentos TITUS|Aplicación Azure Information Protection [[1]](#footnote-1)<br /><br /> Foxit Reader<br /><br />Documentos TITUS|Aplicación Azure Information Protection [[1]](#footnote-1)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook para iPad y iPhone [[4]](#footnote-4)<br /><br />OWA para iOS [[3]](#footnote-3)<br /><br />TITUS Mail|Aplicación Azure Information Protection [[1]](#footnote-1): texto, imágenes<br /><br />Documentos TITUS: pfile|
|**Android**|GigaTrust App para Android<br /><br />Office Online [[2]](#footnote-2)<br /><br />Office Mobile (solo Azure RMS) [[1]](#footnote-1)|Aplicación Azure Information Protection [[1]](#footnote-1)<br /><br />GigaTrust App para Android<br /><br />Foxit Reader<br /><br />Aplicación RMS sharing [[1]](#footnote-1)|9Folders [[4]](#footnote-4)<br /><br />Aplicación Azure Information Protection [[1]](#footnote-1)<br /><br />GigaTrust App para Android [[4]](#footnote-4)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook para Android [[4]](#footnote-4)<br /><br />OWA para Android [[3]](#footnote-3) y [[7]](#footnote-7)<br /><br />Correo electrónico de Samsung (S3 y versiones posteriores) [[7]](#footnote-7)<br /><br />TITUS Classification for Mobile|Aplicación Azure Information Protection [[1]](#footnote-1): texto, imágenes|
|**OS X**|Office 2011 (solo AD RMS)<br /><br />Office 2016 para Mac<br /><br />Office Online [[2]](#footnote-2)|Foxit Reader<br /><br />Aplicación RMS sharing [[1]](#footnote-1)|Outlook 2011 (solo AD RMS)<br /><br />Outlook 2016 para Mac<br /><br />Outlook para Mac|Aplicación RMS sharing [[1]](#footnote-1): texto, imágenes, pfile|
|**Windows 10 Mobile**|Aplicaciones de Office Mobile (solo Azure RMS) [[1]](#footnote-1)|No compatible|Citrix WorxMail [[6]](#footnote-6)<br /><br />Correo de Outlook|No compatible|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [[2]](#footnote-2)|No compatible|Outlook 2013 RT<br /><br />Aplicación de correo para Windows<br /><br />Correo de Windows [[4]](#footnote-4)|Siemens JT2Go: archivos JT|
|**Windows Phone 8.1**|Office Mobile (solo AD RMS)|Aplicación RMS sharing [[1]](#footnote-1)|Outlook Mobile [[4]](#footnote-4)|Aplicación RMS sharing [[1]](#footnote-1): texto, imágenes, pfile|
|**Blackberry 10**|No compatible|No compatible|Correo electrónico de Blackberry [[4]](#footnote-4)|No compatible|


##### <a name="footnote-1"></a>Nota al pie 1
Admite la visualización de contenido protegido.

##### <a name="footnote-2"></a>Nota al pie 2 
Admite la visualización de documentos protegidos cuando se carga un documento desprotegido en una biblioteca protegida de SharePoint Online y OneDrive para la Empresa. 

##### <a name="footnote-3"></a>Nota al pie 3
Si un destinatario recibe un correo electrónico protegido y no usa Exchange como servidor de correo o si el remitente pertenece a otra organización, este contenido solo se puede abrir en un cliente de correo electrónico enriquecido, como Outlook. Este contenido no se puede abrir desde Outlook Web Access.

##### <a name="footnote-4"></a>Nota al pie 4
Usa Exchange ActiveSync IRM, que debe habilitar el administrador de Exchange. Los usuarios pueden usar la opción de ver, responder y responder a todos para los mensajes de correo electrónico protegidos, pero no pueden proteger por su cuenta los mensajes de correo electrónico nuevos.

Si un destinatario recibe un correo electrónico protegido y no usa Exchange como servidor de correo o si el remitente pertenece a otra organización, este contenido solo se puede abrir en un cliente de correo electrónico enriquecido, como Outlook. Este contenido no se puede abrir desde Outlook Web Access o desde clientes de correo electrónico móvil que usan IRM de Exchange Active Sync.

##### <a name="footnote-5"></a>Nota al pie 5
Admite la visualización y la edición de documentos protegidos. Para más información, vea la siguiente entrada en el blog de Office: [Azure Rights Management support comes to Office for iPad and iPhone](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/) (La compatibilidad de Azure Rights Management llega a Office para iPad y iPhone).

##### <a name="footnote-6"></a>Nota al pie 6
Para obtener más información, vea la [documentación del producto para WorxMail](http://docs.citrix.com/en-us/worx-mobile-apps/10/xmob-worx-mail.html) de Citrix.

##### <a name="footnote-7"></a>Nota al pie 7
Para más información, vea la siguiente entrada en el blog de Office: [OWA for Android now available on select devices](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/) (OWA para Android ahora disponible en algunos dispositivos).

## <a name="more-information-about-azure-rms-support-for-office"></a>Más información sobre la compatibilidad de Azure RMS con Office

Azure RMS se integra estrechamente en las aplicaciones de Word, Excel, PowerPoint y Outlook, donde esta funcionalidad se conoce a menudo como Information Rights Management (IRM). Las siguientes ediciones del cliente de Office admiten la protección de archivos y correos electrónicos con Azure RMS:

- Office Professional Plus 2016

- Office Professional Plus 2013

- Office Professional Plus 2010

Todas las ediciones de Office (salvo Office 2007) pueden consumir contenido protegido.

Azure RMS con Office Professional Plus 2010 u Office Professional 2010:

- Requiere la aplicación de uso compartido Rights Management para Windows

- No se admite en Windows 10

### <a name="more-information-about-the-azure-information-protection-app-for-ios-and-android"></a>Más información sobre la aplicación Azure Information Protection para iOS y Android

La aplicación Azure Information Protection para iOS y Android reemplaza a la aplicación RMS sharing para esos dispositivos. Ofrece las mismas funciones y, además, es compatible con mensajes de correo electrónico con protección de derechos y archivos PDF con protección de derechos en SharePoint Online.

Si los dispositivos iOS y Android están inscritos en Microsoft Intune, puede implementar y administrar esta aplicación con una aplicación administrada por directivas. Para más información, consulte [Configure and deploy mobile application management policies in the Microsoft Intune console](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console) (Configuración e implementación de directivas de administración de aplicaciones móviles en la consola de Microsoft Intune). Para completar el paso 2 de esta documentación de Intune, siga las instrucciones para publicar una aplicación administrada por directiva.

Para más información, vea las [Preguntas más frecuentes para la aplicación Microsoft Azure Information Protection para iOS y Android](../rms-client/mobile-app-faq.md).


### <a name="more-information-about-the-rights-management-sharing-application"></a>Más información sobre la aplicación Rights Management sharing

Para obtener más información acerca de la aplicación de uso compartido Rights Management para Windows, consulte los recursos siguientes:

-   [Guía del administrador de la aplicación Rights Management sharing](../rms-client/sharing-app-admin-guide.md)

-   [Guía de usuario de la aplicación Rights Management sharing](../rms-client/sharing-app-user-guide.md)

Para obtener más información acerca de la aplicación de uso compartido Rights Management para plataformas móviles, consulte los recursos siguientes:

-   Descargue la aplicación correspondiente en los vínculos de la [página de Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970)

-   [Preguntas frecuentes para la aplicación Microsoft Rights Management sharing para plataformas móviles](https://technet.microsoft.com/dn451248)

> [!NOTE]
> La aplicación RMS sharing para iOS y Android se ha reemplazado por la aplicación Azure Information Protection.

### <a name="more-information-about-other-applications-that-support-azure-rms"></a>Más información sobre otras aplicaciones que admiten Azure RMS

Aparte de las aplicaciones de la tabla, cualquier aplicación que permita integrar la API de RMS con Azure RMS, a saber:

- Aplicaciones de línea de negocio escritas internamente con RMS SDK.

- Aplicaciones de proveedores de software escritas con RMS SDK.

Para más información sobre el SDK, vea [Microsoft Rights Management SDK](../develop/developers-guide.md).

### <a name="applications-that-are-not-supported-by-azure-rms"></a>Aplicaciones no compatibles con Azure RMS

Las siguientes aplicaciones no son compatibles actualmente con Azure RMS:

-   Microsoft Office para Mac 2011

-   Microsoft OneDrive para la Empresa para SharePoint Server 2013

-   Visor de XPS
 
Además, la aplicación de uso compartido de RMS presenta la restricciones siguientes:

-   En equipos con Windows: se necesita una versión mínima de Windows 7 Service Pack 1

## <a name="onpremises-servers-that-support-azure-rights-management-data-protection"></a>Servidores locales compatibles con la protección de datos de Azure Rights Management

Los siguientes productos de servidor local son compatibles con Azure Information Protection al usar el conector de Azure Rights Management. Este conector actúa como una interfaz de comunicaciones (una retransmisión) entre los servidores locales y el servicio Azure Rights Management usado por Azure Information Protection para proteger los documentos y los correos electrónicos de Office. 

Para usar este conector, necesita configurar la sincronización de directorios entre los bosques de Active Directory y Azure Active Directory.

-   **Exchange Server**:

    -   Exchange Server 2016

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server**:

    -   Office SharePoint Server 2016

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **Servidores de archivos que ejecutan Windows Server y usan Infraestructura de clasificación de archivos (FCI)**:

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > Como los servidores de archivos con Windows Server 2008 R2 no tienen una acción de tarea de administración de archivos integrada para aplicar la protección de Rights Management, puede usar el conector de Rights Management para este escenario. Sin embargo, puede usar Infraestructura de clasificación de archivos y Azure RMS en estos sistemas operativos si configura una tarea de administración de archivos personalizada para ejecutar un ejecutable o script que pueda proteger archivos mediante Azure RMS. Por ejemplo, un script de Windows PowerShell que usa los [cmdlets de protección de RMS](https://msdn.microsoft.com/library/azure/mt433195.aspx).
    > 
    > También puede usar estos cmdlets con servidores que ejecuten versiones posteriores de Windows Server, con la ventaja de que estos cmdlets pueden proteger todos los tipos de archivo. El conector RMS solo protege archivos de Office. Para obtener instrucciones sobre los procedimientos, consulte [Protección de RMS con la infraestructura de clasificación de archivos de Windows Server &#40;FCI&#41](../rms-client/configure-fci.md).

El conector de Rights Management es compatible con Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2.

Para más información sobre cómo configurar el conector de Rights Management para estos servidores locales, vea [Implementación del conector de Azure Rights Management](../deploy-use/deploy-rms-connector.md).




<!--HONumber=Nov16_HO1-->


