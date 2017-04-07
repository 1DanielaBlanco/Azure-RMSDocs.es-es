---
title: "Retirada y desactivación de Azure RMS"
description: "Información e instrucciones si decide que ya no quiere usar este servicio de protección de la información de Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: f577337cf7ce904a82ff23b165fdc7befe319092
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="decommissioning-and-deactivating-azure-rights-management"></a>Retirada y desactivación de Azure Rights Management

>*Se aplica a: Azure Information Protection, Office 365*

El usuario siempre controla si la organización protege el contenido con el servicio Azure Rights Management de Azure Information Protection y, si decide dejar de usar este servicio de protección de la información, puede estar seguro de que podrá acceder al contenido que haya protegido anteriormente. Si ya no necesita acceso continuo al contenido protegido anteriormente, puede desactivar el servicio y dejar que expire su suscripción a Azure Information Protection. Por ejemplo, esto sería adecuado si ha completado la prueba de Azure Information Protection antes de implementarlo en un entorno de producción.

Pero, si ha implementado Azure Information Protection en documentos y correos electrónicos protegidos de producción, asegúrese de que tiene una copia de la clave de inquilino de Azure Information Protection antes de desactivar el servicio Azure Rights Management y realice esta acción antes de que expire la suscripción, ya que esto garantizará que pueda conservar el acceso al contenido protegido por Azure Rights Management después de desactivar el servicio. Si ha usado la solución “aportar tu propia clave” (BYOK) para generar y administrar su propia clave en un HSM, ya dispondrá de su clave de inquilino de Azure Information Protection. Pero si fue Microsoft quien se encargó de administrarla (valor predeterminado), consulte las instrucciones para exportar su clave de inquilino en el artículo [Operaciones para la clave de inquilino de Azure Rights Management](operations-tenant-key.md).

> [!TIP]
> Incluso después de que expire la suscripción, el inquilino de Azure Information Protection seguirá estando disponible para el uso de contenido durante un período adicional. Sin embargo, ya no podrá exportar su clave de inquilino.

Cuando tenga su clave de inquilino de Azure Information Protection, puede implementar Rights Management de forma local (AD RMS) e importar su clave de inquilino como dominio de publicación de confianza (TPD). Después, tiene las opciones siguientes para retirar la implementación de Azure Information Protection:

|Si este es su caso...|… haz esto:|
|----------------------------|--------------|
|Quiere que todos los usuarios sigan usando Rights Management, pero usa una solución local en lugar de Azure Information Protection    →|Use el cmdlet [Set-AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx) para dirigir a los usuarios existentes a su implementación local cuando consuman contenido protegido después de este cambio. Los usuarios usarán automáticamente la instalación de AD RMS para consumir el contenido protegido.<br /><br />Para que los usuarios consuman contenido que se protegió antes de este cambio, redirija a los clientes a la implementación local mediante la clave del Registro **LicensingRedirection** para Office 2016 o Office 2013, como se describe en la [sección de detección del servicio](../rms-client/client-deployment-notes.md) en las notas de implementación del cliente de RMS, y la clave del Registro **LicenseServerRedirection** para Office 2010, como se describe en [Configuración del Registro de Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Desea dejar de usar por completo las tecnologías de Rights Management    →|Conceda [derechos de superusuario](../deploy-use/configure-super-users.md) a un administrador designado y proporciónele la [herramienta de protección de RMS](http://www.microsoft.com/en-us/download/details.aspx?id=47256).<br /><br />Después, el administrador puede usar la herramienta para descifrar en bloque archivos de carpetas protegidos con el servicio Azure Rights Management para desproteger los archivos y, por lo tanto, permitir su lectura sin una tecnología de Rights Management, como Azure Information Protection o AD RMS. Esta herramienta se puede usar para el servicio Azure Rights Management de Azure Information Protection y para AD RMS, para que tenga la opción de descifrar los archivos antes o después de desactivar el servicio Azure Rights Management, o bien una combinación.|
|No puede identificar todos los archivos protegidos por el servicio Azure Rights Management de Azure Information Protection, o bien quiere que todos los usuarios puedan leer automáticamente los archivos protegidos que faltaban    →|Implemente una configuración del Registro en todos los equipos cliente mediante la clave del Registro **LicensingRedirection** para Office 2016 y Office 2013, como se describe en la [sección de detección del servicio](../rms-client/client-deployment-notes.md) en las notas de implementación del cliente de RMS, y la clave del Registro **LicenseServerRedirection** para Office 2010, como se describe en [Configuración del Registro de Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).<br /><br />Asimismo, implemente otra configuración del Registro para impedir que los usuarios protejan archivos nuevos estableciendo **DisableCreation** en **1**, como se describe en [Configuración del Registro de Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Necesita un servicio de recuperación manual y controlada para los archivos que se perdieron    →|Conceda [derechos de superusuario](../deploy-use/configure-super-users.md) a los usuarios designados de un grupo de recuperación de datos y proporcióneles la [herramienta de protección de RMS](http://www.microsoft.com/en-us/download/details.aspx?id=47256) para que puedan desproteger archivos cuando se lo soliciten los usuarios estándar.<br /><br />En todos los equipos, implemente la configuración del Registro para impedir que los usuarios protejan archivos nuevos estableciendo **DisableCreation** en **1**, como se describe en [Configuración del Registro de Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
Para más información sobre los procedimientos descritos en esta tabla, consulte los recursos siguientes:

-   Para obtener información sobre AD RMS y referencias de implementación, vea [Introducción a Active Directory Rights Management Services](https://technet.microsoft.com/library/hh831364.aspx).

-   Para obtener instrucciones sobre cómo importar la clave de inquilino de Azure Information Protection como archivo TPD, vea [Adición de un dominio de publicación de confianza](https://technet.microsoft.com/library/cc771460.aspx).

-   Para instalar el módulo de Windows PowerShell para Azure Rights Management para establecer la URL de migración, vea [Instalación de Windows PowerShell para Azure Rights Management](install-powershell.md).

Cuando esté preparado para desactivar el servicio Azure Rights Management para su organización, siga las instrucciones siguientes.

## <a name="deactivating-rights-management"></a>Desactivación de Rights Management
Use uno de los procedimientos siguientes para desactivar [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

> [!TIP]
> También puede usar el cmdlet [Disable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629422.aspx) de Windows PowerShell para desactivar [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].

#### <a name="to-deactivate-rights-management-from-the-office-365-admin-center"></a>Para desactivar Rights Management desde el centro de administración de Office 365

1. Vaya a la [página de Rights Management](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) para los administradores de Office 365.
    
    Si se le solicita que inicie sesión, use una cuenta de administrador global de Office 365.    

2. En la página **Rights Management** , haga clic en **Desactivar**.

3.  Cuando el sistema le pregunte **¿Desea desactivar Rights Management?**, haga clic en **Desactivar**.

Ahora debería ver **Rights Management no está activado** y la opción para activarlo.

#### <a name="to-deactivate-rights-management-from-the-azure-classic-portal"></a>Para desactivar Rights Management desde el Portal de Azure clásico

1.  Inicie sesión en el [Portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=275081).

2.  En el panel izquierdo, haga clic en **ACTIVE DIRECTORY**.

3.  En la página **Active Directory** , haga clic en **RIGHTS MANAGEMENT**.

4.  Asegúrese de seleccionar el nombre del inquilino, haga clic en **DEACTIVATE** y confirme la acción.

El **ESTADO DE RIGHTS MANAGEMENT** debe indicar ahora **Inactivo** y la opción **DESACTIVAR** debe aparecer reemplazada por **ACTIVAR**.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


