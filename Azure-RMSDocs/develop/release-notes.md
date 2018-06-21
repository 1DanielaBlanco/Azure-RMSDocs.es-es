---
title: Novedades y notas de la versión
description: Se describen los cambios y las características importantes de esta versión y las anteriores.
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 09/25/2017
ms.topic: article
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4fa1c686-b00b-4734-9abb-141ce582a6af
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.openlocfilehash: 130da5ecf3fb95297f9bc335b1ea5023d53c589f
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/29/2018
ms.locfileid: "28878942"
---
# <a name="whats-new-and-release-notes"></a>Novedades y notas de la versión

## <a name="whats-new"></a>Novedades

En este tema se describen los cambios y las características importantes de esta nueva versión del SDK de RMS v4.x.

-   [Novedades de julio de 2017](#new-for-july-2017)
-   [Actualización de octubre de 2016](#October-2016-update)
-   [Actualización de junio de 2016](#new-for-June-2016)
-   [Actualización de diciembre de 2015](#december-2015-update)
-   [Actualización de julio de 2015: se agrega compatibilidad para Linux / desarrollo de C++](#july-2015-update-adds-support-for-linux-c-developm)
-   [Actualización de mayo de 2015: se agrega control de registro](#may-2015-update-adds-logging-control)
-   [Actualización de febrero de 2015: se agrega compatibilidad para las aplicaciones de la Tienda Windows](#february-2015-update-adds-windows-store-application-support)
-   [Actualización de enero de 2015: se agrega compatibilidad para la plataforma WinPhone](#january-2015-update-adds-winphone-platform-support)
-   [Actualización de octubre de 2014: se actualiza Microsoft RMS SDK 4.1](#october-2014-update-upgrade-to-microsoft-rms-sdk-4-1)
-   [Notas de la versión](#release-notes)
-   [Preguntas más frecuentes](#frequently-asked-questions)

### <a name="new-for-july-2017"></a>Novedades de julio de 2017

La actualización de la versión de julio incluyó el incremento de la revisión del SDK, ahora 4.2.5.

- La aplicación puede ahora **establecer el nivel de registro sobre la marcha** con Android SDK. Para más información, consulte [Procedimiento para habilitar el registro de rendimiento y errores](https://docs.microsoft.com/information-protection/develop/enabling-logging)
- El SDK de iOS no es compatible con el nivel de registro. 
- El SDK ahora devuelve un error para los tokens de acceso NULL.

### <a name="october-2016-update"></a>Actualización de octubre de 2016

- Implementa algunas correcciones de errores de back-end.
- Habilita bitcode para el SDK de Apple iOS y OSX.

### <a name="june-2016-update"></a>Actualización de junio de 2016

- **Compatibilidad con la autenticación moderna**: trae el inicio de sesión basado en la Biblioteca de autenticación de Active Directory (ADAL) a las aplicaciones habilitadas para RMS. Habilita características de inicio de sesión, como la autenticación multifactor (MFA), los proveedores de identidades de terceros basados en SAML con las aplicaciones cliente de RMS, tarjetas inteligentes y la autenticación basada en certificados, y elimina la necesidad de aplicaciones habilitadas para RMS para usar el protocolo de autenticación básico.
- **Compatibilidad con el seguimiento de documentos**: los desarrolladores ahora pueden habilitar el seguimiento de documentos al proteger los documentos en sus aplicaciones
- Mejoras de rendimiento
- Correcciones de errores

### <a name="december-2015-update"></a>Actualización de diciembre de 2015

RMS SDK para dispositivos está pasa ahora a la versión 4.2 y agrega:

-   Seguimiento de documentos (solo RMS en línea) para sistemas operativos Android e iOS/OS X.

    Para más información e instrucciones de uso sobre iOS/OS X, consulte la clase [MSLicenseMetadata](https://msdn.microsoft.com/library/mt573683.aspx), que proporciona información de seguimiento y el método de registro de seguimiento del documento adicional [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx). Existen incorporaciones similares a [LicenseMetadata](https://msdn.microsoft.com/library/mt573675.aspx) y [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) para Android.

    Para una descripción detallada de la característica de seguimiento de documentos, consulte [Uso del seguimiento de documentos](how-to-use-document-tracking.md).

-   Conjunto de métodos sincrónicos paralelos a las versiones asincrónicas de la API de Android:

    [CustomProtectedInputStream.create synchronous method](https://msdn.microsoft.com/library/mt631362.aspx) (Método sincrónico CustomProtectedInputStream.create)

    [CustomProtectedOutputStream.create synchronous method](https://msdn.microsoft.com/library/mt631363.aspx) (Método sincrónico CustomProtectedOutputStream.create)

    [ProtectedFileInputStream.create synchronous method](https://msdn.microsoft.com/library/mt631375.aspx) (Método sincrónico ProtectedFileInputStream.create)

    [ProtectedFileOutputStream.create synchronous method](https://msdn.microsoft.com/library/mt631376.aspx) (Método sincrónico ProtectedFileOutputStream.create)

    [TemplateDescriptor.getTemplates synchronous method](https://msdn.microsoft.com/library/mt631380.aspx) (Método sincrónico TemplateDescriptor.getTemplates)

    [UserPolicy.acquire synchronous method](https://msdn.microsoft.com/library/mt631384.aspx) (Método sincrónico UserPolicy.acquire)

    [UserPolicy.create (PolicyDescriptor…) synchronous method**](https://msdn.microsoft.com/library/mt631385.aspx) [Método sincrónico UserPolicy.create (PolicyDescriptor...)**]

    [UserPolicy.create (TemplateDescriptor…) synchronous method**](https://msdn.microsoft.com/library/mt631386.aspx) [Método sincrónico UserPolicy.create (TemplateDescriptor...)**]

-   Se ha agregado una clase [ProtectedBuffer](https://msdn.microsoft.com/library/mt631369.aspx) nueva a la API de Android.
-   Actualizaciones para mejorar la mensajería de error y la experiencia de solución de problemas.
-   Mejoras de rendimiento significativas para las operaciones criptográficas.

### <a name="july-2015-update---adds-support-for-linux--c-development"></a>Actualización de julio de 2015: se agrega compatibilidad para Linux / desarrollo de C++

Esta versión agrega las siguientes actualizaciones:

-   RMS SDK 4.1 para las plataformas Linux

    Para más información, consulte [Introducción](get-started.md).

### <a name="may-2015-update---adds-logging-control"></a>Actualización de mayo de 2015: se agrega control de registro

En esta versión se agrega compatibilidad para las siguientes actualizaciones:

-   iOS

    El cifrado y descifrado de aplicaciones funcionan independientemente y en paralelo.

    Para más información, consulte [MSProtector](https://msdn.microsoft.com/library/mt210993.aspx).

    Configuración del control de nivel de registro habilitada.

    Para más información, consulte [Procedimiento para habilitar el registro de rendimiento y errores](enabling-logging.md)

    Se agregó compatibilidad para el borrado de memoria caché.

    Para más información, consulte [MSProtection:resetStateWithCompletionBlock](https://msdn.microsoft.com/library/mt210991.aspx).

### <a name="february-2015-update---adds-windows-store-application-support"></a>Actualización de febrero de 2015: se agrega compatibilidad para las aplicaciones de la Tienda Windows

En esta versión se agrega compatibilidad para las aplicaciones de la Tienda Windows y se proporciona paridad funcional con las versiones para Windows Phone, Android e iOS/OS X de RMS SDK 4.1.

### <a name="january-2015-update---adds-winphone-platform-support"></a>Actualización de enero de 2015: se agrega compatibilidad para la plataforma WinPhone

En esta versión se agrega compatibilidad para las aplicaciones del sistema operativo de Windows Phone y se proporciona paridad funcional con las versiones para Android e iOS/OS X de RMS SDK 4.1.

### <a name="october-2014-update---upgrade-to-microsoft-rms-sdk-41"></a>Actualización de octubre de 2014: se actualiza Microsoft RMS SDK 4.1

La versión 4.1 de RMS SDK agrega las siguientes características nuevas a Google Android y Apple iOS / OS X.

-   Extensiones para la API de SDK para Android e iOS/OS X para el procesamiento del *consentimiento del usuario*, lo cual permite al usuario confirmar los comportamientos del SDK. Actualmente, el seguimiento de documentos y el acceso a direcciones URL de servicio de AD RMS desconocidas son los tipos de consentimiento admitidos.

    Para más información, consulte a modo de ejemplo la versión de API de Android de la [interfaz ConsentCallback](https://msdn.microsoft.com/library/dn833503.aspx).

-   Ahora se admiten iOS 8 y OS X 10.10 (Yosemite). También se han realizado algunos cambios de nombre de propiedad necesarios para Xcode 6.

    Por ejemplo MSUserPolicy.name ha cambiado a [MSUserPolicy.policyName](https://msdn.microsoft.com/library/dn790799.aspx).

## <a name="release-notes"></a>Notas de la versión

En esta sección se destaca la información sobre la versión actual y las anteriores de las API de Microsoft Rights Management SDK 4.x que, como desarrollador, debe tener en cuenta.

**AD RMS SDK 4.1:versión de disponibilidad global para las plataformas iOS / OS X y Android**

-   **Compatibilidad con AD RMS**: los administradores de TI pueden usar las aplicaciones habilitadas para RMS en dispositivos móviles con las nuevas extensiones para dispositivos móviles del servidor de AD RMS.
-   **Consumo sin conexión**: los usuarios finales pueden acceder a datos protegidos mediante RMS sin conexión.
-   **Autenticación segregada**: los desarrolladores pueden usar su propia biblioteca de autenticación para Azure RMS y AD RMS (o usar la [Biblioteca de autenticación de Azure AD [ADAL]](https://MSDN.Microsoft.Com/library/jj573266.aspx) recomendada).
-   **Interfaz de usuario segregada**: los desarrolladores pueden compilar la interfaz de usuario para proteger y consumir documentos protegidos con RMS.
-   **API rediseñada**: los desarrolladores ahora pueden disfrutar de una API de cifrado y descifrado sencilla y transparente, que proporciona una experiencia de usuario y comportamientos de RMS coherentes, con el mínimo esfuerzo.

**Se aplica a todas las plataformas**

-   Las API de RMS SDK 4.x no son *seguras para subprocesos*.

**Android**

-   Al usar una aplicación de ejemplo en un dispositivo Kindle de Amazon® para ver datos adjuntos .ptxt, primero debe descargar el archivo para poder verlo.

    **Solución**: problema conocido que se abordará más adelante.

-   Una aplicación que usa el SDK se puede bloquear si se permiten varias instancias.

    **Solución**: asegúrese de que la aplicación no admite llamadas de varias instancias a la API de Android.

-   Cuando uso el método [ProtectedFileOutputStream](https://msdn.microsoft.com/library/dn790855.aspx).write (byte\[\] array, int offset, int length) con una longitud distinta del valor *array.length*, no puedo consumir el contenido con el SDK después.

    **Solución**: este es un problema conocido. Para mitigarlo, pase siempre una matriz *byte \[\]* con el mismo valor de longitud que el parámetro de longitud o use el método [ProtectedFileOutputStream](https://msdn.microsoft.com/library/dn790855.aspx).write(byte\[\] array).

**iOS y OS X**

-   Hay dos dialectos del portugués que admiten nuestros SDK de iOS y OS X. Por desgracia, debido a un error, actualmente no admitimos la primera localización por completo. Debido a este error, el portugués no es totalmente compatible. La mayor parte del texto está traducida, pero la interfaz de usuario, no.

    1. Portugués

    2. Portugués (Portugal)

**Solo iOS**

-   RMS SDK 4.x no muestra el indicador de actividad de red.

    Se trata de un comportamiento opcional conocido de iOS según las directrices de interfaz humana de Apple.

**Solo OS X**

-   RMS SDK 4.x no muestra el indicador de actividad de red.

    Se trata de un comportamiento opcional conocido de OS X según las directrices de interfaz humana de Apple.

-   **Solución**: crear una aplicación de interfaz de múltiples documentos (MDI) con nuestro SDK de OS X mediante la siguiente orientación.

    Los métodos siguientes no se deben ejecutar al mismo tiempo. Con el fin de supervisar la finalización de la ejecución, utilice el método de bloqueo de finalización como se ha indicado.

    - [MSProtectedData.protectedDataWithProtectedFile](https://msdn.microsoft.com/library/dn758351.aspx)
    - [MSCustomProtectedData.customProtectedDataWithPolicy](https://msdn.microsoft.com/library/dn758315.aspx)



**Nota**: Las aplicaciones de MDI no son compatibles con nuestra API de iOS.

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

**Todas las plataformas**

**P**: No veo una interfaz de usuario de selección de **permisos personalizados** en el flujo de trabajo de protección. ¿Por qué?

**R**: Es un problema conocido, que se abordará más adelante.

**P**: ¿Cómo puedo obtener nuevos inquilinos organizativos para probar el SDK y las aplicaciones de ejemplo?

**R**: Para solicitar credenciales para las organizaciones de prueba de Azure AD RMS, envíe un mensaje de correo electrónico a <rmcstbeta@microsoft.com>.

**P**: No veo ninguna explicación de la jerarquía de prueba en la documentación. ¿Por qué?

**R**: No hay ningún concepto de jerarquía de prueba con los nuevos AD RMS SDK. Siempre se trabaja con la jerarquía de producción.

**P**: En la versión 2.1 de RMS SDK, se necesitaba un manifiesto generado para cada aplicación que implementara protección de información. ¿Sigue siendo el caso para la versión 4.0 y posteriores del SDK?

**R**: No, los manifiestos ya no son necesarios para la versión 3.0 y las posteriores de Rights Management SDK.

**Android**

**P**: ¿Con qué entornos de desarrollo se ha probado el SDK?

**A**: Eclipse Juno con Google API 15 y versiones posteriores.

**P**: ¿Se puede llamar a un método de cancelación cancel() desde el subproceso de la interfaz de usuario?
**R**: Se debe llamar al método cancel() desde un subproceso ajeno a la interfaz de usuario, ya que puede anular una conexión de red.

**iOS**

**P**: ¿Qué plataformas se han verificado para el desarrollo de SDK?

**R**: Xcode 5.0 con iOS 7 y versiones posteriores.

**P**: He llamado a un método cancel() en una operación, pero sigue apareciendo una notificación de que la operación ha finalizado. ¿Por qué?

**R**: No todas las operaciones se pueden cancelar, por lo que las operaciones de cancelación se ejecutan lo mejor posible.

**OS X**

**P**: El marco de la aplicación de ejemplo está adaptado a Xcode 5, ¿puedo trabajar con Xcode 4.6?

**R**: El SDK de OS X funciona con Xcode 4.6 y las versiones posteriores únicamente, así como con OS X 10.8 y las versiones posteriores.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
