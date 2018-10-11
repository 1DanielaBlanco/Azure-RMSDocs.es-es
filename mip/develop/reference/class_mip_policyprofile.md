---
title: Clase mip PolicyProfile
description: Referencia de la clase mip PolicyProfile
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 387e28780cb0ef02d56050f534d4783fdebc286e
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446894"
---
# <a name="class-mippolicyprofile"></a>Clase mip::PolicyProfile 
[PolicyProfile](class_mip_policyprofile.md) es la clase raíz para el uso de las operaciones de Microsoft Information Protection. Una aplicación típica solo necesitará una clase [PolicyProfile](class_mip_policyprofile.md), pero puede crear varios perfiles si es necesario.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Obtiene la configuración establecida en el perfil.
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  Inicia la operación de los motores de la lista.
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  Inicia la descarga el motor de directivas con el identificador especificado.
public void AddEngineAsync(const PolicyEngine::Settings& settings, const std::shared_ptr<void>& context)  |  Comienza a agregar un nuevo motor de directivas al perfil.
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  Inicia la eliminación del motor de directivas con el identificador especificado. Todos los datos para el perfil dado se eliminarán.
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Obtiene la configuración establecida en el perfil.

  
**Devuelve**: configuración establecida en el perfil.
  
### <a name="listenginesasync"></a>ListEnginesAsync
Inicia la operación de los motores de la lista.

Parámetros:  
* **context**: un parámetro que se pasará en las funciones de observador. 


Se llamará a [PolicyProfile::Observer](class_mip_policyprofile_observer.md) después de la realización correcta o de un error.
  
### <a name="unloadengineasync"></a>UnloadEngineAsync
Inicia la descarga el motor de directivas con el identificador especificado.

Parámetros:  
* **id**: el identificador único del motor. 


* **context**: un parámetro que se desviará de forma opaca a las funciones de observador. 


Se llamará a [PolicyProfile::Observer](class_mip_policyprofile_observer.md) después de la realización correcta o de un error.
  
### <a name="addengineasync"></a>AddEngineAsync
Comienza a agregar un nuevo motor de directivas al perfil.

Parámetros:  
* **settings**: el objeto [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md) que especifica la configuración del motor. 


* **context**: un parámetro que se desviará a las funciones de observador. 


Se llamará a [PolicyProfile::Observer](class_mip_policyprofile_observer.md) después de la realización correcta o de un error.
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
Inicia la eliminación del motor de directivas con el identificador especificado. Todos los datos para el perfil dado se eliminarán.

Parámetros:  
* **id**: el identificador único del motor. 


* **context**: un parámetro que se pasará en las funciones de observador. 


Se llamará a [PolicyProfile::Observer](class_mip_policyprofile_observer.md) después de la realización correcta o de un error.