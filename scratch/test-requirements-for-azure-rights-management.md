---
title: PRUEBA Requisitos de Azure Rights Management
ms.custom: na
ms.reviewer: na
ms.service: rights-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: TEST
author: Cabailey
---
# ANTES: Requisitos de Azure Rights Management
Para implementar Microsoft Azure Rights Management (Azure RMS) en su organización, asegúrese de que cumple con los siguientes requisitos previos. Podrá entonces usar el [Plan para la implementación de Azure Rights Management](deployment-roadmap.md) a fin de implementar Rights Management para su organización.

|Requisito|Más información|
|---------------|--------------------|
|Una suscripción en la nube para RMS|Su organización debe tener una suscripción en la nube que admita RMS.<br /><br />Para obtener información sobre licencias, consulte la sección [Suscripciones en la nube que son compatibles con Azure RMS](requirements-azure-rms.md#BKMK_SupportedSubscriptions) de este tema.|
|Directorio de Azure AD|Su organización debe tener un directorio de Azure AD que admita la autenticación de usuario para RMS. Además, si quiere usar las cuentas de usuario de su directorio local (AD DS), también deberá configurar la integración de directorios.<br /><br />Multi-Factor Authentication (MFA) es compatible con Azure RMS si tiene el software cliente necesario y la infraestructura de MFA configurada correctamente.<br /><br />Para obtener más información, consulte la sección [Directorio de Azure AD](requirements-azure-rms.md#BKMK_AzureADTenant) de este tema.|
|Dispositivos cliente|Los usuarios deben tener dispositivos cliente (equipo o dispositivo móvil) que ejecuten un sistema operativo compatible con RMS.<br /><br />Para obtener más información, consulte la sección [Dispositivos cliente que son compatibles con Azure RMS](requirements-azure-rms.md#BKMK_SupportedDevices) de este tema.|
|Aplicaciones|Los usuarios deben ejecutar aplicaciones que sean compatibles con RMS.<br /><br />Para obtener más información, consulte la sección [Aplicaciones que son compatibles con Azure RMS](requirements-azure-rms.md#BKMK_SupportedApplications) de este tema.|
|Infraestructura compatible con la conectividad a Internet y dependiente de los servicios en la nube|Si tiene un firewall o dispositivos de red que intervengan que se deben configurar para permitir conexiones específicas, consulte [Office 365 URLs and IP address ranges](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) (Direcciones URL e intervalos de direcciones IP de Office 365).<br /><br />La lista de direcciones URL y direcciones IP de la sección **Office 365 portal and identity** (Identidad y portal de Office 365) es aplicable al portal de Office 365, a los recursos de Azure Active Directory y a Azure Rights Management. Siga las instrucciones de este artículo para suscribirse a una fuente RSS y mantenerse así al día de los cambios que se realicen en esta información.<br /><br />Además de la información del artículo de Office específica de Azure RMS:<br /><br />No termine la conexión TLS de cliente a servicio (por ejemplo, para realizar una inspección de los paquetes). Al hacerlo, se interrumpe la asignación de certificados que los clientes de RMS utilizan con las entidades de certificación administradas por Microsoft para ayudar a proteger su comunicación con Azure RMS.<br /><br />No utilice una configuración de proxy web que autentique en nombre de un usuario.|

Si desea usar Azure RMS con servidores locales, se admiten los siguientes productos:

-   Exchange Server

-   Servidor de SharePoint

-   Servidores de archivos de Windows Server que son compatibles con la Infraestructura de la clasificación de archivos

Para obtener más información sobre los requisitos adicionales de Azure RMS para este escenario, consulte la sección [Servidores locales compatibles con Azure RMS](requirements-azure-rms.md#BKMK_SupportedServers) de este tema.

> [!IMPORTANT]
> El siguiente escenario de implementación no es compatible:
> 
> -   Ejecución de AD RMS y Azure RMS en paralelo en la misma organización, salvo durante la migración, tal como se describe en [Migrating from AD RMS to Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) (Migración de AD RMS a Azure Rights Management).
> 
> Hay una ruta de acceso de migración compatible [de AD RMS a Azure RMS](http://technet.microsoft.com/library/Dn858447.aspx) y de [Azure RMS a AD RMS](http://msdn.microsoft.com/library/azure/dn629429.aspx). Si implementa Azure RMS y después decide que ya no quiere usar este servicio en la nube, consulte [Decommissioning and Deactivating Azure Rights Management](decommission-deactivate.md) (Retirada y desactivación de Azure Rights Management).

Use las secciones siguientes para obtener más información acerca de los requisitos de Azure RMS.

## <a name="BKMK_SupportedSubscriptions"></a>Suscripciones en la nube que son compatibles con Azure RMS
Para usar Azure RMS, su organización debe tener al menos una de las siguientes suscripciones con un número suficiente de licencias para usuarios y servicios que protegerán archivos y mensajes de correo electrónico. Si tiene un servicio que aplicará protección para los usuarios (propietarios de los archivos o mensajes de correo electrónico), esos usuarios necesitan una de estas licencias. Los usuarios que solo consumen (por ejemplo, leen y editan) estos datos protegidos no necesita una licencia.

-   Office 365

-   Azure Rights Management Premium (anteriormente Azure RMS Standalone)

-   Enterprise Mobility Suite

-   RMS para usuarios

Use las secciones siguientes para obtener más información y conocer las opciones de registro.

Para ver una comparación de las licencias de las funcionalidades de Azure RMS correspondientes a las suscripciones de pago, consulte [Comparison of Rights Management Services (RMS) Offerings](http://technet.microsoft.com/dn858608) (Comparación de las ofertas de Rights Management Services [RMS]).

¿Tiene preguntas adicionales sobre las licencias de Azure RMS? Descargue **Preguntas más frecuentes sobre licencias para Azure Rights Management** desde la página [Comprar Azure Rights Management](https://www.microsoft.com/en-us/server-cloud/products/azure-rights-management/Purchasing.aspx). 

### Suscripción a Office 365
[Evaluación gratuita de 30 días: Enterprise E3](http://go.microsoft.com/fwlink/p/?LinkID=403802)

Esta suscripción está diseñada para organizaciones que quieran usar los servicios en línea de Office y usar su característica Information Rights Management, que utiliza Azure RMS. Sin embargo, no todas las suscripciones de Office 365 incluyen Azure RMS.

|Opción de obtención de licencias|Office 365 Empresa Essentials|Office 365 Empresa Premium|Office 365 Enterprise E1<br /><br />Office 365 Educación A1|Office 365 Enterprise E3<br /><br />Office 365 Educación A3<br /><br />Office 365 Administración Pública G3|Office 365 Enterprise E4<br /><br />Office 365 Educación A4<br /><br />Office 365 Administración Pública G4|Office 365 Enterprise E5<br /><br />Office 365 Educación A5<br /><br />Office 365 Administración Pública G5|Office 365 Enterprise K1|SharePoint plan 1<br />SharePoint plan 2|Exchange Online plan 1<br />Exchange Online plan 2|
|--------------------|----------------------------------|-------------------------------|-------------------------------------------------------|-----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|----------------------------|----------------------------------------|--------------------------------------------------|
|Information Rights Protection (IRM)|No|No|No|Sí|Sí|Sí|No|No|No|

### Suscripción a Azure Rights Management Premium
[Prueba gratuita de 30 días](https://portal.microsoftonline.com/Signup/MainSignUp15.aspx?&amp;OfferId=A43415D3-404C-4df3-B31B-AAD28118A778&amp;dl=RIGHTSMANAGEMENT&amp;ali=1)

Esta suscripción antes se denominaba Azure RMS Standalone y está diseñada para organizaciones que quieren usar Azure RMS pero no disponen de ninguna suscripción que incluya Azure RMS. Por ejemplo, si tiene una suscripción para Office 365 Empresa Essentials u Office 365 Enterprise E1, estas suscripciones no incluyen Azure RMS (vea la tabla de la sección anterior). Para usar Azure RMS, puede comprar una suscripción a Azure Rights Management Premium (o comprar otra suscripción, como Office 365 Enterprise E4, que incluye Azure RMS).

Para obtener más información, consulte [Microsoft Azure Rights Management](http://products.office.com/business/microsoft-azure-rights-management).

Esta suscripción también ofrece un período de evaluación para probar Azure RMS para 25 usuarios, de manera gratuita. Si la suscripción expira antes de comprar una suscripción de reemplazo, vea la siguiente sección, “¿Qué ocurre cuando expira la suscripción de prueba?”

|Opción de obtención de licencias|Office 365 Empresa Essentials|Office 365 Empresa Premium|Office 365 Enterprise E1<br /><br />Office 365 Educación A1|Office 365 Enterprise E3<br /><br />Office 365 Educación A3<br /><br />Office 365 Administración Pública G3|Office 365 Enterprise E4<br /><br />Office 365 Educación A4<br /><br />Office 365 Administración Pública G4|Office 365 Enterprise E5<br /><br />Office 365 Educación A5<br /><br />Office 365 Administración Pública G5|Office 365 Enterprise K1|SharePoint plan 1<br />SharePoint plan 2|Exchange Online plan 1<br />Exchange Online plan 2|
|--------------------|----------------------------------|-------------------------------|-------------------------------------------------------|-----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|----------------------------|----------------------------------------|--------------------------------------------------|
|Information Rights Protection (IRM)|Sí|Sí [nota al pie 1]|Sí|Sí|Sí|Sí|Sí|Sí|Sí|
Nota al pie 1: Para Empresa Premium, hay algunas restricciones de cliente: puede proteger el contenido y consumir contenido protegido con RMS mediante Outlook Web App y la aplicación RMS sharing. Puede consumir contenido protegido en todas las demás aplicaciones de Office, donde se incluyen Office Online y las aplicaciones cliente para Office 365 Empresa Premium.

#### <a name="BKMK_TrialExpiryBehavior"></a>¿Qué ocurre cuando la suscripción de prueba expira?
Si su suscripción de prueba expira, perderá acceso al contenido protegido al usar su suscripción de prueba para Azure RMS. Sin embargo, si después compra una suscripción que admite Azure RMS, el acceso se restaura automáticamente.

Una excepción a la pérdida de acceso tras la expiración es si su organización usó Azure RMS con el RMS para la suscripción de individuos antes de que obtuviera la suscripción de prueba. A continuación, permanece el acceso al contenido anteriormente protegido, incluso después de que expire la suscripción de prueba.

### Suscripción a Enterprise Mobility Suite
[Prueba gratuita de 30 días](http://go.microsoft.com/fwlink/?LinkId=615385)

Esta suscripción está diseñada para organizaciones que quieran usar una combinación de Azure Active Directory Premium, Windows Intune y Azure Rights Management. Para obtener más información, vea [Información general de Enterprise Mobility Suite](http://go.microsoft.com/fwlink/?LinkId=615386).

|Opción de obtención de licencias|Office 365 Empresa Essentials|Office 365 Empresa Premium|Office 365 Enterprise E1<br /><br />Office 365 Educación A1|Office 365 Enterprise E3<br /><br />Office 365 Educación A3<br /><br />Office 365 Administración Pública G3|Office 365 Enterprise E4<br /><br />Office 365 Educación A4<br /><br />Office 365 Administración Pública G4|Office 365 Enterprise E5<br /><br />Office 365 Educación A5<br /><br />Office 365 Administración Pública G5|Office 365 Enterprise K1|SharePoint plan 1<br />SharePoint plan 2|Exchange Online plan 1<br />Exchange Online plan 2|
|--------------------|----------------------------------|-------------------------------|-------------------------------------------------------|-----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|----------------------------|----------------------------------------|--------------------------------------------------|
|Information Rights Protection (IRM)|Sí|Sí [nota al pie 1]|Sí|Sí|Sí|Sí|Sí|Sí|Sí|
Nota al pie 1: Para Empresa Premium, hay algunas restricciones de cliente: puede proteger el contenido y consumir contenido protegido con RMS mediante Outlook Web App y la aplicación RMS sharing. Puede consumir contenido protegido en todas las demás aplicaciones de Office, donde se incluyen Office Online y las aplicaciones cliente para Office 365 Empresa Premium.

### Suscripción a RMS para usuarios
Esta suscripción está diseñada para usuarios de una organización que no hayan implementado Azure RMS o AD RMS. Permite que estas personas lean contenido que se ha protegido por una organización que usa Azure RMS, a la vez que pueden proteger su propio contenido.

Para obtener más información, consulte [RMS for Individuals and Azure Rights Management](rms-for-individuals.md) (RMS para usuarios y Azure Rights Management).

## <a name="BKMK_AzureADTenant"></a>Directorio de Azure AD
Debe disponer de un directorio de Azure AD para poder usar Azure RMS. Use la cuenta de la organización para este directorio para poder iniciar sesión en el Portal de Azure clásico, en donde, por ejemplo, podrá configurar y administrar las plantillas de Rights Management.

Si no dispone aún de suscripción de Azure para su organización, puede obtener una si se registra para una prueba gratuita: vaya a la página [Introducción a Azure](https://account.windowsazure.com/organization) y siga las instrucciones.

Para obtener más información, consulte los recursos siguientes en la documentación de Azure Active Directory:

-   [¿Qué es un directorio de Azure AD?](http://msdn.microsoft.com/library/185da266-58a9-43e6-9c66-2c8f702545c6)

-   [Cómo se asocian las suscripciones a Azure con Azure AD](http://msdn.microsoft.com/library/edf05c2e-944a-4da5-a330-dc9dc479f127)

Si quiere integrar su directorio de Azure AD con sus bosques de AD locales, vea [Integración de directorios](http://msdn.microsoft.com/library/bf82bdff-2467-403b-8c1a-0e9eebcf31e8).

> [!NOTE]
> Si tiene dispositivos móviles o equipos Mac que realizan la autenticación localmente mediante AD FS o un proveedor de autenticación equivalente:
> 
> -   Debe usar AD FS en la versión mínima de servidor de **Windows Server 2012 R2** o un proveedor de autenticación alternativo que admita el protocolo OAuth 2.0.

### <a name="BKMK_MFA"></a>Multi-Factor Authentication (MFA) y Azure RMS
Para usar Multi-Factor Authentication (MFA) con Azure RMS hace falta como mínimo uno de los siguientes:

-   Office 2013 (versión mínima):

    -   Si tiene Office 2013, también debe instalar la [actualización del 9 de junio de 2015 para Office 2013 (KB3054853)](https://support.microsoft.com/kb/3054853). Para obtener más información sobre esta actualización y sobre la manera en que la autenticación moderna proporciona el inicio de sesión basado en la Biblioteca de autenticación de Active Directory (ADAL) para Office 2013, vea [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/) (Anuncio de la vista previa pública de la autenticación moderna de Office 2013) en el blog de Office.

-   Aplicación para uso compartido de Rights Management para Windows:

    -   Debe tener instalada la versión mínima de 1.0.1908.0, lo que puede confirmar mediante el Panel de control, Programas y características. Para obtener más información sobre la aplicación de uso compartido, consulte [Rights Management Sharing Application for Windows](sharing-app-windows.md) (Aplicación de uso compartido Rights Management para Windows).

-   Aplicación para uso compartido de Rights Management para dispositivos móviles y equipos Mac:

    -   Asegúrese de que tiene la última versión instalada. La compatibilidad con MFA se incluyó en la versión de septiembre de 2015 de la aplicación para uso compartido de RMS.

A continuación, configure la solución MFA:

-   Para inquilinos administrados por Microsoft (dispone de Azure Active Directory u Office 365):

    -   Configure Azure MFA para aplicar MFA en los usuarios. Para obtener instrucciones, consulte [Introducción a Azure Multi-Factor Authentication en la nube](https://azure.microsoft.com/documentation/articles/multi-factor-authentication-get-started-cloud/) en la documentación de Azure.

        Para obtener más información sobre Azure MFA, consulte [¿Qué es Azure Multi-Factor Authentication?](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/)

-   Para inquilinos federados (los servidores de federación funcionan localmente):

    -   Configure los servidores de federación para Azure Active Directory u Office 365. Por ejemplo, si usa AD FS, consulte [Configurar métodos de autenticación adicionales para AD FS](https://technet.microsoft.com/library/dn758113.aspx) en TechNet.

        Para obtener más información sobre este escenario, vea [The Works with Office 365 – Identity program now streamlined](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/) (Programa Works with Office 365 – Identity ahora simplificado) en el blog de Office.

## <a name="BKMK_SupportedDevices"></a>Dispositivos cliente que son compatibles con Azure RMS
Use las secciones siguientes para identificar qué dispositivos son compatibles con Azure Rights Management (RMS) y qué capacidades de RMS admiten:

-   [Equipos](requirements-azure-rms.md#BKMK_RMSSupportedComputers)

-   [Dispositivos móviles](requirements-azure-rms.md#BKMK_RMSSupportedMobileDevices)

-   [Capacidades de dispositivo de cliente](requirements-azure-rms.md#BKMK_ClientCapabilities)

### <a name="BKMK_RMSSupportedComputers"></a>Equipos
Los siguientes sistemas operativos de equipo son compatibles con Azure Rights Management:

-   **Windows 7** (x86, x64)

-   **Windows 8** (x86, x64)

-   **Windows 8.1** (x86, x64)

-   **Windows 10** (x86, x64)

-   **Mac OS X**: versión mínima de Mac OS X 10.8 (Mountain Lion)

### <a name="BKMK_RMSSupportedMobileDevices"></a>Dispositivos móviles
Los sistemas operativos de dispositivos móviles siguientes son compatibles con Azure Rights Management:

-   **Windows Phone**: Windows Phone 8.1

-   **Teléfonos y tabletas Android**: versión mínima de Android 4.0.3

-   **iPhone y iPad**: versión mínima de iOS 7.0

-   **Tabletas Windows RT**: Windows 8.1 RT

### <a name="BKMK_ClientCapabilities"></a>Capacidades de dispositivo de cliente
No todos los dispositivos de cliente admitidos son compatibles actualmente con todas las capacidades de RMS. Use la tabla siguiente para identificar qué aplicaciones admiten las capacidades de RMS, y las excepciones.

A menos que se indique de otra manera, las funcionalidades admitidas se aplican a Azure RMS y AD RMS. Además, la compatibilidad de AD RMS en iOS, Android, OS X y Windows Phone 8.1 requiere la [Extensión de dispositivos móviles de Active Directory Rights Management Services](http://technet.microsoft.com/library/a69ead9d-7dd3-4b38-9830-4728e9757341).

Información acerca de las columnas de la tabla:

-   **PDF protegido:** archivos que tienen una extensión de nombre de archivo .ppdf y que se crean automáticamente al usar la aplicación RMS sharing para compartir archivos de Office y archivos PDF por correo electrónico. La aplicación de uso compartido RMS incluye un lector para archivos PDF protegidos. Si anteriormente había creado archivos PDF que había protegido con Azure RMS o AD RMS, puede seguir leyendo estos archivos en dispositivos Windows, iOS y Android mediante Foxit Reader y Nitro Pro.

-   **Correo electrónico:** los clientes de correo electrónico enumerados pueden proteger el propio mensaje de correo electrónico, lo que hará que también se protejan automáticamente los archivos adjuntos. En este escenario, la característica de vista previa del cliente puede mostrar el contenido protegido (mensaje y datos adjuntos) a destinatarios autorizados. Sin embargo, si un mensaje de correo electrónico no está protegido pero los datos adjuntos si lo están, la característica de vista previa no puede mostrar dichos datos a destinatarios autorizados.

-   **Otros tipos de archivo:** los archivos de texto e imagen incluyen archivos que tienen una extensión de nombre de archivo como .txt, .xml, .jpg y .jpeg. Estos archivos cambian su extensión de nombre de archivo después de que se protegen de forma nativa con RMS y se hacen de solo lectura. Los archivos que no se pueden proteger de forma nativa pasan a tener una extensión de nombre de archivo .pfile después de que RMS los proteja de forma genérica. Para obtener más información, vea las secciones [Niveles de protección: nativo y genérico](https://technet.microsoft.com/library/dn339003.aspx) y [Tipos de archivo y extensiones de nombre de archivo admitidos](https://technet.microsoft.com/library/dn339003.aspx) en la [Guía de administrador de la aplicación de uso compartido Rights Management](http://technet.microsoft.com/library/dn339003%28v=ws.10%29.aspx).

|**Sistema operativo de dispositivo**|Word, Excel, PowerPoint|PDF protegido|Correo electrónico|Otros tipos de archivo|
|-------------------------------|---------------------------|-----------------|---------|--------------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Aplicaciones de Office Mobile (solo Azure RMS) [nota al pie 1]<br /><br />Office Online [nota al pie 2]|Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br />Aplicación RMS sharing|Outlook 2010<br /><br />Outlook 2013<br /><br />Outlook Web App (OWA) [nota al pie 3]<br /><br />Correo de Windows [nota al pie 4]|Aplicación RMS sharing para Windows: texto, imágenes, pfile<br /><br />Siemens JT2Go: archivos JT (solo Windows 10)|
|**iOS**|Office para iPad y iPhone [nota al pie 5]<br /><br />Office Online [nota al pie 2]<br /><br />Documentos TITUS|Foxit Reader<br /><br />Aplicación RMS sharing [nota al pie 1]<br /><br />Documentos TITUS|NitroDesk [nota al pie 4]<br /><br />Outlook para iPad y iPhone [nota al pie 4]<br /><br />OWA para iOS [nota al pie 3]<br /><br />TITUS Mail|Aplicación RMS sharing [nota al pie 1]: texto, imágenes, pfile<br /><br />Documentos TITUS: pfile|
|**Android**|GigaTrust App para Android<br /><br />Office Online [nota al pie 2]|GigaTrust App para Android<br /><br />Foxit Reader<br /><br />Aplicación RMS sharing [nota al pie 1]|9Folders [nota al pie 4]<br /><br />GigaTrust App para Android [nota al pie 4]<br /><br />NitroDesk [nota al pie 4]<br /><br />OWA para Android [nota al pie 3 y 6]<br /><br />Correo electrónico de Samsung (S3 y versiones posteriores) [nota al pie 6]<br /><br />TITUS Classification for Mobile|Aplicación RMS sharing [nota al pie 1]: texto, imágenes, pfile|
|**OS X**|Office 2011 (solo AD RMS)<br /><br />Office 2016 para Mac<br /><br />Office Online [nota al pie 2]|Foxit Reader<br /><br />Aplicación RMS sharing [nota al pie 1]|Outlook 2011 (solo AD RMS)<br /><br />Outlook 2016 para Mac<br /><br />Outlook para Mac|Aplicación RMS sharing [nota al pie 1]: texto, imágenes, pfile|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [nota al pie 2]|No compatible|Outlook 2013 RT<br /><br />Aplicación de correo para Windows<br /><br />Correo de Windows [nota al pie 4]|Siemens JT2Go: archivos JT|
|**Windows Phone 8,1**|Office Mobile (solo AD RMS)|Aplicación RMS sharing [nota al pie 1]|Outlook Mobile [nota al pie 4]|Aplicación RMS sharing [nota al pie 1]: texto, imágenes, pfile|
|**Blackberry 10**|No compatible|No admitida|Correo electrónico de Blackberry [nota al pie 4]|No compatible|
Nota al pie 1: Admite la visualización de contenido protegido.

Nota al pie 2: Admite la visualización de contenido protegido en SharePoint Online, OneDrive para la Empresa y Outlook Web Access.

Nota al pie 3: Si un destinatario tiene un buzón de Exchange local y recibe un correo electrónico protegido, este contenido solo se puede abrir en un cliente de correo electrónico enriquecido, como Outlook.  Este contenido no se puede abrir desde Outlook Web Access.

Nota al pie 4: Usa Exchange ActiveSync IRM, que debe habilitar el administrador de Exchange. Los usuarios pueden usar la opción de ver, responder y responder a todos para los mensajes de correo electrónico protegidos, pero no pueden proteger por su cuenta los mensajes de correo electrónico nuevos.

Si un destinatario tiene un buzón de Exchange local y recibe un correo electrónico protegido de otra organización que usa Exchange, este contenido solo se puede abrir en un cliente de correo electrónico enriquecido, como Outlook.  Este contenido no se puede abrir desde un dispositivo que use Exchange Active Sync IRM.

Nota al pie 5: Admite la visualización y la edición de documentos protegidos. Para obtener más información, consulte la siguiente entrada en el blog de Office: [Azure Rights Management support comes to Office for iPad and iPhone](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/) (La compatibilidad de Azure Rights Management llega a Office para iPad y iPhone).

Nota al pie 6: Para obtener más información, consulte la siguiente entrada en el blog de Office: [OWA for Android now available on select devices](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/) (OWA para Android ahora disponible en algunos dispositivos).

> [!TIP]
> Para obtener más información sobre la inminente implementación de compatibilidad con RMS en Office para diferentes plataformas, vea la siguiente entrada del blog de Office: [Office everywhere, encryption everywhere](http://blogs.office.com/2015/02/18/office-everywhere-encryption-everywhere/) (Office en todas partes, cifrado en todas partes).

## <a name="BKMK_SupportedApplications"></a>Aplicaciones que son compatibles con Azure RMS
Las aplicaciones siguientes son compatibles de forma nativa con Azure RMS, lo que significa que RMS se integra estrechamente en estas aplicaciones mediante API de RMS para admitir restricciones de uso. Estas aplicaciones son conocidas también como fundamentadas en RMS:

-   **Aplicaciones de Microsoft Office** (Word, Excel, PowerPoint y Outlook) de los conjuntos de aplicaciones siguientes puede proteger contenido mediante Azure RMS:

    -   Office 365 ProPlus

    -   Office 365 Enterprise E3

    -   Office 365 Enterprise E4

    -   Office 365 Enterprise E5

    -   Office Professional Plus 2016

    -   Office Professional Plus 2013

    -   Office Professional Plus 2010

    Otras ediciones de Office (con la excepción de Office 2007) pueden consumir contenido protegido.

    > [!NOTE]
    > Azure RMS con Office Professional Plus 2010 u Office Professional 2010:
    > 
    > -   Requiere la aplicación de uso compartido Rights Management para Windows
    > -   No se admite en Windows 10

-   **La aplicación de uso compartido Rights Management para Windows**

    Para obtener más información acerca de la aplicación de uso compartido Rights Management para Windows, consulte los recursos siguientes:

    -   [Guía de administrador de la aplicación de uso compartido Rights Management](http://technet.microsoft.com/library/dn339003.aspx)

    -   [Guía de usuario de la aplicación de uso compartido Rights Management](http://technet.microsoft.com/library/dn339006.aspx)

-   **La aplicación de uso compartido Rights Management para plataformas móviles**

    Para obtener más información acerca de la aplicación de uso compartido Rights Management para plataformas móviles, consulte los recursos siguientes:

    -   Descargue la aplicación correspondiente en los vínculos de la [página de Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970)
 
    -   [Preguntas frecuentes para la aplicación de uso compartido Rights Management de Microsoft para plataformas móviles](http://technet.microsoft.com/dn451248)

-   **Otras aplicaciones compatibles con las API de RMS**:

    -   Aplicaciones de línea de negocio que se han escrito internamente mediante RMS SDK

    -   Aplicaciones de proveedores de software que se han escrito mediante RMS SDK

    Para obtener más información sobre el SDK, consulte [Microsoft Rights Management SDK](http://msdn.microsoft.com/library/hh552972%28v=vs.85%29.aspx) (SDK de Microsoft Rights Management).

> [!IMPORTANT]
> Las aplicaciones siguientes no son compatibles actualmente con Azure RMS:
> 
> -   Microsoft Office para Mac 2011
> -   Microsoft OneDrive para la Empresa para SharePoint Server 2013
> -   Visor de XPS
> 
> Además, la aplicación de uso compartido de RMS presenta la restricciones siguientes:
> 
> -   En equipos con Windows: se necesita una versión mínima de Windows 7 Service Pack 1

Para obtener más información sobre cómo estas aplicaciones admiten Azure RMS, consulte [How Applications Support Azure Rights Management](applications-support.md) (Cómo son compatibles las aplicaciones con Azure Rights Management).

Para obtener información sobre cómo configurarlas, consulte [Configuring Applications for Azure Rights Management](configure-applications.md) (Configuración de aplicaciones para Azure Rights Management).

## <a name="BKMK_SupportedServers"></a>Servidores locales compatibles con Azure RMS
Los siguientes servidores locales son compatibles con Azure RMS cuando se usa el conector Azure RMS, que actúa como una interfaz de comunicaciones (una retransmisión) entre los servidores locales y Azure RMS. Además, esta configuración precisa que defina la sincronización de directorios entre sus bosques de Active Directory y Azure Active Directory.

-   **Exchange Server**:

    -   Exchange Server 2016

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server**:

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **Servidores de archivos que ejecutan Windows Server y usan Infraestructura de clasificación de archivos (FCI)**:

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > Dado que los servidores de archivos con Windows Server 2008 R2 no tienen una acción de tarea de administración de archivos integrada para aplicar protección RMS, puede usar el conector RMS para este escenario. Sin embargo, puede usar Infraestructura de clasificación de archivos y Azure RMS en estos sistemas operativos si configura una tarea de administración de archivos personalizada para ejecutar un ejecutable o script que pueda proteger archivos mediante Azure RMS. Por ejemplo, un script de Windows PowerShell que usa los [cmdlets de protección de RMS](https://msdn.microsoft.com/library/azure/mt433195.aspx).
    > 
    > También puede usar estos cmdlets con servidores que ejecuten versiones posteriores de Windows Server, con la ventaja de que estos cmdlets pueden proteger todos los tipos de archivo. El conector RMS solo protege archivos de Office. Para obtener instrucciones sobre los procedimientos, consulte [RMS Protection with Windows Server File Classification Infrastructure &#40;FCI&#41;](configure-fci.md) (Protección de RMS con la infraestructura de clasificación de archivos de Windows Server &#40;FCI&#41;).

El conector RMS es compatible en Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2.

Para obtener más información sobre cómo configurar el conector RMS para estos servidores locales, consulte [Deploying the Azure Rights Management Connector](deploy-rms-connector.md) (Implementar el conector de Azure Rights Management).

## Véase también
[Introducción a Azure Rights Management](getting-started-with-azure-rights-management.md)



<!--HONumber=Apr16_HO3-->


