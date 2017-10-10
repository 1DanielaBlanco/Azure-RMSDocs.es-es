---
title: "Paso 1 del tutorial de inicio rápido - AIP"
description: "Paso 1 de un tutorial de introducción para probar rápidamente Azure Information Protection: active el servicio de protección."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
ms.openlocfilehash: 91eb9ec61f4fa1ebd7aac3cf0c244878ef450bb9
ms.sourcegitcommit: faaab68064f365c977dfd1890f7c8b05a144a95c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2017
---
# <a name="step-1-activate-protection"></a>Paso 1: Activar la protección
 
>*Se aplica a: Azure Information Protection*

> [!NOTE]
>Incluso si ya ha activado el servicio Azure Rights Management para su inquilino, realice este paso para confirmar el estado de activación. Entre las instrucciones se incluye iniciar sesión en Azure Portal y crear la hoja Azure Information Protection, a fin de prepararse para el paso 2. 

Cuando se activa el servicio Azure Rights Management, puede proteger los documentos y correos electrónicos más confidenciales de la organización y realizar un seguimiento de cómo se usan los documentos protegidos cuando los comparte con otros usuarios. Existen diferentes maneras de activar la protección, como por ejemplo, usar Windows PowerShell y los portales de administración.

Para este tutorial usaremos Azure Portal, que es donde también se configuran las etiquetas para los usuarios. 

## <a name="to-activate-the-azure-rights-management-service"></a>Para activar el servicio Azure Rights Management

1. Inicie sesión en [Azure Portal](https://portal.azure.com) como administrador global o administrador de seguridad para su inquilino.

2. En el menú del concentrador, haga clic en **Nuevo** y, después, desde la lista **MARKETPLACE**, seleccione **Seguridad e identidad**. 
    
3.  En la hoja **Seguridad e identidad**, en la lista **APLICACIONES DESTACADAS**, seleccione **Azure Information Protection**. Después, en la hoja **Azure Information Protection**, haga clic en **Crear**.
    
    Mediante esta acción se crea la hoja **Azure Information Protection**, de modo que la próxima vez que inicie sesión en el portal pueda seleccionar el servicio desde la lista **Más servicios** del centro. 
    
    > [!TIP] 
    > Seleccione **Anclar al panel** para crear un icono de **Azure Information Protection** en el panel, de modo que pueda omitir el examen del servicio la próxima vez que inicie sesión en el portal.

4. Observe la información que aparece en la página **Inicio rápido** que se abre automáticamente la primera vez que se conecta al servicio. Puede volver a esta información más adelante. Para este tutorial, seleccione **Activación de la protección**. 

5. Ahora verá si el servicio Azure Rights Management está activado para el inquilino. 
    
    - Si el servicio está activado, verá el siguiente mensaje de confirmación:
        
        ![Estado de Azure Information Protection para Azure RMS](../media/info-protect-azurerms-activated.png)
        
    - Si el servicio no está activado, lo verá en la información de estado y aparecerá la opción para activarlo:
        
        ![Estado de Azure Information Protection para Azure RMS](../media/info-protect-azurerms-deactivated.png)

6. Si el servicio no está activado, seleccione **Activar**. 

    Una vez completada la activación, en la barra de información se verá **Activation finished successfully** (La activación ha finalizado correctamente).

Eso es todo lo que tiene que hacer en este primer paso para completar el tutorial. Ahora puede ir al paso 2.

|Si desea obtener más información|Información adicional|
|--------------------------------|--------------------------|
|Sobre la activación de Rights Management|[Activar Rights Management de Azure](../deploy-use/activate-service.md)|


>[!div class="step-by-step"]
[&#171; Introducción](infoprotect-quick-start-tutorial.md)
[Paso 2 &#187;](infoprotect-tutorial-step2.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
