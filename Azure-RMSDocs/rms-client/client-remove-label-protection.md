---
title: Eliminación de etiquetas de Azure Information Protection
description: Instrucciones para quitar etiquetas de clasificación y la protección de archivos que se han etiquetado con Azure Information Protection o que se han protegido con Rights Management.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ''
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 6e68a3ab1aca0d32f8105bad7d2b5e8985dab1ae
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="user-guide-remove-labels-and-protection-from-files-and-emails-that-have-been-labeled-by-azure-information-protection-or-protected-by-rights-management"></a>Guía del usuario: Eliminación de etiquetas y protección de archivos y correos electrónicos etiquetados con Azure Information Protection o protegidos con Rights Management

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8 y Windows 7 con SP1*

Cuando el [cliente de Azure Information Protection está instalado en el equipo](install-client-app.md), puede quitar etiquetas de clasificación y la protección de archivos y correos electrónicos.

Si la etiqueta eliminada está configurada para aplicar protección, esta acción también quita la protección del archivo. Puede que se le solicite que indique por qué va a quitar la etiqueta.

> [!IMPORTANT]
> Debe ser el propietario del archivo para quitar la protección, o bien que se le deben haber concedido permisos para quitar la protección (el permiso Extraer o Control total de Rights Management).

Si desea elegir una etiqueta diferente o un conjunto diferente de la configuración de protección, no es necesario quitar la etiqueta o la protección. En su lugar, elija una nueva etiqueta y, si es necesario, puede definir permisos personalizados. 

Puede quitar etiquetas y protección de correos electrónicos y documentos de Office cuando los crea o edita desde las aplicaciones de escritorio de Office: **Word**, **Excel**, **PowerPoint** y **Outlook**. 

También puede quitar etiquetas y protección con el **Explorador de archivos**, que admite tipos de archivos adicionales y es una forma cómoda de quitar etiquetas y protección de varios archivos a la vez.

## <a name="using-office-apps-to-remove-labels-and-protection-from-documents-and-emails"></a>Uso de aplicaciones de Office para quitar las etiquetas y la protección de documentos y correos electrónicos

En la barra de Information Protection, haga clic en el icono **Editar etiqueta**:

![Barra de Azure Information Protection - Eliminar etiqueta](../media/delete-label.png)

Si el icono **Eliminar etiqueta** no está disponible inmediatamente, haga clic primero en el icono **Editar etiqueta**:

![Barra de Azure Information Protection - Editar etiqueta](../media/edit-label.png)

> [!NOTE]
> Si no ve esta barra de Information Protection en las aplicaciones de Office:
> 
> - Puede que no tenga [instalado](install-client-app.md) el cliente de Azure Information Protection, o que este se encuentre en ejecución en el [modo de solo protección](client-protection-only-mode.md).

## <a name="using-file-explorer-to-remove-labels-and-protection-from-files"></a>Uso del Explorador de archivos para quitar etiquetas y la protección de archivos

Con el Explorador de archivos, puede quitar rápidamente las etiquetas y la protección de un solo archivo, de varios archivos o de una carpeta. Cuando seleccione una carpeta, todos los archivos que contiene y sus subcarpetas se seleccionan automáticamente. 

1.  En el Explorador de archivos, seleccione un archivo, varios archivos o una carpeta. Haga clic con el botón derecho y seleccione **Clasificar y proteger**.

2. Para quitar una etiqueta: en el cuadro de diálogo **Clasificar y proteger: Azure Information Protection**, haga clic en **Eliminar etiqueta**. Si la etiqueta se ha configurado para aplicar protección, dicha protección se quita automáticamente.

3. Para quitar la protección personalizada de un solo archivo: en el cuadro de diálogo **Clasificar y proteger: Azure Information Protection**, desactive la opción **Protect with custom permissions** (Proteger con permisos personalizados).
    
4. Para quitar la protección personalizada de varios archivos: en el cuadro de diálogo **Clasificar y proteger: Azure Information Protection**, haga clic en **Remove custom permissions** (Quitar permisos personalizados).

5. Haga clic en **Aplicar** y espere a que aparezca el mensaje **Trabajo finalizado** para ver los resultados. A continuación, haga clic en **Cerrar**.


## <a name="other-instructions"></a>Otras instrucciones
Puede encontrar más instrucciones sobre procedimientos en la guía del usuario de Azure Information Protection:

- [¿Qué desea hacer?](client-user-guide.md#what-do-you-want-to-do)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]