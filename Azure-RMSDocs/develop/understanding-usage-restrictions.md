---
title: "Descripción de las restricciones de uso | Azure RMS"
description: Todas las aplicaciones habilitadas para RMS deben aplicar restricciones de uso.
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: E388B16C-ECDA-4696-A040-D457D3C96766
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: cc383728d487cac45e59ef34ca43ba47c4db237b


---

# <a name="understanding-usage-restrictions"></a>Descripción de las restricciones de uso

Todas las aplicaciones habilitadas para RMS deben aplicar restricciones de uso. Una restricción de uso es una condición que se produce cuando un usuario intenta realizar una acción (p. ej. imprimir un documento), pero la directiva de RMS para ese documento no le concede el permiso o el derecho a realizar esa acción (p. ej. el derecho PRINT).

Los permisos de un usuario en relación con un documento se pueden consultar mediante la función [IpcAccessCheck](https://msdn.microsoft.com/library/hh535253.aspx).

## <a name="understanding-usage-restrictions"></a>Descripción de las restricciones de uso

-   Familiarícese con derechos estándar de RMS

    Para obtener el conjunto completo de derechos de RMS que puede exigir la aplicación, consulte [Usage restriction reference](usage-restriction-reference.md) (Referencia de restricción de uso).

    Tenga en cuenta es posible crear derechos definidos para la aplicación que sean específicos para su situación y que vayan más allá de los derechos de RMS.

-   Identificación de los puntos de cumplimiento de restricción de uso

    Un *punto de cumplimiento de restricción de uso* es un lugar en el flujo de control de la aplicación donde es necesario aplicar una restricción de uso. El tema [Usage restriction reference](usage-restriction-reference.md) (Referencia de restricción de uso) proporciona varios ejemplos de puntos de cumplimiento comunes.

    Evalúe su propia aplicación para determinar los puntos de cumplimiento de restricción pertinentes.

    Es posible que la aplicación no necesite todos los puntos de cumplimiento que se describen en [Usage restriction reference](usage-restriction-reference.md) (Referencia de restricción de uso). Por ejemplo, si la aplicación no permite a los usuarios imprimir contenido, no es necesario comprobar el derecho **IPC\_GENERIC\_PRINT**.

-   Actualización del código para realizar una comprobación de acceso en cada punto de cumplimiento

    Para obtener instrucciones acerca de cómo aplicar derechos específicos, consulte [Usage restriction reference](usage-restriction-reference.md) (Referencia de restricción de uso).

## <a name="related-topics"></a>Temas relacionados

* [IpcAccessCheck](https://msdn.microsoft.com/library/hh535253.aspx)
* [Referencia de restricción de uso](usage-restriction-reference.md)
 

 



<!--HONumber=Nov16_HO2-->


