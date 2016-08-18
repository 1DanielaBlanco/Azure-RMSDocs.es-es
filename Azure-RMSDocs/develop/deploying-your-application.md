---
title: "Implementación de la aplicación | Azure RMS"
description: "En este tema se describen las opciones y el proceso de implementación de la aplicación con derechos habilitados"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4B785564-6839-49ED-A243-E2A6DFF88B2E
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 982021a2e972023b04e6483348a7c27aa029e198
ms.openlocfilehash: 8308e2db84e13c6b8c85a1a3ae6c01fc0aabee75


---

# Implementación en el entorno de producción


En este tema se describen las opciones y el proceso de implementación de la aplicación con derechos habilitados.

## Solicitar un contrato de licencia de producción

 Para poder distribuir una aplicación desarrollada con Rights Management Services SDK 2.1, debe pedir un contrato de licencia de producción que le permita obtener un certificado de producción.

> [!IMPORTANT]
> Si va a ejecutar la aplicación cliente con RMS basado en Azure, deberá crear sus propios inquilinos. Para obtener más información, vea [Azure RMS requirements: Cloud subscriptions that support Azure RMS](../get-started/requirements-subscriptions.md) (Requisitos de Azure RMS: Suscripciones en la nube que son compatibles con Azure RMS).
> Para más información sobre la ejecución con Azure RMS, vea [Enable your service application to work with cloud based RMS](how-to-use-file-api-with-aadrm-cloud.md) (Habilitar la aplicación de servicio para que funcione con RMS basado en la nube).

Para obtener el certificado, solicite un contrato de licencia de producción.

Envíe un mensaje de correo a [RMLA@microsoft.com](mailto:rmla@microsoft.com) e incluya la siguiente información:

- Nombre completo de la empresa
- Dirección física de la empresa (incluya población, estado, país o región y código postal)
- Dirección de correo de la empresa (incluya población, estado, país o región y código postal)
- Números de teléfono y fax de la empresa
- Dirección URL de la empresa
- País o región de constitución
- Nombre de la aplicación o del producto
- Nombre y apellidos del solicitante
- Puesto o posición del solicitante
- Dirección de correo electrónico del solicitante

Aunque no es estrictamente necesario disponer de una cuenta de correo electrónico, las comunicaciones del proceso de solicitud normalmente se realizan por correo electrónico. En Microsoft Outlook.com puede obtener una cuenta de correo electrónico gratuita. Si no tiene una cuenta ni quiere tenerla, puede enviar una solicitud escrita mecanografiada a la siguiente dirección:

      Active Directory Rights Management License Agreements (ADRMLA)

      Microsoft Corporation

      One Microsoft Way

      Redmond, WA 98052-6399

Cuando solicite un contrato, haga lo siguiente:
- Envíe la información, en inglés, tal y como debería aparecer en el contrato.
- Envíe toda la información solicitada. El procesamiento de la solicitud puede retrasarse si falta información o está incompleta.

El equipo de Active Directory Rights Management Licensing Agreement (ADRMLA) responderá a la solicitud remitida por correo electrónico en un plazo de tres días hábiles; el plazo es más amplio si se envía la solicitud por servicio postal. La respuesta incluirá el formulario del contrato de licencia e instrucciones adicionales. Lea, firme y devuelva todas las páginas del contrato al equipo de ADRMLA. No cambie las fuentes ni el formato de los párrafos del contrato de licencia.

Asegúrese de seguir las instrucciones que reciba del equipo de ADRMLA. Las instrucciones enumeran los elementos de información digital necesarios para tramitar la solicitud de certificado. Siga las instrucciones paso a paso para evitar retrasos.

El equipo de ADRMLA le remitirá el certificado de producción una vez creado. Tenga en cuenta que el equipo de ADRMLA puede tardar hasta 15 días hábiles en remitirle el certificado por correo electrónico. Este plazo se extiende si la comunicación se realiza por servicio postal.


## Opciones y requisitos de instalación del cliente de Rights Management Services 2.1

Dado que ha usado RMS SDK 2.1, necesitará que el cliente de Active Directory Rights Management Services 2.1 se implemente en el equipo del usuario final.

### Cliente de RMS 2.1

El cliente de RMS 2.1. es un software diseñado para los equipos cliente con el fin de ayudar a proteger el acceso al flujo de información y su uso a través de las aplicaciones que usan RMS, tanto si están instaladas en su infraestructura local como en un centro de datos de Microsoft.

