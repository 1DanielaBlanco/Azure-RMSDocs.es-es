---
title: Paso 3 del tutorial de inicio rápido - AIP
description: 'Paso 3 de un tutorial de introducción para probar rápidamente Azure Information Protection: instalación del cliente.'
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/18/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 209815b9-81c9-430c-a82f-32cac991449b
ms.openlocfilehash: 363902fac8036b118ce28c3ea87c812e262c3d47
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
ms.locfileid: "30206084"
---
# <a name="step-3-install-the-client"></a>Paso 3: instalar el cliente

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

En este paso, instalará el cliente de Azure Information Protection de forma que la directiva que acaba de configurar se descargará en un equipo PC de Windows y mostrará las etiquetas de las aplicaciones de Office.


## <a name="install-the-azure-information-protection-client"></a>Instalar el cliente de Azure Information Protection

1. En un equipo que tenga Office instalado (pero Word no esté abierto en estos momentos), vaya al [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) y descargue **AzInfoProtection.exe**.
    
2. Ejecute el archivo ejecutable que acaba de descargar y siga las indicaciones para instalar el cliente.
    
    Para este tutorial, no importa si selecciona la opción para instalar una directiva de demostración, porque nuestra directiva que acabamos de configurar se descargará de Azure y reemplazará la directiva de demostración si está instalada. Pero puede usar la opción de la directiva de demostración si solo quiere probar las etiquetas predeterminadas sin conectarse a Azure Information Protection. 

## <a name="verify-the-installation"></a>Comprobar la instalación

Compruebe que la instalación se ha realizado correctamente al abrir Word y un nuevo documento en blanco (no lo guarde en este momento). Si se le solicita que escriba su nombre de usuario y contraseña, escriba los detalles de la cuenta de administrador global. 

Si esta es la primera vez que ha instalado el cliente, aparecerá una página de **Enhorabuena** con instrucciones básicas. Después de leerla, haga clic en **Cerrar**.

Cuando se cargue el documento, debería ver dos cosas:

![Paso 3 del tutorial de inicio rápido de Azure Information Protection: se ha instalado el cliente](../media/word2016-calloutsv2.png)

- En la pestaña **Inicio**, un nuevo grupo **Protección**, con un botón denominado **Proteger**.
    
    Haga clic en **Proteger** > **Ayuda y comentarios** y, en el cuadro de diálogo **Microsoft Azure Information Protection**, confirme el estado del cliente. Debe aparecer **Connected as** (Conectado como) y su nombre de usuario. Asimismo, debe ver también una hora y fecha recientes de la última conexión y cuándo se instaló la directiva de Information Protection. Compruebe que el nombre de usuario que se muestra es correcto para su inquilino.

- Un nueva barra se muestra debajo de la cinta de opciones; la barra de Information Protection. Muestra el título **Sensibilidad** y las etiquetas que hemos visto en Azure Portal. 

Ahora está listo para ver Azure Information Protection en acción.

|Si desea obtener más información|Información adicional|
|--------------------------------|--------------------------|
|Sobre la instalación del cliente de Azure Information Protection|[Descarga e instalación del cliente de Azure Information Protection](../rms-client/install-client-app.md)|
|Instrucciones para administradores sobre el cliente de Azure Information Protection|[Guía de administrador de cliente de Azure Information Protection](../rms-client/client-admin-guide.md)|


>[!div class="step-by-step"]
[&#171; Paso 2](infoprotect-tutorial-step2.md)
[Paso 4 &#187;](infoprotect-tutorial-step4.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]