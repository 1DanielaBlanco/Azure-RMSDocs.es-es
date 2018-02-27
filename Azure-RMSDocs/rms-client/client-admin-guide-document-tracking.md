---
title: Seguimiento de documentos para Azure Information Protection
description: "Instrucciones e información para que los administradores configuren y usen Seguimiento de documentos para Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 983ecdc9-5631-48b8-8777-f4cbbb4934e8
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 727ff705c4a90a9c029820332983b4cf7bec5e05
ms.sourcegitcommit: 31c79d948ec3089a4dc65639f1842c07c7aecba6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/20/2018
---
# <a name="admin-guide-configuring-and-using-document-tracking-for-azure-information-protection"></a>Guía del administrador: Configuración y uso de Seguimiento de documentos para Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Si tiene una [suscripción que admite el seguimiento de documentos](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features), el sitio de seguimiento de documentos está habilitado de manera predeterminada para todos los usuarios de su organización. El seguimiento de documentos proporciona información para usuarios y administradores sobre cuándo se accedió a un documento protegido y, en caso de ser necesario, se puede revocar un documento al que se hizo seguimiento.

## <a name="privacy-controls-for-your-document-tracking-site"></a>Controles de privacidad para el sitio de seguimiento de documentos

Si mostrar toda esta información de seguimiento de documentos está prohibido en su organización debido a los requisitos de privacidad, puede deshabilitar el seguimiento de documentos mediante el cmdlet [Disable-AadrmDocumentTrackingFeature](/powershell/module/aadrm/disable-aadrmdocumenttrackingfeature). 

Este cmdlet deshabilita el acceso al sitio de seguimiento de documentos para que ninguno de los usuarios de la organización pueda hacer seguimiento ni revocar el acceso a documentos que se han protegido. Puede volver a habilitar el seguimiento de documentos en cualquier momento con el cmdlet [Enable-AadrmDocumentTrackingFeature](/powershell/module/aadrm/enable-aadrmdocumenttrackingfeature), así como comprobar si el seguimiento de documentos está actualmente habilitado o deshabilitado mediante [Get-AadrmDocumentTrackingFeature](/powershell/module/aadrm/get-aadrmdocumenttrackingfeature). Para ejecutar estos cmdlets, debe tener como mínimo la versión **2.3.0.0** del módulo de Azure Rights Management (AADRM) para PowerShell. 

Cuando el sitio de seguimiento de documentos está habilitado, de manera predeterminada, muestra información como las direcciones de correo electrónico de las personas que intentaron acceder a los documentos protegidos, cuándo intentaron hacerlo y su ubicación. Este nivel de información puede resultar útil para determinar cómo se usan los documentos compartidos y si se deben revocar en caso de detectar actividad sospechosa. Sin embargo, por motivos de privacidad, es posible que tenga que deshabilitar esta información de usuario para algunos o la totalidad de los usuarios. 

Si tiene usuarios para los que no debe haber otros usuarios realizando un seguimiento de esta actividad, agréguelos a un grupo que se almacena en Azure AD y especifique este grupo con el cmdlet [Set-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/Set-AadrmDoNotTrackUserGroup). Cuando ejecute este cmdlet, debe especificar un grupo único. Sin embargo, el grupo puede contener grupos anidados. 

Para estos miembros del grupo, los usuarios no pueden ver ninguna actividad en el sitio de seguimiento de documentos cuando esa actividad esté relacionada con documentos que compartían con ellos. Además, no se envía ninguna notificación por correo electrónico al usuario que compartió el documento.

Cuando usa esta configuración, todos los usuarios pueden seguir usando el sitio de seguimiento de documentos y revocar el acceso a los documentos que han protegido. Sin embargo, no observan actividad para los usuarios que especificó con el cmdlet Set-AadrmDoNotTrackUserGroup.

