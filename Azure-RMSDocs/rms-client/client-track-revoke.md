---
title: "Seguimiento y revocación de documentos - Azure Information Protection"
description: "Una vez protegidos los documentos, puede realizar un seguimiento de como los usan las personas. Si es necesario, también puede revocar el acceso a estos documentos si las personas ya no pueden leerlos."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: a79c6d1ff5b3a031138cb3d4dde179909134353a
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="track-and-revoke-your-documents-when-you-use-azure-information-protection"></a>Seguimiento y revocación de documentos cuando se usa Azure Information Protection

>*Se aplica a: Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*

Una vez protegidos los documentos mediante Azure Information Protection, puede realizar el seguimiento de cómo los usan las personas. Si es necesario, también puede revocar el acceso a ellos si las personas ya no pueden leerlos. Para ello, use el **sitio de seguimiento de documentos**, al que puede tener acceso desde equipos Windows, equipos Mac e incluso tabletas y teléfonos.

Cuando tenga acceso a este sitio, inicie sesión para hacer un seguimiento de sus documentos. Siempre que la organización tenga una [suscripción que admite el seguimiento y la revocación de documentos](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features) y usted tenga asignada una licencia para esta suscripción, puede ver quién intentó abrir los documentos que protegió y si lo lograron (se autenticaron correctamente) o no. También verá cada intento de acceso al documento y su ubicación en ese momento. Además:

-   Si quiere dejar de compartir un documento: Haga clic en **Revocar el acceso**, anote el período de tiempo que el documento seguirá estando disponible y decida si va a dejar que la gente sepa que va a revocar el acceso al documento anteriormente compartido. También, proporcione un mensaje personalizado. Al revocar un documento, no se elimina el documento que se ha compartido, pero los usuarios autorizados ya no podrán abrirlo:
    
    ![Icono de revocación de acceso en el sitio de Seguimiento de documentos](../media/tracking-site-revoke-access-icon.png)

-   Si quiere exportar a Excel: haga clic en **Exportar a CSV**, para que luego pueda modificar los datos y crear sus propias vistas y gráficos:
    
    ![Icono Exportar a CSV en el sitio de Seguimiento de documentos](../media/tracking-site-export-icon.png)

-   Si quiere configurar notificaciones por correo electrónico: haga clic en **Configuración** y seleccione cómo, y si, se le notificará por correo electrónico cuando se acceda al documento:
    
    ![Icono Exportar a CSV en el sitio de Seguimiento de documentos](../media/tracking-site-settings-email.png)

- Si quiere realizar un seguimiento de los documentos compartidos y revocarlos para otros usuarios: los administradores de Azure Information Protection pueden realizar un seguimiento y revocar los documentos protegidos para otros haciendo clic en el icono Administrador. Solo los administradores ven este icono:
    
    ![Icono Administrador en el sitio de Seguimiento de documentos](../media/tracking-site-admin-icon.png)

Para realizar el seguimiento de un documento protegido, debe registrarse en el sitio de Seguimiento de documentos. Para ello, utilice el Explorador de archivos o las aplicaciones de Office.

## <a name="using-office-to-track-or-revoke-the-document"></a>Uso de Office para realizar un seguimiento del documento o revocarlo

Para las aplicaciones de Office, Word, Excel y PowerPoint: 

1. Abra el documento protegido del que desea realizar un seguimiento o que desea revocar.

2. En la pestaña **Inicio**, en el grupo **Protección**, haga clic en **Proteger** > **Realizar un seguimiento y revocar**:

    ![Opción realizar seguimiento](../media/track-usage-callout.png)

Si estas opciones no aparecen en sus aplicaciones de Office, es probable que el cliente de Azure Information Protection no esté instalado en su equipo, que deba reiniciar dichas aplicaciones o que deba reiniciar el equipo para finalizar la instalación. Para más información sobre cómo instalar el cliente de Azure Information Protection, consulte [Descarga e instalación del cliente de Azure Information Protection](install-client-app.md).

## <a name="using-file-explorer-to-track-or-revoke-the-document"></a>Uso del Explorador de archivos para realizar un seguimiento del documento o revocarlo

1. Haga clic con el botón derecho en el archivo protegido y seleccione **Clasificar y proteger**.

2. En el cuadro de diálogo **Clasificar y proteger: Azure Information Protection**, seleccione **Realizar un seguimiento y revocar**.

    ![Icono de Realizar un seguimiento y revocar en el cuadro de diálogo Clasificar y proteger: Azure Information Protection](../media/track-and-revoke.png)


### <a name="using-a-web-browser-track-and-revoke-documents-that-you-have-registered"></a>Uso de un explorador web para realizar un seguimiento de documentos que ha registrado y revocarlos

Después de haber registrado el documento protegido mediante el uso de las aplicaciones de Office o del Explorador de archivos, puede realizar un seguimiento de ellos y revocarlos mediante un explorador web compatible:

- Para un equipo con Windows, un equipo Mac o un dispositivo móvil, visite el [sitio de Seguimiento de documentos](https://go.microsoft.com/fwlink/?LinkId=529562).

    **Exploradores admitidos**: se recomienda usar por lo menos la versión 10 de Internet Explorer, pero puede usar cualquiera de los siguientes exploradores para el sitio de Seguimiento de documentos:

    -   Internet Explorer: La versión 10 como mínimo

    -   Internet Explorer 9 con al menos MS12-037: Actualización de seguridad acumulativa para Internet Explorer:: June 12, 2012

    -   Mozilla Firefox: La versión 12 como mínimo

    -   Apple Safari 5: La versión 5 como mínimo

    -   Google Chrome: La versión 18 como mínimo


## <a name="other-instructions"></a>Otras instrucciones
Puede encontrar más instrucciones sobre procedimientos en la guía del usuario de Azure Information Protection:

- [¿Qué desea hacer?](client-user-guide.md#what-do-you-want-to-do)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]