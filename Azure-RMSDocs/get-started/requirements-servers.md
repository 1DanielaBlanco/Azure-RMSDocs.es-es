---
title: "Compatibilidad de servidor para la protección de datos de Azure RMS - AIP"
description: Identifique los productos del servidor local que pueden usar el servicio Azure Rights Management de Azure Information Protection con el conector de Rights Management.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/22/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e7d91f2d-d6a7-4c7e-821f-c94e4be9967d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 87e887bb121b3d92065153a5d264767ef87d517b
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2017
---
# <a name="on-premises-servers-that-support-azure-rights-management-data-protection"></a>Servidores locales compatibles con la protección de datos de Azure Rights Management

>*Se aplica a: Azure Information Protection, Office 365*

Los siguientes productos de servidor local son compatibles con Azure Information Protection al usar el conector de Azure Rights Management. Este conector actúa como una interfaz de comunicaciones (una retransmisión) entre los servidores locales y el servicio Azure Rights Management usado por Azure Information Protection para proteger los documentos y los correos electrónicos de Office. 

Para usar este conector, necesita configurar la sincronización de directorios entre los bosques de Active Directory y Azure Active Directory.

-   **Exchange Server**:

    -   Exchange Server 2016

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server**:

    -   Office SharePoint Server 2016

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **Servidores de archivos que ejecutan Windows Server y usan Infraestructura de clasificación de archivos (FCI)**:

    -   Windows Server 2016

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > Como los servidores de archivos con Windows Server 2008 R2 no tienen una acción de tarea de administración de archivos integrada para aplicar la protección de Rights Management, puede usar el conector de Rights Management para este escenario. Sin embargo, puede usar Infraestructura de clasificación de archivos y Azure RMS en estos sistemas operativos si configura una tarea de administración de archivos personalizada para ejecutar un ejecutable o script que pueda proteger archivos mediante Azure RMS. Por ejemplo, un script de Windows PowerShell que usa los [cmdlets AzureInformationProtection](/powershell/azureinformationprotection/vlatest/aip).
    > 
    > También puede usar estos cmdlets con servidores que ejecuten versiones posteriores de Windows Server, con la ventaja de que estos cmdlets pueden proteger todos los tipos de archivo. El conector RMS solo protege archivos de Office. Para obtener instrucciones sobre los procedimientos, consulte [Protección de RMS con la infraestructura de clasificación de archivos de Windows Server &#40;FCI&#41](../rms-client/configure-fci.md).

El conector de Rights Management es compatible con Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2.

Para más información sobre cómo configurar el conector de Rights Management para estos servidores locales, vea [Implementación del conector de Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## <a name="next-steps"></a>Pasos siguientes
Para buscar otros requisitos, consulte [Requisitos de Azure Rights Management](requirements-azure-rms.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]