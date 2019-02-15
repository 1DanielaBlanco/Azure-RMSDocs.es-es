---
title: Terminología de Azure Information Protection
description: ¿No entiende el significado de una palabra, una frase o un acrónimo relacionados con Microsoft Azure Information Protection? Busque aquí la definición de los términos y las abreviaturas que son específicos de Azure Information Protection o que tienen un significado específico cuando se usan en el contexto de este servicio.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/01/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 742877bf-26f5-40e3-b1f7-8475e7c3ce11
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: b94a08a1201f3bedfcaa8264a75e30f2bb77232d
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56255162"
---
# <a name="terminology-for-azure-information-protection"></a>Terminología de Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

¿No entiende el significado de una palabra, una frase o un acrónimo relacionados con Microsoft Azure Information Protection? Busque aquí la definición de los términos y las abreviaturas que son específicos de Azure Information Protection o que tienen un significado específico cuando se usan en el contexto de este servicio.

|Término|Definición|
|--------|--------------|
|AADRM|Nombre del módulo de PowerShell para el servicio Azure Rights Management, derivado de la abreviatura no oficial de Azure Rights Management cuando se llamaba (Windows) Azure Active Directory Rights Management.|
|activar|Habilite el servicio Azure Rights Management para que una organización pueda proteger sus documentos y correos electrónicos. Esta acción también habilita las características de IRM en Exchange Online y SharePoint Online.|
|Active Directory Rights Management Services|En ocasiones se abrevia como *AD RMS*.<br /><br />Un rol de Windows Server que ofrece protección de administración de derechos mediante cifrado y directivas para ayudar a proteger los documentos, los archivos y el correo electrónico.|
|AD RMS|Consulte *Active Directory Rights Management Services*|
AzureInformationProtection|Nombre del módulo de PowerShell para el cliente de Azure Information Protection.
|Azure Information Protection|Servicio basado en la nube que usa etiquetas para clasificar y proteger documentos y correos electrónicos. Azure Rights Management proporciona la protección mediante el cifrado, la identidad y las directivas de autorización.|
Cliente de Azure Information Protection|Lado cliente de Azure Information Protection que permite a los usuarios, administradores y servicios usar las etiquetas y la configuración de la directiva de Azure Information Protection.|
|Etiqueta de Azure Information Protection|Elemento que aplica un valor de clasificación a los documentos y correos electrónicos y, opcionalmente, puede protegerlos.|
|Directiva de Azure Information Protection|Configuración definida por el administrador para clientes y servicios que usan la configuración de directivas y las etiquetas de Azure Information Protection.|
|Analizador de Azure Information Protection|Servicio que se ejecuta en Windows Server y le permite detectar, clasificar y proteger documentos en carpetas locales, recursos compartidos de red y sitios y bibliotecas de SharePoint Server.|
|Visor de Azure Information Protection|Aplicación que se ejecuta en equipos y dispositivos móviles Windows, para mostrar los archivos protegidos.|
|Azure Rights Management|En ocasiones, se abrevia como *Azure RMS*.<br /><br />Un servicio de Azure usado por Azure Information Protection que, mediante cifrado y directivas, ayuda a proteger los documentos, los archivos y el correo electrónico.  También se conoce como *servicio de Azure Rights Management*. Entre los nombres anteriores se incluyen:<br /><br />- *Windows Azure Active Directory Rights Management*: con frecuencia abreviado como Servicio de Windows Azure AD Rights Management.<br /><br />- *RMS Online*: el nombre que se propuso originalmente, que a veces puede ver en los mensajes de error y las entradas de archivos de registro.|
|Azure RMS|Vea *Azure Rights Management*.|
|plantilla predeterminada|Plantilla de protección que se crea automáticamente al obtener una suscripción de Azure Information Protection, por lo que inmediatamente puede empezar a proteger los documentos y correos electrónicos que contienen información confidencial.|
|BYOK|Consulte *Traiga su propia clave*.|
|Traiga su propia clave|Con frecuencia abreviado como *BYOK*.<br /><br />Una opción de configuración y topología que eligen las organizaciones que quieren generar y administrar su propia clave de inquilino de Azure Information Protection.|
|clave de contenido|Clave exclusiva que crean las aplicaciones habilitadas para RMS para cada documento o correo electrónico que está protegido mediante Rights Management y contribuye a limitar el riesgo de divulgación de la información.|
|consumir|Para abrir un documento o correo electrónico para leerlo o usarlo cuando ese archivo está protegido por Rights Management. Para un documento, el consumo incluye la edición de nuevo contenido y la incorporación de este a un documento protegido. Para un mensaje de correo electrónico, el consumo incluye la respuesta a un mensaje protegido.|
|desactivar|Deshabilitar el servicio Rights Management para que la organización ya no pueda usar Azure Information Protection.|
|plantilla de departamento|Una plantilla de protección que se crea y se configura para que esté visible para los usuarios seleccionados, en lugar de que la vean todos los usuarios de la organización. También se conoce como *plantilla con ámbito*.|
|aplicaciones habilitadas|Aplicaciones que admiten de forma nativa Rights Management, lo que incluye las aplicaciones de Office, como Word y Excel. Los vendedores de software independientes (ISV) y los desarrolladores también pueden escribir aplicaciones que admitan Rights Management de forma nativa.|
|administración de derechos empresariales|Un término genérico del sector que se usa a menudo para describir los productos y las soluciones que ayudan a las organizaciones a proteger la información patentada o valiosa mediante una combinación de herramientas de autorización mediante cifrado y directivas. Azure Information Protection es un ejemplo de solución de administración de derechos empresariales (ERM).|
|ERM|Consulte *administración de derechos empresariales*|
|protección genérica|Un nivel de protección que cifra cualquier tipo de archivo y evita que gente no autorizada abra el archivo. Después de abrir el archivo, deja de estar cifrado y se puede usar en una aplicación que no admite Rights Management de forma nativa.|
|HYOK|Ver *mantenga su propia clave*.|
|mantenga su propia clave|Con frecuencia abreviado como *HYOK*.<br /><br />Una opción de configuración y topología de una organización que quiere generar y almacenar sus propias claves de forma local, normalmente por motivos normativos o de cumplimiento.|
|objeto clave|En el contexto de la clave de inquilino, se trata de una entidad que contiene los metadatos necesarios para las operaciones criptográficas del servicio de Azure Rights Management.|
|label|Consulte *Etiqueta de Azure Information Protection*.|
|protección de la información|En ocasiones abreviada como *PI*.<br /><br />Un término genérico del sector que hace referencia a la protección de los datos y los archivos frente al acceso no autorizado, incluso después de que los datos y los archivos atraviesan los límites de la organización mediante correo electrónico o uso compartido de documentos. Microsoft Azure Information Protection es un ejemplo de solución de protección de la información (IP).|
|Information Rights Management|Con frecuencia abreviado como *IRM*.<br /><br />Término usado en conjunto con los servicios de Office, como Exchange Server, Word y SharePoint Online, para describir la posibilidad de admitir los servicios de Microsoft Rights Management.|
|IRM|Consulte *Information Rights Management*|
|Cifrado de mensajes de Office|Con frecuencia abreviado como *OME*.<br /><br />Las nuevas funcionalidades de Cifrado de mensajes de Office 365 tienen integración nativa con el servicio Azure Rights Management para proporcionar la misma protección de correo electrónico para usuarios internos y externos, actualización automática de plantillas y compatibilidad con el escenario Aportar su propia clave (BYOK). La implementación de OME anterior se diseñó solo para destinatarios externos, requería una regla de flujo de correo y no era compatible con BYOK.|
|MSDRM|A veces, se considera una referencia del cliente de RMS 1.0, que se sustituyó por el nuevo cliente, MSIPC. Este cliente anterior admite aplicaciones que se desarrollan con el SDK de RMS 1.0 y admite Office 2010 y Office 2007, Exchange 2010 y Exchange 2013, y SharePoint 2010 y SharePoint 2007.|
|MSIPC|A veces considerada como referencia para el cliente RMS 2.0, que sustituye al antiguo cliente RMS, MSDRM. Este último cliente admite aplicaciones que se desarrollan con RMS SDK 2.0 y es compatible con Office 365 ProPlus, Office 2019, Office 2016, Office 2013, SharePoint 2013 y el cliente de Azure Information Protection.|
|protección nativa|Un nivel de protección disponible en todas las aplicaciones habilitadas que evita que gente no autorizada abra un archivo y que, además, aplica directivas más estrictas, como solo lectura y la imposibilidad de imprimir. Además, esta protección permanece con el archivo, incluso cuando el archivo se reenvía a otras personas o se guarda en una ubicación pública a la que otros puedan acceder.|
|.pfile|Extensión del nombre de archivo que se anexa a todos los archivos que un servicio de administración de derechos protege de manera genérica.|
|nivel de permisos|Una agrupación lógica de derechos de uso que facilitan a los usuarios finales y administradores la elección de opciones de configuración basadas en roles. Por ejemplo, Revisor y Coautor.|
|proteger|Aplicar controles de administración de derechos a archivos o a mensajes de correo electrónico mediante directivas de cifrado, identidad y control de acceso para ayudar a proteger los datos.|
|plantilla de protección|También se conoce como *plantilla de directiva de permisos*, *plantilla de Rights Management* y *plantilla de RMS*.<br /><br />Grupo de configuraciones de protección que administrada un administrador y que incluyen los derechos de uso definidos para los usuarios autorizados y controles de acceso para la expiración y el acceso sin conexión. |
|publish|Proteger un archivo a fin de evitar el acceso y el uso no autorizados. También se usa como un término junto con plantillas de protección y la directiva de Azure Information Protection, para hacer que estos elementos estén disponibles para su uso para los clientes y los servicios.|
|conector de Rights Management|Retransmisión de proxy de salida que se puede implementar para los servicios locales, como Exchange Server y SharePoint, a fin de proteger los datos mediante el servicio Azure Rights Management.|
|Emisor de Rights Management|Cuenta que se ha usado para proteger un documento o correo electrónico.|
|Propietario de Rights Management|Cuenta que conserva el control total de un documento o correo electrónico protegidos mediante la concesión automática del derecho de uso Control total de Rights Management. No cuenta con fecha de expiración ni opciones sin conexión.|
|servicios de Rights Management|Término genérico que se aplica tanto a la versión en la nube de Rights Management (Azure Rights Management) como a la versión local de Rights Management (AD RMS).|
|Aplicación de uso compartido Rights Management|Ahora se ha sustituido por el cliente de Azure Information Protection.|
|RMS|Consulte *servicios de Rights Management*|
|conector RMS|Consulte *conector de Rights Management*|
|RMS para usuarios|Suscripción gratuita para que un usuario use Rights Management cuando la organización no tenga una suscripción a Office 365 o Azure Active Directory.|
|Aplicación RMS sharing|Consulte *Rights Management sharing*.|
|Plantilla de RMS|Consulte *plantilla de protección*.|
|modo de solo protección|Un modo de funcionamiento para el cliente de Azure Information Protection cuando no hay ninguna directiva de Azure Information Protection para aplicar las etiquetas. En este modo, no se muestran las etiquetas de clasificación, pero los usuarios de todos modos pueden aplicar la protección de Rights Management.|
|escáner|Consulte *Analizador de Azure Information Protection*.|
|superusuario|Grupo de administradores de gran confianza que pueden descifrar y obtener acceso a los archivos que la organización ha protegido mediante un servicio de administración de derechos. Normalmente, se necesita este nivel de acceso para la exhibición de documentos electrónicos legales y para los equipos de auditoría.|
|clave de inquilino|También se conoce como la clave del Certificado emisor de licencias de servidor (SLC).<br /><br />La clave que es exclusiva de una organización y que, en definitiva, asegura todas las funciones criptográficas de Rights Management que se relacionan con esta clave de inquilino.|
|desproteger|Quitar controles de protección de los archivos o mensajes de correo electrónico que usaban directivas de cifrado, identidad, derechos de uso y control de acceso para ayudar a proteger los datos.|
|licencia de uso|Certificado de cada documento que se concede a un usuario que abre un archivo o un mensaje de correo electrónico protegido mediante un servicio de administración de derechos. Este certificado contiene los derechos del usuario relativos al archivo o mensaje de correo electrónico y la clave de cifrado que se usó para cifrar el contenido, así como las restricciones de acceso adicionales definidas en la directiva del documento.|

