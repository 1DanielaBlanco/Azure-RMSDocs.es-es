---
title: "Implementación de la aplicación (AIP)"
description: "En este tema se describe la implementación de la aplicación y los pasos para realizar el proceso."
keywords: implementar, RMS, AIP
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 03/13/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4B785564-6839-49ED-A243-E2A6DFF88B2E
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.openlocfilehash: 300fb1d14bc4eda93b0e40ffbd9e6c2329c88517
ms.sourcegitcommit: e21fb3385de6f0e251167e5dc973e90f0e7f2bcf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2018
---
# <a name="deploy-into-production"></a>Implementación en producción

Este tema le guía por el proceso de implementación de la aplicación habilitada para Azure Information Protection (AIP)/Rights Management Services (RMS).

## <a name="request-an-information-protection-integration-agreement-ipia"></a>Solicitud de un contrato de Information Protection Integration (IPIA)
Para poder lanzar una aplicación desarrollada con AIP/RMS, es necesario solicitar y rellenar un contrato formal con Microsoft.

### <a name="begin-the-process"></a>Comenzar el proceso
Obtenga su IPIA mediante el envío de un correo electrónico a **IPIA@microsoft.com** con la siguiente información:

**Asunto:** Solicitud de IPIA para *nombre de la empresa*

En el cuerpo del correo electrónico, incluya:
- Nombre de la aplicación y del producto
- Nombre y apellidos del solicitante
- Dirección de correo electrónico del solicitante

### <a name="next-steps"></a>Pasos siguientes
Tras la recepción de la solicitud de IPIA, le enviaremos un formulario (como un documento de Word).
Revise los términos y las condiciones del IPIA y devuelva el formulario a **IPIA@microsoft.com** con la siguiente información:
- Nombre legal de la empresa
- Estado o provincia (Estados Unidos y Canadá) o el país de incorporación
- Dirección URL de la empresa
- Dirección de correo electrónico de la persona de contacto
- Direcciones adicionales de la empresa (opcional)
- Nombre de la aplicación de empresa
- Descripción breve de la aplicación
- *Id. de inquilino de Azure*
- *Identificador de la aplicación*
- Contactos de la empresa, correo electrónico y teléfono para la correspondencia en caso de situaciones críticas

### <a name="completing-the-agreement"></a>Completar el contrato
Cuando recibamos su formulario, le enviaremos el vínculo IPIA final para firmarlo digitalmente. Después de que lo firme, lo firmará el representante de Microsoft adecuado, con lo que el contrato quedará completado.

### <a name="already-have-a-signed-ipia"></a>¿Ya tiene un IPIA firmado?
Si ya tiene un IPIA firmado y desea agregar un nuevo *identificador de aplicación* para una aplicación que va a lanzar, envíe un correo electrónico a **IPIA@microsoft.com** y proporciónenos la siguiente información:
- Nombre de la aplicación de empresa
- Descripción breve de la aplicación
- Identificador de inquilino de Azure (aunque sea el mismo que antes)
- Identificador de la aplicación
- Contactos de la empresa, correo electrónico y teléfono para la correspondencia en caso de situaciones críticas

Tras el envío del correo electrónico, espere hasta 72 horas para el acuse de recibo.

## <a name="deploying-to-the-client-environment"></a>Implementación en el entorno del cliente

Para implementar la aplicación, creada con las herramientas Azure Information Protection (AIP) y Rights Management Services (RMS), necesitará implementar el cliente de RMS 2.1 en la máquina del usuario final.

### <a name="rms-client-21"></a>Cliente de RMS 2.1
El cliente de RMS 2.1. está diseñado para proteger el acceso al flujo de información y su uso a través de las aplicaciones habilitadas para AIP y RMS, tanto si están instaladas en su infraestructura local como en un centro de datos de Microsoft.

El cliente de RMS 2.1 no es un componente del sistema operativo Windows. El cliente se suministra como una descarga opcional que se puede, con confirmación y la aceptación de su contrato de licencia, distribuir libremente con la aplicación.

> [!IMPORTANT]
> El cliente de RMS 2.1 es específico de la arquitectura y debe coincidir con la arquitectura del sistema operativo de destino.


## <a name="rms-client-21-installation-options"></a>Opciones de instalación del cliente de RMS 2.1

### <a name="creating-your-deployment-package"></a>Creación del paquete de implementación

