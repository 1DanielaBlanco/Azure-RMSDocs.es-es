---
title: "Configuración de la directiva de Azure Information Protection"
description: "Para configurar la protección, la clasificación y el etiquetado, debe configurar la directiva de Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: b946dff4782d1b5571aa0438d1681030f0de092f
ms.sourcegitcommit: f0402cf14506b4c61a156a2baf7e69b7b16883a1
translationtype: HT
---
# <a name="configuring-azure-information-protection-policy"></a>Configuración de la directiva de Azure Information Protection

>*Se aplica a: Azure Information Protection*

Para configurar la protección, la clasificación y el etiquetado, debe configurar la directiva de Azure Information Protection. Esta directiva se descarga luego en los equipos que tienen instalado el [cliente de Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Para configurar la directiva de Azure Information Protection:

1. En una nueva ventana del explorador, inicie sesión en [Azure Portal](https://portal.azure.com) como administrador global.

2. Vaya a la hoja **Azure Information Protection**: por ejemplo, en el menú del centro, haga clic en **Más servicios** y comience a escribir **Information Protection** en el cuadro Filtro. De los resultados, seleccione **Azure Information Protection**. 

    A continuación, verá la hoja **Azure Information Protection**, donde puede abrir la directiva **Global** que todos los usuarios obtienen. Opcionalmente, también puede agregar y editar las directivas de ámbito. La directiva **Global** de Azure Information Protection contiene los siguientes elementos que puede configurar:

    - Etiquetas que permiten a los usuarios clasificar documentos y correos electrónicos.

    - Título e información sobre herramientas de la barra de Information Protection que ven los usuarios en sus aplicaciones de Office.

    - La opción para exigir clasificación cuando los usuarios guarden documentos y envíen correos electrónicos.

    - La opción para establecer una etiqueta predeterminada como punto de partida para clasificar documentos y correos electrónicos.

    - La opción para pedir a los usuarios que proporcionen un motivo cuando seleccionen una etiqueta con un nivel de confidencialidad inferior al original.

    - La opción para etiquetar automáticamente un mensaje de correo, basándose en sus datos adjuntos.

    - La opción para proporcionar un vínculo de ayuda personalizado para los usuarios.

Azure Information Protection incluye una [directiva predeterminada](configure-policy-default.md), que contiene cinco etiquetas principales. Estas etiquetas se pueden usar con la gama completa de los datos que una organización normalmente crea y almacena, desde la clasificación más baja de datos personales, a la clasificación más alta de información extremadamente confidencial. Puede utilizar las etiquetas predeterminadas sin cambios, o puede personalizarlas. También puede eliminarlas y crear otras nuevas.

Cuando realice cambios en una hoja de Azure Information Protection, haga clic en **Guardar** para guardar los cambios o en **Descartar** para volver a la última configuración guardada. 

Cuando haya terminado de realizar los cambios que desee, haga clic en **Publicar**. 

El cliente de Azure Information Protection busca cambios cada vez que se inicia una aplicación de Office compatible y descarga los cambios en su directiva de Azure Information Protection más reciente. Desencadenadores adicionales que actualizan la directiva en el cliente:

- Haga clic con el botón derecho para clasificar y proteger un archivo o carpeta.

- Ejecución de cmdlets de PowerShell para etiquetado y protección (Get-AIPFileStatus y Set-AIPFileLabel).

- Cada 24 horas.


## <a name="configuring-your-organizations-policy"></a>Configuración de la directiva de la organización

Use la siguiente información como ayuda para configurar la directiva de Azure Information Protection:

- [Directiva predeterminada de Azure Information Protection](configure-policy-default.md)

- [Configuración de directivas](configure-policy-settings.md)

- [Creación de una nueva etiqueta](configure-policy-new-label.md)

- [Eliminación o cambio de orden de una etiqueta](configure-policy-delete-reorder.md)

- [Cambio o personalización de una etiqueta existente](configure-policy-change-label.md)

- [Configuración de una etiqueta para la protección](configure-policy-protection.md)

- [Configuración de una etiqueta para marcas visuales](configure-policy-markings.md)

- [Configuración de las condiciones para la clasificación automática y recomendada](configure-policy-classification.md)

- [Configuración de la directiva para usuarios específicos mediante directivas de ámbito](configure-policy-scope.md)

## <a name="next-steps"></a>Pasos siguientes

Para ver un ejemplo de cómo personalizar la directiva predeterminada y ver el comportamiento resultante en una aplicación de Office, pruebe el [tutorial de inicio rápido de Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
