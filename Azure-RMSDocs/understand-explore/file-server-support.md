---
title: "Cómo los servidores de archivos que usan FCI son compatibles con Azure RMS desde AIP"
description: "Cómo la infraestructura de clasificación de archivos de Windows Server puede utilizarse con Azure RMS al implementar el conector RMS para proteger automáticamente los documentos de Office."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/17/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8fdad425-5daf-4ce1-822f-9d2fb0b87df1
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 3f7a06edc5d685d9ca103d9e7cd0f70c3a5f7874
ms.sourcegitcommit: 55a71f83947e7b178930aaa85a8716e993ffc063
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2017
---
# <a name="how-file-servers-that-run-windows-server-and-use-file-classification-infrastructure-fci-support-azure-rights-management"></a>Cómo los servidores de archivos que ejecutan Windows Server y usan la infraestructura de clasificación de archivos (FCI) son compatibles con Azure Rights Management

>*Se aplica a: Azure Information Protection, Office 365*


Cuando configuras Windows Server para usar Infraestructura de clasificación de archivos, esta característica del administrador de recursos del servidor de archivos puede examinar archivos locales y determinar si contienen datos sensibles. Para archivos que cumplan este criterio, se etiquetan con propiedades de clasificación que define un administrador. Entonces, la Infraestructura de clasificación de archivos puede tomar medidas, según lo estipulado en la clasificación. Una de estas acciones es aplicar la protección de la información mediante [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] y la implementación del conector de Rights Management (también conocido como conector de RMS). Los archivos de Office se protegen así automáticamente con Azure RMS.

Para proteger todos los tipos de archivo, no use el conector de RMS. En su lugar, ejecute un script de Windows PowerShell que usa los cmdlets del [módulo de Azure Information Protection](../rms-client/client-admin-guide-powershell.md).

Las directivas de clasificación se pueden configurar completamente y son enormemente ampliables para que puedas prevenir la pérdida potencial de datos de usuarios autorizados y no autorizados. Incluso pueden ayudar a reducir el riesgo de que los administradores de la red pierdan datos, ya que se pueden configurar directivas que no requieran que dichos administradores tengan acceso a los archivos.

Para obtener instrucciones sobre cómo implementar y configurar el conector de RMS para archivos de Office, consulte [Implementación del conector de Azure Rights Management](../deploy-use/deploy-rms-connector.md).

Para obtener instrucciones sobre cómo usar el script de Windows PowerShell para todos los tipos de archivos, consulte [Protección de RMS con la infraestructura de clasificación de archivos de Windows Server &#40; FCI &#41;](../rms-client/configure-fci.md).



## <a name="next-steps"></a>Pasos siguientes
Ahora que comprende cómo las aplicaciones y los servicios admiten Azure RMS, puede que le interese comparar Azure RMS con la versión local de Rights Management, Active Directory Rights Management Services (AD RMS). Para ver una comparación de características, requisitos y controles de seguridad, consulte [Comparing Azure Rights Management and AD RMS](compare-azure-rms-ad-rms.md) (Comparación de Azure Rights Management y AD RMS).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