Esta configuración solo afecta a los usuarios finales. Los administradores de Azure Information Protection siempre pueden realizar un seguimiento de las actividades de todos los usuarios, incluso cuando aquellos usuarios se especifican mediante Set-AadrmDoNotTrackUserGroup. Para más información sobre cómo los administradores pueden realizar un seguimiento de documentos para usuarios, consulte la sección [Realizar un seguimiento y revocar documentos para usuario](#tracking-and-revoking-documents-for-users).

Puede usar el cmdlet [Clear-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/Clear-AadrmDoNotTrackUserGroup) si ya no necesita esta opción. También puede quitar usuarios de manera selectiva si los quita del grupo, pero tenga en cuenta la [caché de grupo](../plan-design/prepare.md#group-membership-caching-by-azure-information-protection). Puede usar el cmdlet [Get-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/get-AadrmDoNotTrackUserGroup) para comprobar si esta opción está en uso actualmente. Para ejecutar los cmdlets de esta configuración de grupo, debe tener como mínimo la versión **2.10.0.0** del módulo de Azure Rights Management (AADRM) para PowerShell.

Para más información sobre cada uno de estos cmdlets, use los vínculos que se proporcionan. Para obtener instrucciones de instalación del módulo de PowerShell, vea [Instalación del módulo de PowerShell para AADRM](../deploy-use/install-powershell.md). Si ya descargó e instaló el módulo, compruebe el número de versión. Para ello, ejecute: `(Get-Module aadrm –ListAvailable).Version`


## <a name="destination-urls-used-by-the-document-tracking-site"></a>Direcciones URL de destino que usa el sitio de seguimiento de documentos

Las siguientes direcciones URL se usan para seguimiento de documentos y se deben permitir en todos los dispositivos y servicios entre los clientes que ejecutan el cliente de Azure Information Protection e Internet. Por ejemplo, agregue estas direcciones URL a los firewalls o a los sitios de confianza si usa Internet Explorer con seguridad mejorada.

-  `https://*.azurerms.com`

- `https://*.microsoftonline.com`

- `https://*.microsoftonline-p.com`

- `https://ecn.dev.virtualearth.net`

Estas direcciones URL son estándar para el servicio de Azure Rights Management, a excepción de la dirección URL virtualearth.net que se usa para que los mapas de Bing muestren la ubicación del usuario.

## <a name="tracking-and-revoking-documents-for-users"></a>Realizar un seguimiento y revocar documentos para usuarios

Cuando los usuarios inician sesión en el sitio de Seguimiento de documentos, pueden realizar un seguimiento de documentos que han protegido con el cliente de Azure Information Protection o que han compartido con la aplicación Rights Management sharing o también revocarlos. Si inicia sesión como administrador de Azure Information Protection (administrador global), puede hacer clic en el icono Administrador, lo que permite utilizar el modo Administrador. Este modo permite ver los documentos que han seleccionado los usuarios de su organización para su seguimiento mediante el cliente de Azure Information Protection, o bien que han compartido usando la aplicación para uso compartido de Rights Management:

![Icono Administrador en el sitio de Seguimiento de documentos](../media/tracking-site-admin-icon.png)

> [!NOTE] 
> Si no ve este icono, a pesar de ser un administrador global, es porque aún no ha compartido ningún documento. En este caso, utilice la siguiente dirección URL para acceder al sitio de seguimiento de documentos: https://portal.azurerms.com/#/admin

Las acciones que realiza en el modo de administrador se auditan y registran en los archivos de registro de uso y debe confirmar para continuar. Para obtener más información sobre este registro, consulte la sección siguiente.

Cuando está en el modo de administrador, puede buscar por usuario o documento. Si busca por usuario, verá todos los documentos que el usuario especificado ha seleccionado para su seguimiento mediante el cliente de Azure Information Protection, o bien que han compartido usando la aplicación para uso compartido de Rights Management. 

Si busca por documento, verá todos los usuarios de su organización que han hecho un seguimiento de un documento mediante el cliente de Azure Information Protection, o bien que lo han compartido usando la aplicación para uso compartido de Rights Management. Después, puede profundizar en los resultados de búsqueda para realizar un seguimiento de los documentos que han protegido los usuarios y revocar estos documentos, si es necesario. 

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

- [Personalizaciones](client-admin-guide-customizations.md)

- [Archivos de cliente y registro de uso](client-admin-guide-files-and-logging.md)

- [Tipos de archivos admitidos](client-admin-guide-file-types.md)

- [Comandos de PowerShell](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
