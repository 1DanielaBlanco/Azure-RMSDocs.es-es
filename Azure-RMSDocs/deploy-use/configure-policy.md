---
title: "Configuración de la directiva de Azure Information Protection"
description: "Para configurar la protección, la clasificación y el etiquetado, debe configurar la directiva de Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/12/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 7a4922384a228457b683653e80afe4b8c8db6df2
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2017
---
<a id="configuring-azure-information-protection-policy" class="xliff"></a>

# Configuración de la directiva de Azure Information Protection

>*Se aplica a: Azure Information Protection*

Para configurar la protección, la clasificación y el etiquetado, debe configurar la directiva de Azure Information Protection. Esta directiva se descarga luego en los equipos que tienen instalado el [cliente de Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

<a id="subscription-support" class="xliff"></a>

## Compatibilidad con la suscripción

La directiva de Azure Information Protection admite distintos niveles de suscripciones:

- Azure Information Protection P2: compatibilidad con todas las características de clasificación, etiquetado y protección.

- Azure Information Protection P1: compatibilidad con la mayoría de las características de clasificación, etiquetado y protección, pero no con la clasificación automática o HYOK.

- Office 365 que incluye el servicio de Azure Rights Management: compatibilidad con la protección, pero no con la clasificación ni el etiquetado.

Las opciones que requieren una suscripción de Azure Information Protection P2 ahora se identifican en el portal.

Si tiene una combinación de suscripciones para los usuarios de su inquilino, es su responsabilidad asegurarse de que la directiva de Azure Information Protection que los usuarios descargan no contiene opciones de configuración que su cuenta no tienen licencia para usar. Cuando configura opciones cuyas licencias no tienen todos los usuarios, use directivas con ámbito para que los usuarios no estén configurados para usar características cuyas licencias no poseen.

Para más información sobre las suscripciones, consulte [¿Qué suscripción necesito para Azure Information Protection y qué características se incluyen?](../get-started/faqs.md#what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included)

Para más información sobre cómo configurar las directivas con ámbito, consulte [Configuración de la directiva para usuarios específicos mediante directivas de ámbito](configure-policy-scope.md).

<a id="how-to-configure-the-azure-information-protection-policy" class="xliff"></a>

## Para configurar la directiva de Azure Information Protection

1. En una nueva ventana del explorador, inicie sesión en [Azure Portal](https://portal.azure.com) como administrador de seguridad o administrador global.

2. Vaya a la hoja **Azure Information Protection**: por ejemplo, en el menú del centro, haga clic en **Más servicios** y comience a escribir **Information Protection** en el cuadro Filtro. De los resultados, seleccione **Azure Information Protection**. 
    
    La primera vez que se conecte al servicio, la página **Inicio rápido** se abrirá automáticamente. Para configurar la directiva que reciben todos los usuarios, haga clic en **Directiva global** para abrir la hoja **Policy: Global** (Directiva: Global). Esta hoja se abre automáticamente para las conexiones subsiguientes al servicio a fin de ver y editar la directiva global que reciben todos los usuarios. 
    
    La directiva de Azure Information Protection contiene los siguientes elementos que puede configurar:
    
    - Etiquetas que permiten a los usuarios clasificar documentos y correos electrónicos.
    
    - Título e información sobre herramientas de la barra de Information Protection que ven los usuarios en sus aplicaciones de Office.
    
    - La opción para exigir clasificación cuando los usuarios guarden documentos y envíen correos electrónicos.
    
    - La opción para establecer una etiqueta predeterminada como punto de partida para clasificar documentos y correos electrónicos.
    
    - La opción para pedir a los usuarios que proporcionen un motivo cuando seleccionen una etiqueta con un nivel de confidencialidad inferior al original.
    
    - La opción para etiquetar automáticamente un mensaje de correo, basándose en sus datos adjuntos.
    
    - La opción para proporcionar un vínculo de ayuda personalizado para los usuarios.

Azure Information Protection incluye una [directiva predeterminada](configure-policy-default.md), que contiene cinco etiquetas principales. Estas etiquetas se pueden usar con la gama completa de los datos que una organización normalmente crea y almacena, desde la clasificación más baja de datos personales, a la clasificación más alta de información extremadamente confidencial. 

Puede utilizar las etiquetas predeterminadas sin cambios, o puede personalizarlas. También puede eliminarlas y crear otras nuevas. Para más información, use los vínculos que aparecen en la siguiente sección para ubicar las opciones pertinentes y cómo configurarlas. 

Cuando realice cambios en una hoja de Azure Information Protection, haga clic en **Guardar** para guardar los cambios o en **Descartar** para volver a la última configuración guardada. 

Cuando haya terminado de realizar los cambios que desee, haga clic en **Publicar**. 

El cliente de Azure Information Protection busca cambios cada vez que se inicia una aplicación de Office compatible y descarga los cambios en su directiva de Azure Information Protection más reciente. Desencadenadores adicionales que actualizan la directiva en el cliente:

- Haga clic con el botón derecho para clasificar y proteger un archivo o carpeta.

- Ejecución de los [cmdlets de PowerShell](../rms-client/client-admin-guide-powershell.md) para etiquetado y protección (Get-AIPFileStatus, Set-AIPFileClassification, and Set-AIPFileLabel).

- Cada 24 horas.

>[!NOTE]
>Cuando el cliente descargue la directiva, tenga en cuenta que deberá esperar unos minutos antes de que esté totalmente operativa. El tiempo real varía según factores como el tamaño y la complejidad de la configuración de la directiva y la conectividad de red. Si la acción resultante de las etiquetas no coincide con los cambios más recientes, deje pasar hasta 15 minutos y vuelva a intentarlo.

<a id="configuring-your-organizations-policy" class="xliff"></a>

### Configuración de la directiva de la organización

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

- [Configuración y administración de plantillas](configure-policy-templates.md)

- [Configuración de etiquetas para distintos idiomas](configure-policy-languages.md)

<a id="next-steps" class="xliff"></a>

## Pasos siguientes

Para ver un ejemplo de cómo personalizar la directiva predeterminada y ver el comportamiento resultante en una aplicación de Office, pruebe el [tutorial de inicio rápido de Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
