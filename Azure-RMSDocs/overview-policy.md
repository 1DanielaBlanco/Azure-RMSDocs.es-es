---
title: Información general de la directiva de Azure Information Protection
description: Descripción de las etiquetas y la configuración de una directiva de Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/12/2018
ms.topic: conceptual
ms.service: information-protection
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: e66a2c117523eb01089881b8210f12ed2f657ed4
ms.sourcegitcommit: 1d2912b4f0f6e8d7596cbf31e2143a783158ab11
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/12/2018
ms.locfileid: "53304900"
---
# <a name="overview-of-the-azure-information-protection-policy"></a>Información general de la directiva de Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Una directiva de Azure Information Protection contiene los siguientes elementos que puede configurar:
    
- Qué etiquetas se incluyen que permiten a los administradores y usuarios clasificar (y opcionalmente, proteger) documentos y correos electrónicos.

- Título e información sobre herramientas de la barra de Information Protection que ven los usuarios en sus aplicaciones de Office.

- La opción para establecer una etiqueta predeterminada como punto de partida para clasificar documentos y correos electrónicos.

- La opción para exigir clasificación cuando los usuarios guarden documentos y envíen correos electrónicos.

- La opción para pedir a los usuarios que proporcionen un motivo cuando seleccionen una etiqueta con un nivel de confidencialidad inferior al original.

- La opción para etiquetar automáticamente un mensaje de correo, basándose en sus datos adjuntos.

- La opción para controlar si la barra de Information Protection se muestra en las aplicaciones de Office.

- La opción para controlar si se muestra el botón No reenviar en Outlook.

- La opción que permite a los usuarios especificar sus propios permisos para documentos.

- La opción para proporcionar un vínculo de ayuda personalizado para los usuarios.

Azure Information Protection incluye una [directiva predeterminada](configure-policy-default.md), que contiene cinco etiquetas principales. Dos de estas etiquetas contienen subetiquetas para proporcionar subcategorías, cuando sea necesario. Cuando se configura una etiqueta para subetiquetas, los usuarios no pueden seleccionar la principal, sino que deben seleccionar una de las subetiquetas.

Las etiquetas de Azure Information Protection se pueden usar con la gama completa de los datos que una organización normalmente crea y almacena, desde la clasificación más baja de datos personales, a la clasificación más alta de información extremadamente confidencial. 

Puede utilizar las etiquetas predeterminadas sin cambios, o puede personalizarlas. También puede eliminarlas y crear otras nuevas. Para obtener todas las instrucciones, consulte [Configuración de la directiva de Azure Information Protection](configure-policy.md).


## <a name="next-steps"></a>Pasos siguientes

Para obtener ejemplos de cómo personalizar la directiva de Azure Information Protection y ver el comportamiento resultante para los usuarios, pruebe los siguientes tutoriales:

- [Edit the Azure Information Protection policy and create a new label and create a new label](infoprotect-quick-start-tutorial.md) (Edición de la directiva de Azure Information Protection y creación de una nueva etiqueta)

- [Configure Azure Information Protection policy settings that work together](infoprotect-settings-tutorial.md) (Configuración de los parámetros de la directiva de Azure Information Protection que funcionan en conjunto)
