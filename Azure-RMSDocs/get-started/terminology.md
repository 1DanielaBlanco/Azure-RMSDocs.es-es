---
title: "Terminología de Azure Information Protection"
description: "¿No entiende el significado de una palabra, una frase o un acrónimo relacionados con Microsoft Azure Information Protection? Busque aquí la definición de los términos y las abreviaturas que son específicos de Azure Information Protection o que tienen un significado específico cuando se usan en el contexto de este servicio."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 742877bf-26f5-40e3-b1f7-8475e7c3ce11
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: a5cfa773d440e92fe9d3e88e242dfb25f7174400


---

# <a name="terminology-for-azure-information-protection"></a>Terminología de Azure Information Protection

>*Se aplica a: Azure Information Protection, Office 365*

¿No entiende el significado de una palabra, una frase o un acrónimo relacionados con Microsoft Azure Information Protection? Busque aquí la definición de los términos y las abreviaturas que son específicos de Azure Information Protection o que tienen un significado específico cuando se usan en el contexto de este servicio.

|Término|Definición|
|--------|--------------|
|AADRM|Nombre del módulo de Windows PowerShell para el servicio Azure Rights Management, que se derivó de la abreviatura no oficial de [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] cuando se llamaba (Windows) Azure Active Directory Rights Management.|
|activar|Habilitar el servicio [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] para que una organización pueda proteger sus documentos y correos electrónicos. Esta acción también habilita las características de Rights Management en Exchange Online y SharePoint Online.|
|Active Directory Rights Management Services|En ocasiones se abrevia como *AD RMS*.<br /><br />Un rol de Windows Server que brinda protección de administración de derechos mediante cifrado y directivas para ayudar a proteger los documentos, los archivos y el correo electrónico.|
|AD RMS|Consulte *Active Directory Rights Management Services*|
|Azure Information Protection|Un servicio basado en la nube que usa la clasificación, el etiquetado y la protección para ayudar a que los documentos y los correos electrónicos estén seguros. Azure Rights Management proporciona la protección mediante el cifrado, la identidad y las directivas de autorización.|
|Azure Rights Management|En ocasiones, se abrevia como *Azure RMS*.<br /><br />Un servicio de Azure usado por Azure Information Protection que, mediante cifrado y directivas, ayuda a proteger los documentos, los archivos y el correo electrónico.  También se conoce como *servicio de Azure Rights Management*. Entre los nombres anteriores se incluyen:<br /><br />- *Windows Azure Active Directory Rights Management*: Con frecuencia abreviado como servicio Windows Azure AD Rights Management.<br /><br />- *RMS Online*: Nombre que se propuso originalmente, que a veces puede ver en los mensajes de error y en las entradas de archivos de registro.|
|Azure RMS|Consulte *Azure Rights Management*.|
|BYOK|Consulte *Traiga su propia clave*.|
|Traiga su propia clave|Con frecuencia abreviado como *BYOK*.<br /><br />Una opción de configuración y topología que eligen las organizaciones que quieren generar y administrar su propia clave de inquilino de Azure Information Protection.|
|clave de contenido|Una clave exclusiva que crean las aplicaciones habilitadas para RMS para cada documento o correo electrónico que está protegido mediante [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] y que ayuda a limitar el riesgo de divulgación de la información.|
|consumir|Desbloquear un archivo para leerlo o usarlo cuando ese archivo está protegido por [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].|
|desactivar|Deshabilitar el servicio Rights Management para que la organización ya no pueda usar Azure Information Protection.|
|plantilla de departamento|Una plantilla de directiva de derechos que se crea (una plantilla personalizada) y se configura para que esté visible para los usuarios seleccionados, en lugar de que la vean todos los usuarios de la organización.|
|aplicaciones habilitadas|Aplicaciones que admiten de forma nativa Rights Management, lo que incluye las aplicaciones de Office, como Word y Excel. Los fabricantes de software independientes (ISV) y los desarrolladores también pueden escribir aplicaciones que admitan [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] de forma nativa.|
|administración de derechos empresariales|Un término genérico del sector que se usa a menudo para describir los productos y las soluciones que ayudan a las organizaciones a proteger la información patentada o valiosa mediante una combinación de herramientas de autorización mediante cifrado y directivas. Azure Information Protection es un ejemplo de solución de administración de derechos empresariales (ERM).|
|ERM|Consulte *administración de derechos empresariales*|
|protección genérica|Un nivel de protección que cifra cualquier tipo de archivo y evita que gente no autorizada abra el archivo. Después de abrir el archivo, deja de estar cifrado y se puede usar en una aplicación que no admite [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] de forma nativa.|
|HYOK|Ver *mantenga su propia clave*.|
|mantenga su propia clave|Con frecuencia abreviado como *HYOK*.<br /><br />Una opción de configuración y topología de una organización que quiere generar y almacenar sus propias claves de forma local, normalmente por motivos normativos o de cumplimiento.|
|protección de la información|En ocasiones abreviada como *PI*.<br /><br />Un término genérico del sector que hace referencia a la protección de los datos y los archivos frente al acceso no autorizado, incluso después de que los datos y los archivos atraviesan los límites de la organización mediante correo electrónico o uso compartido de documentos. Microsoft Azure Information Protection es un ejemplo de solución de protección de la información (IP).|
|Information Rights Management|Con frecuencia abreviado como *IRM*.<br /><br />Término usado en conjunto con los servicios de Office, como Exchange Server, Word y SharePoint Online, para describir la posibilidad de admitir los servicios de Microsoft Rights Management.|
|IRM|Consulte *Information Rights Management*|
|MSDRM|A veces, se considera una referencia del cliente de RMS 1.0, que se sustituyó por el nuevo cliente, MSIPC. Este cliente anterior admite aplicaciones que se desarrollan con el SDK de RMS 1.0 y admite Office 2010 y Office 2007, Exchange 2010 y Exchange 2013, y SharePoint 2010 y SharePoint 2007.|
|MSPIC|A veces considerada como referencia para el cliente RMS 2.0, que sustituye al antiguo cliente RMS, MSDRM. Este último cliente admite aplicaciones que se desarrollan con RMS SDK 2.0 y es compatible con Office 2016 y Office 2013, SharePoint 2013, la aplicación RMS sharing y el cliente de Azure Information Protection.|
|protección nativa|Un nivel de protección disponible en todas las aplicaciones habilitadas que evita que gente no autorizada abra un archivo y que, además, aplica directivas más estrictas, como solo lectura y la imposibilidad de imprimir. Además, esta protección permanece con el archivo, incluso cuando el archivo se reenvía a otras personas o se guarda en una ubicación pública a la que otros puedan acceder.|
|.pfile|Extensión del nombre de archivo que se anexa a todos los archivos que un servicio de administración de derechos protege de manera genérica.|
|.ppdf|Extensión del nombre de archivo que un servicio de administración de derechos crea al generar automáticamente una copia en PDF de un archivo (de Word, Excel, PowerPoint o PDF) que comparte por correo electrónico, de modo que el archivo pueda leerse (pero no editarse) en todos los dispositivos.|
|nivel de permisos|Una agrupación lógica de derechos de uso que facilitan a los usuarios finales y administradores la elección de opciones de configuración basadas en roles. Por ejemplo, Revisor y Coautor.|
|proteger|Aplicar controles de administración de derechos a archivos o a mensajes de correo electrónico mediante directivas de cifrado, identidad y control de acceso para ayudar a proteger los datos.|
|publish|Proteger un archivo a fin de evitar el acceso y el uso no autorizados.|
|conector de Rights Management|Retransmisión de proxy de salida que se puede implementar para los servicios locales, como Exchange Server y SharePoint, a fin de proteger los datos mediante el servicio Azure Rights Management.|
|servicios de Rights Management|Término genérico que se aplica a la versión en la nube de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] ([!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]) y a la versión local de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] (AD RMS).|
|Aplicación de uso compartido Rights Management|Ahora se ha reemplazado por el cliente de Azure Information Protection, una aplicación opcional para dispositivos con Windows y la mayoría de los dispositivos móviles más conocidos, que admite el uso compartido seguro de archivos de forma local y por correo electrónico.|
|RMS|Consulte *servicios de Rights Management*|
|conector RMS|Consulte *conector de Rights Management*|
|RMS para usuarios|Suscripción gratuita para que un usuario utilice [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] cuando la organización no tenga una suscripción a Office 365 o Azure Active Directory.|
|Aplicación RMS sharing|Consulte *Rights Management sharing*.|
|superusuario|Grupo de administradores de gran confianza que pueden descifrar y obtener acceso a los archivos que la organización ha protegido mediante un servicio de administración de derechos. Normalmente, se necesita este nivel de acceso para la exhibición de documentos electrónicos legales y para los equipos de auditoría.|
|clave de inquilino|También se conoce como la clave del Certificado emisor de licencias de servidor (SLC).<br /><br />La clave que es exclusiva de una organización y que, en definitiva, asegura todas las funciones criptográficas de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] que se relacionan con esta clave de inquilino.|
|desproteger|Quitar controles de administración de derechos de los archivos o mensajes de correo electrónico que usaban directivas de cifrado, identidad y control de acceso para ayudar a proteger los datos.|
|licencia de uso|Certificado de cada documento que se concede a un usuario que abre un archivo o un mensaje de correo electrónico protegido mediante un servicio de administración de derechos. Este certificado contiene los derechos del usuario relativos al archivo o mensaje de correo electrónico y la clave de cifrado que se usó para cifrar el contenido, así como las restricciones de acceso adicionales definidas en la directiva del documento.|

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



<!--HONumber=Feb17_HO4-->


