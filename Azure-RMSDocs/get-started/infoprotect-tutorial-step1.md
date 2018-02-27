---
title: "Paso 1 del tutorial de inicio rápido - AIP"
description: "Paso 1 de un tutorial de introducción para probar rápidamente Azure Information Protection: active el servicio de protección."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/21/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
ms.openlocfilehash: 952431771e89e934be4a725ece4f3d9cd47165fe
ms.sourcegitcommit: 67750454f8fa86d12772a0075a1d01a69f167bcb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2018
---
# <a name="step-1-activate-protection"></a>Paso 1: Activar la protección
 
>*Se aplica a: Azure Information Protection*

> [!NOTE]
>Aunque el servicio de Azure Rights Management esté activado para su inquilino, siga este paso para confirmar el estado de activación. Entre las instrucciones se incluye iniciar sesión en Azure Portal y crear la hoja Azure Information Protection, a fin de prepararse para el paso 2.

Cuando se activa el servicio de Azure Rights Management, puede proteger los documentos y correos electrónicos más confidenciales de la organización. También puede realizar un seguimiento de cómo se usan estos documentos protegidos cuando los comparte con otros usuarios. 

Hay diferentes métodos para activar la protección. Puede usar PowerShell y los portales de administración. Sin embargo, para este tutorial usamos Azure Portal, que es donde también se configuran las etiquetas para los usuarios. 

## <a name="to-activate-the-azure-rights-management-service"></a>Para activar el servicio Azure Rights Management

1. Inicie sesión en [Azure Portal](https://portal.azure.com) con la cuenta de administrador global del inquilino. 
    
    Si no es el administrador global, puede usar uno de los siguientes [roles administrativos](/azure/active-directory/active-directory-assign-admin-roles-azure-portal): **administrador de Information Protection** o **administrador de seguridad**.

2. En el menú del concentrador, haga clic en **Crear un recurso** y, después, en la lista **MARKETPLACE**, seleccione **Seguridad e identidad**. 
    
3.  En la hoja **Seguridad e identidad**, en la lista **APLICACIONES DESTACADAS**, seleccione **Azure Information Protection**. Después, en la hoja **Azure Information Protection**, haga clic en **Crear**.
    
    Con esta acción se crea la hoja **Azure Information Protection**, de modo que la próxima vez que inicie sesión en el portal pueda seleccionar el servicio en la lista **Todos los servicios** del concentrador. 
    
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
