---
title: "Cómo se registran los usuarios en RMS para individuos | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a60731bd-f78d-4f00-bb3e-354637b312ab
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: 19252180802c69d6e5d6bf22c71ff3bcba96fb36


---

# Cómo se registran los usuarios a RMS para individuos

*Se aplica a: Azure Rights Management*

Para registrarse en esta cuenta gratuita, los usuarios lo solicitan visitando la [página de Microsoft Rights Management](https://portal.aadrm.com/)y proporcionan su dirección de correo electrónico profesional o educativa. 

La forma más habitual de redirigir a los usuarios a esta página de suscripción es mediante un mensaje de correo electrónico con un archivo adjunto protegido, que contiene instrucciones sobre cómo suscribirse. Recibirán un correo electrónico de respuesta de Microsoft. Después de eso podrán completar el proceso de suscripción especificando los detalles para crear la cuenta. Cuando reciban una confirmación por correo electrónico de Microsoft, este mensaje de correo electrónico final les enviará a una página donde podrán descargar la aplicación de uso compartido para diferentes dispositivos y se incluirá un vínculo en la guía del usuario.

## Para registrarse en RMS como usuarios

1.  Con un equipo Windows o Mac, vaya a la [página de Microsoft Rights Management](https://portal.aadrm.com).

2.  Escriba la dirección de correo electrónico que usa para la empresa, como **janetm@contoso.com** o **p.dover@fabrikam.com**.

    > [!IMPORTANT]
    > No se admiten cuentas de correo electrónico personales, de modo que no se puede introducir una cuenta Microsoft (conocida anteriormente como Microsoft Live ID) u otra cuenta personal que pueda usar en casa perteneciente a tu proveedor de Internet.

3.  Haga clic en **Introducción**.

    Microsoft usa su dirección de correo electrónico para comprobar si su organización ya tiene una [suscripción de pago que incluya Azure RMS](../get-started/requirements-subscriptions.md). Si ese es el caso, no necesita RMS para usuarios, por lo que iniciará sesión inmediatamente y se cancelará la suscripción de autoservicio de RMS para usuarios. Si no se encuentra una suscripción de pago a Azure RMS, continuará con el paso siguiente.

4.  Espere un mensaje de correo electrónico de confirmación, que se enviará a la dirección que haya suministrado. Procederá de Microsoft (DoNotReply@microsoft.com) y en el asunto se leerá **Microsoft RMS**.

5.  Cuando reciba el correo electrónico, haga clic en el vínculo de las instrucciones para finalizar el proceso de registro.

6.  El vínculo le lleva a una página de **Microsoft Rights Management** nueva para que suministre los detalles de su cuenta. Escriba su nombre y su apellido, escriba y confirme una contraseña de su elección, seleccione su país en la lista desplegable (o el país más cercano si el suyo no aparece) y, a continuación, haga clic en **Crear**.

7.  Espere recibir otro mensaje de correo electrónico de Microsoft que confirmará que la cuenta ya está lista para usarse.

8.  Cuando reciba el correo electrónico, haga clic en el vínculo para iniciar sesión y lea las instrucciones para descargar e instalar la aplicación de uso compartido, o haga clic en el vínculo Ayuda para leer la guía de usuario de la aplicación de uso compartido.

Una vez se ha creado la cuenta, ya puede empezar el proceso de protección de archivos y de lectura de archivos protegidos por otros usuarios. Cuando se le pida que inicie sesión para proteger o leer archivos protegidos, escriba la dirección de correo electrónico y la contraseña que ha usado para crear la cuenta para RMS para usuarios.

## Información técnica del proceso de registro
RMS para usuarios usa un proceso de suscripción de autoservicio empleado también por otros servicios que usan la tecnología basada en la nube de Microsoft para autenticar a los usuarios.

Esto es lo que sucede en segundo plano cuando un usuario se suscribe a RMS para usuarios y su organización no tiene una suscripción a Office 365 o a Azure y, por lo tanto, tampoco tiene ningún directorio de Azure para autenticar a los usuarios:

1.  Cuando el primer usuario de una organización solicita un suscripción de RMS para usuarios, el nombre de dominio que proporcione en su dirección de correo electrónico se comprobará para consultar si ya está asociado con un inquilino de Azure. Si no hay ningún inquilino, se crea automáticamente un nuevo inquilino y un directorio de Azure para la organización, que contiene una cuenta para este primer usuario. A diferencia de lo que sucede con una suscripción de pago de Azure, esta primera cuenta no es un administrador global, sino un usuario estándar. La nueva cuenta utiliza la dirección de correo electrónico y la contraseña que el usuario proporcionó.

    > [!NOTE]
    > Algunos nombres de dominio no se pueden utilizar para crear el directorio y, por tanto, no se pueden usar en RMS para individuos. La lista de nombres de dominio bloqueados se puede ver en este archivo de Notación de objetos JavaScript: [http://portal.aadrm.com/content/blocked_domains.json](http://portal.aadrm.com/content/blocked_domains.json)

    Si se encuentra un inquilino, se comprueba si ya tiene una suscripción para Azure RMS. Si no se encuentra ninguna suscripción, puede agregarse la suscripción a RMS para usuarios gratuita.

2.  A la organización se le concede una suscripción a RMS para individuos. Ahora, este usuario puede ser autenticado por Azure, por lo que ya puede proteger archivos y leer los que otros usuarios protegiesen mediante Azure Rights Management. Para proteger archivos y leer los protegidos, el usuario debe tener una aplicación habilitada para RMS, como la [aplicación para uso compartido de Rights Management](../rms-client/sharing-app-windows.md) gratuita.

3.  Cuando un segundo usuario de la misma organización solicita una suscripción a RMS para usuarios, se agregará una nueva cuenta de usuario al directorio de Azure creado anteriormente, mediante la suscripción a RMS para usuarios de la organización. Este segundo usuario podrá hacer lo mismo que puede hacer el primer usuario (proteger archivos y leer los protegidos), pero, además, estos dos usuarios podrán colaborar desde este momento con más facilidad y seguridad, ya que podrán aplicar plantillas predeterminadas de forma muy rápida a archivos que limitan el acceso a cuentas del directorio de Azure de su organización.

4.  Los usuarios posteriores de la misma organización seguirán el mismo patrón, es decir, agregarán cuentas de usuario (cuando se suscriban nuevos usuarios) al directorio de Azure de la organización. Cuantas más cuentas se agreguen al directorio, más usuarios podrán colaborar de forma segura con compañeros de trabajo y socios, y les resultará más sencillo evitar que personas no autorizadas lean archivos a los que no deberían tener acceso.

A lo largo de este proceso, no hay cargos adicionales para la organización y no es preciso que se efectúe ningún tipo de trabajo por parte del departamento de TI. Sin embargo, el departamento de TI podría optar por hacer alguna de las siguientes acciones:

-   **Administración de las cuentas y proceso de registro**: los administradores de TI pueden asumir la titularidad de las cuentas y el directorio creados automáticamente en Azure. Pueden administrar las cuentas mediante la implementación de soluciones de integración del directorio, como sincronización de contraseña e inicio de sesión único. O bien, pueden impedir que los usuarios creen cuentas o se suscriban a RMS para usuarios.

    Para más información, consulte [Cómo pueden los administradores controlar las cuentas creadas para RMS para individuos](rms-for-individuals-take-control.md).

-   **Administrar Rights Management**: Los administradores de TI pueden convertir la suscripción a RMS para usuarios de la organización a una suscripción de pago que incluya Azure Rights Management. Cuando lleven a cabo esta conversión, el directorio y las cuentas existentes de Azure no podrán ser objeto de una transición sencilla para usuarios existentes que estén usando RMS para usuarios. Cualquier archivo que los usuarios hayan protegido con anterioridad permanecerá protegido con las mismas directivas y las personas a las que les garantizaron permisos para usar los archivos todavía podrán usar los archivos del mismo modo.

    Cuando emprenda este proceso, su organización se beneficiará de poder integrar Rights Management en sus flujos de trabajo, servicios y almacenes de datos. Además, podrá administrar Rights Management porque tendrá el control sobre la clave de inquilino de su organización para Azure Rights Management. Ahora puedes tomar las decisiones siguientes:

    -   Configurar Exchange y SharePoint para admitir Azure Rights Management, aunque se estén ejecutando de forma local. Exchange y SharePoint son servicios en línea compatibles de forma nativa y son admitidos por un conector para los servidores locales. Para obtener más información, vea:

        -   Las secciones Exchange Online y SharePoint Online desde [Office 365: configuración para clientes y servicios en línea](../deploy-use/configure-office365.md)

        -   [Implementación del conector de Azure Rights Management](../deploy-use/deploy-rms-connector.md)

    -   Llevar a cabo descubrimientos electrónicos en los datos pertenecientes a una compañía, de modo que pueda, si es necesario, descifrar archivos que estuviesen protegidos usando Rights Management. Para más información, consulte [Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos](../deploy-use/configure-super-users.md).

    -   Registrar toda la actividad de cómo se ha usado Rights Management en su organización. Esta es una acción muy potente, ya que no solo puede supervisar qué archivos están protegidos y quién está accediendo a esos archivos protegidos, sino que también puede identificar comportamientos sospechosos potenciales procedentes de personas no autorizadas, que estén intentando acceder a los archivos protegidos. Para más información, consulte [Registro y análisis del uso de Azure Rights Management](../deploy-use/log-analyze-usage.md).

    -   Proporcionar a los usuarios la capacidad de realizar un seguimiento de sus documentos protegidos y revocarlos, si estas características son compatibles con su [suscripción a Azure RMS](https://technet.microsoft.com/dn858608). Para más información, consulte [Realizar un seguimiento de los archivos y revocarlos](../rms-client/sharing-app-track-revoke.md) en la [guía de usuario de la aplicación RMS sharing](../rms-client/sharing-app-user-guide.md).

    -   Implemente una solución "Aporta tu propia clave" (BYOK) para que la clave de inquilino para Azure Rights Management se genere de forma local, siguiendo las políticas de TI y se transfiera de modo seguro a Microsoft mediante un módulo de seguridad de hardware (HSM). Para más información, consulte [Planeamiento e implementación de la clave de inquilino de Azure Rights Management](../plan-design/plan-implement-tenant-key.md).


## Pasos siguientes
Consulte [Cómo pueden los administradores controlar las cuentas creadas para RMS para usuarios](rms-for-individuals-take-control.md).





<!--HONumber=Jul16_HO3-->


