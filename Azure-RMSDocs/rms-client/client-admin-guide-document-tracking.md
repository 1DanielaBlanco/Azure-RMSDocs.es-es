---
title: Seguimiento de documentos para Azure Information Protection
description: "Instrucciones e información para que los administradores configuren y usen el seguimiento de documentos de Azure Information Protection."
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
ms.openlocfilehash: bbbc9a274ea815577109276bceb0b08617f03809
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/29/2018
---
# <a name="admin-guide-configuring-and-using-document-tracking-for-azure-information-protection"></a>Guía de administración: Configuración y uso del seguimiento de documentos de Azure Information Protection

>*Es válida para: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Si tiene una [suscripción que admita el seguimiento de documentos](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features), el sitio de seguimiento de documentos se habilita de forma predeterminada para todos los usuarios de la organización. El seguimiento de documentos proporciona información para los usuarios y administradores sobre cuándo se accedió a un documento protegido y, si es necesario, se puede revocar un documento sometido a seguimiento.

## <a name="privacy-controls-for-your-document-tracking-site"></a>Controles de privacidad para el sitio de seguimiento de documentos

Si mostrar toda la información de seguimiento de documentos está prohibido en una organización debido a los requisitos de privacidad, puede deshabilitar el seguimiento con el cmdlet [Disable-AadrmDocumentTrackingFeature](/powershell/module/aadrm/disable-aadrmdocumenttrackingfeature). 

Este cmdlet deshabilita el acceso al sitio de seguimiento de documentos para que ningún usuario de la organización pueda realizar el seguimiento ni revocar el acceso a los documentos que se hayan protegido. Puede volver a habilitar el seguimiento de documentos en cualquier momento con el cmdlet [Enable-AadrmDocumentTrackingFeature](/powershell/module/aadrm/enable-aadrmdocumenttrackingfeature), así como comprobar si el seguimiento de documentos está habilitado o deshabilitado actualmente mediante [Get AadrmDocumentTrackingFeature](/powershell/module/aadrm/get-aadrmdocumenttrackingfeature). Para ejecutar estos cmdlets, debe tener al menos la versión **2.3.0.0** del módulo de Azure Rights Management (AADRM) para PowerShell. 

Cuando el sitio de seguimiento de documentos está habilitado, de forma predeterminada, se muestra información como las direcciones de correo electrónico de las personas que intentaron acceder a los documentos protegidos, cuándo y su ubicación. Este nivel de información puede resultar útil para determinar cómo se usan los documentos compartidos y si se deben revocar en el caso de que se observe alguna actividad sospechosa. Sin embargo, por motivos de privacidad, es posible que tenga que deshabilitar esta información de usuario para algunos de los usuarios o para todos ellos. 

Si tiene usuarios cuya actividad no debería ser seguida por otros, agréguelos a un grupo que se almacene en Azure Active Directory y especifique este grupo con el cmdlet [Set-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/Set-AadrmDoNotTrackUserGroup). Cuando ejecute este cmdlet, debe especificar un único grupo. Sin embargo, el grupo puede contener grupos anidados. 

Para estos miembros del grupo, los usuarios no pueden ver ninguna actividad en el sitio de seguimiento de documentos cuando esa actividad esté relacionada con los documentos que compartían con ellos. Además, no se envían notificaciones por correo electrónico al usuario que compartió el documento.

Cuando se usa esta configuración, todos los usuarios pueden seguir usando el sitio de seguimiento de documentos y revocar el acceso a los documentos que hayan protegido. Sin embargo, no verán la actividad de aquellos usuarios que haya especificado con el cmdlet Set-AadrmDoNotTrackUserGroup.

