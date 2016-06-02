---
# required metadata

title: Requisitos de RMS de Azure&#58; Servidores locales que son compatibles con Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e7d91f2d-d6a7-4c7e-821f-c94e4be9967d

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Requisitos de Azure RMS: Servidores locales que son compatibles con Azure RMS

*Se aplica a: Azure Rights Management, Office 365*

Los siguientes servidores locales son compatibles con Azure RMS cuando se usa el conector Azure RMS, que actúa como una interfaz de comunicaciones (una retransmisión) entre los servidores locales y Azure RMS. Además, esta configuración precisa que defina la sincronización de directorios entre sus bosques de Active Directory y Azure Active Directory.

-   **Exchange Server**:

    -   Exchange Server 2016

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server**:

    -   Office SharePoint Server 2016

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **Servidores de archivos que ejecutan Windows Server y usan Infraestructura de clasificación de archivos (FCI)**:

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > Dado que los servidores de archivos con Windows Server 2008 R2 no tienen una acción de tarea de administración de archivos integrada para aplicar protección RMS, puede usar el conector RMS para este escenario. Sin embargo, puede usar Infraestructura de clasificación de archivos y Azure RMS en estos sistemas operativos si configura una tarea de administración de archivos personalizada para ejecutar un ejecutable o script que pueda proteger archivos mediante Azure RMS. Por ejemplo, un script de Windows PowerShell que usa los [cmdlets de protección de RMS](https://msdn.microsoft.com/library/azure/mt433195.aspx).
    > 
    > También puede usar estos cmdlets con servidores que ejecuten versiones posteriores de Windows Server, con la ventaja de que estos cmdlets pueden proteger todos los tipos de archivo. El conector RMS solo protege archivos de Office. Para obtener instrucciones sobre los procedimientos, consulte [Protección de RMS con la infraestructura de clasificación de archivos de Windows Server &#40;FCI&#41](../rms-client/configure-fci.md).

El conector RMS es compatible en Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2.

Para más información sobre cómo configurar el conector RMS para estos servidores locales, consulte [Implementación del conector de Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## Pasos siguientes
Para buscar otros requisitos, consulte [Requisitos de Azure Rights Management](requirements-azure-rms.md).


<!--HONumber=May16_HO2-->


