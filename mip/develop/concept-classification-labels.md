---
title: 'Conceptos: etiquetas de clasificación'
description: Este artículo le ayudará a entender cómo se usan las etiquetas en la clasificación de datos.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a32193194b9806dbab5066db27192265566ca44f
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446658"
---
# <a name="microsoft-information-protection-sdk---classification-label-concepts"></a>SDK de Microsoft Information Protection: conceptos de etiquetas de clasificación

Como parte de una estrategia de protección de datos completa, las organizaciones deben implementar un sistema de clasificación de datos que describa los niveles de confidencialidad de los datos de la organización y después asignar los atributos del documento a esas clasificaciones.

Los atributos relacionados con la clasificación suelen implicar el **riesgo** para la organización si ese documento o esos datos se pierden o quedan en manos equivocadas. En el conocido sistema de clasificación del gobierno de los Estados Unidos, hay tres niveles de clasificación. Cada una tiene una definición que describe cuándo se debe aplicar esa clasificación:

* **Alto secreto**: se aplicará a la información, la divulgación no autorizada de la cual podría esperarse razonablemente que ocasione daños excepcionalmente graves a la seguridad nacional que la autoridad original de clasificación es capaz de identificar o describir.
* **Secreto**: se aplicará a la información, la divulgación no autorizada de la cual podría esperarse razonablemente que ocasione daños graves a la seguridad nacional que la entidad original de clasificación es capaz de identificar o describir.
* **Confidencial**: se aplicará a la información, la divulgación no autorizada de la cual podría esperarse razonablemente que ocasione daños a la seguridad nacional que la entidad original de clasificación es capaz de identificar o describir.
* **Sin clasificar**: en realidad, esta no es una clasificación, sino la ausencia de una de las tres anteriores.

En una aplicación del sector privado o comercial, podemos definir una lista similar a la predeterminada en el servicio Azure Information Protection, con valores monetarios asociados.

* **Extremadamente confidencial**: se aplicará a la información, la divulgación no autorizada de la cual podría esperarse razonablemente que ocasione daños superiores a 1 000 000 $.
* **Confidencial**: se aplicará a la información, la divulgación no autorizada de la cual podría esperarse razonablemente que ocasione daños superiores a 100 000 $.
* **General**: se aplicará a la información, la divulgación no autorizada de la cual podría esperarse razonablemente que ocasione pocos daños medibles
* **Pública**: se aplicará a la información destinada al consumo público y externo. 
* **No comercial**: se aplicará a la información que no está relacionada con el negocio de la empresa, de forma directa o indirecta.

Cada clasificación describe el riesgo para la empresa en caso de divulgación no autorizada de dicha información. Tras identificar esta clasificación y las condiciones, deben identificarse los atributos que ayuden a los propietarios de los datos a comprender qué clasificación deben aplicar.

## <a name="labeling"></a>Etiquetado

El acto de asociar una clasificación de datos con un conjunto de información se conoce como **etiquetado**. Dado que el SDK de MIP tratar de aplicar las **etiquetas** de clasificación en los documentos, no nos referimos a las clasificaciones, sino a las etiquetas. Un usuario o proceso ya **clasificó** los datos según el conocimiento de la información: el SDK de MIP **etiquetará** la información.

## <a name="labels-in-the-mip-sdk"></a>Etiquetas en el SDK de MIP

Las etiquetas son un componente fundamental de los SDK de MIP. Las etiquetas generan el etiquetado, la protección y el distintivo de contenido de todos los documentos que toca el SDK. El SDK puede hacer lo siguiente:

* Aplicar etiquetas a los documentos
* Leer las etiquetas existentes en los documentos
* Cambiar una etiqueta existente y justificación de orden si lo exige la directiva
* Quitar una etiqueta de un documento

La etiqueta aplicará protección y distintivo de contenido en función de la etiqueta de configuración que los administradores hayan definido en el Centro de cumplimiento y seguridad. 

## <a name="miplabel-vs-mipcontentlabel"></a>mip::Label vs. mip::ContentLabel

Existen dos tipos de etiqueta en el SDK de MIP. `Label` y `ContentLabel`.

* Label: etiqueta que puede aplicar un usuario o proceso, tal como se define en la directiva de la organización.
* ContentLabel: etiqueta que ya existe en un documento o en la información. Se puede leer, actualizar o quitar. 

En otras palabras, `ContentLabel` es un `Label` que se ha aplicado a un fragmento de información.

## <a name="metadata"></a>Metadatos

El SDK también admite la adición de metadatos adicionales a los documentos en forma de pares clave/valor. Si su organización tiene subclasificaciones o etiquetas que describen la información de una manera más específica, el SDK puede usarse para aplicar esos metadatos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más detalles sobre el sistema de clasificación del gobierno de los Estados Unidos, consulte https://www.gpo.gov/fdsys/pkg/FR-2010-01-05/html/E9-31418.htm.
