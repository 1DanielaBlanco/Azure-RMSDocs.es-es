---
# required metadata

title: Mejoras de este SDK | Azure RMS
description: En este tema se describe cómo RMS SDK 2.1 constituye una mejora considerable sobre el SDK original de Active Directory Rights Management Services.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 622D5C6E-07D5-4C71-A99D-9823C1FE6936
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** El contenido de este SDK no es actual. Durante un breve periodo podrá encontrar la [versión actual](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx) de la documentación en MSDN. **
# Mejoras de este SDK
En este tema se describe cómo Rights Management Services SDK 2.1 de es una mejora considerable sobre el [SDK original de Active Directory Rights Management Services](https://msdn.microsoft.com/library/Cc530379) en términos del trabajo del desarrollador para crear una aplicación habilitada para derechos.

**Superficie de API**: la superficie de la API se ha reducido considerablemente gracias a la abstracción, que libera muchos de los detalles de implementación del back-end. Desde una superficie de API de 84 funciones para el SDK de RMS, el SDK 2.1 de RMS incluye solo 20 funciones de API. La mayoría de las aplicaciones tendrán que utilizar solo un pequeño subconjunto de esta superficie de API.

**Tiempo de preparación**: con SDK 2.1 de RMS, podrá seguir una guía paso a paso para identificar qué recursos de la aplicación son confidenciales y cómo protegerlos. En esto se diferencia del SDK de RMS, con el que había que tener información detallada de los certificados, los formatos y las topologías y escribir código complejo de multithreading.

**Compatibilidad con varias topologías**: el SDK 2.1 de RMS le ayuda a minimizar la reescritura de código; la aplicación debería funcionar con todas las topologías, dado que eliminamos la complejidad de la topología para el desarrollador. Con el SDK de RMS, había que conocer todas las topologías compatibles y luego escribir y probar código específico para cada una.

**A prueba de futuro**: el SDK 2.1 de RMS le ayuda a minimizar la reescritura de código con habilitación para derechos; la aplicación debería funcionar ahora en cualquier entorno de RMS y aprovechar automáticamente las nuevas características cuando se publican actualizaciones de características fundamentales de RMS. En esto se diferencia del SDK de AD RMS, donde había que actualizar la aplicación para aprovechar las nuevas características explícitamente.

**Aviso importante**  
Todos los temas del [SDK original de Active Directory Rights Management Services](https://msdn.microsoft.com/library/Cc530379) en la biblioteca de MSDN comienzan ahora con la siguiente declaración de compatibilidad:

La funcionalidad de aprovechamiento del SDK de AD RMS expuesta por el cliente en Msdrm.dll está disponible para su uso en Windows Server 2008, Windows Vista, Windows Server 2008 R2, Windows 7, Windows Server 2012 y Windows 8. En versiones posteriores podría modificarse o no estar disponible. En su lugar, utilice el [SDK 2.1 de Active Directory Rights Management Services](microsoft-information-protection-and-control-client-portal.md), que aprovecha la funcionalidad expuesta por el cliente en *Msipc.dll*.

 

## Temas relacionados ##
* [Información general](ad-rms-overview.md)
* [Active Directory Rights Management Services SDK](https://msdn.microsoft.com/library/Cc530379)
* [Rights Management Services SDK 2.1](microsoft-information-protection-and-control-client-portal.md)
 

 


<!--HONumber=Jun16_HO1-->