Esta configuración solo afecta a los usuarios finales. Los administradores de Azure Information Protection siempre pueden hacer un seguimiento de las actividades de todos los usuarios, incluso cuando esos usuarios se especifican mediante el cmdlet Set-AadrmDoNotTrackUserGroup. Para más información acerca de cómo los administradores pueden realizar un seguimiento de los documentos de los usuarios, consulte la sección [Seguimiento y revocación de documentos de los usuarios](#tracking-and-revoking-documents-for-users) sección.

Puede usar el cmdlet [Clear-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/Clear-AadrmDoNotTrackUserGroup) si ya no necesita esta opción. O bien, para quitar usuarios de manera selectiva, quítelos del grupo, pero tenga en cuenta el [almacenamiento en caché de grupos](../plan-design/prepare.md#group-membership-caching-by-azure-information-protection). Puede comprobar si esta opción se usa actualmente con el cmdlet [Get-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/get-AadrmDoNotTrackUserGroup). Para ejecutar los cmdlets para esta configuración de grupo, debe tener al menos la versión **2.10.0.0** del módulo de Azure Rights Management (AADRM) para PowerShell.

Para más información acerca de cada uno de estos cmdlets, use los vínculos proporcionados. Para instrucciones de instalación del módulo de PowerShell, consulte [Instalación de Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md). Si ya descargó e instaló el módulo, compruebe el número de versión ejecutando `(Get-Module aadrm –ListAvailable).Version`


## <a name="destination-urls-used-by-the-document-tracking-site"></a>Direcciones URL de destino que usa el sitio de seguimiento de documentos

Las siguientes direcciones URL se utilizan para el seguimiento de documentos y se deben permitir en todos los dispositivos y servicios entre los clientes que ejecutan el cliente de Azure Information Protection e Internet. Por ejemplo, agregue estas direcciones URL a los firewalls o a los sitios de confianza, si está usando Internet Explorer con seguridad mejorada.

-  `https://*.azurerms.com`

- `https://*.microsoftonline.com`

- `https://*.microsoftonline-p.com`

- `https://ecn.dev.virtualearth.net`

Estas direcciones URL son estándar para el servicio Azure Rights Management, a excepción de virtualearth.net que se usa para que los mapas de Bing muestren la ubicación del usuario.

## <a name="tracking-and-revoking-documents-for-users"></a>Seguimiento y revocación de documentos de los usuarios

Cuando los usuarios inician sesión en el sitio de seguimiento de documentos, pueden realizar el seguimiento de los documentos que se hayan protegido mediante el cliente de Azure Information Protection o que se hayan compartido con la aplicación Microsoft Rights Management sharing application, y también puede revocar dichos documentos. Al iniciar la sesión como administrador de Azure Information Protection (administrador global), puede hacer clic en el icono Administrador, que pasa al modo de administrador. Este modo le permite ver los documentos que los usuarios de la organización han seleccionado para realizar el seguimiento con el cliente de Azure Information Protection o bien que han compartido con la aplicación Microsoft Rights Management sharing application:

![Icono del administrador en el sitio de seguimiento de documentos](../media/tracking-site-admin-icon.png)

> [!NOTE] 
> Si no ve este icono a pesar de ser un administrador global, es porque aún no ha compartido ningún documento. En este caso, utilice la siguiente dirección URL para acceder al sitio de seguimiento de documentos: https://portal.azurerms.com/#/admin

Las acciones que realiza en modo de administrador se auditan y registran en los archivos de registro de uso, y debe confirmar para continuar. Para más información sobre este registro, consulte la siguiente sección.

Cuando está en el modo de administrador, puede buscar por usuario o por documento. Si busca por usuario, verá todos los documentos que el usuario especificado haya seleccionado para realizar su seguimiento con el cliente de Azure Information Protection o bien que haya compartido con la aplicación Microsoft Rights Management sharing application. 

Si busca por documento, verá todos los usuarios de la organización que realizaron el seguimiento de dicho documento con el cliente de Azure Information Protection o que compartieron con la aplicación Microsoft Rights Management sharing application. A continuación, puede profundizar en los resultados de la búsqueda para realizar un seguimiento de los documentos que los usuarios hayan protegido y revocar dichos documentos, si es necesario. 

Para salir del modo de administrador, haga clic en **X** junto a **Salir del modo de administrador**:

![Salida del modo de administrador en el sitio de seguimiento de documentos](../media/tracking-site-exit-admin-icon.png)

Para obtener instrucciones acerca de cómo usar el sitio de seguimiento de documentos, consulte [Seguimiento y revocación de documentos](client-track-revoke.md) en el manual del usuario.

## <a name="usage-logging-for-the-document-tracking-site"></a>Registro de uso para el sitio de seguimiento de documentos

Dos campos de los archivos de registro de uso son aplicables al seguimiento de documentos: **AdminAction** y **ActingAsUser**.

**AdminAction**: este campo tiene el valor true cuando un administrador usa el sitio de seguimiento de documentos en el modo de administrador, por ejemplo, para revocar un documento en nombre de un usuario o para ver cuándo se ha compartido. Este campo está vacío cuando un usuario inicia sesión en el sitio de seguimiento de documentos.

**ActingAsUser**: cuando el campo AdminAction es true, este campo contiene el nombre de usuario en nombre del que el administrador actúa, como la búsqueda del usuario o del propietario del documento. Este campo está vacío cuando un usuario inicia sesión en el sitio de seguimiento de documentos. 

También hay tipos de solicitud que registran cómo los usuarios y administradores usan el sitio de seguimiento de documentos. Por ejemplo, **RevokeAccess** es el tipo de solicitud cuando un usuario o un administrador en nombre de un usuario ha revocado un documento en el sitio de seguimiento de documentos. Utilice este tipo de solicitud en combinación con el campo AdminAction para determinar si el usuario ha revocado su propio documento (el campo AdminAction está vacío) o si un administrador ha revocado un documento en nombre del usuario (el campo AdminAction es true).


Para más información sobre el registro de uso, consulte [Registro y análisis del uso del servicio Azure Rights Management](../deploy-use/log-analyze-usage.md)



## <a name="next-steps"></a>Pasos siguientes
Ahora que ha configurado el sitio de seguimiento de documentos para el cliente de Azure Information Protection, consulte lo siguiente para obtener información adicional que podría necesitar para la compatibilidad con este cliente:

- [Personalizaciones](client-admin-guide-customizations.md)

- [Archivos de cliente y registro de uso](client-admin-guide-files-and-logging.md)

- [Tipos de archivos compatibles](client-admin-guide-file-types.md)

- [Comandos de PowerShell](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
