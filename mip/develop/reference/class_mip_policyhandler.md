---
title: clase mip::PolicyHandler
description: Documenta la clase mip::policyhandler de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: a03d9b90d1436cf4b53fd9cabf2177b27183679b
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259259"
---
# <a name="class-mippolicyhandler"></a>clase mip::PolicyHandler 
Esta clase proporciona una interfaz para todas las funciones de controlador de directiva de un archivo.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
Public std:: shared_ptr\<ContentLabel\> GetSensitivityLabel (ExecutionState const & estado)  |  Obtiene la etiqueta de confidencialidad del contenido existente.
Public std:: vector\<std:: shared_ptr\<acción\> \> ComputeActions (ExecutionState const & estado)  |  Ejecuta las reglas en el controlador según el estado especificado y devuelve la lista de acciones que se van a ejecutar.
public void NotifyCommittedActions(const ExecutionState& state)  |  Se realiza una llamada a las acciones calculadas que se han aplicado y los datos se confirman en el disco.
  
## <a name="members"></a>Miembros
  
### <a name="getsensitivitylabel-function"></a>Función GetSensitivityLabel
Obtiene la etiqueta de confidencialidad del contenido existente.

Parámetros:  
* **state**: Estado actual del contenido 



  
**Devuelve**: La etiqueta que se aplica actualmente al contenido. Si no se etiqueta, no se devolverá nada.
  
### <a name="computeactions-function"></a>Función ComputeActions
Ejecuta las reglas en el controlador según el estado especificado y devuelve la lista de acciones que se van a ejecutar.

Parámetros:  
* **state**: el estado de ejecución actual del contenido en donde se ejecutan las reglas. 



  
**Devuelve**: Lista de acciones que deben aplicarse en el contenido.
  
### <a name="notifycommittedactions-function"></a>Función NotifyCommittedActions
Se realiza una llamada a las acciones calculadas que se han aplicado y los datos se confirman en el disco.

Parámetros:  
* **state**: el estado de ejecución actual del contenido después de haber confirmado las acciones. 


: Esta llamada envía un evento de auditoría
