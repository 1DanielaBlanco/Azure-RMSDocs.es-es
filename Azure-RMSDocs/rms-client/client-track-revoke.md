---
title: "Seguimiento y revocación de documentos protegidos cuando se usa Azure Information Protection | Azure Information Protection"
description: "Una vez protegidos los documentos, puede realizar un seguimiento de como los usan las personas. Si es necesario, también puede revocar el acceso a estos documentos si las personas ya no pueden leerlos."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 1107f484f204e64d76c389daef4d9decbfbb20e8
ms.openlocfilehash: e83d0352003fa3790fd4f8d5c59f4f7b40ef4265


---

# <a name="track-and-revoke-your-documents-when-you-use-azure-information-protection"></a>Seguimiento y revocación de documentos cuando se usa Azure Information Protection

>*Se aplica a: Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*

**[Esta versión del cliente está en versión preliminar y sujeta a cambios.]**

Una vez protegidos los documentos mediante Azure Information Protection, puede realizar el seguimiento de cómo los usan las personas. Si es necesario, también puede revocar el acceso a ellos si las personas ya no pueden leerlos. Para ello, use el **sitio de seguimiento de documentos**, al que puede tener acceso desde equipos Windows, equipos Mac e incluso tabletas y teléfonos.

<div style="padding-top: 56.25%; position: relative; width: 100%;">
<iframe style="position: absolute;top: 0;left: 0;right: 0;bottom: 0;" width="100%" height="100%" src="https://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation/player" frameborder="0" allowfullscreen></iframe>
</div>

Cuando tenga acceso a este sitio, inicie sesión para hacer un seguimiento de sus documentos. Siempre que la organización tenga una [suscripción que admite el seguimiento y la revocación de documentos](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features) y usted tenga asignada una licencia para esta suscripción, puede ver quién intentó abrir los documentos que protegió y si lo lograron (se autenticaron correctamente) o no. También verá cada intento de acceso al documento y su ubicación en ese momento. Además:

-   Si quiere dejar de compartir un documento: Haga clic en **Revocar el acceso**, anote el período de tiempo que el documento seguirá estando disponible y decida si va a dejar que la gente sepa que va a revocar el acceso al documento anteriormente compartido. También, proporcione un mensaje personalizado. Al revocar un documento, no se elimina el documento que se ha compartido, pero los usuarios autorizados ya no podrán abrirlo.

-   Si quiere exportar a Excel: haga clic en **Exportar a CSV**, para que luego pueda modificar los datos y crear sus propias vistas y gráficos.

-   Si quiere configurar notificaciones por correo electrónico: Haga clic en **Configuración** y seleccione cómo, y si, se le notificará por correo electrónico cuando se acceda al documento.

- Si quiere realizar un seguimiento de los documentos compartidos y revocarlos para otros usuarios: los administradores de Azure Information Protection pueden realizar un seguimiento y revocar los documentos protegidos para otros haciendo clic en el icono Administrador. Solo los administradores ven este icono.

-   Si tiene alguna pregunta o quiere proporcionar comentarios sobre el sitio de seguimiento de documentos: Haga clic en el icono de ayuda para obtener acceso a [P+F sobre el seguimiento de documentos](http://go.microsoft.com/fwlink/?LinkId=523977).

## <a name="using-office-to-access-the-document-tracking-site"></a>Uso de Office para tener acceso al sitio de seguimiento de documentos

-   Para las aplicaciones de Office, Word, Excel, PowerPoint y Outlook: en la pestaña **Inicio** del grupo **Protección**, haga clic en **Proteger** > **Track usage** (Seguimiento del uso).

Si estas opciones no aparecen en sus aplicaciones de Office, es probable que el cliente de Azure Information Protection no esté instalado en su equipo, que deba reiniciar dichas aplicaciones o que deba reiniciar el equipo para finalizar la instalación. Para más información sobre cómo instalar el cliente de Azure Information Protection, consulte [Descarga e instalación del cliente de Azure Information Protection](install-client-app.md).


### <a name="other-ways-to-track-and-revoke-your-documents"></a>Otras maneras de realizar el seguimiento de los documentos y revocarlos
Además de realizar el seguimiento de los documentos en equipos Windows mediante aplicaciones de Office, también puede usar estas alternativas:

-   **Usar un explorador web**: Este método funciona en todos los dispositivos admitidos.

-   **Usar el Explorador de archivos**: Este método funciona en equipos Windows.

#### <a name="using-a-web-browser-to-access-the-doc-tracking-site"></a>Uso de un explorador web para obtener acceso al sitio de seguimiento de documentos

-   Mediante un explorador compatible, vaya al [sitio de seguimiento de documentos](https://go.microsoft.com/fwlink/?LinkId=529562).

    Exploradores admitidos: Se recomienda usar por lo menos la versión 10 de Internet Explorer, pero puede usar cualquiera de los siguientes exploradores para el sitio de seguimiento de documentos:

    -   Internet Explorer: La versión 10 como mínimo

    -   Internet Explorer 9 con al menos MS12-037: Actualización de seguridad acumulativa para Internet Explorer:: June 12, 2012

    -   Mozilla Firefox: La versión 12 como mínimo

    -   Apple Safari 5: La versión 5 como mínimo

    -   Google Chrome: La versión 18 como mínimo

#### <a name="using-file-explorer-to-access-the-doc-tracking-site"></a>Uso del Explorador de archivos para obtener acceso al sitio de seguimiento de documentos

-   Haga clic con el botón derecho en el archivo, seleccione **Classify and protect (preview)** (Clasificar y proteger [versión preliminar]) y en **Azure Information Protection Viewer**, seleccione el icono Track Usage (Seguimiento del uso).


## <a name="other-instructions"></a>Otras instrucciones
Para obtener instrucciones sobre procedimientos, consulte las siguientes secciones de la guía de usuario de Azure Information Protection:

-   [¿Qué desea hacer?](client-user-guide.md#what-do-you-want-to-do)





<!--HONumber=Dec16_HO1-->


