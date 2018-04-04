---
title: Seguimiento y revocación de documentos - Azure Information Protection
description: Una vez protegidos los documentos, puede realizar un seguimiento de como los usan las personas. Si es necesario, también puede revocar el acceso a estos documentos si las personas ya no pueden leerlos.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 84f5f0ed8b98895b8c056ff03295afef379e6b74
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="user-guide-track-and-revoke-your-documents-when-you-use-azure-information-protection"></a>Guía del usuario: Seguimiento y revocación de documentos cuando se usa Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8 y Windows 7 con SP1*

Una vez protegidos los documentos mediante Azure Information Protection, puede realizar el seguimiento de cómo los usan las personas. Si es necesario, también puede revocar el acceso a ellos si las personas ya no pueden leerlos. Para ello, utilice el **sitio de seguimiento de documentos**. Puede obtener acceso a este sitio desde equipos Windows y Mac e incluso tabletas y teléfonos.

Cuando tenga acceso a este sitio, inicie sesión para hacer un seguimiento de sus documentos. Si la organización tiene una [suscripción que admite el seguimiento y la revocación de documentos](https://www.microsoft.com/cloud-platform/azure-information-protection-features) y usted tiene asignada una licencia para esta suscripción, puede ver quién intentó abrir los documentos que protegió y si lo lograron (se autenticaron correctamente) o no. También verá cada intento de acceso al documento y su ubicación en ese momento. Además:

- Si necesita dejar de compartir un documento: 
    
    - Haga clic en **Revocar acceso**. Fíjese en el período de tiempo en el que el documento sigue disponible. Decida si quiere permitir a los usuarios saber que revocará el acceso al documento que ha compartido anteriormente mediante un mensaje personalizado. Al revocar un documento, no se elimina el documento que se ha compartido, pero los usuarios autorizados ya no pueden abrirlo:
        
        ![Icono de revocación de acceso en el sitio de Seguimiento de documentos](../media/tracking-site-revoke-access-icon.png)
        
- Si desea exportar a Excel: 
    
    - Haga clic en **Exportar a CSV** para que pueda modificar los datos y crear sus propias vistas y gráficos:
         
        ![Icono Exportar a CSV en el sitio de Seguimiento de documentos](../media/tracking-site-export-icon.png)
         
- Si desea configurar notificaciones por correo electrónico: 
     
    - Haga clic en **Configuración** y seleccione si se le enviará un correo electrónico cuando se acceda a los documentos y cómo:
        
        ![Icono Exportar a CSV en el sitio de Seguimiento de documentos](../media/tracking-site-settings-email.png)

- Si desea hacer seguimiento de los documentos compartidos y revocarlos para otros usuarios:
    
    - Los administradores de Azure Information Protection pueden hacer clic en el icono Administrador para hacer un seguimiento de los documentos protegidos y revocarlos para otros usuarios cuando estos hayan registrado sus documentos en el sitio de seguimiento de documentos. Solo los administradores ven este icono:
        
        ![Icono Administrador en el sitio de Seguimiento de documentos](../media/tracking-site-admin-icon.png)
        
        Si no ve este icono, a pesar de ser un administrador global, es porque aún no ha compartido ningún documento. En este caso, use la siguiente dirección URL para acceder al sitio de seguimiento de documentos: https://portal.azurerms.com/#/admin

A menos que sea administrador, solo puede hacer seguimiento y revocar los documentos que protegió. No puede hacer seguimiento de los correos electrónicos que protegió mediante el sitio de seguimiento de documentos.

> [!NOTE] 
> Si el administrador configuró controles de privacidad para el sitio de seguimiento de documentos, es posible que no vea cuando los usuarios de la organización tengan acceso a un documento al que hace seguimiento. Un administrador puede excluir a todos los usuarios o solo a algunos de ellos. Sin embargo, siempre puede revocar el acceso a los documentos a los que hace seguimiento.

Para hacer seguimiento de un documento que protegió, debe usar el equipo Windows para registrarlo con el sitio de seguimiento de documentos. Para ello, utilice el Explorador de archivos o las aplicaciones de Office.

## <a name="using-office-to-track-or-revoke-the-document"></a>Uso de Office para realizar un seguimiento del documento o revocarlo

Para las aplicaciones de Office, Word, Excel y PowerPoint: 

1. Abra el documento protegido del que desea realizar un seguimiento o que desea revocar.

2. En la pestaña **Inicio**, en el grupo **Protección**, haga clic en **Proteger** > **Realizar un seguimiento y revocar**:

    ![Opción realizar seguimiento](../media/track-usage-callout.png)
    
    Si no ve estas opciones en las aplicaciones de Office, es posible que sea debido a una de estas razones:
    
    - El cliente de Azure Information Protection no está instalado en su equipo.
    
    - Hay que reiniciar las aplicaciones de Office.
    
    - El equipo debe reiniciarse para finalizar la instalación.
    
Para más información sobre cómo instalar el cliente de Azure Information Protection, consulte [Descarga e instalación del cliente de Azure Information Protection](install-client-app.md).

## <a name="using-file-explorer-to-track-or-revoke-the-document"></a>Uso del Explorador de archivos para realizar un seguimiento del documento o revocarlo

1. Haga clic con el botón derecho en el archivo protegido y seleccione **Clasificar y proteger**.

2. En el cuadro de diálogo **Clasificar y proteger: Azure Information Protection**, seleccione **Realizar un seguimiento y revocar**.

    ![Icono de Realizar un seguimiento y revocar en el cuadro de diálogo Clasificar y proteger: Azure Information Protection](../media/track-and-revoke.png)


### <a name="using-a-web-browser-to-track-and-revoke-documents-that-you-have-registered"></a>Uso de un explorador web para realizar un seguimiento de documentos que ha registrado y revocarlos

Después de haber registrado el documento protegido mediante el uso de las aplicaciones de Office o del Explorador de archivos, puede realizar un seguimiento de ellos y revocarlos mediante un explorador web compatible:

- Para un equipo con Windows, un equipo Mac o un dispositivo móvil, visite el [sitio de Seguimiento de documentos](https://go.microsoft.com/fwlink/?LinkId=529562).

    **Exploradores admitidos**: se recomienda usar por lo menos la versión 10 de Internet Explorer, pero puede usar cualquiera de los siguientes exploradores para el sitio de Seguimiento de documentos:

    - Internet Explorer: La versión 10 como mínimo

    - Internet Explorer 9 con al menos MS12-037: Actualización de seguridad acumulativa para Internet Explorer:: June 12, 2012

    - Mozilla Firefox: La versión 12 como mínimo

    - Apple Safari 5: La versión 5 como mínimo

    - Google Chrome: La versión 18 como mínimo


## <a name="other-instructions"></a>Otras instrucciones
Puede encontrar más instrucciones sobre procedimientos en la guía del usuario de Azure Information Protection:

- [¿Qué desea hacer?](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Información adicional para los administradores    
Consulte [Configuración y uso de Seguimiento de documentos para Azure Information Protection](client-admin-guide-document-tracking.md) en la [guía del administrador](client-admin-guide.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]