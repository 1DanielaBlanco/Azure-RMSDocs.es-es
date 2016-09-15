---
title: "Seguimiento y revocación de documentos cuando se usa la aplicación RMS sharing | Azure RMS"
description: "Después de haber protegido los documentos mediante la aplicación RMS sharing, puede realizar el seguimiento de cuántas personas usan tales documentos protegidos. Si es necesario, también puede revocar el acceso a estos documentos cuando ya no desee seguir compartiéndolos."
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 61f349ce-bdd2-45c1-acc5-bc83937fb187
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 44541b6fe2567d23174b26cb42fec0731f5d3f58
ms.openlocfilehash: 2117291a7204dae86b3a6d378ab6af4d84435417


---

# Seguimiento y revocación de documentos cuando se utiliza la aplicación RMS sharing

>*Se aplica a: Azure Rights Management, Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*

Una vez que haya protegido sus documentos mediante la aplicación de uso compartido de RMS, si su organización usa Azure Rights Management en lugar de Active Directory Rights Management Services, podrá hacer un seguimiento del uso que se hace de sus documentos protegidos. Si es necesario, también puede revocar el acceso a estos documentos cuando ya no desee seguir compartiéndolos. Para ello, use el **sitio de seguimiento de documentos**, al que puede tener acceso desde equipos Windows, equipos Mac e incluso tabletas y teléfonos.

<div style="padding-top: 56.25%; position: relative; width: 100%;">
<iframe style="position: absolute;top: 0;left: 0;right: 0;bottom: 0;" width="100%" height="100%" src="https://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation/player" frameborder="0" allowfullscreen></iframe>
</div>

Cuando tenga acceso a este sitio, inicie sesión para hacer un seguimiento de sus documentos. Siempre que la organización tenga una [suscripción que admite el seguimiento y la revocación de documentos](https://technet.microsoft.com/dn858608.aspx) y usted tenga asignada una licencia para esta suscripción, puede ver quién intentó abrir los documentos que protegió y si lo lograron (se autenticaron correctamente) o no. las veces que intentaron acceder al documento y su ubicación en el tiempo. Además:

-   Si quiere dejar de compartir un documento: Haga clic en **Revocar el acceso**, anote el período de tiempo que el documento seguirá estando disponible y decida si va a dejar que la gente sepa que va a revocar el acceso al documento anteriormente compartido. También, proporcione un mensaje personalizado. Al revocar un documento, no elimina el documento que ha compartido, pero los usuarios autorizados ya no podrán abrirlo.

-   Si quiere exportar a Excel: haga clic en **Exportar a CSV**, para que luego pueda modificar los datos y crear sus propias vistas y gráficos.

-   Si quiere configurar notificaciones por correo electrónico: Haga clic en **Configuración** y seleccione cómo, y si, se le notificará por correo electrónico cuando se acceda al documento.

- Si quiere realizar un seguimiento y revocar documentos compartidos para otros usuarios: los administradores de Azure RMS pueden realizar un seguimiento y revocar documentos para otros usuarios al hacer clic en el icono de administración. Solo los administradores ven este icono.

-   Si tiene alguna pregunta o quiere proporcionar comentarios sobre el sitio de seguimiento de documentos: Haga clic en el icono de ayuda para obtener acceso a [P+F sobre el seguimiento de documentos](http://go.microsoft.com/fwlink/?LinkId=523977).

## Uso de Office para tener acceso al sitio de seguimiento de documentos

-   Para las aplicaciones de Office, Word, Excel y PowerPoint: En la pestaña **Inicio** del grupo **RMS** , haga clic en **Uso compartido seguro**y luego haga clic en **Hacer seguimiento de uso**.

    ![Seguimiento de uso desde aplicaciones de Office cuando se usa la aplicación RMS sharing ](../media/ADRMS_MSRMSApp_OfficeToolbarTrackUsage.png)

-   En Outlook: En la pestaña **Inicio** , en el grupo  **RMS** , haga clic en **Hacer seguimiento de uso**:

    ![Selección del seguimiento de uso desde Outlook al usar la aplicación RMS sharing ](../media/ADRMS_MSRMSApp_OutlookTrackUsage.png)

Si no ve estas opciones de RMS, es probable que la aplicación RMS sharing no esté instalada en el equipo, que no esté instalada la última versión o que el equipo deba reiniciarse para completar la instalación. Para más información sobre cómo instalar la aplicación de uso compartido, consulte [Descarga e instalación de la aplicación Rights Management sharing](install-sharing-app.md).

> [!NOTE] 
> Si tiene instalada la versión preliminar del [cliente de Azure Information Protection](../information-protection/info-protect-client.md) (versión 1.0.233 o posterior), también puede acceder al sitio de seguimiento de documentos mediante el botón **Proteger**: 
> 
> - En una aplicación de Office, en la pestaña **Inicio**, en el grupo **Protección**, haga clic en **Proteger** > **Hacer seguimiento de uso**. 

### Otras maneras de realizar el seguimiento de los documentos y revocarlos
Además de realizar el seguimiento de los documentos en equipos Windows mediante aplicaciones de Office, también puede usar estas alternativas:

-   **Usar un explorador web**: Este método funciona en todos los dispositivos admitidos.

-   **Usar el Explorador de archivos**: Este método funciona en equipos Windows.

-   **Usar un mensaje de correo electrónico de Outlook**: Este método funciona en equipos Windows.

#### Uso de un explorador web para obtener acceso al sitio de seguimiento de documentos

-   Mediante un explorador compatible, vaya al [sitio de seguimiento de documentos](http://go.microsoft.com/fwlink/?LinkId=529562).

    Exploradores admitidos: Se recomienda usar por lo menos la versión 10 de Internet Explorer, pero puede usar cualquiera de los siguientes exploradores para el sitio de seguimiento de documentos:

    -   Internet Explorer: La versión 10 como mínimo

    -   Internet Explorer 9 con al menos MS12-037: Actualización de seguridad acumulativa para Internet Explorer:: June 12, 2012

    -   Mozilla Firefox: La versión 12 como mínimo

    -   Apple Safari 5: La versión 5 como mínimo

    -   Google Chrome: La versión 18 como mínimo

#### Uso del Explorador de archivos para obtener acceso al sitio de seguimiento de documentos

-   Haga clic con el botón derecho en el archivo, seleccione **Proteger con RMS** y, luego, **Hacer seguimiento de uso**.

    ![Selección del seguimiento de uso desde Explorer al usar la aplicación RMS sharing](../media/ADRMS_MSRMSApp_ExplorerTrackUsage.png)

#### Uso de un mensaje de correo electrónico de Outlook para obtener acceso al sitio de seguimiento de documentos

-   En un mensaje de correo electrónico, en la pestaña **Mensaje** , vaya al grupo  **RMS** y haga clic en **Uso compartido protegido**y, luego, en **Hacer seguimiento de uso**:

    ![Selección del seguimiento de uso desde Outlook al usar la aplicación RMS sharing](../media/ADRMS_MSRMSApp_OutlookMessageTrackUsage.png)

## Ejemplos y otras instrucciones
Para obtener ejemplos de cómo puede usar la aplicación para uso compartido de Rights Management e instrucciones de procedimientos, consulte las siguientes secciones de la guía de usuario de la aplicación para uso compartido de Rights Management:

-   [Ejemplos de uso de la aplicación RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [¿Qué desea hacer?](sharing-app-user-guide.md#what-do-you-want-to-do)

## Véase también
[Guía de usuario de la aplicación de uso compartido Rights Management](sharing-app-user-guide.md)



<!--HONumber=Aug16_HO4-->


