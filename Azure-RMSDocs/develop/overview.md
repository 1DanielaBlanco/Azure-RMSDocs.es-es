---
title: "Información general - RMS SDK 4.2 | Azure RMS"
description: "AD RMS y Azure RMS son tecnologías de protección de la información con la que es más fácil proteger la información digital frente al uso no autorizado."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8A13494E-C1D7-407D-BCD1-A406915EA578
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: 65113e57c57621faf9e4625bf224a3f70e9b2e1d


---

# <a name="overview"></a>Información general

Microsoft Rights Management SDK 4.2 es una tecnología de protección de la información disponible para varias plataformas.  Se trata de un marco de trabajo o kit de desarrollo de software (SDK) que está diseñado para equipos cliente y dispositivos con el objetivo de ayudar a proteger el acceso a la información que circula por aplicaciones con “derechos habilitados”, así como el uso de esa información. Los SDK de esas plataformas proporcionan una API sencilla con la que el desarrollador de una aplicación puede proteger o consumir contenido digital, recuperar plantillas y adquirir directivas de un servidor, además de otras tareas relacionadas con la administración de derechos.

Para más información sobre las plataformas compatibles actualmente, visite nuestro portal de documentación para desarrolladores de [Microsoft Rights Management SDK](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md).

Estos son algunos de los posibles escenarios:

-   Un bufete de abogados quiere evitar que los mensajes de correo confidenciales se impriman o reenvíen desde un dispositivo móvil.
-   Los desarrolladores de un software de fabricación y diseño asistido por PC quieren limitar el acceso con capacidad de dibujo a un pequeño grupo de usuarios pertenecientes a la división de investigación y sin necesidad de usar contraseñas.
-   Los propietarios de una aplicación móvil de diseño gráfico quieren usar una única licencia que permita la visualización gratuita de copias de baja resolución de sus imágenes, pero que requiera un pago para tener acceso a las versiones de alta resolución.
-   Los propietarios de una biblioteca de documentos en línea quieren habilitar derechos para ver, imprimir o editar documentos basados en la identidad del usuario, cuando los documentos se descargan en un dispositivo móvil.
-   Una gran compañía quiere publicar información confidencial de sus empleados en un sitio web interno con limitación de los privilegios de visualización y edición a determinados usuarios.

MS RMS SDK 4.2 se puede descargar, con la confirmación y la aceptación de su contrato de licencia, y se puede distribuir libremente con el software de terceros para habilitar el acceso de cliente a contenidos que se han protegido con derechos mediante el uso y la implementación de servidores de AD RMS en su entorno o servicios de Azure RMS. Para más información, vea [Get started](get-started.md) (Introducción).

## <a name="sdk-highlights"></a>Información destacada del SDK


Entre las interesantes características de MS RMS SDK 4.2, se incluyen las siguientes:

-   **API rediseñada**: MS RMS SDK 4.2 API se ha rediseñado para simplificarla al máximo. Ahora, los desarrolladores pueden disfrutar de una API de cifrado y descifrado sencilla y sin trabas que proporciona unos comportamientos de RMS uniformes, sin apenas esfuerzo.
-   **Compatibilidad híbrida para AD RMS y Azure RMS**: una única aplicación habilitada para RMS puede consumir y proteger el contenido tanto del servidor de AD RMS (con la extensión para dispositivos móviles de AD RMS) como del servicio de Azure RMS. MS RMS SDK 4.2 descubre de manera transparente el extremo pertinente que los administradores de TI pueden configurar.
-   **Aporte su propia biblioteca de autenticación**: como desarrollador de aplicaciones, puede elegir la biblioteca de autenticación que se usa con MS RMS SDK 4.2. Tanto si se trata de la [Biblioteca de autenticación de Azure AD](https://msdn.microsoft.com/library/jj573266.aspx) o de la biblioteca personalizada de su organización, MS RMS SDK 4.2 aísla la pila de autenticación para que pueda elegir la biblioteca que mejor se adapte a sus necesidades.
-   **Aporte su propia interfaz de usuario**: MS RMS SDK 4.2 ahora permite implementar una interfaz de usuario personalizada. Con MS RMS SDK 4.2 no es obligatorio que las aplicaciones usen una de las interfaces de usuario integradas, ni para proteger el contenido, ni para elegir plantillas, ni para mostrar y cambiar los permisos al consumir contenido protegido. Pero si quiere, puede usar las bibliotecas de interfaces de usuario de Microsoft RMS para todas las plataformas a través de nuestra [cuenta de GitHub](https://github.com/AzureAD/).
-   **Acceso protegido a contenido sin conexión**: MS RMS SDK 4.2 permite que los usuarios de su aplicación tengan acceso a contenido protegido incluso sin conexión a Internet. MS RMS SDK 4.2 almacena en caché de forma segura las directivas de consumo del contenido protegido para que sus usuarios puedan tener acceso sin conexión a datos protegidos mediante RMS.

Use la guía de [Introducción](get-started.md) para empezar un proyecto de aplicación para dispositivos con información protegida.

## <a name="related-topics"></a>Temas relacionados

* [Microsoft Rights Management SDK](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md)
* [Introducción](get-started.md)
* [Biblioteca de autenticación de Azure AD](https://msdn.microsoft.com/en-us/library/jj573266.aspx)
* [Cuenta de GitHub](https://github.com/AzureAD/)
 

 






<!--HONumber=Nov16_HO2-->


