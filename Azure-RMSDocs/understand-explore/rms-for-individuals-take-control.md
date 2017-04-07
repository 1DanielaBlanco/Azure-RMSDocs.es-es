---
title: Control de las cuentas creadas para RMS para individuos - AIP
description: "Cómo puede controlar las cuentas de usuario de Azure Active Directory si no desea convertir la suscripción a RMS para usuarios de la organización en una suscripción de pago."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a83880d0-f0f9-4a32-9e00-2f6635d7cc8d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 666408da3bfa0095db1cb6ff956c9a118201cefb
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="how-administrators-can-control-the-accounts-created-for-rms-for-individuals"></a>Cómo pueden los administradores controlar las cuentas creadas para RMS para usuarios

>*Se aplica a: Azure Information Protection*


Si no desea convertir su suscripción de RMS para usuarios de la organización en una suscripción de pago, todavía puede controlar las cuentas de usuario del directorio de Azure que creó para su organización de los modos que se indican a continuación:

-   Implemente soluciones de integración de directorio para Azure Active Directory y su infraestructura de servicios de dominio de Active Directory. Puede sincronizar cuentas y contraseñas para que los usuarios no tengan que crear nuevas cuentas para utilizar Rights Management y se aplicarán sus políticas de contraseñas locales a las cuentas nuevas de Azure. También puede sincronizar contraseñas para que los usuarios no tengan que recordar una contraseña diferente para utilizar Rights Management.

-   Puede impedir que los usuarios se suscriban para usar Azure Rights Management con la suscripción a RMS para usuarios. En la mayoría de casos, existen muy pocas ventajas en hacerlo, ya que los usuarios o bien compartirán archivos sin protección (lo que podría poner a la compañía en riesgo) o bien utilizarán otro mecanismo de protección de archivos que no le dé la opción al departamento de TI de tener acceso a los datos. Sin embargo, si quiere evitar que los usuarios se suscriban para usar RMS para usuarios, lleve a cabo uno de los procedimientos siguientes después de asumir la titularidad del directorio de su organización en Azure:

    -   Impida que todos los usuarios se suscriban para obtener suscripciones de autoservicio, lo que incluye RMS para individuos.  Actualmente, no puede establecer esto por servicio; la configuración se aplica a todas las suscripciones de Azure que usan el proceso de autoservicio. Para ello, establezca el parámetro **AllowAdHocSubscriptions** en False con el cmdlet [Set-MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) del módulo de PowerShell para Azure Active Directory. Por ejemplo: **Set-MsolCompanySettings -AllowAdHocSubscriptions $false**

    -   Impida que los usuarios creen una cuenta nueva en Azure, lo que significa que solo los usuarios que ya tienen una cuenta de Azure pueden suscribirse para obtener suscripciones de autoservicio, lo que incluye RMS para usuarios.  Para ello, establezca el parámetro **AllowEmailVerifiedUsers** en False con el cmdlet [Set-MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) del módulo de PowerShell para Azure Active Directory. Por ejemplo: **Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true**

    -   Sincronice su infraestructura de Servicios de dominio de Active Directory con Azure Active Directory. Esta acción evita que se creen cuentas nuevas cuando los usuarios se suscriben para obtener suscripciones de autoservicio como RMS para usuarios, y puede suprimir o deshabilitar cuentas creadas previamente en el directorio de Azure.

Para controlar las cuentas de usuario en el directorio de Azure, o para impedir que los usuarios se suscriban a RMS para usuarios, debe tener una suscripción de Azure y ser titular del directorio. Si todavía no tiene una suscripción a Azure, puede obtener una sin cargo alguno. Si se creó un directorio automáticamente durante el proceso de autoservicio, asuma la titularidad del dominio que se usó para crearla. Si ya tiene un directorio en Azure pero los usuarios especificaron un dominio nuevo que se usa en su organización, combine ese dominio con el directorio existente. Para obtener más información, consulte las instrucciones de [¿Qué es la suscripción de autoservicio de Azure?](https://azure.microsoft.com/documentation/articles/active-directory-self-service-signup/)


## <a name="next-steps"></a>Pasos siguientes

Si los usuarios en lugar de los administradores pueden crear sus cuentas en Azure Active Directory para RMS para personas, ¿cómo puede saber si lo han realizado?  Consulte [Cómo averiguar si los usuarios se suscribieron para obtener RMS para usuarios](rms-for-individuals-identify-sign-up.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]