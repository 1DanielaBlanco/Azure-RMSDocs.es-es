---
title: Registro de uso y archivos de cliente de Azure Information Protection
description: Información sobre el registro de uso y los archivos de cliente de cliente de Azure Information Protection para Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/06/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 5a34ab85-773f-4782-ba09-c321cddf5bc0
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 7e72aa9af0d248f54880f8b5bb6df0ce75018f2b
ms.sourcegitcommit: bf58c5d94eb44a043f53711fbdcf19ce503f8aab
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47211231"
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
    
    - Definir etiqueta (inferior): id. de información 101
    
    - Definir etiqueta (superior): id. de información 101
    
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

- Permisos personalizados (si procede) que incluyen los [derechos de uso por su nombre de codificación](../configure-usage-rights.md#usage-rights-and-descriptions) para los usuarios, grupos u organizaciones especificados
    
Para obtener más información sobre el registro de uso del servicio de protección, vea [Registro y análisis del uso del servicio Azure Rights Management](../log-analyze-usage.md)

Para obtener más información sobre el registro de uso del servicio de protección, vea [Registro y análisis del uso del servicio Azure Rights Management](../log-analyze-usage.md)

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha identificado todos los archivos de registro asociados con el cliente de Azure Information Protection, vea la siguiente información adicional que puede necesitar para la compatibilidad con este cliente:

- [Personalizaciones](client-admin-guide-customizations.md)

- [Seguimiento de documentos](client-admin-guide-document-tracking.md)

- [Tipos de archivos admitidos](client-admin-guide-file-types.md)

- [Comandos de PowerShell](client-admin-guide-powershell.md)

