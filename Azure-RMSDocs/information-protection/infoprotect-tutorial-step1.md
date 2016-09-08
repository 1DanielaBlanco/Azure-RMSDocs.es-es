---
title: "Paso 1 del tutorial de inicio rápido de Azure Information Protection | Azure Rights Management"
description: "Paso 1 del tutorial introductorio rápido para probar Microsoft Azure Information Protection para su organización, que contiene solo 4 pasos que deberían tardar unos 10 minutos."
author: cabailey
manager: mbaldwin
ms.date: 07/291/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
translationtype: Human Translation
ms.sourcegitcommit: c9f9211e7c1dcf293caf81475515114b5433d6a7
ms.openlocfilehash: b608ee307bf7388ab7c7ed70cc1286db5df176c8


---

# Paso 1: Activación del servicio Rights Management
 
>*Se aplica a: Azure Information Protection (versión preliminar)*

**[Esta información es preliminar y está sujeta a cambios. ]**

> [!NOTE]
>Si solo quiere clasificar los datos y no protegerlos con Azure Rights Management, o si ya ha activado Azure Rights Management para su inquilino, vaya directamente al [siguiente paso](infoprotect-tutorial-step2.md). 

Con Azure Rights Management activado, puede proteger los documentos y archivos más confidenciales después de clasificarlos. Para activar Azure Rights Management, puede usar el centro de administración de Office 365 o el Portal de Azure clásico:

-   Si tiene una suscripción de Office 365 que incluya Azure Rights Management, o una suscripción de Office 365 que excluya Azure Rights Management pero tiene una suscripción de Azure RMS Premium: **use el centro de administración de Office 365**.

-   Si no tiene una suscripción a Office 365: **use el Portal de Azure clásico**.

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

Por el momento, no haga clic en **Características avanzadas**. Esto le llevará al Portal de Azure clásico, donde podrá configurar plantillas personalizadas, que no son necesarias en este tutorial. En su lugar, puede cerrar el centro de administración de Office 365.

### Para activar Rights Management desde el Portal de Azure clásico

1.  Vaya al [Portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=275081) e inicie sesión con su cuenta de administrador global de Azure Active Directory.

2.  En el panel izquierdo, haga clic en **ACTIVE DIRECTORY**.

3.  En la página **Active Directory** , haga clic en **RIGHTS MANAGEMENT**.

4.  Seleccione el directorio que administrará para [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], haga clic en **ACTIVAR** y confirme la acción.

El **ESTADO DE RIGHTS MANAGEMENT** debe indicar ahora **Activo** y la opción **ACTIVAR** debe aparecer reemplazada por **DESACTIVAR**.

Aunque puede configurar otras opciones de Rights Management en el portal, en este tutorial no es necesario, así que puede cerrar el Portal de Azure clásico.

Eso es todo lo que tiene que hacer en este primer paso. El servicio de Azure Rights Management está activado para que, más adelante en el tutorial, pueda seleccionar una de las plantillas predeterminadas de Azure Rights Management para proteger los documentos y los correos electrónicos clasificados como confidenciales.

En el caso de una implementación de producción, probablemente quiera configurar plantillas personalizadas además de (o en lugar de) las dos plantillas predeterminadas de Azure Rights Management. Pero las plantillas personalizadas no son necesarias para este tutorial, por lo que puede ir al paso 2.

|Si desea obtener más información|Información adicional|
|--------------------------------|--------------------------|
|Sobre la activación de Rights Management|[Activar Rights Management de Azure](../deploy-use/activate-service.md)|
|Acerca de las plantillas predeterminadas y del modo de crear nuevas plantillas personalizadas|[Configuración de plantillas personalizadas para Azure Rights Management](../deploy-use/configure-custom-templates.md)|

>[!div class="step-by-step"]
[&#171; Introducción](infoprotect-quick-start-tutorial.md)
[Paso 2 &#187;](infoprotect-tutorial-step2.md)



<!--HONumber=Aug16_HO4-->


