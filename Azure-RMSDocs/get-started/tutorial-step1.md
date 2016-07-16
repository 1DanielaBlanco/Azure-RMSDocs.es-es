---
title: "Tutorial de inicio rápido de Azure RMS - Paso 1 | Azure RMS"
description: "El primer paso de un tutorial para probar rápidamente Microsoft Azure Rights Management para su organización en solo 5 pasos que deberían tomarle menos de 15 minutos."
keywords: 
author: Cabailey
manager: mbaldwin
ms.date: 06/29/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.assetid: 7c4798e6-34a0-4c3f-a47f-505764ddf322
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: fab51fefed8d3a347a52ab7c118bb40b3cc23b37
ms.openlocfilehash: 80f2742bbaab9d3252cec6f6c709012ca81218d5


---



# Inicio rápido de Azure RMS; paso 1: activación del servicio Rights Management

*Se aplica a: Azure Rights Management, Office 365*


Saltar a: 
> [!div class="op_single_selector"]
- [Introducción](quick-start-tutorial.md)
- [Paso 1: Activación de Azure RMS](tutorial-step1.md)
- [Paso 2: Instalación de la aplicación RMS sharing](tutorial-step2.md)
- [Paso 3: Envío del documento confidencial por correo electrónico](tutorial-step3.md)
- [Paso 4: El destinatario lee el documento](tutorial-step4.md)
- [Paso 5: Seguimiento del documento](tutorial-step5.md)


![Paso 1 del tutorial de inicio rápido de Azure RMS](../media/AzRMS_QuickStartSteps1.PNG)

Aunque es posible que tenga una suscripción que admita la Azure Rights Management, el servicio viene desactivado de forma predeterminada. Para activarlo, puede usar el centro de administración de Office 365 o el Portal de Azure clásico:

-   Si tiene una suscripción de Office 365 que incluya Azure Rights Management, o una suscripción de Office 365 que excluya Azure Rights Management pero tiene una suscripción de Azure RMS Premium: **use el centro de administración de Office 365**.

-   Si no tiene una suscripción a Office 365: **use el Portal de Azure clásico**.

![Capturas de pantalla del paso 1 del tutorial](../media/AzRMS_Tutorial_1_Screenshots.png)

### Para activar Rights Management desde el centro de administración clásico de Office 365

> [!NOTE]
> Si usa la **versión preliminar del Centro de administración de Office 365** en lugar del centro de administración clásico de Office 365, puede usar las instrucciones de [Activación de Azure Rights Management desde la versión preliminar del Centro de administración de Office 365](../deploy-use/activate-office365-preview.md), o cambie a la versión clásica para usar estas instrucciones. Para cambiar, haga clic en **Go to the old admin center** (Ir al centro de administración antiguo) en la página **principal** después de haber iniciado sesión.

1.  Vaya al [Portal de Office 365](https://portal.office.com/) e inicie sesión con su cuenta de administrador global de Office 365.

2.  Si el centro de administración de Office 365 no se muestra automáticamente, seleccione el icono del iniciador de la aplicación en la parte superior izquierda y elija **Admin**. El icono **Admin** se muestra únicamente a los administradores de Office 365.

    > [!TIP]
    > Para obtener ayuda con el centro de administración, consulte [Sobre el Centro de administración de Office 365: ayuda para el administrador](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547).

3.  En el panel izquierdo, expanda **CONFIGURACIÓN DEL SERVICIO**.

4.  Haga clic en **Rights Management**.

5.  En la página **RIGHTS MANAGEMENT** , haga clic en **Administrar**.

6.  En la página **Rights Management** , haga clic en **Activar**.

7.  Cuando el sistema le pregunte **¿Desea activar Rights Management?**, haga clic en **Activar**.

Ahora debería ver el texto **Rights Management está activada** y la opción para desactivarla (es posible que deba actualizar la página manualmente).

Por el momento, no haga clic en **Características avanzadas**. Esto le llevará al Portal de Azure clásico, donde podrá configurar las plantillas, que no son necesarias en este tutorial. En su lugar, puede cerrar el centro de administración de Office 365.

### Para activar Rights Management desde el Portal de Azure clásico

1.  Vaya al [Portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=275081) e inicie sesión con su cuenta de administrador global de Azure Active Directory.

2.  En el panel izquierdo, haga clic en **ACTIVE DIRECTORY**.

3.  En la página **Active Directory** , haga clic en **RIGHTS MANAGEMENT**.

4.  Seleccione el directorio que administrará para [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], haga clic en **ACTIVAR** y confirme la acción.

El **ESTADO DE RIGHTS MANAGEMENT** debe indicar ahora **Activo** y la opción **ACTIVAR** debe aparecer reemplazada por **DESACTIVAR**.

Aunque puede configurar otras opciones de Rights Management en el portal, en este tutorial no es necesario, así que puede cerrar el Portal de Azure clásico.

Eso es todo lo que necesita hacer en este primer paso. El servicio está activado para que todos los usuarios de su organización puedan empezar a proteger los documentos importantes y confidenciales. En un entorno de producción, es posible que desee restringir quién puede hacer esto al inicio a fin de llevar a cabo una implementación por fases. Sin embargo, esto no es necesario para este tutorial.

Aunque las plantillas personalizadas no se incluyen aquí, probablemente desee configurar algunas en una implementación de producción. Las plantillas permiten a los usuarios aplicar rápida y fácilmente la configuración de derechos cuando necesitan proteger archivos. Al activar Rights Management, obtendrá automáticamente 2 plantillas predeterminadas, que probablemente desee complementar con sus propias plantillas personalizadas en un entorno de producción. Sin embargo, las plantillas no son necesarias para este tutorial, así que ya puede ir al paso siguiente.

|Si desea obtener más información|Información adicional|
|--------------------------------|--------------------------|
|Acerca de la activación de Rights Management y el control de quién puede proteger archivos y correo electrónico cuando el servicio está activado|[Activar Rights Management de Azure](../deploy-use/activate-service.md)|
|Acerca de las plantillas predeterminadas y del modo de crear nuevas plantillas personalizadas|[Configuración de plantillas personalizadas para Azure Rights Management](../deploy-use/configure-custom-templates.md)|


>[!div class="step-by-step"]
[« Introducción](quick-start-tutorial.md)
[Paso 2 »](tutorial-step2.md)


<!--HONumber=Jun16_HO5-->


