---
title: "Clasificación de archivos y correos electrónicos mediante Azure Information Protection"
description: "Instrucciones sobre cómo clasificar sus documentos y correos electrónicos."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/20/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d65c7690-fab7-4823-845c-8c73903e9c79
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: aee3ec8673217cf130c4705e750532c7aeefe084
ms.sourcegitcommit: f1d0b899e6d79ebef3829f24711f947316bca8ef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="user-guide-classify-a-file-or-email-by-using-azure-information-protection"></a>Guía del usuario: Clasificación de un archivo o correo electrónico con Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8 y Windows 7 con SP1*

> [!NOTE]
> Siga estas instrucciones para clasificar (pero no proteger) los documentos y correos electrónicos. Si también necesita proteger los documentos y correos electrónicos, consulte las [instrucciones sobre clasificación y protección](client-classify-protect.md). Si no está seguro de qué conjunto de instrucciones debe usar, póngase en contacto con el administrador o el departamento de soporte técnico.

La manera más fácil de clasificar sus documentos y correos electrónicos es crearlos o editarlos con las aplicaciones de escritorio de Office: **Word**, **Excel**, **PowerPoint** y **Outlook**. 

Aun así, también puede clasificar archivos mediante el **Explorador de archivos**. Este método es compatible con tipos de archivo adicionales y es una manera muy útil de clasificar varios archivos a la vez. 

## <a name="using-office-apps-to-classify-your-documents-and-emails"></a>Uso de las aplicaciones de Office para clasificar documentos y correos electrónicos

Use la barra de Azure Information Protection y seleccione una de las etiquetas configuradas para usted. 

Por ejemplo, en la siguiente imagen se muestra que el documento aún no se ha etiquetado, porque en **Confidencialidad** aparece **Sin establecer**. Para establecer una etiqueta, como "General", haga clic en **General**. Si no está seguro de qué etiqueta aplicar en el documento o correo electrónico actual, utilice la información sobre herramientas de etiquetas para obtener más detalles sobre cada etiqueta y cuándo aplicarla. 

![Ejemplo de barra de Azure Information Protection](../media/info-protect-bar-not-set-callout.png)

Si ya se ha aplicado la etiqueta al documento y desea cambiarla, puede seleccionar una etiqueta diferente. Si las etiquetas no se muestran en la barra, primero haga clic en el icono **Editar etiqueta**, junto al valor de la etiqueta actual.

> [!TIP]
> También puede seleccionar etiquetas desde el botón **Proteger**, en la pestaña **Archivo**.

Además de seleccionar manualmente las etiquetas, estas también pueden aplicarse como sigue:

- El administrador ha configurado una etiqueta predeterminada, que puede mantener o cambiar.

- El administrador ha configurado avisos recomendados para seleccionar una etiqueta específica cuando se detecta información confidencial. Puede aceptar la recomendación (y se aplica la etiqueta), o rechazarla (no se aplica la etiqueta recomendada).

### <a name="exceptions-for-the-azure-information-protection-bar"></a>Excepciones de la barra de Azure Information Protection 

##### <a name="dont-see-this-information-protection-bar-in-your-office-apps"></a>¿No aparece la barra de Information Protection en las aplicaciones de Office?

- Puede ser que no tenga [instalado](install-client-app.md) el cliente de Azure Information Protection.

- Tiene instalado el cliente, pero el administrador ha establecido una configuración que no muestra la barra. En su lugar, seleccione las etiquetas desde el botón **Proteger**, en la pestaña **Archivo** de la cinta de Office. 

##### <a name="is-the-label-that-you-expect-to-see-not-displayed-on-the-bar"></a>¿La etiqueta que esperaba ver no aparece en la barra? 

- Si el administrador ha configurado recientemente una etiqueta nueva, intente cerrar todas las instancias de la aplicación de Office y vuelva a abrirla. Esta acción comprueba si las etiquetas han experimentado algún cambio.

- La etiqueta debe estar en una directiva de ámbito que no incluye su cuenta. Póngase en contacto con el Servicio de asistencia o con el administrador.


## <a name="using-file-explorer-to-classify-files"></a>Uso del Explorador de archivos para clasificar archivos

Con el Explorador de archivos, puede clasificar rápidamente un solo archivo, varios archivos o una carpeta. 

Cuando seleccione una carpeta, todos los archivos que contenga y sus subcarpetas se seleccionarán automáticamente para la clasificación que haya establecido. Sin embargo, los nuevos archivos que se creen en esa carpeta o en las subcarpetas no se clasificarán automáticamente.

Cuando utilice el Explorador de archivos para clasificar los archivos, si una o varias de las etiquetas aparecen atenuadas, significa que los archivos que ha seleccionado no admiten la clasificación sin también protegerlos.

La Guía de administración contiene una lista completa de los tipos de archivo que admite clasificación sin protección: [Tipos de archivos compatibles solo para clasificación](client-admin-guide-file-types.md#file-types-supported-for-classification-only).

### <a name="to-classify-a-file-by-using-file-explorer"></a>Para clasificar un archivo mediante el Explorador de archivos

1. En el Explorador de archivos, seleccione un archivo, varios archivos o una carpeta. Haga clic con el botón derecho y seleccione **Clasificar y proteger**. Por ejemplo:
    
    ![Explorador de archivos Menú contextual Clasificar y proteger con Azure Information Protection](../media/right-click-classify-protect-folder.png)

2. En el cuadro de diálogo **Clasificar y proteger: Azure Information Protection**, use las etiquetas del mismo modo que en una aplicación de Office, lo que establece la clasificación definida por el administrador. 
    
    Si no se puede seleccionar ninguna etiqueta (aparecen atenuadas), significa que el archivo seleccionado no admite la clasificación. Por ejemplo:
    
    ![Ninguna etiqueta disponible en el cuadro de diálogo Clasificar y proteger: Azure Information Protection**](../media/info-protect-dialog-labels-dimmed.png)

3. Si ha seleccionado un archivo que no admite la clasificación, haga clic en **Cerrar**. No puede clasificar este archivo si no lo protege también.
    
    Si ha seleccionado una etiqueta, haga clic en **Aplicar** y espere a que aparezca el mensaje **Trabajo finalizado** para ver los resultados. A continuación, haga clic en **Cerrar**.

Si cambia de opinión en relación con la etiqueta que ha elegido, simplemente repita este proceso y elija otra etiqueta.

La clasificación que ha especificado permanece con el archivo, incluso si lo envía por correo electrónico o lo guarda en otra ubicación. 
## <a name="other-instructions"></a>Otras instrucciones
Puede encontrar más instrucciones sobre procedimientos en la guía del usuario de Azure Information Protection:

- [¿Qué desea hacer?](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Información adicional para los administradores    
Consulte [Configuración de la directiva de Azure Information Protection](../deploy-use/configure-policy.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
