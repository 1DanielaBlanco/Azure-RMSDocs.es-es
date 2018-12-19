---
title: Instrucciones de procedimiento para escenarios comunes que usan Azure Information Protection.
description: Identifique los casos de uso que clasifican y protegen los datos de su organización mediante el uso de Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/08/2018
ms.topic: conceptual
ms.service: information-protection
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 7986648999a830985c4dbd1f31855bb222a443c2
ms.sourcegitcommit: 2a1c0882d2b0400f4da6370dbc1830df09867e3d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53218381"
---
# <a name="how-to-guides-for-common-scenarios-that-use-azure-information-protection"></a>Guías de procedimientos para escenarios comunes que usan Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Hay muchas maneras de usar Azure Information Protection para clasificar y, opcionalmente, proteger documentos y correos electrónicos de su organización. 

Las implementaciones que tienen más éxito son aquellas que identifican casos de uso específicos que proporcionan el mayor beneficio comercial para la organización. Utilice la siguiente lista de instrucciones y escenarios comunes para poner en marcha su implementación.

## <a name="common-scenarios"></a>Escenarios frecuentes

|Escenario: Deseo...|Instrucciones|
|----------------|---------------|
|Buscar la información confidencial que mi organización almacena de forma local|[Inicio rápido: Búsqueda de la información confidencial de los archivos almacenados en un entorno local](quickstart-findsensitiveinfo.md)|
|Permitir que los usuarios protejan con facilidad los correos electrónicos que contienen información confidencial|[Inicio rápido: Configuración de una etiqueta para usuarios para proteger fácilmente los correos electrónicos que contienen información confidencial](quickstart-label-dnf-protectedemail.md)|
|Permitir que los usuarios clasifiquen con facilidad los datos tal como se han creado o editado y protegerlos si contienen información confidencial| [Tutorial: Edición de directivas y creación de una etiqueta](infoprotect-quick-start-tutorial.md)|
|Permitir que los usuarios colaboren con facilidad en un documento protegido|[Configuring secure document collaboration by using Azure Information Protection](secure-collaboration-documents.md) (Configuración de la colaboración con documentos segura mediante Azure Information Protection)|
|Proteger automáticamente los correos electrónicos de los usuarios que se envían fuera de la organización| [Configuración de reglas de flujo de correo para etiquetas de Azure Information Protection](configure-exo-rules.md)
|Clasificar y proteger automáticamente los datos existentes en mis almacenes de datos locales|[Implementación del analizador de Azure Information Protection](deploy-aip-scanner.md)|
|Usar mis propias claves para proteger los datos de mi organización| [Planificación e implementación de la clave de inquilino](plan-implement-tenant-key.md)|
|Migrar desde AD RMS|[Migración desde AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md)|

## <a name="additional-deployment-instructions"></a>Instrucciones de implementación adicionales

Nuestro [blog técnico de Azure Information Protection](https://aka.ms/AIPblog) contiene instrucciones paso a paso adicionales de nuestro equipo de Ingeniería de experiencia del cliente. Por ejemplo:

- [Using Azure Information Protection to protect PDF’s and Adobe Acrobat Reader to view them](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Using-Azure-Information-Protection-to-protect-PDF-s-and-Adobe/ba-p/282010) (Uso de Azure Information Protection para proteger archivos PDF y de Adobe Acrobat Reader para verlos)

- [Cataloging your Sensitive Data with AIP, Even Before Configuring Labels!](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Cataloging-your-Sensitive-Data-with-AIP-Even-Before-Configuring/ba-p/267241) (Catalogación de la información confidencial con AIP, incluso antes de configurar etiquetas.)

- [Azure Information Protection Scanner Express Installation](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-Scanner-Express-Installation/ba-p/265424) (Instalación rápida del analizador de Azure Information Protection)

- [Discovery of Sensitive Data Using the AIP Scanner (AIP Premium P1)](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Discovery-of-Sensitive-Data-Using-the-AIP-Scanner-AIP-Premium-P1/ba-p/252040) (Detección de información confidencial mediante el analizador de AIP [AIP Premium P1])

## <a name="next-steps"></a>Pasos siguientes

¿No ve su escenario en la lista? Consulte el [plan para la implementación](deployment-roadmap.md) para obtener una lista completa de pasos de planeación e implementación.

Si está dando sus primeros pasos en Azure Information Protection, consulte [¿Qué es Azure Information Protection?](what-is-information-protection.md) para ver una introducción rápida al servicio antes de comenzar la implementación.
