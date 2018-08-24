---
title: Novedades y notas de la versión
description: Se describen las características y los cambios importantes de esta nueva versión y de las anteriores.
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 09/25/2017
ms.topic: article
ms.service: information-protection
ms.assetid: 4fa1c686-b00b-4734-9abb-141ce582a6af
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.openlocfilehash: d0edc0337e7913b1d149f6e84cb0ce7536528ffb
ms.sourcegitcommit: 7ba9850e5bb07b14741bb90ebbe98f1ebe057b10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2018
ms.locfileid: "42807107"
---
# <a name="whats-new-and-release-notes"></a>Novedades y notas de la versión

## <a name="whats-new"></a>Novedades

En este tema se describen las características y los cambios importantes de esta nueva versión de RMS  SDK v4.x.

-   [Novedades de julio de 2017](#new-for-july-2017)
-   [Actualización de octubre de 2016](#October-2016-update)
-   [Actualización de junio de 2016](#new-for-June-2016)
-   [Actualización de diciembre de 2015](#december-2015-update)
-   [Actualización de julio de 2015: se agrega compatibilidad con desarrollo en C++ y Linux](#july-2015-update-adds-support-for-linux-c-developm)
-   [Actualización de mayo de 2015: se agrega control de registro](#may-2015-update-adds-logging-control)
-   [Actualización de febrero de 2015: se agrega compatibilidad con aplicaciones de la Tienda Windows](#february-2015-update-adds-windows-store-application-support)
-   [Actualización de enero de 2015: se agrega compatibilidad con la plataforma WinPhone](#january-2015-update-adds-winphone-platform-support)
-   [Actualización de octubre de 2014: se actualiza a Microsoft RMS SDK 4.1](#october-2014-update-upgrade-to-microsoft-rms-sdk-4-1)
-   [Notas de la versión](#release-notes)
-   [Preguntas más frecuentes](#frequently-asked-questions)

### <a name="new-for-july-2017"></a>Novedades de julio de 2017

La actualización para la versión de julio incluía aumentar la revisión del SDK, ahora 4.2.5.

- SDK de Android: La aplicación ahora puede **establecer el nivel de registro sobre la marcha** con Android SDK. Para más información, vea [How to: Enable error and performance logging](https://docs.microsoft.com/information-protection/develop/enabling-logging) (Procedimiento para habilitar el registro de rendimiento y errores).
- El SDK de iOS no es compatible con el nivel de registro. 
- El SDK ahora devuelve un error para un token de acceso NULL.

### <a name="october-2016-update"></a>Actualización de octubre de 2016

- Se implementan algunas correcciones de errores de back-end.
- Se habilita Bitcode para el SDK de Apple iOS/OSX.

### <a name="june-2016-update"></a>Actualización de junio de 2016

- **Compatibilidad con la autenticación moderna**: proporciona inicio de sesión basado en la biblioteca de autenticación de Active Directory (ADAL) para las aplicaciones con RMS habilitado. Permite características de inicio de sesión como Multi-Factor Authentication (MFA), proveedores de identidades de terceros basados en SAML con aplicaciones cliente de RMS y autenticación con tarjetas inteligentes y basada en certificados. También elimina la necesidad de usar el protocolo de autenticación básica con las aplicaciones con RMS habilitado.
- **Compatibilidad con Seguimiento de documentos**: ahora los desarrolladores pueden habilitar el seguimiento de documentos al proteger los documentos en sus aplicaciones.
- Mejoras en el rendimiento
- Correcciones de errores

### <a name="december-2015-update"></a>Actualización de diciembre de 2015

Con esta versión, RMS SDK para dispositivos pasa a la versión 4.2 y agrega lo siguiente:

-   Seguimiento de documentos, RMS Online solo, para sistemas operativos Android e iOS/OS X.

    Para más información e instrucciones de uso sobre iOS/OSX, vea la clase [MSLicenseMetadata](https://msdn.microsoft.com/library/mt573683.aspx), que proporciona información de seguimiento y el método de registro de seguimiento de documentos adicional en [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx). Existen adiciones similares para Android a [LicenseMetadata](https://msdn.microsoft.com/library/mt573675.aspx) y [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx).

    Para ver una descripción detallada de la característica de seguimiento de documentos, consulte [Uso del seguimiento de documentos](how-to-use-document-tracking.md).

-   Un conjunto de métodos sincrónicos equivalentes a las versiones asincrónicas de la API de Android:

    [Método sincrónico CustomProtectedInputStream.create](https://msdn.microsoft.com/library/mt631362.aspx)

    [Método sincrónico CustomProtectedOutputStream.create](https://msdn.microsoft.com/library/mt631363.aspx)

    [Método sincrónico ProtectedFileInputStream.create](https://msdn.microsoft.com/library/mt631375.aspx)

    [Método sincrónico ProtectedFileOutputStream.create](https://msdn.microsoft.com/library/mt631376.aspx)

    [Método sincrónico TemplateDescriptor.getTemplates](https://msdn.microsoft.com/library/mt631380.aspx)

    [Método sincrónico UserPolicy.acquire](https://msdn.microsoft.com/library/mt631384.aspx)

    [Método sincrónico UserPolicy.create (PolicyDescriptor…)**](https://msdn.microsoft.com/library/mt631385.aspx)

    [Método sincrónico UserPolicy.create (TempalteDescriptor…)](https://msdn.microsoft.com/library/mt631386.aspx)

-   Se ha agregado una nueva clase [ProtectedBuffer](https://msdn.microsoft.com/library/mt631369.aspx) a la API de Android.
-   Actualizaciones para mejorar la experiencia de mensajería de errores y solución de problemas.
-   Mejoras de rendimiento significativas en las operaciones criptográficas.

### <a name="july-2015-update---adds-support-for-linux--c-development"></a>Actualización de julio de 2015: se agrega compatibilidad con el desarrollo de C++ y Linux

Esta versión agrega las siguientes actualizaciones:

-   RMS SDK 4.1 para plataformas Linux

    Para más información, vea [Get started](get-started.md) (Introducción).

### <a name="may-2015-update---adds-logging-control"></a>Actualización de mayo de 2015: se agrega control de registro

Esta versión agrega compatibilidad con las siguientes actualizaciones:

-   iOS

    El cifrado y descifrado de aplicaciones puede funcionar independientemente y en paralelo.

    Para obtener más información, consulte [MSProtector](https://msdn.microsoft.com/library/mt210993.aspx).

    Configuración de control de nivel de registro habilitada.

    Para más información, vea [How to: Enable error and performance logging](enabling-logging.md) (Procedimiento para habilitar el registro de rendimiento y errores).

    Se agregó compatibilidad de borrado de memoria caché.

    Para obtener más información, consulte [MSProtection:resetStateWithCompletionBlock](https://msdn.microsoft.com/library/mt210991.aspx).

### <a name="february-2015-update---adds-windows-store-application-support"></a>Actualización de febrero de 2015: se agrega compatibilidad con la aplicación de la Tienda Windows

Esta versión agrega compatibilidad con las aplicaciones de la Tienda Windows y proporciona las mismas funciones en las versiones de RMS SDK 4.1 para Windows Phone, Android e iOS/OSX.

### <a name="january-2015-update---adds-winphone-platform-support"></a>Actualización de enero de 2015: se agrega compatibilidad con la plataforma WinPhone

Esta versión agrega compatibilidad con el sistema operativo Windows Phone y proporciona las mismas funciones en las versiones de RMS SDK 4.1 para Android e iOS/OS X.

### <a name="october-2014-update---upgrade-to-microsoft-rms-sdk-41"></a>Actualización de octubre de 2014: se actualiza a Microsoft RMS SDK 4.1

La versión 4.1 de RMS SDK agrega las siguientes características nuevas a Google Android y Apple iOS/OS X.

-   Extensiones de API del SDK de Android y iOS/OS X para el procesamiento de *consentimientos de usuario*, que permite la confirmación de usuario de comportamientos de SDK. Actualmente, el seguimiento de documentos y el acceso a direcciones URL de servicio de AD RMS desconocidas son los tipos de consentimiento admitidos.

    Para obtener más información, consulte un ejemplo de la versión de API para Android de la [interfaz ConsentCallback](https://msdn.microsoft.com/library/dn833503.aspx).

-   Ahora iOS 8 y OS X 10.10 (Yosemite) son compatibles. También se han realizado algunos cambios en los nombres de propiedad, necesarios para Xcode 6.

    Ejemplo: MSUserPolicy.name ahora es [MSUserPolicy.policyName](https://msdn.microsoft.com/library/dn790799.aspx).

## <a name="release-notes"></a>Notas de la versión

En esta sección se detalla información sobre las versiones actuales y anteriores de las API de Microsoft Rights Management SDK 4.x que, como desarrollador, le conviene conocer.

**AD RMS SDK 4.1: versión de disponibilidad global para plataformas iOS/OS X y Android**

-   **Compatibilidad de AD RMS:** los administradores de TI pueden usar aplicaciones habilitadas para RMS en los dispositivos móviles gracias a las nuevas extensiones para dispositivo móvil del servidor de AD RMS.
-   **Uso sin conexión:** los usuarios finales pueden tener acceso sin conexión a los datos protegidos mediante RMS.
-   **Autenticación segregada**: los desarrolladores pueden usar su propia biblioteca de autenticación para Azure RMS y AD RMS, o bien usar, tal como se recomienda, la [biblioteca de autenticación de Azure AD (ADAL)](https://MSDN.Microsoft.Com/library/jj573266.aspx).
-   **Interfaz de usuario por separado:** los desarrolladores pueden crear sus propias interfaces de usuario para proteger y usar documentos protegidos con RMS.
-   **API rediseñada**: ahora los desarrolladores pueden disfrutar de una API de cifrado y descifrado sencilla y sin trabas que proporciona una experiencia de usuario y unos comportamientos de RMS uniformes, sin apenas esfuerzo.

**Comunes a todas las plataformas**

-   Las API de RMS SDK 4.x no son *seguras para subprocesos*.

**Android**

-   Cuando se usa una aplicación de ejemplo en un dispositivo Kindle de Amazon® para ver datos adjuntos .ptxt, antes debe descargar el archivo para poder verlo.

    **Solución**: este es un problema conocido que se abordará más adelante.

-   Una aplicación que usa el SDK se puede bloquear si se permiten varias instancias.

    **Solución:** asegúrese de que la aplicación no admite llamadas de instancias múltiples a la API de Android.

-   Cuando uso el método [ProtectedFileOutputStream](https://msdn.microsoft.com/library/dn790855.aspx).write(byte\[\] array, int offset, int length) con una longitud distinta al valor de *array.length*, luego no puedo usar el contenido con el SDK.

    **Solución:** este es un problema conocido. Para mitigarlo, pase siempre una matriz *byte \[\]* con el mismo valor de longitud que el parámetro de longitud o use el método [ProtectedFileOutputStream](https://msdn.microsoft.com/library/dn790855.aspx).write(byte\[\] array).

**iOS y OS X**

-   Hay dos dialectos del portugués que nuestros SDK de iOS y OS X admiten. Desafortunadamente, debido a un error, a día de hoy no se admite la primera localización por completo. A causa de este error, el idioma portugués no es totalmente compatible. La mayor parte del texto está traducida, pero no la interfaz de usuario.

    1. Portugués

    2. Portugués (Portugal)

**Solo iOS**

-   RMS SDK 4.x no muestra el indicador de actividad de red.

    Se trata de un comportamiento opcional conocido de iOS según las directrices de interfaz humana de Apple.

**Solo OS X**

-   RMS SDK 4.x no muestra el indicador de actividad de red.

    Se trata de un comportamiento opcional conocido de OSX según las directrices de interfaz humana de Apple.

-   **Solución:** para crear una aplicación de interfaz de múltiples documentos (MDI) con nuestro SDK de OS X, use las siguientes directrices.

    Los siguientes métodos no se deben ejecutar al mismo tiempo. Para supervisar la finalización de la ejecución, use el método de bloqueo de finalización, según se indica.

    - [MSProtectedData.protectedDataWithProtectedFile](https://msdn.microsoft.com/library/dn758351.aspx)
    - [MSCustomProtectedData.customProtectedDataWithPolicy](https://msdn.microsoft.com/library/dn758315.aspx)



**Nota:** las aplicaciones MDI no son compatibles con nuestra API de iOS.

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

**Todas las plataformas**

**P:** No veo ninguna interfaz de usuario de selección de **permisos personalizados** en el flujo de trabajo de protección. ¿Por qué?

**R:** Este es un problema conocido que se abordará más adelante.

**P:** ¿Cómo puedo obtener nuevos inquilinos organizativos para probar el SDK y las aplicaciones de ejemplo?

**R**: Para pedir credenciales para las organizaciones de prueba de Azure AD RMS, envíe un correo electrónico a <rmcstbeta@microsoft.com>.

**P:** No veo ninguna explicación de la jerarquía de prueba en la documentación. ¿Por qué?

**R:** No hay ningún concepto de jerarquía de prueba en los nuevos AD RMS SDK. Siempre se trabajará con la jerarquía de producción.

**P**: En la versión 2.1 de RMS SDK se necesitaba un manifiesto generado para cada aplicación que implementaba información de protección. ¿Esto sigue siendo así en las versiones 4.0 y posteriores del SDK?

**R:** No. Los manifiestos ya no son necesarios en las versiones 3.0 y posteriores de Rights Management SDK.

**Android**

**P:** ¿Con qué entornos de desarrollo se ha probado el SDK?

**R:** Eclipse Juno con Google API 15 y versiones posteriores.

**P:** ¿Puedo llamar al método de cancelación cancel() desde el subproceso de interfaz de usuario?
**R:** Debe llamar a cancel() desde un subproceso que no sea de interfaz de usuario, dado que puede anular una conexión de red.

**iOS**

**P:** ¿Qué plataformas se han comprobado para el desarrollo del SDK?

**R:** Xcode 5.0 con iOS 7 y versiones posteriores.

**P:** He llamado a un método cancel() en una operación, pero sigue apareciendo una notificación de operación completada. ¿Por qué?

**R:** No todas las operaciones se pueden cancelar. Una operación de cancelación se ejecuta de la mejor forma posible.

**OS X**

**P**: El marco de la aplicación de ejemplo está adaptado a Xcode 5, ¿puedo trabajar con Xcode 4.6?

**R:** El SDK de OS X funciona solo con Xcode 4.6 y versiones posteriores, así como con OS X 10.8 y versiones posteriores.