El cliente de RMS 2.1 no es un componente del sistema operativo Windows. El cliente de RMS 2.1 se distribuye como una descarga opcional que, con la confirmación y la aceptación de su contrato de licencia, se puede distribuir libremente con el software de terceros para habilitar el contenido de acceso de cliente que está protegido por derechos mediante el uso y la implementación de servidores de RMS en su entorno.


> [!IMPORTANT]
> El cliente de AD RMS 2.1 es específico de la arquitectura y debe coincidir con la arquitectura del sistema operativo de destino.


## Opciones de instalación del cliente de RMS 2.1

-   **Redistribución del cliente de RMS 2.1**

    Se recomienda que incluya el paquete de instalador del cliente de RMS con la aplicación o la solución mediante su tecnología de instalación preferida. El cliente RMS se puede redistribuir libremente e incluirse con otras aplicaciones y soluciones de TI.

    Puede instalar el cliente de RMS 2.1 de forma interactiva mediante el instalador del cliente de RMS 2.1 o bien instalarlo de forma silenciosa. Los pasos de integración son los siguientes:

    -   Descargar el instalador del cliente de RMS 2.1.
    -   Integrar el instalador del cliente de RMS 2.1 para que se ejecute con el instalador de la aplicación.

    Dos buenos ejemplos de la integración del cliente de RMS 2.1 con la aplicación son el paquete del instalador de RMS SDK 2.1 y el paquete del Explorador de carpetas protegidas con derechos. Pruebe a instalarlos para entender este enfoque.

-   **Hacer que el cliente de RMS 2.1 sea un requisito previo para la instalación de la aplicación**

    En este caso, creará un requisito previo para que se produzca un error en la instalación de la aplicación si el cliente de RMS 2.1 no está presente en el equipo del usuario final.

    Si el cliente no está presente, proporcione un mensaje de error que informe al usuario de dónde puede descargar una copia del cliente de RMS 2.1.

    Si el cliente está presente, continúe con la instalación de la aplicación.

## Habilitar Azure Rights Management Services con la aplicación

> [!NOTE]
> Si ha migrado al nuevo modelo de ADAL para la autenticación, no hace falta que instale SIA. Para obtener más información, vea [ADAL authentication for your RMS enabled application](adal-auth.md) (Autenticación de ADAL de la aplicación habilitada para RMS).
> También puede **certificar la aplicación para Windows 10**. Si actualiza la aplicación para que use la autenticación ADAL en lugar del Ayudante para el inicio de sesión de Microsoft Online, usted y sus clientes podrán: Usar Multi-Factor Authentication. Instalar el cliente de RMS 2.1 sin necesidad de tener privilegios administrativos en el equipo.


Para que el usuario final aproveche Azure Rights Management Services, debe implementar *Microsoft Online Services - Ayudante para el inicio de sesión (SIA)*. Como desarrollador de la aplicación, no sabe si el usuario final usará RMS (de forma local) o Azure Rights Management Services (servicio en la nube).


> [!IMPORTANT]
> Para ejecutar la aplicación cliente de RMS SDK 2.1 con Azure RMS, debe crear sus propios inquilinos. Para obtener más información, vea [Azure RMS requirements: Cloud subscriptions that support Azure RMS](../get-started/requirements-subscriptions.md) (Requisitos de Azure RMS: Suscripciones en la nube que son compatibles con Azure RMS).

-   Descargue el [Asistente para el inicio de sesión de Microsoft Online Services](http://www.microsoft.com/en-us/download/details.aspx?id=28177), que podrá conseguir en el Centro de descarga de Microsoft.
-   Asegúrese de que la implementación de una aplicación con derechos habilitados incluye una comprobación de los requisitos previos para la selección de este servicio.
-   Para realizar sus propias pruebas y para que los usuarios finales usen el servicio en línea, vea el tema de TechNet [Configuring Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx) (Configuración de Rights Management).

Para obtener más información sobre cómo habilitar la aplicación para que use RMS para Azure Rights Management Services, vea [Enable your application to work with cloud based RMS](how-to-use-file-api-with-aadrm-cloud.md) (Habilitar la aplicación para que funcione con RMS basado en la nube).

## Temas relacionados

* [Microsoft Online Services - Ayudante para el inicio de sesión](http://www.microsoft.com/en-us/download/details.aspx?id=28177)
* [Configuración de Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx)
* [Enable your application to work with cloud based RMS (Habilitar la aplicación para que funcione con RMS basado en la nube)](how-to-use-file-api-with-aadrm-cloud.md)
 

 



<!--HONumber=Jul16_HO1-->


