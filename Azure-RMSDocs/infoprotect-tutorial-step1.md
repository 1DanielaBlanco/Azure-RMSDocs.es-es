---
title: Paso 1 del tutorial de inicio rápido - AIP
description: 'Paso 1 de un tutorial de introducción para probar rápidamente Azure Information Protection: active el servicio de protección.'
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/28/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
ms.openlocfilehash: 82a3f71a4c1bb99fc4d0af74f49dd43a706cb132
ms.sourcegitcommit: 26a2c1becdf3e3145dc1168f5ea8492f2e1ff2f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2018
ms.locfileid: "44147702"
---
# <a name="step-1-activate-protection"></a>Paso 1: Activar la protección
 
>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

> [!NOTE]
>Aunque la protección esté activada para su inquilino, siga este paso para confirmar el estado de activación. Entre las instrucciones se incluye iniciar sesión en Azure Portal y crear la hoja Azure Information Protection, a fin de prepararse para el paso 2.

Cuando se activa la protección en Azure Information Protection, puede proteger los documentos y correos electrónicos más confidenciales de la organización. También puede realizar un seguimiento de cómo se usan estos documentos protegidos cuando los comparte con otros usuarios. 

Hay diferentes métodos para activar la protección. Puede usar PowerShell y los portales de administración. Sin embargo, para este tutorial usamos Azure Portal, que es donde también se configuran las etiquetas para los usuarios. 

## <a name="to-activate-protection"></a>Para activar la protección

1. Inicie sesión en [Azure Portal](https://portal.azure.com) con la cuenta de administrador global del inquilino. 
    
    Si no es el administrador global, puede usar uno de los siguientes [roles administrativos](/azure/active-directory/active-directory-assign-admin-roles-azure-portal): **administrador de Information Protection** o **administrador de seguridad**.

2. En el menú del concentrador, seleccione **Crear un recurso** y, a continuación, en el cuadro de búsqueda de Marketplace, escriba **Azure Information Protection**. 
    
3. En la lista de resultados, seleccione **Azure Information Protection**. En la hoja **Azure Information Protection**, haga clic en **Crear**.
    
    > [!TIP] 
    > Opcionalmente, seleccione **Anclar al panel** para crear un icono de **Azure Information Protection** en el panel, de modo que pueda omitir el examen del servicio la próxima vez que inicie sesión en el portal.
    
    Haga clic en **Crear** de nuevo.

4. Observe la información que aparece en la página **Inicio rápido** que se abre automáticamente la primera vez que se conecta al servicio. Puede volver a esta información más adelante. Para este tutorial, seleccione **ADMINISTRAR** > **Activación de la protección**. 

5. Ahora verá si la protección está activada para el inquilino. 
    
    - Si la protección está activada, verá el siguiente mensaje de confirmación:
        
        ![Estado de Azure Information Protection para Azure RMS](./media/info-protect-azurerms-activated.png)
        
    - Si la protección no está activada, lo verá en la información de estado y se mostrará la opción para activarlo:
        
        ![Estado de Azure Information Protection para Azure RMS](./media/info-protect-azurerms-deactivated.png)

6. Si la protección no está activada, seleccione **Activar**. 

    Una vez completada la activación, en la barra de información se verá **Activation finished successfully** (La activación ha finalizado correctamente).

Eso es todo lo que tiene que hacer en este primer paso para completar el tutorial. Ahora puede ir al paso 2.

|Si desea obtener más información|Información adicional|
|--------------------------------|--------------------------|
|Acerca de cómo activar la protección|[Activar Rights Management de Azure](activate-service.md)|


>[!div class="step-by-step"]
[&#171; Introducción](infoprotect-quick-start-tutorial.md)
[Paso 2 &#187;](infoprotect-tutorial-step2.md)

