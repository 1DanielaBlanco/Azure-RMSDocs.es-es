---
title: 'Conceptos: etiquetas de clasificación'
description: Este artículo le ayudará a entender cómo se usan las etiquetas en la clasificación de datos.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: c913eab399eebbdc9af82d7365ea68c9a8430de9
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259344"
---
# <a name="microsoft-information-protection-sdk---classification-label-concepts"></a>SDK de Microsoft Information Protection: conceptos de etiquetas de clasificación

Como parte de una estrategia de protección de datos completa, las organizaciones deben implementar un sistema de clasificación de datos que describa los niveles de confidencialidad de los datos de la organización y después asignar los atributos del documento a esas clasificaciones.

Los atributos relacionados con la clasificación suelen implicar el **riesgo** para la organización si ese documento o esos datos se pierden o quedan en manos equivocadas. En el conocido sistema de clasificación del gobierno de los Estados Unidos, hay tres niveles de clasificación. Cada una tiene una definición que describe cuándo se debe aplicar esa clasificación:

* **Alto secreto**: Se aplicará a la información, la divulgación no autorizada de los cuales razonablemente podía ocasionar daños excepcionalmente grave a la seguridad nacional que es capaz de identificar o describir la entidad original de clasificación.
* **Secret**: Se aplicará a la información, la divulgación no autorizada de los cuales razonablemente podía provocar daños graves para la seguridad nacional que es capaz de identificar o describir la entidad original de clasificación.
* **Confidencial**: Se aplicará a la información, la divulgación no autorizada de los cuales razonablemente podía ocasionar daños a la seguridad nacional que es capaz de identificar o describir la entidad original de clasificación.
* **Sin clasificar**: Esto no es realmente una clasificación, pero en su lugar la ausencia de uno de los tres anteriores.

En una aplicación del sector privado o comercial, podemos definir una lista similar a la predeterminada en el servicio Azure Information Protection, con valores monetarios asociados.

* **Extremadamente confidencial**: Se aplicará a la información, la divulgación no autorizada de los cuales razonablemente podía provocar daños mayores millones de USD $1.
* **Confidencial**: Se aplicará a la información, la divulgación no autorizada de los cuales razonablemente podía ocasionar daños mayores de USD $100K.
* **General**: Se aplicará a la información, la divulgación no autorizada de los cuales razonablemente podía provocar daños medibles poco.
* **Public**: Se aplicará a la información destinada para consumo público, externo. 
* **No sea de empresa**: Se aplicará a la información que no está relacionada con el negocio de empresa, directa o indirecta.

Cada clasificación describe el riesgo para la empresa en caso de divulgación no autorizada de dicha información. Tras identificar esta clasificación y las condiciones, deben identificarse los atributos que ayuden a los propietarios de los datos a comprender qué clasificación deben aplicar.

## <a name="labeling"></a>Etiquetado

El acto de asociar una clasificación de datos con un conjunto de información se conoce como **etiquetado**. Dado que el SDK de MIP tratar de aplicar las **etiquetas** de clasificación en los documentos, no nos referimos a las clasificaciones, sino a las etiquetas. Un usuario o proceso ya se ha **clasificado** los datos según el conocimiento de la información: El SDK de MIP, a continuación, le **etiqueta** la información.

## <a name="labels-in-the-mip-sdk"></a>Etiquetas en el SDK de MIP

Las etiquetas son un componente fundamental de los SDK de MIP. Las etiquetas generan el etiquetado, la protección y el distintivo de contenido de todos los documentos que toca el SDK. El SDK puede hacer lo siguiente:

* Aplicar etiquetas a los documentos
* Leer las etiquetas existentes en los documentos
* Cambiar una etiqueta existente y justificación de orden si lo exige la directiva
* Quitar una etiqueta de un documento

La etiqueta aplicará protección y distintivo de contenido en función de la etiqueta de configuración que los administradores hayan definido en el Centro de cumplimiento y seguridad. 

## <a name="miplabel-vs-mipcontentlabel"></a>mip::Label vs. mip::ContentLabel

Existen dos tipos de etiqueta en el SDK de MIP. `Label` y `ContentLabel`.

* Etiqueta: Una etiqueta que se puede aplicar a un usuario o proceso tal como se define en la directiva organizativa.
* ContentLabel: En un documento o la información que ya existe una etiqueta. Se puede leer, actualizar o quitar. 

En otras palabras, `ContentLabel` es un `Label` que se ha aplicado a un fragmento de información.

## <a name="metadata"></a>Metadatos

El SDK también admite la adición de metadatos adicionales a los documentos en forma de pares clave/valor. Si su organización tiene subclasificaciones o etiquetas que describen la información de una manera más específica, el SDK puede usarse para aplicar esos metadatos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más detalles sobre el sistema de clasificación del gobierno de los Estados Unidos, consulte https://www.gpo.gov/fdsys/pkg/FR-2010-01-05/html/E9-31418.htm.
