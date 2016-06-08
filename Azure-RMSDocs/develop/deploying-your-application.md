---
# required metadata

title: Implementación de la aplicación | Azure RMS
description: En este tema se describen las opciones y el proceso de implementación de la aplicación con derechos habilitados
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4B785564-6839-49ED-A243-E2A6DFF88B2E
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** El contenido de este SDK no es actual. Durante un breve periodo podrá encontrar la [versión actual](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx) de la documentación en MSDN. **
# Deploying your application (Implementación de la aplicación)


En este tema se describen las opciones y el proceso de implementación de la aplicación con derechos habilitados.

> [!IMPORTANT]
> Este es un procedimiento recomendado para probar la aplicación de Rights Management Services SDK 2.1 primero en el entorno de preproducción de RMS, en un servidor RMS. Luego, si quiere que su cliente tenga la posibilidad de usar la aplicación con el servicio de Azure RMS, pase a las pruebas en ese entorno. Para obtener más información, consulte [Enable your service application to work with cloud based RMS](how-to-use-file-api-with-aadrm-cloud.md) (Habilitar la aplicación de servicio para que funcione con RMS basado en la nube).

 

## Opciones de instalación para Active Directory Rights Management Services Client 2.1

Una vez que haya creado el archivo de manifiesto con un certificado de producción, la aplicación estará lista para implementarse. Dado que ha usado RMS SDK 2.1, necesitará que el cliente de Active Directory Rights Management Services 2.1 se implemente en el equipo del usuario final.

### Cliente de AD RMS 2.1

El cliente de AD RMS 2.1. es un software diseñado para los equipos cliente con el fin de ayudar a proteger el flujo del acceso a la información y su uso a través de las aplicaciones que usan AD RMS, tanto si están instaladas en su infraestructura local como en un centro de datos de Microsoft.

El cliente de AD RMS 2.1 no es un componente del sistema operativo Windows. El cliente de AD RMS 2.1 se distribuye como una descarga opcional que, con la confirmación y la aceptación de su contrato de licencia, se puede distribuir libremente con el software de terceros para habilitar el contenido de acceso de cliente que está protegido por derechos mediante el uso y la implementación de servidores de AD RMS en su entorno.

> [!IMPORTANT] El cliente de AD RMS 2.1 es específico de la arquitectura y debe coincidir con la arquitectura del sistema operativo de destino.


## Opciones de instalación del cliente de AD RMS 2.1

-   **Redistribuir el cliente de AD RMS 2.1**

    Se recomienda que incluya el paquete de instalador del cliente de RMS con la aplicación o la solución mediante su tecnología de instalación preferida. El cliente RMS se puede redistribuir libremente e incluirse con otras aplicaciones y soluciones de TI.

    Puede instalar el cliente de AD RMS 2.1 de forma interactiva mediante el instalador del cliente de AD RMS 2.1 o bien instalarlo de forma silenciosa. Los pasos de integración son los siguientes:

    -   Descargar el instalador del cliente de RMS 2.1.
    -   Integrar el instalador del cliente de AD RMS 2.1 para que se ejecute con el instalador de la aplicación.

    Dos buenos ejemplos de la integración del cliente de AD RMS 2.1 con la aplicación son el paquete del instalador de RMS SDK 2.1 y el paquete del Explorador de carpetas protegidas con derechos. Pruebe a instalarlos para entender este enfoque.

-   **Hacer que el cliente de AD RMS 2.1 sea un requisito previo para la instalación de la aplicación**

    En este caso, creará un requisito previo para que se produzca un error en la instalación de la aplicación si el cliente de AD RMS 2.1 no está presente en el equipo del usuario final.

    Si el cliente no está presente, proporcione un mensaje de error que informe al usuario de dónde puede descargar una copia del cliente de AD RMS 2.1.

    Si el cliente está presente, continúe con la instalación de la aplicación.

## Habilitar Azure Rights Management Services con la aplicación

> [!NOTE]
> Si ha migrado al nuevo modelo de ADAL para la autenticación, no hace falta que instale SIA. Para obtener más información, vea la autenticación de ADAL de la aplicación habilitada para RMS.

- **Certificar la aplicación para Windows 10**: si actualiza la aplicación para que use la autenticación de ADAL en lugar del Ayudante para el inicio de sesión de Microsoft Online, usted y sus clientes podrán:
  - Usar Multi-Factor Authentication.
  - Instalar el cliente de RMS 2.1 sin necesidad de tener privilegios administrativos en el equipo.
 
  Para que el usuario final aproveche Azure Rights Management Services, debe implementar el *Ayudante para el inicio de sesión de Online Services*. Como desarrollador de la aplicación, no sabe si el usuario final usará RMS (de forma local) o Azure Rights Management Services (servicio en la nube).

> [!IMPORTANT]
> Para ejecutar la aplicación cliente de RMS SDK 2.1 con Azure RMS, debe solicitar un inquilino de Azure RMS. Envíe un correo electrónico a <rmcstbeta@microsoft.com> con su solicitud de inquilino.

-   Descargue el [Asistente para el inicio de sesión de Microsoft Online Services](http://www.microsoft.com/en-us/download/details.aspx?id=28177), que podrá conseguir en el Centro de descarga de Microsoft.
-   Asegúrese de que la implementación de una aplicación con derechos habilitados incluye una comprobación de los requisitos previos para la selección de este servicio.
-   Para realizar sus propias pruebas y para que los usuarios finales usen el servicio en línea, vea el tema de TechNet [Configuring Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx) (Configuración de Rights Management).

Para obtener más información sobre cómo habilitar la aplicación para que use RMS para Azure Rights Management Services, vea [Enable your application to work with cloud based RMS](how-to-use-file-api-with-aadrm-cloud.md) (Habilitar la aplicación para que funcione con RMS basado en la nube).

## Temas relacionados

* [How-to use (Procedimientos)](how-to-use-msipc.md)
* [Microsoft Online Services - Ayudante para el inicio de sesión](http://www.microsoft.com/en-us/download/details.aspx?id=28177)
* [Configuración de Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx)
* [Enable your application to work with cloud based RMS (Habilitar la aplicación para que funcione con RMS basado en la nube)](how-to-use-file-api-with-aadrm-cloud.md)
 

 





<!--HONumber=Jun16_HO1-->


