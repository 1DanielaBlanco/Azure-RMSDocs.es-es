---
title: Registro de uso y archivos de cliente de Azure Information Protection
description: Información sobre el registro de uso y los archivos de cliente de cliente de Azure Information Protection para Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/25/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5a34ab85-773f-4782-ba09-c321cddf5bc0
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 13f82bc12fd77d4f145b059c2962af01094760c3
ms.sourcegitcommit: 5892db302bdf96538ecb3af8e3c2f678f5d1ebe2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="admin-guide-azure-information-protection-client-files-and-client-usage-logging"></a>Guía del administrador: Registro de uso de cliente y archivos de cliente de Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2*

Después de haber instalado el cliente de Azure Information Protection, tiene que saber dónde se encuentran los archivos y supervisar cómo se usa el cliente.

## <a name="file-locations-for-the-azure-information-protection-client"></a>Ubicaciones de archivo del cliente de Azure Information Protection

Archivos de cliente:   

- Para los sistemas operativos de 64 bits: **\Archivos de programa (x86)\Microsoft Azure Information Protection**

- Para los sistemas operativos de 32 bits: **\Archivos de programa\Microsoft Azure Information Protection**

Archivos de registros de cliente y archivos de directiva actualmente instalado:

- Para los sistemas operativos de 32 y 64 bits: **%localappdata%\Microsoft\MSIP**

## <a name="usage-logging-for-the-azure-information-protection-client"></a>Registro de uso del cliente de Azure Information Protection

El cliente registra la actividad del usuario en el registro de eventos local de Windows **Aplicaciones y servicios** > **Azure Information Protection**. Los eventos incluyen la siguiente información:

- Versión de cliente, identificador de directiva

- Direcciones IP del usuario con sesión iniciada

- Nombre y ubicación del archivo

- Acción:

    - Definir etiqueta: id. de información 101
    
    - Definir etiqueta (inferior): id. de información 102
    
    - Definir etiqueta (superior): id. de información 103
    
    - Quitar etiqueta: id. de información 104
   
    - Sugerencia recomendada: información 105
    
    - Aplicar protección personalizada: id. de información 201
    
    - Quitar protección personalizada: id. de información 202
    
    - Inicio de sesión (operativo): id. de información 902
    
    - Descargar directiva (operativo): id. de información 901
    
- Origen de la acción:
    
    - Manual 
    
    - Recomendado
    
    - Automático  
    
    - Sistema (para iniciar sesión y descargar la directiva)
    
    - Default
    
- Etiqueta antes y después de la acción 
    
- Protección antes y después de la acción
    
- Justificación de usuario (si procede)
    

Para obtener más información sobre el registro de uso del servicio Azure Rights Management, vea [Registro y análisis del uso del servicio Azure Rights Management](../deploy-use/log-analyze-usage.md)



## <a name="next-steps"></a>Pasos siguientes
Ahora que ha identificado todos los archivos de registro asociados con el cliente de Azure Information Protection, vea la siguiente información adicional que puede necesitar para la compatibilidad con este cliente:

- [Personalizaciones](client-admin-guide-customizations.md)

- [Seguimiento de documentos](client-admin-guide-document-tracking.md)

- [Tipos de archivos admitidos](client-admin-guide-file-types.md)

- [Comandos de PowerShell](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
