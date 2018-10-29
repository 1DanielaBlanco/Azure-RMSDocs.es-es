---
title: 'Cliente de etiquetado unificado de Azure Information Protection: Información de publicación de versión'
description: Vea la información de versión del cliente de etiquetado unificado de Azure Information Protection para Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/23/2018
ms.topic: conceptual
ms.service: information-protection
ms.reviewer: maayan
ms.suite: ems
ms.openlocfilehash: a1544e0fa3c6d09328d1801a75ffbccd496e3482
ms.sourcegitcommit: b275c1f82bf9176fe3fb36016c6f8692b8418295
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2018
ms.locfileid: "49951846"
---
# <a name="azure-information-protection-unified-labeling-client-version-release-information"></a>Cliente de etiquetado unificado de Azure Information Protection: Información de publicación de versión

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2*

> [!NOTE]
> Este cliente está en versión preliminar y sujeto a cambios. Usa el almacén de etiquetado unificado y descarga la directiva con etiquetas del Centro de seguridad y cumplimiento de Office 365. [Más información](/Office365/SecurityCompliance/sensitivity-labels)

Puede descargar la versión preliminar más reciente del cliente de etiquetado unificado de Azure Information Protection del [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=57440).

### <a name="release-information"></a>Información de versión

Use la siguiente información para ver los elementos compatibles con la versión preliminar más reciente del cliente de etiquetado unificado de Azure Information Protection. 

Este cliente se instala como un complemento de Office para los equipos Windows y tiene los mismos [requisitos previos](../requirements.md) que el cliente de Azure Information Protection que descarga la directiva de Azure.

## <a name="current-preview-version"></a>Versión preliminar actual

**Lanzamiento**: 16/10/2018

Esta versión preliminar del cliente de etiquetado unificado de Azure Information Protection para Windows admite las siguientes características: 

- Actualización del cliente de Azure Information Protection

- Etiquetado manual que aplica clasificación y protección para Word, Excel, PowerPoint y Outlook.

- Distintivo visual (encabezados, pies de página y marcas de agua)

- Etiquetado predeterminado 

- Etiquetas que aplican No reenviar

- Petición de justificación si los usuarios reducen el nivel de confidencialidad

- Cuadro de diálogo Ayuda y comentarios, que incluye restablecimiento de configuración y exportación de registros

- Actualización de directiva desde el Centro de seguridad y cumplimiento cada cuatro horas, por aplicación de Office.

Las siguientes características no funcionan en esta versión preliminar:

- Clasificación automática y recomendada

- Permisos personalizados

- Visor para archivos de imagen y texto protegidos, archivos PDF protegidos y archivos protegidos genéricamente

- Explorador de archivos, acciones de botón derecho para clasificar y proteger archivos

- Comandos de PowerShell para clasificar y proteger archivos desde la línea de comandos

- Detector para detectar, etiquetar y proteger archivos en almacenes de datos locales

- Compatibilidad con idiomas distintos del inglés

## <a name="instructions"></a>Instrucciones

1. Instale el cliente mediante las siguientes instrucciones: [User Guide: Download and install the Azure Information Protection client (Preview)](install-unifiedlabelingclient-app.md) (Guía del usuario: Descargar e instalar el cliente de Azure Information Protection [Versión preliminar]). 

2. Use el cliente en aplicaciones de Office como si fuera el cliente de Azure Information Protection, salvo que el botón de la cinta de Office se denomina **Confidencialidad** en lugar de **Proteger**:
    
    - [Clasificación de un archivo o una dirección de correo electrónico](client-classify.md) 
    
    - [Clasificación y protección de un archivo o una dirección de correo electrónico](client-classify-protect.md)

3. Personalice la experiencia: 
    
    - Para enviar comentarios o formular preguntas sobre este cliente de versión preliminar, use el [sitio de Yammer de Azure Information Protection](https://www.yammer.com/AskIPTeam).
    
    - Para notificar problemas con este cliente de versión preliminar, use la opción **Ayuda y comentarios** del botón **Confidencialidad** de la cinta de opciones. En el cuadro de diálogo, exporte los registros y, luego, adjunte estos archivos de registro al correo electrónico que se crea con la opción **Notificar un problema**. 

