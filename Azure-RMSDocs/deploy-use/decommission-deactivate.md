---
title: "Retirada y desactivación de Azure RMS"
description: "Información e instrucciones en caso de que ya no quiera usar el servicio de protección basado en la nube de Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/13/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 14887bb14599b24d95a19ee111ec3ab30ea95612
ms.sourcegitcommit: c157636577db2e2a2ba5df81eb985800cdb82054
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2018
---
# <a name="decommissioning-and-deactivating-protection-for-azure-information-protection"></a>Retirada y desactivación de la protección de Azure Information Protection

>*Se aplica a: Azure Information Protection, Office 365*

Usted siempre tiene el control sobre si su organización protege contenido mediante el servicio de Azure Rights Management de Azure Information Protection. Si decide que ya no quiere usar este servicio de protección de la información, puede estar seguro de que no perderá el acceso al contenido que haya protegido.

Si ya no necesita acceso continuo al contenido protegido anteriormente, desactive el servicio y deje que expire su suscripción a Azure Information Protection. Por ejemplo, esto sería adecuado si ha completado la prueba de Azure Information Protection antes de implementarlo en un entorno de producción.

Pero si ha implementado Azure Information Protection en producción y ha protegido documentos y correos electrónicos, debe asegurarse de que tiene una copia de la clave de inquilino de Azure Information Protection antes de desactivar el servicio Azure Rights Management. Asegúrese de que cuenta con una copia de la clave antes de que expire la suscripción, para estar seguro de que sigue teniendo acceso al contenido protegido con Azure Rights Management después de que se haya desactivado el servicio. Si ha usado la solución “Bring Your Own Key” (BYOK) para generar y administrar su propia clave en un HSM, ya dispondrá de una clave de inquilino de Azure Information Protection. Pero si fue Microsoft quien se encargó de administrarla (valor predeterminado), consulte las instrucciones para exportar su clave de inquilino en el artículo [Operaciones para la clave de inquilino de Azure Rights Management](operations-tenant-key.md).

> [!TIP]
> Incluso después de que expire la suscripción, el inquilino de Azure Information Protection seguirá estando disponible para el uso de contenido durante un período adicional. Sin embargo, ya no podrá exportar su clave de inquilino.

Cuando tenga su clave de inquilino de Azure Information Protection, puede implementar Rights Management de forma local (AD RMS) e importar su clave de inquilino como dominio de publicación de confianza (TPD). Después, tiene las opciones siguientes para retirar la implementación de Azure Information Protection:

