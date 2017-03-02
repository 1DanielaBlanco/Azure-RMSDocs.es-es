---
title: "Modo de solo protección para Azure Information Protection"
description: "Información para los usuarios que ejecutan el cliente de Azure Information Protection en modo de solo protección."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 16042717-0d7a-41f5-87e3-12826fda35df
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 55254496b23e49fe7e2dbd19721a824739004b21
ms.lasthandoff: 02/24/2017


---

# <a name="protection-only-mode-for-the-azure-information-protection-client"></a>Modo de solo protección para el cliente de Azure Information Protection

Cuando se ejecuta el cliente de Azure Information Protection sin una directiva de Azure Information Protection, se muestra en modo de **solo protección**. Por ejemplo, si utiliza el Explorador de archivos de Windows, haga clic con el botón derecho en **Clasificar y proteger**:

![Modo de solo protección](../media/protection-only-mode.png)

 Este modo se ejecuta en los siguientes escenarios:

- La organización no tiene una suscripción para Azure Information Protection (para clasificación y protección de datos), pero tiene una suscripción para el servicio Azure Rights Management (para protección de datos con Office 365). 
    - Este es un escenario admitido y puede usar el cliente de Azure Information Protection para proteger archivos y ver los archivos protegidos.

- La organización tiene una suscripción para Azure Information Protection, pero no puede descargar la directiva de Azure Information Protection. 
    - Esto puede suceder debido a una configuración incorrecta o porque el inicio de sesión no es correcto. Póngase en contacto con el Servicio de asistencia o el administrador, pero, mientras tanto, puede usar el cliente de Azure Information Protection para proteger archivos y ver los archivos protegidos.

## <a name="limitations-for-protection-only-mode"></a>Limitaciones para el modo de solo protección

- En las aplicaciones de Office, no se muestra la barra de Azure Information Protection. Al hacer clic en **Proteger** > **Mostrar barra**, esta opción de menú no está disponible.

- Cuando se usa el cuadro de diálogo **Clasificar y proteger: Azure Information Protection** con el Explorador de archivos, no ve las etiquetas de clasificación. En su lugar, como se muestra en la imagen anterior, verá una opción para seleccionar plantillas de Rights Management (RMS). 

## <a name="supported-tasks-for-protection-only-mode"></a>Tareas admitidas para el modo de solo protección

- Proteger (y desproteger) documentos y correos electrónicos desde aplicaciones de Office mediante la característica Information Rights Management (IRM) de Office; por ejemplo: haga clic en **Archivo** > **Información** > **Proteger documento** > **Restringir acceso**. Para más información, vea [Uso de protección de la información con Office 365, Office 2016 u Office 2013](../deploy-use/help-users.md).

- Proteger (y desproteger) archivos con el Explorador de archivos de Windows: haga clic con el botón derecho en el archivo, los archivos o la carpeta > **Clasificar y proteger**. Para aplicar la protección que ha configurado el administrador, en el cuadro de diálogo **Clasificar y proteger: Azure Information Protection**, haga clic en **Seleccionar plantilla** y elija una de las plantillas disponibles.

- Ver los archivos protegidos mediante el visor de Azure Information Protection.

- Acceder al sitio de Seguimiento de documentos desde las aplicaciones de Office. Sin embargo, debe tener una suscripción válida para realizar un seguimiento de los documentos y revocarlos desde este sitio.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]  

