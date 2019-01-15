---
title: Notas de la versión
description: Actualizaciones del SDK por revisión y otra información para desarrolladores.
keywords: ''
author: bryanla
ms.author: bryanla
manager: mbaldwin
ms.date: 10/18/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: CE379738-4E1D-42AD-83F4-F89B70456EBB
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.openlocfilehash: 8132fd2afba45402f8f9c835f2d6db69dd8e81f2
ms.sourcegitcommit: bd2b31dd97c8ae08c28b0f5688517110a726e3a1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2019
ms.locfileid: "54071208"
---
# <a name="release-notes"></a>Notas de la versión

Este artículo contiene información importante sobre esta versión y versiones anteriores de RMS SDK 2.1.

## <a name="october-2017---update"></a>Actualización de octubre de 2017

- Adición de dos nuevas API para la inicialización y desinicialización del entorno. Para obtener información, consulte [IpcInitializeEnvironment](https://msdn.microsoft.com/library/hh535289.aspx) y [IpcUninitializeEnvironment](https://msdn.microsoft.com/library/hh535289.aspx).
- Ahora se admiten los tipos de archivo de Visio. Para más información, vea [File API configuration](file-api-configuration.md) (Configuración de API de archivo).

## <a name="february-2016---sdk-documentation-update"></a>Actualización de documentación del SDK de febrero de 2016

>[!Note]
> Las actualizaciones de la documentación de características de esta sección se aplican a la descarga del SDK con fecha de 11/12/2015.

- **Flujo de autenticación mejorado** gracias a la autenticación de OAuth2 basada en token mediante la [biblioteca de autenticación de Azure Active Directory (ADAL)](https://azure.microsoft.com/documentation/articles/active-directory-authentication-libraries/). Para obtener más información sobre este proceso y sus extensiones de API, consulte [ADAL authentication for your RMS enabled application](how-to-use-adal-authentication.md) (Autenticación de ADAL de la aplicación habilitada para RMS).

- **Actualización de ADAL**. Si actualiza la aplicación para que use la autenticación de ADAL en lugar del Ayudante para el inicio de sesión de Microsoft Online, usted y sus clientes podrán:

 - Usar Multi-Factor Authentication.
 - Instalar el cliente de RMS 2.1 sin necesidad de tener privilegios administrativos en el equipo.
 - Certificar la aplicación para Windows 10

- **Compatibilidad con el Ayudante para el inicio de sesión (SIA) de Microsoft Online mientras se quita RMS SDK.** Seguiremos admitiendo el uso del SIA durante seis meses, después de lo cual dejará de ser compatible.


## <a name="december-2015-update"></a>Actualización de diciembre de 2015

- Se han implementado mejoras de rendimiento en varias áreas como:
    - Publicar desde el servidor de licencias principal cuando se usan servidores de solo licencia.
    - Se producen errores en RMS SDK 2.1 mucho antes cuando no hay conexión de red.

- Actualizaciones para mejorar la experiencia de mensajería de errores y solución de problemas.
- Observe que también se ha actualizado la lista de [plataformas compatibles](supported-platforms.md).
- Se ha eliminado de RMS SDK 2.1 la necesidad del entorno de preproducción y el uso de un manifiesto de aplicación. Se han quitado estas secciones de este conjunto de documentación para desarrolladores y se ha simplificado y reorganizado la documentación en general.

## <a name="may-2015-update"></a>Actualización de mayo de 2015

-   **RMS basado en la nube y aplicaciones de servicio** - [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx) necesita tres datos: clave simétrica, **AppPrincipalId** y **TenantBposId**. Hemos actualizado este artículo para incluir instrucciones de procesamiento de esta información. Para consultar esta actualización, vea la versión revisada de [Habilitación de la aplicación de servicio para que funcione con RMS basado en la nube](how-to-use-file-api-with-aadrm-cloud.md).

## <a name="april-2015-update"></a>Actualización de abril de 2015

-   Ya es posible realizar el **seguimiento de documentos** gracias a un conjunto de nuevas API. Para más información, vea [Tracking Content](tracking-content.md) (Seguimiento de contenido).
-   **Tipo de cifrado**: ahora se admite control de nivel de API para la selección del paquete de cifrado. Para más información, vea [Working with encryption](working-with-encryption.md) (Uso de cifrado).

    **Nota:**  La marca **IPC\_LI\_DEPRECATED\_ENCRYPTION\_ALGORITHMS** dejará de exponerse en la API. Esto significa que las aplicaciones futuras ya no se compilarán si hacen referencia a esta marca, pero las ya desarrolladas seguirán funcionando dado que respetaremos la marca de forma privada en el código de la API. Todavía será posible beneficiarse de la antigua marca de algoritmos de cifrado: solo es necesario cambiar una marca. Para más información, vea [Working with encryption](working-with-encryption.md) (Uso de cifrado).

-   Las **aplicaciones en modo de servidor**, que usan [valores del modo de API](https://msdn.microsoft.com/library/hh535236.aspx) de **IPC\_API\_MODE\_SERVER**, ya no necesitan un manifiesto de aplicación. Podrá probar la aplicación en un servidor RMS de producción y no será necesario obtener una licencia de producción cuando pase al entorno de producción. Para más información sobre las aplicaciones de modo de servidor, vea [Application types](application-types.md) (Tipos de aplicación).
-   El **registro** ahora se implementa a través de archivo y de métodos de seguimiento de eventos para Windows.
-   Si está usando una **máquina con Windows 7 SP1 o Windows Server 2008 R2**, vea la nota que sigue a "Notas importantes para desarrolladores".

## <a name="january-2015-update"></a>Actualización de enero de 2015

-   **Aumento del tamaño de los archivos protegidos compatibles (pfile)**: ahora se admiten tamaños de archivo pfile superiores a un giga (1 GB). Para obtener más información sobre los archivos pfile, vea [Supported File Formats](supported-file-formats.md) (Formatos de archivo compatibles).
-   **Registro mejorado para un mejor diagnóstico**: los niveles de registro mostrarán **ERROR** o **WARNING** en los mensajes que deban revisarse. El resto de los mensajes, incluidas las excepciones que se siguen mostrando, se registrarán como **INFO**.

    Elegimos este enfoque para que no pierda ningún detalle. Ahora, solo los mensajes importantes se muestran con el nivel WARNING.

-   **Adquisición de plantillas de empresa**: correcciones importantes en el código de adquisición de plantillas, basadas en los informes y los comentarios de los clientes.
-   Coherencia mejorada para la localización

## <a name="october-2014-update"></a>Actualizaciones de octubre de 2014

-   Se han actualizado los comportamientos predeterminados del componente de API de archivo del SDK. Para más información, vea [File API configuration](file-api-configuration.md) (Configuración de API de archivo).
-   La nueva característica de notificaciones por correo electrónico se describe en el artículo de notas de desarrollador, [Habilitación de la notificación por correo electrónico](how-to-enable-email-notification.md).

## <a name="july-2014-update"></a>Actualización de julio de 2014

El componente de la API de archivo del SDK se ha ampliado y ofrece las siguientes características:

-   Identifican qué protector se va a usar.
-   Proporcionan protección por RMS y el nivel de granularidad de un archivo.

    Funciones agregadas en esta versión:

    **Nota:** Para las extensiones de API de archivo, se han agregado más tipos y estructuras de datos compatibles aparte de los aquí mencionados. Todos los artículos que se han actualizado para esta versión están marcados como **preliminar y sujeto a cambios**.

    -   [IpcfOpenFileOnHandle](https://msdn.microsoft.com/library/dn771751.aspx)
    -   [IpcfOpenFileOnILockBytes](https://msdn.microsoft.com/library/dn771752.aspx)
    -   [IpcfGetFileProperty](https://msdn.microsoft.com/library/dn771749.aspx)
    -   [IpcfLogicalFileRangeToRawFileRange](https://msdn.microsoft.com/library/dn771750.aspx)
    -   [IpcfReadFile](https://msdn.microsoft.com/library/dn771753.aspx)
    -   [IpcfSetEndOfFile](https://msdn.microsoft.com/library/dn771754.aspx)
    -   [IpcfWriteFile](https://msdn.microsoft.com/library/dn771756.aspx)

## <a name="april-2014-update"></a>Actualización de abril de 2014

-   El **uso de memoria de la API de archivo**, especialmente para archivos PFile grandes, se ha mejorado considerablemente.
-   El **identificador de contenido** se puede escribir ahora mediante la propiedad **IPC\_LI\_CONTENT\_ID**. Para obtener más información, vea [License property types](https://msdn.microsoft.com/library/hh535287.aspx) (Tipos de propiedades de licencias).
-   **Requisito de manifiesto de producción**: cuando la aplicación o el servicio habilitados para RMS se ejecutan en modo de servidor, ya no se pide ningún manifiesto. Para más información, vea [Application types](application-types.md) (Tipos de aplicación).
-   **Actualizaciones de la documentación**

    **Práctica recomendada de pruebas**: guía agregada para el uso de un servidor local antes de las pruebas con Azure RMS. Para más información, vea [Enable your service application to work with cloud based RMS](how-to-use-file-api-with-aadrm-cloud.md) (Habilitar la aplicación de servicio para que funcione con RMS basado en la nube).

## <a name="important-developer-notes"></a>Notas importantes para desarrolladores

-   **Compatibilidad nativa para todos los tipos de archivo**

    Puede agregarse compatibilidad nativa para cualquier tipo de archivo (extensión) con esta versión de Rights Management Services SDK 2.1. Por ejemplo, en el caso de cualquier extensión &lt;ext&gt; (que no es de Office ni pdf), se usará \*.p&lt;ext&gt; si la configuración de administración de esa extensión es "NATIVE".

    Para más información sobre los tipos de archivo compatibles, vea [File API configuration](file-api-configuration.md) (Configuración de la API de archivo).

-   **Las máquinas con Windows 7 SP1 y Windows Server 2008 R2 SP1** sin la actualización [KB2533623](https://support.microsoft.com/kb/2533623), pueden generar el siguiente error al proteger un archivo de Office: "El parámetro es incorrecto. Código de error 0x80070057". Si aparece este error, instale la actualización y vuelva a intentarlo. Si todavía ve errores, póngase en contacto con el alias RMS SDK Beta Feedback <rmcstbeta@microsoft.com>.

    **Nota**  A partir de la versión de abril de 2015, se agrega una comprobación al proceso de instalación de este KB.

     

-   **Integración de la API de archivo**

    La API de archivo de Active Directory Rights Management Services, con la adición de la API de archivo, ofrece las siguientes ventajas y capacidades.

      - Puede proteger los datos confidenciales de forma automática sin necesidad de conocer los detalles de la implementación de Information Rights Management (IRM) usados por los distintos formatos de archivo.

      - Los archivos de Microsoft Office, los archivos Portable Document Format (PDF) y otros tipos de archivo determinados pueden protegerse con la protección nativa. Para ver una lista completa de los tipos de archivo que pueden protegerse mediante protección nativa, vea [File API configuration](file-api-configuration.md) (Configuración de la API de archivo).

      - Todos los archivos, excepto los archivos del sistema y los archivos de Office, se pueden proteger con el formato de archivo protegido de RMS (PFile).

    La API de archivo se implementa a través de estas cuatro funciones nuevas: [IpcfDecryptFile](https://msdn.microsoft.com/library/dn133058.aspx), [IpcfEncryptFile](https://msdn.microsoft.com/library/dn133059.aspx), [IpcfGetSerializedLicenseFromFile](https://msdn.microsoft.com/library/dn133060.aspx) y [IpcfIsFileEncrypted](https://msdn.microsoft.com/library/dn133061.aspx).

    La API de archivo requiere que el cliente de Rights Management Services 2.1 esté instalado en el equipo cliente y que el equipo tenga conectividad con un servidor RMS. Para obtener más información sobre el servidor RMS, el cliente de RMS y su funcionalidad, consulte el contenido de TechNet sobre la [documentación para profesionales de TI para RMS](https://technet.microsoft.com/library/cc771234(v=ws.10).aspx).

-   **Problema**: al crear una licencia desde cero, se deben conceder explícitamente derechos de propiedad.

    **Solución**: la aplicación debe agregar explícitamente derechos **Owner** al propietario de la licencia cuando se crea una licencia desde cero con [IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx). Para más información, vea [Add explicit owner rights](add-explicit-owner-rights.md) (Incorporación de derechos de propiedad explícitos).

-   **Problema**: si una aplicación llama a [IpcProtectWindow](https://msdn.microsoft.com/library/hh535268.aspx) o [IpcUnprotectWindow](https://msdn.microsoft.com/library/hh535272.aspx) dos veces en la misma ventana y con el mismo identificador, RMS SDK 2.1 devolverá un error en **HRESULT**.

    **Solución**: si quiere instrucciones específicas sobre este problema, vea la sección Comentarios de [IpcProtectWindow](https://msdn.microsoft.com/library/hh535268.aspx) e [IpcUnprotectWindow](https://msdn.microsoft.com/library/hh535272.aspx).

-   **Problema**: al compilar para varias arquitecturas, debe usar esta guía.

    **Solución**: si quiere usar Ipcsecproc\*isv.dll con una arquitectura diferente (por ejemplo, si tiene instalado el SDK de 64 bits en un equipo de 64 bits, pero ahora quiere implementarlo en un equipo de 32 bits que necesita Ipcsecproc\*isv.dll), deberá instalar el SDK de 32 bits en un equipo distinto y copiar ahí los archivos Ipcsecproc\*isv.dll desde la carpeta "%PROGRAMFILES%\\Microsoft Information Protection And Control" (la ubicación predeterminada o la que eligió al instalar el SDK).

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

**P**: ¿Cuál es el comportamiento predeterminado del idioma con las funciones que toman un parámetro LCID?

**R**: Use 0 para la configuración regional predeterminada. En este caso, AD RMS Client 2.1 busca nombres y descripciones en la siguiente secuencia y recupera el primer resultado disponible:

    1 - User preferred LCID.
    2 - System locale LCID.
    3 - The first available language specified in the Rights Management Server (RMS) template.

Si no se puede recuperar ningún nombre ni ninguna descripción, se devuelve un error. Solo puede haber un nombre y una descripción para un LCID específico.
