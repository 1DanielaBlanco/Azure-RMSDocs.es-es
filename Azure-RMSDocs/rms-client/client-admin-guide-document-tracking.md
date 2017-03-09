---
title: Seguimiento de documentos para Azure Information Protection
description: "Instrucciones e información para que los administradores configuren y usen Seguimiento de documentos para Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 983ecdc9-5631-48b8-8777-f4cbbb4934e8
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: aa3b80b7369348f87adc440d6f7a91977aa0fc7c
ms.lasthandoff: 02/24/2017


---


# <a name="configuring-and-using-document-tracking-for-azure-information-protection"></a>Configuración y uso de Seguimiento de documentos para Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8 y Windows 7 con SP1*

Si tiene una [suscripción que admite el seguimiento de documentos](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features), el sitio de seguimiento de documentos está habilitado de manera predeterminada para todos los usuarios de su organización. El seguimiento de documentos mostrará información, como las direcciones de correo electrónico de las personas que intentaron acceder a documentos protegidos que los usuarios compartieron, cuándo estas personas intentaron obtener acceso a ellos y su ubicación. Si mostrar esta información está prohibido en su organización debido a los requisitos de privacidad, puede deshabilitar el acceso al sitio de seguimiento de documentos mediante el cmdlet [Disable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623032). Puede volver a habilitar el acceso al sitio en cualquier momento, mediante [Enable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037), así como comprobar si el acceso está actualmente habilitado o deshabilitado mediante [Get AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037).

Para ejecutar estos cmdlets, debe tener como mínimo la versión **2.3.0.0** del módulo de Azure Rights Management para Windows PowerShell. Para obtener instrucciones de instalación, consulte [Instalación de Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md).

> [!TIP]
> Si ya descargó e instaló el módulo, compruebe el número de versión. Para ello, ejecute: `(Get-Module aadrm –ListAvailable).Version`

Las direcciones URL siguientes se usan para el seguimiento de documentos y se deben permitir (por ejemplo, agregarlas a sus sitios de confianza si está usando Internet Explorer con seguridad mejorada):

-   https://&#42;.azurerms.com

-   https://ecn.dev.virtualearth.net

    > [!NOTE]
    > Esta dirección URL es para mapas de Bing.

-   https://&#42;.microsoftonline.com

-   https://&#42;.microsoftonline-p.com

## <a name="tracking-and-revoking-documents-for-users"></a>Realizar un seguimiento y revocar documentos para usuarios

Cuando los usuarios inician sesión en el sitio de Seguimiento de documentos, pueden realizar un seguimiento de documentos que han protegido con el cliente de Azure Information Protection o que han compartido con la aplicación Rights Management sharing o también revocarlos. Si inicia sesión como administrador de Azure Information Protection (administrador global), puede hacer clic en el icono Administrador, lo que permite cambiar al modo Administrador para poder ver los documentos que han compartido los usuarios de la organización:

![Icono Administrador en el sitio de Seguimiento de documentos](../media/tracking-site-admin-icon.png)

Las acciones que realiza en el modo de administrador se auditan y registran en los archivos de registro de uso y debe confirmar para continuar. Para obtener más información sobre este registro, consulte la sección siguiente.

Cuando está en el modo de administrador, puede buscar por usuario o documento. Si quiere buscar por usuario, verá todos los documentos que ha compartido el usuario especificado. Si quiere buscar por documento, verá todos los usuarios de la organización que han compartido ese documento. Después, puede profundizar en los resultados de búsqueda para realizar un seguimiento de los documentos que han compartido los usuarios y revocar estos documentos, si es necesario. 

Para salir del modo de administrador, haga clic en la **X** junto a **Salir del modo de administrador**:

![Salir del modo de administrador en el sitio de Seguimiento de documentos](../media/tracking-site-exit-admin-icon.png)

Para obtener instrucciones sobre cómo usar el sitio de seguimiento de documentos, consulte [Seguimiento y revocación de documentos](client-track-revoke.md) en el manual del usuario.

## <a name="usage-logging-for-the-document-tracking-site"></a>Registro de uso del sitio de seguimiento de documentos

Dos campos de los archivos de registro de uso se aplican al seguimiento de documentos: **AdminAction** y **ActingAsUser**.

**AdminAction**: este campo tiene un valor de true cuando un administrador usa el sitio de seguimiento de documentos en modo de administrador, por ejemplo, para revocar un documento en nombre de un usuario o para ver cuándo se ha compartido. Este campo está vacío cuando un usuario inicia sesión en el sitio de seguimiento de documentos.

**ActingAsUser**: cuando el campo AdminAction es true, este campo contiene el nombre de usuario del que el administrador actúa en nombre, como la búsqueda de usuario o propietario del documento. Este campo está vacío cuando un usuario inicia sesión en el sitio de seguimiento de documentos. 

También hay tipos de solicitudes que registran cómo los usuarios y administradores usan el sitio de seguimiento de documentos. Por ejemplo, **RevokeAccess** es el tipo de solicitud cuando un usuario o un administrador en nombre de un usuario ha revocado un documento en el sitio de seguimiento de documentos. Use este tipo de solicitud en combinación con el campo AdminAction para determinar si el usuario ha revocado su propio documento (el campo AdminAction está vacío) o un administrador ha revocado un documento en nombre de un usuario (el campo AdminAction es true).


Para obtener más información sobre el registro de uso, consulte [Registro y análisis del uso del servicio Azure Rights Management](../deploy-use/log-analyze-usage.md).



## <a name="next-steps"></a>Pasos siguientes
Ahora que ha configurado el sitio de Seguimiento de documentos para el cliente de Azure Information Protection, vea la siguiente información adicional que puede necesitar para la compatibilidad con este cliente:

- [Archivos de cliente y registro de uso](client-admin-guide-files-and-logging.md)

- [Tipos de archivos admitidos](client-admin-guide-file-types.md)

- [Comandos de PowerShell](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

