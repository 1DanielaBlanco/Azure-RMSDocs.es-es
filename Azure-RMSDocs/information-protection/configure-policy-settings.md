---
title: "Configuración global de directivas para Azure Information Protection | Azure Information Protection"
description: Hay tres configuraciones en la directiva de Azure Information Protection que se aplican a todos los usuarios y todos los dispositivos.
manager: mbaldwin
ms.date: 09/14/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
translationtype: Human Translation
ms.sourcegitcommit: 801ca11da602d4acb9c398c9a89aeb33e45cb0f4
ms.openlocfilehash: d4e96321069b27ed832af3bfb6d995e0d3c5d450


---

# Configuración global de directivas para Azure Information Protection

>*Se aplica a: Azure Information Protection (versión preliminar)*

**[Esta información es preliminar y está sujeta a cambios. ]**

Hay tres configuraciones en la directiva de Azure Information Protection que se aplican a todos los usuarios y todos los dispositivos:

![Configuración global de directivas de Azure Information Protection](../media/info-protect-policy-settings.png)


Para establecer la configuración:

1. Si aún no lo ha hecho, en una nueva ventana del explorador, inicie sesión en [Azure Portal](https://portal.azure.com) y, después, navegue hasta la hoja **Azure Information Protection**. 
    
    Por ejemplo, en el menú del centro, haga clic en **Más servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. En la hoja **Azure Information Protection**, configure estos valores globales:

    - **All documents and emails must have a label** (Todos los documentos y correos electrónicos deben tener una etiqueta): cuando establece esta opción en **On** (Activado), todos los documentos guardados y correos electrónicos enviados deben tener aplicada una etiqueta. El etiquetado puede asignarlo manualmente un usuario, se puede asignar automáticamente como resultado de una [condición](configure-policy-classification.md) o asignarse de forma predeterminada (configurando la opción **Select the default label** [Seleccionar la etiqueta predeterminada]). 

    Si cuando un usuario guarda un documento o envía un correo electrónico no se asigna una etiqueta, se le pide que seleccione una etiqueta:

    ![Mensaje de Azure Information Protection si la nueva clasificación es más baja](../media/info-protect-enforce-label.png)

    - **Select the default label** (Seleccionar la etiqueta predeterminada): cuando configure esta opción, seleccione la etiqueta que se asignará a documentos y correos electrónicos que no tienen una. No se puede configurar una etiqueta como predeterminada si tiene etiquetas secundarias. 

    - **Users must provide justification to set a lower classification label, remove a label, or remove protection** (Los usuarios deben proporcionar una justificación para establecer una etiqueta de clasificación inferior, quitar una etiqueta o quitar la protección): cuando se **activa** esta opción y un usuario realiza una de estas acciones (por ejemplo, si cambia la etiqueta **Secret** por **Personal**), se solicita al usuario que indique el motivo de esta acción. Por ejemplo, el usuario podría explicar que el documento ya no contiene información confidencial. La acción y el motivo de justificación se registran en el registro de eventos local de Windows: **Aplicación** > **Microsoft Azure Information Protection**.  

    ![Mensaje de Azure Information Protection si la nueva clasificación es más baja](../media/info-protect-lower-justification.png)

    Esta opción no es aplicable a las etiquetas secundarias.

3. Para guardar los cambios, haga clic en **Guardar**.

4. Para que los cambios estén disponibles para los usuarios, haga clic en **Publicar**.

## Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organization-s-policy) (Configuración de la directiva de la organización).  












<!--HONumber=Sep16_HO3-->


