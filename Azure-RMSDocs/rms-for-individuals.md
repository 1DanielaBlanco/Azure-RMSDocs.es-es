---
title: RMS para individuos y Azure Information Protection
description: Información sobre RMS para individuos, una suscripción gratuita de autoservicio para los usuarios que hayan enviado archivos protegidos, pero que no pueden autenticarse porque su departamento de TI no administra una cuenta para ellos en Azure.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/02/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 2efcb440-fefd-45e9-872b-f471573aadf2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 947461f31c6c9d8ef8a97d07c78370153169af03
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56252447"
---
# <a name="rms-for-individuals-and-azure-information-protection"></a>RMS para individuos y Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

RMS para usuarios es una suscripción gratuita de autoservicio para los usuarios que necesitan abrir archivos que ha protegido Azure Information Protection. Si estos usuarios no se pueden autenticar con Azure Active Directory, este servicio de suscripción gratuita puede crear una cuenta en Azure Active Directory para un usuario. El resultado es que estos usuarios podrán autenticarse con su dirección de correo de empresa y abrir los archivos protegidos en sus equipos o dispositivos móviles.

RMS para usuarios utiliza la suscripción de autoservicio de Azure Active Directory. Si los usuarios han creado cuentas para su organización mediante esta suscripción, como administrador para su organización, puede reclamar la propiedad y [tomar el control de sus cuentas](/azure/active-directory/users-groups-roles/domains-admin-takeover#external-admin-takeover). 


> [!NOTE]
> Esta suscripción gratuita constituye una opción para ayudar a garantizar que las personas autorizadas ajenas a la organización siempre puedan leer archivos protegidos por la organización. Otra opción sería enviar por correo electrónico los documentos siguiendo los pasos de [Cifrado de mensajes de Office 365 con nuevas capacidades](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e). Esta solución de correo electrónico funciona con todas las direcciones de correo en todos los dispositivos, y es la manera recomendada de compartir de forma segura información y ver documentos de Office en un explorador con personas ajenas a la organización.
> 
> Otra opción es usar cuentas Microsoft. Sin embargo, no todas las aplicaciones pueden abrir contenido protegido cuando se usa una cuenta Microsoft para la autenticación. [Más información](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents) 

Para registrarse en esta cuenta gratuita, los usuarios van a la [página de Microsoft Azure Information Protection](https://aka.ms/rms-signup) y proporcionan su dirección de correo electrónico del trabajo. Recibirán un correo electrónico de respuesta de Microsoft. Después de eso podrán completar el proceso de suscripción especificando los detalles para crear la cuenta. 

Cuando se crea la cuenta, en la página final se mostrarán vínculos para descargar el cliente o visor de Azure Information Protection para distintos dispositivos, un vínculo a la guía del usuario y un vínculo para obtener una lista actualizada de las aplicaciones que admiten de forma nativa la protección de Rights Management. 

## <a name="to-sign-up-for-rms-for-individuals"></a>Para registrarse en RMS como usuarios

1. Si usa un equipo Windows o Mac, o un dispositivo móvil, vaya a la [página de Microsoft Azure Information Protection](https://aka.ms/rms-signup).

2. Escriba la dirección de correo electrónico que se ha utilizado para proteger el documento que se debe abrir.

3. Haz clic en **Iniciar sesión**.

    Microsoft usa su dirección de correo electrónico para comprobar si su organización ya tiene una [suscripción a Azure Information Protection Premium](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) o una [suscripción a Office 365 que incluya protección de datos mediante Azure Information Protection](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf). Si se encuentra alguna de estas suscripciones, no necesitará RMS para usuarios. Se iniciará sesión de inmediato y se cancelará el registro de autoservicio de RMS para usuarios. Si no se encuentra una de estas suscripciones, continuará con el paso siguiente.

4. Espere un mensaje de correo electrónico de confirmación, que se enviará a la dirección que haya suministrado. Lo enviará el equipo de Office 365 (support@email.microsoftonline.com), con el asunto **Finalizar la suscripción a Microsoft Azure Information Protection**.

5. Cuando reciba el correo electrónico, haga clic en **Sí, soy yo** para comprobar su dirección de correo electrónico y completar el proceso de suscripción.

6. Ahora verá una página **Una última cosa...** para proporcionar detalles de su cuenta. Escriba su nombre y su apellido, escriba y confirme una contraseña de su elección, y después haga clic en **Iniciar**.

7. Cuando se cree la cuenta, verá una nueva página de Microsoft Azure Information Protection donde podrá descargar e instalar el cliente de Azure Information Protection o hacer clic en el vínculo de la [guía del usuario](./rms-client/client-user-guide.md) para obtener instrucciones de procedimientos para equipos con Windows.

Ahora que ya está creada la cuenta, si se le pide que inicie sesión para proteger o leer archivos protegidos, escriba la misma dirección de correo electrónico y la contraseña que ha usado para crear la cuenta para RMS para usuarios.

> [!IMPORTANT]
> Aunque ahora también puede proteger archivos con esta cuenta, no lo haga hasta que su organización tenga una [suscripción de prueba o de pago](https://azure.microsoft.com/pricing/details/information-protection/) a Azure Information Protection. Si protege los archivos y correos electrónicos mediante esta suscripción gratis y su organización toma el control de su cuenta, es posible que el contenido protegido anteriormente sea inaccesible.


## <a name="next-steps"></a>Pasos siguientes
RMS para usuarios es un ejemplo del uso de una suscripción de autoservicio que es compatible con Azure Active Directory. Para más información sobre cómo funciona, consulte [¿Qué es la suscripción de autoservicio de Azure Active Directory?](/azure/active-directory/users-groups-roles/directory-self-service-signup) en la documentación de Azure Active Directory.

