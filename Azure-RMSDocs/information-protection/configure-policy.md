---
title: "Configuración de la directiva de Azure Information Protection | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 08/08/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 781632c5a28377339431cd6537b1b9e11d0a3259
ms.openlocfilehash: 0e31053a83c30d8552cfb78914d0d13baac25f42


---

# Configuración de la directiva de Azure Information Protection

>*Se aplica a: Azure Information Protection (versión preliminar)*

**[Esta información es preliminar y está sujeta a cambios. ]**

Para configurar la protección, la clasificación y el etiquetado, debe configurar la directiva de Azure Information Protection. Esta directiva se descarga luego en los equipos que tienen instalado el [cliente de Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Para configurar la directiva de Azure Information Protection durante la versión preliminar de Azure Information Protection:

1. Inicie sesión en el [Portal de Azure](https://portal.azure.com).

2. Vaya a la hoja **Azure Information Protection**: por ejemplo, en el menú del concentrador, haga clic en **Examinar** y comience a escribir **Information Protection** en el cuadro Filtro. De los resultados, seleccione **Azure Information Protection**. 

    A continuación, verá la hoja **Azure Information Protection** donde puede configurar la directiva de Azure Information Protection que contiene los siguientes elementos:

    - Título e información sobre herramientas de la barra de Information Protection que ven los usuarios en sus aplicaciones de Office.

    - Etiquetas que permiten a los usuarios clasificar documentos y correos electrónicos.

    - La opción para exigir clasificación cuando los usuarios guarden documentos y envíen correos electrónicos.

    - La opción para establecer una etiqueta predeterminada como punto de partida para clasificar documentos y correos electrónicos.

    - La opción para pedir a los usuarios que proporcionen un motivo cuando seleccionen una etiqueta con un nivel de confidencialidad inferior al original.


Azure Information Protection viene con una [directiva predeterminada](configure-policy-default.md), que contiene las etiquetas **Personal**, **Público**, **Interno**, **Confidencial** y **Secreto**. Puede utilizar las etiquetas predeterminadas sin cambios, o puede personalizarlas. También puede eliminarlas y crear otras nuevas.

Cuando realice cambios en una hoja de Azure Information Protection, haga clic en **Guardar** para guardar los cambios o en **Descartar** para volver a la última configuración guardada. 

Cuando haya terminado de realizar los cambios que desee, haga clic en **Publicar**. 

El cliente de Azure Information Protection busca cambios cada vez que se inicia una aplicación de Office compatible y descarga los cambios en su directiva de Azure Information Protection.

## Configuración de la directiva de la organización

Use la siguiente información como ayuda para configurar la directiva de Azure Information Protection:

- [La directiva de Azure Information Protection](configure-policy-default.md)

- [Configuración de la directiva global](configure-policy-settings.md)

- [Creación de una nueva etiqueta](configure-policy-new-label.md)

- [Eliminación o cambio de orden de una etiqueta](configure-policy-delete-reorder.md)

- [Cambio o personalización de una etiqueta existente para Azure Information Protection](configure-policy-change-label.md)

- [Configuración de una etiqueta para aplicar protección](configure-policy-protection.md)

- [Configuración de una etiqueta para aplicar marcas visuales](configure-policy-markings.md)

- [Configuración de las condiciones para la clasificación automática y recomendada](configure-policy-classification.md)

## Pasos siguientes

Para ver un ejemplo de cómo personalizar la directiva predeterminada y ver el comportamiento resultante en una aplicación de Office, pruebe el [tutorial de inicio rápido de Azure Information Protection](infoprotect-quick-start-tutorial.md).




<!--HONumber=Aug16_HO2-->


