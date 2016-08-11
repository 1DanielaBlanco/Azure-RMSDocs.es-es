---
title: "Configuración de una etiqueta para aplicar protección de Rights Management | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
translationtype: Human Translation
ms.sourcegitcommit: 00b4cd2b1e7b1196cedd39d7052db534e781bb13
ms.openlocfilehash: 7a20b59c404959c4ec209e8c29ac61ab71233e87


---

# Configuración de una etiqueta para aplicar protección de Rights Management

>*Se aplica a: Azure Information Protection (versión preliminar)*

**[Esta información es preliminar y está sujeta a cambios. ]**

Puede proteger sus documentos y correos electrónicos más confidenciales mediante Azure Rights Management. Esta aplicación utiliza directivas de autorización, identidad y cifrado para ayudar a evitar la pérdida de datos. Esta protección se aplica al configurar una etiqueta para usar una plantilla de Rights Management. 

Esta plantilla puede ser una de las plantillas predeterminadas que se crean automáticamente al activar Azure Rights Management o una plantilla personalizada. Las plantillas departamentales se admiten pero solo aplican la protección cuando el autor del documento o del correo electrónico está dentro del ámbito de la plantilla. Si el usuario no está dentro del ámbito, verá un mensaje para indicar que Azure Information Protection no puede aplicar la etiqueta.

## Funcionamiento de la protección

Cuando un documento o un correo electrónico están protegidos con Azure Rights Management, se cifran en reposo y en tránsito y solo los usuarios autorizados pueden descifrarlos. Este cifrado permanece con el documento o el correo electrónico, incluso si se cambia de nombre. Además, puede configurar derechos y restricciones de uso, como en los ejemplos siguientes:

- Solo los usuarios de su organización pueden abrir el documento o el correo electrónico.

- Solo los usuarios del departamento de marketing pueden editar e imprimir el documento o el correo electrónico, mientras que los demás usuarios de su organización solo pueden verlo.

- Los usuarios no pueden reenviar un correo electrónico.

- Los documentos o los correos electrónicos que se envían a socios comerciales no se pueden abrir después de una fecha especificada.

Para más información sobre las plantillas y cómo configurar estos derechos y restricciones de uso, consulte [Configuración de plantillas personalizadas para Azure Rights Management](../deploy-use/configure-custom-templates.md).

Para más información sobre Azure Rights Management y cómo funciona, consulte [¿Qué es Azure Rights Management?](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> Para configurar una etiqueta para aplicar la protección de Rights Management, se debe activar el servicio Azure Rights Management para su organización. Si aún no lo ha hecho, consulte [Activación de Azure Rights Management](../deploy-use/activate-service.md).


## Para configurar una etiqueta para aplicar la protección de Rights Management

1. Inicie sesión en el [Portal de Azure](https://portal.azure.com).
 
2. En el menú del concentrador, haga clic en **Examinar** y comience a escribir **Información** en el cuadro Filtro. Seleccione **Azure Information Protection**.

3. En la hoja **Azure Information Protection**, seleccione la etiqueta que quiere configurar para aplicar la protección de Rights Management.

4. En la hoja **Etiqueta**, en la sección **Set RMS template for protecting documents and emails containing this label** (Configuración de la plantilla de RMS para proteger documentos y correos electrónicos que contienen esta etiqueta), realice la siguiente configuración:

    - Si se muestra **Select RMS template from** (Seleccionar plantilla de RMS de): seleccione **Azure RMS**. 
    
        No seleccione **AD RMS** ni las opciones de configuración asociadas sin ayuda de Microsoft. Si está interesado en probar Azure Information Protection con Active Directory Rights Management Services, envíe un correo electrónico a askipteam@microsoft.com. 
    
    - En **Select RMS template** (Seleccionar plantilla de RMS): haga clic en el cuadro desplegable y seleccione la plantilla que quiere usar para proteger documentos y correos electrónicos con esta etiqueta.

        > [!NOTE] Si crea una nueva plantilla después de abrir la hoja **Etiqueta**, cierre esta hoja y vuelva al paso 3, así la plantilla recién creada se recuperará de Azure para que la seleccione.

5. Haga clic en **Guardar**.

6. Para que los cambios estén disponibles para los usuarios, en la hoja **Azure Information Protection**, haga clic en **Publicar**.

## Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organization-s-policy) (Configuración de la directiva de la organización).  



<!--HONumber=Jul16_HO5-->


