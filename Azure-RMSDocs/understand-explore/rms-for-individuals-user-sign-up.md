---
title: Registro de usuarios en RMS para individuos - AIP
description: "Suscríbase para recibir las instrucciones de esta cuenta gratuita e información técnica sobre cómo funciona este proceso."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/24/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a60731bd-f78d-4f00-bb3e-354637b312ab
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d1c45c2b97fb3f278a8ecd3ebe9fe37af3ea5d0f
ms.sourcegitcommit: 0fa5dd38c9d66ee2ecb47dfdc9f2add12731485e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2017
---
# <a name="how-users-sign-up-for-rms-for-individuals"></a>Cómo se registran los usuarios a RMS para individuos

>*Se aplica a: Azure Information Protection*

Para registrarse en esta cuenta gratuita, debe solicitarla en la [página de Microsoft Azure Information Protection](https://aka.ms/rms-signup) y proporcionar su dirección de correo electrónico profesional. La forma más habitual de redirigirle a esta página de suscripción es mediante un mensaje de correo electrónico con un archivo adjunto protegido. El mensaje de correo electrónico contiene instrucciones para registrarse. 

Si sigue estas instrucciones, recibirá una respuesta de Microsoft por correo electrónico, tras lo cual podrá completar el proceso de suscripción introduciendo los detalles para crear la cuenta. Una vez hecho esto, en la página final se mostrarán vínculos para descargar el cliente o visor de Azure Information Protection para distintos dispositivos, un vínculo a la guía del usuario y un vínculo para obtener una lista actualizada de las aplicaciones que admiten de forma nativa la protección de Rights Management. 

## <a name="to-sign-up-for-rms-for-individuals"></a>Para registrarse en RMS como usuarios

1.  Si usa un equipo Windows o Mac, o un dispositivo móvil, vaya a la [página de Microsoft Azure Information Protection](https://aka.ms/rms-signup).

2.  Escriba la dirección de correo electrónico que usa para la organización, **janetm@contoso.com** o **p.dover@fabrikam.com**.

    > [!IMPORTANT]
    > No se admiten cuentas de correo electrónico personales, de modo que no se puede introducir una cuenta Microsoft (conocida anteriormente como Microsoft Live ID) u otra cuenta personal que pueda usar en casa perteneciente a tu proveedor de Internet.

3. Haz clic en **Iniciar sesión**.

    Microsoft usa su dirección de correo electrónico para comprobar si su organización ya tiene una [suscripción a Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) o una [suscripción a Office 365 que incluya protección de datos mediante Azure Rights Management](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf). Si se encuentra alguna de estas suscripciones, no necesitará RMS para usuarios. Se iniciará sesión de inmediato y se cancelará el registro de autoservicio de RMS para usuarios. Si no se encuentra una de estas suscripciones, continuará con el paso siguiente.

4. Espere un mensaje de correo electrónico de confirmación, que se enviará a la dirección que haya suministrado. Lo enviará el equipo de Office 365 (support@email.microsoftonline.com), con el asunto **Finalizar la suscripción a Microsoft Azure Information Protection**.

5. Cuando reciba el correo electrónico, haga clic en **Sí, soy yo** para comprobar su dirección de correo electrónico y completar el proceso de suscripción.

6. Ahora verá una página **Una última cosa...** para proporcionar detalles de su cuenta. Escriba su nombre y su apellido, escriba y confirme una contraseña de su elección, y después haga clic en **Iniciar**.

7. Cuando se cree la cuenta, verá una nueva página de Microsoft Azure Information Protection donde podrá descargar e instalar el cliente de Azure Information Protection o hacer clic en el vínculo de la [guía del usuario](../rms-client/client-user-guide.md) para obtener instrucciones de procedimientos para equipos con Windows.

Una vez se ha creado la cuenta, ya puede empezar el proceso de protección de archivos y de lectura de archivos protegidos por otros usuarios. Si se le pide que inicie sesión para proteger o leer archivos protegidos, escriba la misma dirección de correo electrónico y la contraseña que ha usado para crear la cuenta para RMS para usuarios.

## <a name="technical-overview-of-the-sign-up-process"></a>Información técnica del proceso de registro
RMS para usuarios utiliza un proceso de suscripción de autoservicio empleado también por otros servicios que usan la tecnología basada en la nube de Microsoft para autenticar a los usuarios.

Esto es lo que sucede en segundo plano cuando un usuario se suscribe a RMS para usuarios y su organización no tiene una suscripción a Office 365 o a Azure y, por lo tanto, tampoco tiene ningún directorio de Azure para autenticar a los usuarios:

1. Cuando el primer usuario de una organización solicita un suscripción de RMS para usuarios, el nombre de dominio que proporcione en su dirección de correo electrónico se comprobará para consultar si ya está asociado con un inquilino de Azure. Si no hay ningún inquilino, se crea automáticamente un nuevo inquilino y un directorio de Azure para la organización, que contiene una cuenta para este primer usuario. A diferencia de lo que sucede con una suscripción de pago o prueba de Azure, esta primera cuenta no es un administrador global, sino un usuario estándar. La nueva cuenta utiliza la dirección de correo electrónico y la contraseña que el usuario proporcionó.

    > [!NOTE]
    > Algunos nombres de dominio no se pueden utilizar para crear el directorio y, por tanto, no se pueden usar en RMS para individuos.

    Si se encuentra un inquilino, se comprobará si ya tiene una suscripción para Azure Information Protection. Si no se encuentra ninguna suscripción, puede agregarse la suscripción a RMS para usuarios gratuita.

2. A la organización se le concede una suscripción a RMS para individuos. Ahora, Azure podrá autenticar a este usuario, por lo que ya puede proteger archivos y leer lo que otros usuarios han protegido mediante el servicio Azure Rights Management. Para proteger archivos y leer los que están protegidos, el usuario debe tener una aplicación habilitada para RMS, como las aplicaciones de Office o el [cliente de Azure Information Protection](../rms-client/aip-client.md) gratuito.

3. Cuando un segundo usuario de la misma organización solicita una suscripción a RMS para usuarios, se agregará una nueva cuenta de usuario al directorio de Azure creado anteriormente, mediante la suscripción a RMS para usuarios de la organización. Este segundo usuario podrá hacer todo lo que puede hacer el primer usuario (proteger archivos y leer archivos protegidos). Además, estos dos usuarios podrán colaborar desde este momento con más facilidad y seguridad, ya que podrán aplicar plantillas predeterminadas de forma muy rápida a archivos que limitan el acceso a cuentas del directorio de Azure de su organización.

4. Los usuarios posteriores de la misma organización seguirán el mismo patrón, es decir, agregarán cuentas de usuario al directorio de Azure de la organización al registrarse. Cuantas más cuentas se agreguen al directorio, más usuarios podrán colaborar de forma segura con compañeros de trabajo y socios, y les resultará más sencillo evitar que personas no autorizadas lean archivos a los que no deberían tener acceso.

A lo largo de este proceso, no hay cargos adicionales para la organización y no es preciso que se efectúe ningún tipo de trabajo por parte del departamento de TI. Sin embargo, el departamento de TI podría optar por hacer alguna de las acciones siguientes:

- **Administración de las cuentas y proceso de registro**: los administradores de TI pueden asumir la titularidad de las cuentas y el directorio creados automáticamente en Azure. Pueden administrar las cuentas mediante la implementación de soluciones de integración del directorio, como sincronización de contraseña e inicio de sesión único. O bien, pueden impedir que los usuarios creen cuentas o se suscriban a RMS para usuarios.
    
    Para más información, consulte [Cómo pueden los administradores controlar las cuentas creadas para RMS para individuos](rms-for-individuals-take-control.md).

- **Administrar Rights Management**: Los administradores de TI pueden convertir la suscripción a RMS para usuarios de la organización a una suscripción de pago que incluya Azure Rights Management. Cuando lleven a cabo esta conversión, el directorio y las cuentas existentes de Azure no podrán ser objeto de una transición sencilla para usuarios existentes que estén usando RMS para usuarios. Cualquier archivo que los usuarios hayan protegido con anterioridad permanecerá protegido con las mismas directivas y las personas a las que les garantizaron permisos para usar los archivos todavía podrán usar los archivos del mismo modo.
    
    Cuando emprenda este proceso, su organización se beneficiará de poder integrar Rights Management en sus flujos de trabajo, servicios y almacenes de datos. Además, podrá administrar Rights Management porque tendrá el control sobre la clave de inquilino de su organización para Azure Rights Management. Ahora puede realizar las acciones siguientes:
    
    - Configure Exchange y SharePoint para admitir Azure Rights Management, aunque estos servicios se estén ejecutando de forma local. Exchange y SharePoint son servicios en línea compatibles de forma nativa y son admitidos por un conector para los servidores locales. Para obtener más información, vea:
    
        - Las secciones Exchange Online y SharePoint Online desde [Office 365: configuración para clientes y servicios en línea](../deploy-use/configure-office365.md)
        
        - [Implementación del conector de Azure Rights Management](../deploy-use/deploy-rms-connector.md)
        
    - Realice tareas de e-discovery en los datos pertenecientes a una compañía, de modo que los usuarios y los servicios autorizados puedan, si es necesario, descifrar archivos que estuviesen protegidos. Para obtener más información, consulte [Configuring super users for Azure Rights Management and discovery services or data recovery](../deploy-use/configure-super-users.md) (Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos).
    
    - Registre la actividad en el servicio Rights Management. El registro es muy completo, ya que no solo puede supervisar qué archivos están protegidos y quién está accediendo a esos archivos protegidos, sino que también puede identificar comportamientos sospechosos potenciales procedentes de personas no autorizadas, que estén intentando acceder a los archivos protegidos. Para obtener más información, consulte [Registro y análisis del uso del servicio Azure Rights Management](../deploy-use/log-analyze-usage.md).
    
    - Proporcione a los usuarios la capacidad de realizar un seguimiento de sus documentos protegidos y revocarlos, si estas características son compatibles con su suscripción. Para más información, consulte [Realizar el seguimiento y revocar los documentos](../rms-client/client-track-revoke.md) en la [Guía del usuario de Azure Information Protection](../rms-client/client-user-guide.md).
    
    - Implemente una solución Bring Your Own Key (BYOK), de modo que se cree la clave de su inquilino para Azure Information Protection y pueda administrarla. Para más información, vea [Planeamiento e implementación de su clave de inquilino de Azure Information Protection](../plan-design/plan-implement-tenant-key.md).


## <a name="next-steps"></a>Pasos siguientes
Consulte [Cómo pueden los administradores controlar las cuentas creadas para RMS para usuarios](rms-for-individuals-take-control.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]