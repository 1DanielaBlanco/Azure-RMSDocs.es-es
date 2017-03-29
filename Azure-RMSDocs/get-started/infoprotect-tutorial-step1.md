---
title: "Paso 1 del tutorial de inicio rápido - AIP"
description: "Paso 1 de un tutorial de introducción para probar rápidamente Azure Information Protection: activación del servicio Azure Rights Management."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
ms.openlocfilehash: 8ccf0ea41e9465e10408595a3b875704baca93d2
ms.sourcegitcommit: f0402cf14506b4c61a156a2baf7e69b7b16883a1
translationtype: HT
---
# <a name="step-1-activate-the-rights-management-service"></a>Paso 1: Activación del servicio Rights Management
 
>*Se aplica a: Azure Information Protection*

> [!NOTE]
>Si sabe que el servicio Azure Rights Management ya está activado para el inquilino, vaya directamente al [siguiente paso](infoprotect-tutorial-step2.md). 
>
>Si no está seguro de si este servicio está o no activado, siga las instrucciones de este paso para comprobarlo.

Cuando se activa el servicio Azure Rights Management, puede proteger los documentos y correos electrónicos más confidenciales de la organización y realizar un seguimiento de cómo se usan los documentos protegidos cuando los comparte con otros usuarios. Existen diferentes maneras de activar este servicio, como usar Windows PowerShell y los portales de administración.

Para este tutorial, vaya directamente a la página de activación en el portal de administración para administradores de Office 365. Se trata de la misma página que para el portal clásico de Office 365 y la versión preliminar del centro de administración de Office 365. 

Si prefiere navegar por esta página del Portal de administración de Office 365 en lugar de ir directamente a la página, vea las instrucciones completas de [Activar Azure Rights Management](../deploy-use/activate-service.md). Asimismo, use estas instrucciones completas si tiene acceso a Azure Portal pero no al Portal de administración de Office 365.

## <a name="to-activate-the-rights-management-service"></a>Para activar el servicio de Rights Management

1. Abra una nueva ventana del explorador y vaya directamente a la [página de activación de Rights Management](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) para administradores de Office 365.
    
    Si se le solicita que inicie sesión, use una cuenta de administrador global de Office 365.

2. En la página **Rights Management** , haga clic en **Activar**. Si este botón muestra **desactivar**, el servicio ya está activado, y puede ir directamente al [siguiente paso](infoprotect-tutorial-step2.md). 

    ![Paso 1 del tutorial de inicio rápido de Azure Information Protection: activar el servicio](../media/info-protect-activate.png)

3. Cuando se le pregunte **¿Desea activar Rights Management?**, haga clic en **activar** para confirmar.

    Ahora debería ver el texto **Rights Management está activada** y la opción para desactivarla (es posible que deba actualizar la página manualmente).

    Por el momento, no haga clic en **Características avanzadas**. Esto le llevará al Portal de Azure clásico, donde podrá configurar plantillas personalizadas, que no son necesarias en este tutorial. En su lugar, puede cerrar esta página.

Eso es todo lo que tiene que hacer en este primer paso para completar el tutorial. En el caso de una implementación de producción, probablemente quiera configurar plantillas personalizadas además de (o en lugar de) las dos plantillas predeterminadas de Azure Rights Management. Pero las plantillas personalizadas no son necesarias para este tutorial, por lo que puede ir al paso 2.

|Si desea obtener más información|Información adicional|
|--------------------------------|--------------------------|
|Sobre la activación de Rights Management|[Activar Rights Management de Azure](../deploy-use/activate-service.md)|
|Acerca de las plantillas predeterminadas y del modo de crear nuevas plantillas personalizadas|[Configuración de plantillas personalizadas para el servicio Azure Rights Management](../deploy-use/configure-custom-templates.md)|

>[!div class="step-by-step"]
[&#171; Introducción](infoprotect-quick-start-tutorial.md)
[Paso 2 &#187;](infoprotect-tutorial-step2.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
