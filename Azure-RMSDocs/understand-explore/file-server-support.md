---
# required metadata

title: Servidores de archivos que ejecutan Windows Server y usan la infraestructura de clasificación de archivos (FCI) | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8fdad425-5daf-4ce1-822f-9d2fb0b87df1

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Servidores de archivos que ejecutan Windows Server y usan Infraestructura de clasificación de archivos (FCI)

*Se aplica a: Azure Rights Management, Office 365*


Cuando configuras Windows Server para usar Infraestructura de clasificación de archivos, esta característica del administrador de recursos del servidor de archivos puede examinar archivos locales y determinar si contienen datos sensibles. Para archivos que cumplan este criterio, se etiquetan con propiedades de clasificación que define un administrador. Entonces, la Infraestructura de clasificación de archivos puede tomar medidas, según lo estipulado en la clasificación. Una de estas acciones es aplicar la protección de la información mediante [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] y la implementación del conector de Rights Management (también conocido como conector de RMS). Los archivos de Office se protegen así automáticamente con Azure RMS.

Para proteger todos los tipos de archivo, no use el conector RMS. En su lugar ejecute un script de Windows PowerShell usando cmdlets de la [herramienta de protección de RMS](https://www.microsoft.com/en-us/download/details.aspx?id=47256)..

Las directivas de clasificación se pueden configurar completamente y son enormemente ampliables para que puedas prevenir la pérdida potencial de datos de usuarios autorizados y no autorizados. Incluso pueden ayudar a reducir el riesgo de que los administradores de la red pierdan datos, ya que se pueden configurar directivas que no requieran que dichos administradores tengan acceso a los archivos.

Para obtener instrucciones sobre cómo implementar y configurar el conector RMS para archivos de Office, consulte [Deploying the Azure Rights Management connector](../deploy-use/deploy-rms-connector.md) (Implementación del conector de Azure Rights Management)..

Para obtener instrucciones sobre cómo usar el script de Windows PowerShell para todos los tipos de archivos, consulte [RMS Protection with Windows Server File Classification Infrastructure &#40;FCI&#41;](../rms-client/configure-fci.md) (Protección de RMS con la infraestructura de clasificación de archivos de Windows Server &#40;FCI&#41;).



## Pasos siguientes
Ahora que comprende cómo las aplicaciones y los servicios admiten Azure RMS, puede que le interese comparar Azure RMS con la versión local de Rights Management, Active Directory Rights Management Services (AD RMS). Para ver una comparación de características, requisitos y controles de seguridad, consulte [Comparing Azure Rights Management and AD RMS](compare-azure-rms-ad-rms.md) (Comparación de Azure Rights Management y AD RMS)..




<!--HONumber=Apr16_HO4-->