Le recomendamos que agrupe el paquete de instalador del cliente de RMS con la aplicación o la solución mediante su tecnología de instalación preferida. El cliente de RMS se puede redistribuir libremente con otras aplicaciones y soluciones.

Puede instalar el cliente de RMS 2.1 de forma interactiva mediante el instalador del cliente de RMS 2.1 o bien instalarlo de forma silenciosa. Los pasos de integración son los siguientes:

-   Descargar el instalador del cliente de RMS 2.1
-   Integrar el instalador del cliente de RMS 2.1 para que se ejecute con el instalador de la aplicación

Un ejemplo de integración del cliente de RMS 2.1 con su aplicación es el paquete [Rights Protected Folder Explorer](https://technet.microsoft.com/library/rights-protected-folder-explorer(v=ws.10).aspx) (Explorador de carpetas protegidas por derechos). Pruebe a instalarlo para entender este enfoque.

### <a name="make-rms-client-21-a-pre-requisite-for-your-application-install"></a>Hacer que el cliente de RMS 2.1 sea un requisito previo para la instalación de la aplicación

En este caso, creará un requisito previo para que se produzca un error en la instalación de la aplicación si el cliente de RMS 2.1 no está presente en la máquina del usuario final.

Si el cliente no está presente, proporcione un mensaje de error que informe al usuario de dónde puede descargar una copia del cliente de RMS 2.1.

Si el cliente está presente, continúe con la instalación de la aplicación.

## <a name="enabling-azure-information-protection-services-with-your-application"></a>Habilitación de los servicios de Azure Information Protection con la aplicación

> [!NOTE]
> Si ha migrado al nuevo modelo de ADAL para la autenticación, no hace falta que instale **SIA**. Para más información, consulte [Autenticación de ADAL para la aplicación habilitada para RMS](adal-auth.md).
> También puede **certificar la aplicación para Windows 10**: si actualiza la aplicación para que use la autenticación ADAL en lugar del Ayudante para el inicio de sesión de Microsoft Online, usted y sus clientes podrán: Usar Multi-Factor Authentication. Instalar el cliente de RMS 2.1 sin necesidad de tener privilegios administrativos en la máquina.

Para que el usuario final aproveche los servicios de Information Protection, debe implementar *Microsoft Online Services - Ayudante para el inicio de sesión (SIA)*. Como desarrollador de la aplicación, no sabe si el usuario final usará Information Protection a través de RMS (de forma local) o a través de Azure Information Protection.


> [!IMPORTANT]
> Si va a ejecutar la aplicación cliente con RMS basado en Azure, deberá crear sus propios inquilinos. Para más información, consulte [Azure RMS requirements: Cloud subscriptions that support Azure RMS](../get-started/requirements-subscriptions.md) (Requisitos de Azure RMS: suscripciones de nube que admiten Azure RMS).
> Para más información sobre la ejecución con Azure RMS, consulte [Habilitación de la aplicación de servicio para que funcione con RMS basado en la nube](how-to-use-file-api-with-aadrm-cloud.md).

-   Descargue [Microsoft Online Services - Ayudante para el inicio de sesión](http://www.microsoft.com/download/details.aspx?id=28177) del Centro de descarga de Microsoft.
-   Asegúrese de que la implementación de una aplicación con derechos habilitados incluye una comprobación de los requisitos previos para la selección de este servicio.
-   Para realizar sus propias pruebas y para que los usuarios finales usen el servicio en línea, consulte el tema de TechNet [Configuring Rights Management](https://TechNet.Microsoft.Com/library/jj585002.aspx) (Configuración de Rights Management).

También necesitará utilizar esta guía para configurar su aplicación [Configuración de una aplicación de App Service para usar el inicio de sesión de Azure Active Directory](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication).

Para más información sobre cómo permitir que la aplicación use RMS para Azure Rights Management Services, consulte [Habilitación de la aplicación de servicio para que funcione con RMS basado en la nube](how-to-use-file-api-with-aadrm-cloud.md).

## <a name="related-topics"></a>Temas relacionados

* [Microsoft Online Services - Ayudante para el inicio de sesión](http://www.microsoft.com/download/details.aspx?id=28177)
* [Configuración de Rights Management](https://TechNet.Microsoft.Com/library/jj585002.aspx)
* [Habilitación de la aplicación de servicio para que funcione con RMS basado en la nube](how-to-use-file-api-with-aadrm-cloud.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