|Si este es su caso...|… haga esto:|
|----------------------------|--------------|
|Quiere que todos los usuarios sigan usando Rights Management, pero usa una solución local en lugar de Azure Information Protection    →|Use el cmdlet [Set-AadrmMigrationUrl](/powershell/module/aadrm/Set-AadrmMigrationUrl) para dirigir a los usuarios existentes a su implementación local cuando consuman contenido protegido después de este cambio. Los usuarios usarán automáticamente la instalación de AD RMS para consumir el contenido protegido.<br /><br />Para que los usuarios puedan consumir el contenido que estaba protegido antes de este cambio, redirija a los clientes a la implementación local mediante la clave del Registro **LicensingRedirection** para Office 2016 u Office 2013. Para obtener instrucciones, vea la [sección sobre detección del servicio](../rms-client/client-deployment-notes.md) en las notas de la implementación del cliente de RMS y la clave del Registro **LicenseServerRedirection** para Office 2010, descrita en [Office Registry Settings](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx) (Configuración del Registro de Office).|
|Desea dejar de usar por completo las tecnologías de Rights Management    →|Conceda a un administrador designado [derechos de superusuario](../deploy-use/configure-super-users.md) e instale el [cliente de Azure Information Protection](../rms-client/client-admin-guide-install.md) para este usuario.<br /><br />Después, este administrador puede usar el módulo de PowerShell de este cliente para descifrar de forma masiva archivos en carpetas que estaban protegidos mediante el servicio Azure Rights Management. Los archivos vuelven a estar desprotegidos y, por tanto, se pueden leer sin una tecnología de Rights Management, como Azure Information Protection o AD RMS. Dado que este módulo de PowerShell se puede usar con el servicio Azure Rights Management de Azure Information Protection y con AD RMS, tiene la opción de descifrar los archivos antes o después de desactivar el servicio Azure Rights Management, o bien una combinación.|
|No es capaz de identificar todos los archivos que se han protegido mediante el servicio Azure Rights Management de Azure Information Protection, o bien quiere que todos los usuarios puedan leer automáticamente los archivos protegidos que se han perdido    →|Implemente una configuración del Registro en todos los equipos cliente mediante la clave del Registro **LicensingRedirection** para Office 2016 y Office 2013, como se describe en la [sección de detección del servicio](../rms-client/client-deployment-notes.md) en las notas de implementación del cliente de RMS, y la clave del Registro **LicenseServerRedirection** para Office 2010, como se describe en [Configuración del Registro de Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).<br /><br />Asimismo, implemente otra configuración del Registro para impedir que los usuarios protejan archivos nuevos estableciendo **DisableCreation** en **1**, como se describe en [Configuración del Registro de Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Necesita un servicio de recuperación manual y controlada para los archivos que se perdieron    →|Conceda [derechos de superusuario](../deploy-use/configure-super-users.md) a los usuarios designados de un grupo de recuperación de datos e instale el [cliente de Azure Information Protection](../rms-client/client-admin-guide-install.md) para estos usuarios para que puedan desproteger archivos cuando los usuarios estándar soliciten esta acción.<br /><br />En todos los equipos, implemente la configuración del Registro para impedir que los usuarios protejan archivos nuevos estableciendo **DisableCreation** en **1**, como se describe en [Configuración del Registro de Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
Para más información sobre los procedimientos descritos en esta tabla, consulte los recursos siguientes:

- Para obtener información sobre AD RMS y referencias de implementación, vea [Introducción a Active Directory Rights Management Services](https://technet.microsoft.com/library/hh831364.aspx).

- Para obtener instrucciones sobre cómo importar la clave de inquilino de Azure Information Protection como archivo TPD, vea [Adición de un dominio de publicación de confianza](https://technet.microsoft.com/library/cc771460.aspx).

- Para instalar el módulo de Windows PowerShell para Azure Rights Management para establecer la URL de migración, vea [Instalación de Windows PowerShell para Azure Rights Management](install-powershell.md).

- Para usar PowerShell con el cliente de Azure Information Protection, consulte [Uso de PowerShell con el cliente de Azure Information Protection](../rms-client/client-admin-guide-powershell.md).

Cuando esté preparado para desactivar el servicio Azure Rights Management para su organización, siga las instrucciones siguientes.

## <a name="deactivating-rights-management"></a>Desactivación de Rights Management
Use uno de los procedimientos siguientes para desactivar [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

> [!TIP]
> También puede usar el cmdlet [Disable-Aadrm](/powershell/module/aadrm/disable-aadrm) de Windows PowerShell para desactivar [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].

#### <a name="to-deactivate-rights-management-from-the-office-365-admin-center"></a>Para desactivar Rights Management desde el centro de administración de Office 365

1. Vaya a la [página de Rights Management](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) para los administradores de Office 365.
    
    Si se le solicita que inicie sesión, use una cuenta de administrador global de Office 365.    

2. En la página **Rights Management** , haga clic en **Desactivar**.

3.  Cuando el sistema le pregunte **¿Desea desactivar Rights Management?**, haga clic en **Desactivar**.

Ahora debería ver **Rights Management no está activado** y la opción para activarlo.

#### <a name="to-deactivate-rights-management-from-the-azure-portal"></a>Para desactivar Rights Management desde el Portal de Azure

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e [inicie sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal). Después, vaya a la hoja **Azure Information Protection**.
    
    Por ejemplo, en el menú del centro, haga clic en **Más servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. En la hoja inicial de **Azure Information Protection**, seleccione **Protección de la activación**. 

3.  En la hoja **Azure Information Protection - Protección de la activación**, seleccione **Desactivar**. Seleccione **Sí** para confirmar su elección.

En la barra de información se muestra **Deactivation finished successfully** (La desactivación ha finalizado correctamente) y **Activar** reemplaza a **Desactivar**. 


[!INCLUDE[Commenting house rules](../includes/houserules.md)]


