---
# required metadata

title: Obtener una licencia de producción | Azure RMS
description: Para distribuir una aplicación desarrollada con RMS SDK 2.1, se pide un contrato de licencia de producción.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 6749817E-FF34-4384-BF63-39AEA5C372CA
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
# Obtaining a production license (Obtención de una licencia de producción)

Para poder distribuir una aplicación desarrollada con Rights Management Services SDK 2.1, debe pedir un contrato de licencia de producción que le permita obtener un certificado de producción.

> [!IMPORTANT]
> Si va a ejecutar la aplicación cliente con RMS basado en Azure, deberá pedir un inquilino de Azure RMS. Envíe un correo electrónico a <rmcstbeta@microsoft.com> con su solicitud de inquilino.

Para más información sobre la ejecución con Azure RMS, vea [Enable your service application to work with cloud based RMS](how-to-use-file-api-with-aadrm-cloud.md) (Habilitar la aplicación de servicio para que funcione con RMS basado en la nube).


Los certificados de producción y preproducción realizan una función similar, pero están diseñados para usarlos en entornos diferentes. Ambos contienen una cadena de certificados con un certificado de entidad de certificación (CA) de Microsoft en la raíz de confianza. Pero el certificado de preproducción solo se usa al desarrollar una aplicación de RMS. El certificado de producción se usa en entornos posteriores a la distribución. El certificado de producción y la clave privada asociada se usan para crear y firmar un manifiesto que identifica los archivos que pueden o deben cargarse en el espacio de procesos de la aplicación y aquellos que no deben cargarse.

Para más información sobre claves, vea [Probar aplicaciones con derechos habilitados](running-your-first-application.md).

Para obtener el certificado, solicite un contrato de licencia de producción.

## Solicitar un contrato de licencia de producción

-   Envíe un mensaje de correo a [RMLA@microsoft.com](mailto:rmla@microsoft.com) e incluya la siguiente información:

    -   Nombre completo de la empresa

    -   Dirección física de la empresa (incluya población, estado, país o región y código postal)
    -   Dirección de correo de la empresa (incluya población, estado, país o región y código postal)
    -   Números de teléfono y fax de la empresa
    -   Dirección URL de la empresa
    -   País o región de constitución
    -   Nombre de la aplicación o del producto
    -   Nombre y apellidos del solicitante
    -   Puesto o posición del solicitante
    -   Dirección de correo electrónico del solicitante

    Aunque no es estrictamente necesario disponer de una cuenta de correo electrónico, las comunicaciones del proceso de solicitud normalmente se realizan por correo electrónico. En Microsoft Outlook.com puede obtener una cuenta de correo electrónico gratuita. Si no tiene una cuenta ni quiere tenerla, puede enviar una solicitud escrita mecanografiada a la siguiente dirección:

    `Active Directory Rights Management License Agreements (ADRMLA)`

    `Microsoft Corporation`

    `One Microsoft Way`

    `Redmond, WA 98052-6399`

    Cuando solicite un contrato, haga lo siguiente:

    -   Envíe la información, en inglés, tal y como debería aparecer en el contrato.
    -   Envíe toda la información solicitada. El procesamiento de la solicitud puede retrasarse si falta información o está incompleta.

    El equipo de Active Directory Rights Management Licensing Agreement (ADRMLA) responderá a la solicitud remitida por correo electrónico en un plazo de tres días hábiles; el plazo es más amplio si se envía la solicitud por servicio postal. La respuesta incluirá el formulario del contrato de licencia e instrucciones adicionales. Lea, firme y devuelva todas las páginas del contrato al equipo de ADRMLA. No cambie las fuentes ni el formato de los párrafos del contrato de licencia.

    Asegúrese de seguir las instrucciones que reciba del equipo de ADRMLA. Las instrucciones enumeran los elementos de información digital necesarios para tramitar la solicitud de certificado. Siga las instrucciones paso a paso para evitar retrasos.

    El equipo de ADRMLA le remitirá el certificado de producción una vez creado. El certificado se crea a partir del contrato de licencia y de la información digital (incluida una clave pública) que facilite. Tenga en cuenta que el equipo de ADRMLA puede tardar hasta 15 días hábiles en remitirle el certificado por correo electrónico. Este plazo se extiende si la comunicación se realiza por servicio postal.

## Temas relacionados

* [Procedimiento](how-to-use-msipc.md)
* [Prueba de la aplicación con derechos habilitados](running-your-first-application.md)
 

 





<!--HONumber=Jun16_HO1-->


