---
title: 'Información general: SDK de Microsoft Information Protection.'
description: Microsoft Information Protection (MIP) es la unificación de los servicios de clasificación, etiquetado y protección de Microsoft en un kit de desarrollo de software (SDK) y experiencia de administración única.
author: BryanLa
ms.service: information-protection
ms.topic: overview
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 775ae3d524947c8300de0e011b92c2cad106905a
ms.sourcegitcommit: d677088db8588fb2cc4a5d7dd296e76d0d9a2e9c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/03/2018
ms.locfileid: "48251733"
---
# <a name="overview"></a>Introducción

## <a name="microsoft-information-protection"></a>Microsoft Information Protection

Microsoft Information Protection (MIP) es la unificación de los servicios de clasificación, etiquetado y protección de Microsoft en un kit de desarrollo de software (SDK) y experiencia de administración única. La administración unificada se proporciona a través de Office 365, Azure Information Protection, Windows Information Protection y otros servicios de Microsoft. Organizaciones terceras puede usar el SDK para integrarlo con aplicaciones, mediante un servicio de protección y un esquema de etiquetado de datos coherente y estándar.

* [¿Qué es el Centro de seguridad y cumplimiento de Office 365?](https://docs.microsoft.com/office365/securitycompliance/)
* [¿Qué es Azure Information Protection?](/azure/information-protection/understand-explore/what-is-information-protection)
* [¿Cómo funciona la protección en Azure Information Protection?](/azure/information-protection/understand-explore/what-is-information-protection#how-data-is-protected)

## <a name="microsoft-information-protection-sdk"></a>SDK de Microsoft Information Protection

El SDK de MIP expone los servicios de protección y etiquetado del Centro de seguridad y cumplimiento de Office 365 para servicios y aplicaciones de terceros. Los desarrolladores pueden usar el SDK para compilar la compatibilidad nativa para aplicar las etiquetas y la protección a los archivos. Los desarrolladores pueden razonar acerca de las acciones que deben ejecutarse cuando se detectan etiquetas específicas y acerca de la información cifrada con MIP. 

Las etiquetas y la protección que se aplicará a la información en el conjunto de servicios de Microsoft son **coherentes**. La coherencia permite a las aplicaciones y los servicios compatibles con MIP leer y escribir las etiquetas de una manera común y predecible.

Entre los casos de uso de nivel general del SDK de MIP se incluye lo siguiente:

* Una aplicación de línea de negocio que aplica etiquetas de clasificación a los archivos durante la exportación.
* Una aplicación de diseño CAD/CAM proporciona compatibilidad nativa para el etiquetado de Microsoft Information Protection.
* Una solución de prevención de pérdida de datos o un agente de seguridad de acceso a la nube razona acerca de los datos cifrados con Azure Information Protection.

Para obtener una lista más exhaustiva, revise los [conceptos de API](concept-apis-use-cases.md).

## <a name="next-steps"></a>Pasos siguientes

Ahora está listo para empezar a trabajar con el SDK. Lo primero que debe hacer es [completar los pasos de instalación y configuración del SDK de MIP](setup-configure-mip.md) para asegurarse de que su suscripción de Office 365 y el equipo cliente están configurados correctamente.

