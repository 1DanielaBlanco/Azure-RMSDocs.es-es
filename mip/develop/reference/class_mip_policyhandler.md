---
title: clase mip PolicyHandler
description: Referencia de la clase mip PolicyHandler
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 23de5616558a298189cb885727d69a20373a3609
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445944"
---
# <a name="class-mippolicyhandler"></a>clase mip::PolicyHandler 
Esta clase proporciona una interfaz para todas las funciones de controlador de directiva de un archivo.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public std::shared_ptr<ContentLabel> GetSensitivityLabel(const ExecutionState& state)  |  Obtiene la etiqueta de confidencialidad del contenido existente.
public std::vector<std::shared_ptr<Action>> ComputeActions(const ExecutionState& state)  |  Ejecuta las reglas en el controlador según el estado especificado y devuelve la lista de acciones que se van a ejecutar.
 public void NotifyCommittedActions(const ExecutionState& state)  |  Se realiza una llamada a las acciones calculadas que se han aplicado y los datos se confirman en el disco.
  
## <a name="members"></a>Miembros
  
### <a name="contentlabel"></a>ContentLabel
Obtiene la etiqueta de confidencialidad del contenido existente.

Parámetros:  
* **state**: estado actual del contenido. 



  
**Devuelve**: la etiqueta aplicada actualmente en el contenido. Si no se etiqueta, no se devolverá nada.
  
### <a name="action"></a>Acción
Ejecuta las reglas en el controlador según el estado especificado y devuelve la lista de acciones que se van a ejecutar.

Parámetros:  
* **state**: el estado de ejecución actual del contenido en donde se ejecutan las reglas. 



  
**Devuelve**: la lista de acciones que deben aplicarse en el contenido.
  
### <a name="notifycommittedactions"></a>NotifyCommittedActions
Se realiza una llamada a las acciones calculadas que se han aplicado y los datos se confirman en el disco.

Parámetros:  
* **state**: el estado de ejecución actual del contenido después de haber confirmado las acciones. 


: esta llamada envía un evento de auditoría.