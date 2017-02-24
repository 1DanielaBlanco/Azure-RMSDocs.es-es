---
title: Registro de uso y archivos de cliente de Azure Information Protection | Azure Information Protection
description: "Información sobre el registro de uso y los archivos de cliente de cliente de Azure Information Protection para Windows."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5a34ab85-773f-4782-ba09-c321cddf5bc0
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ffed64826982756072456be18cced0226b6bb6cc
ms.openlocfilehash: 279e70416248e51dfc2331945b6193aa285c4003


---


# <a name="azure-information-protection-client-files-and-client-usage-logging"></a>Registro de uso de cliente y archivos de cliente de Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8 y Windows 7 con SP1*

Después de haber instalado el cliente de Azure Information Protection, tiene que saber dónde se encuentran los archivos y supervisar cómo se usa el cliente.

## <a name="file-locations-for-the-azure-information-protection-client"></a>Ubicaciones de archivo del cliente de Azure Information Protection

Archivos de cliente:    

- Para los sistemas operativos de 64 bits: **\Archivos de programa (x86)\Microsoft Azure Information Protection**

- Para los sistemas operativos de 32 bits: **\Archivos de programa\Microsoft Azure Information Protection**

Archivos de registros de cliente y archivos de directiva actualmente instalado:

- Para los sistemas operativos de 32 y 64 bits: **%localappdata%\Microsoft\MSIP**

## <a name="usage-logging-for-the-azure-information-protection-client"></a>Registro de uso del cliente de Azure Information Protection

El cliente registra la actividad del usuario en el registro de eventos local de Windows **Aplicaciones y servicios**, **Azure Information Protection**. Los eventos incluyen la siguiente información:

- Fecha, versión de cliente, id. de directiva

- Nombre de usuario de inicio de sesión, nombre de equipo

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
    
- Etiqueta antes y después de la acción 
    
- Protección antes y después de la acción
    
- Justificación de usuario (si procede)
    

Para obtener más información sobre el registro de uso del servicio Azure Rights Management, vea [Registro y análisis del uso del servicio Azure Rights Management](../deploy-use/log-analyze-usage.md)



## <a name="next-steps"></a>Pasos siguientes
Ahora que ha identificado todos los archivos de registro asociados con el cliente de Azure Information Protection, vea la siguiente información adicional que puede necesitar para la compatibilidad con este cliente:


- [Seguimiento de documentos](client-admin-guide-document-tracking.md)

- [Tipos de archivos admitidos](client-admin-guide-file-types.md)

- [Comandos de PowerShell](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



<!--HONumber=Feb17_HO2-->


