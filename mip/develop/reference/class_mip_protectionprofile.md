---
title: clase mip ProtectionProfile
description: Referencia de la clase mip ProtectionProfile
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a7dffb4a6b1490ef185eb9a5062f394f4509f00a
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446692"
---
# <a name="class-mipprotectionprofile"></a>clase mip::ProtectionProfile 
[ProtectionProfile](class_mip_protectionprofile.md) es la clase raíz para realizar las operaciones de protección.
Una aplicación tiene que crear una clase [ProtectionProfile](class_mip_protectionprofile.md) antes de realizar cualquier operación de protección.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Obtiene la configuración utilizada por [ProtectionProfile](class_mip_protectionprofile.md) durante su inicialización y a lo largo de su vigencia.
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  Inicia la operación de los motores de la lista.
public std::vector<std::string> ListEngines()  |  Muestra una lista de motores.
public void AddEngineAsync(const ProtectionEngine::Settings& settings, const std::shared_ptr<void>& context)  |  Comienza a agregar un nuevo motor de protección al perfil.
public std::shared_ptr<ProtectionEngine> AddEngine(const ProtectionEngine::Settings& settings)  |  Agrega un nuevo motor de protección al perfil.
public void DeleteEngineAsync(const std::string& engineId, const std::shared_ptr<void>& context)  |  Inicia la eliminación del motor de protección con el id. especificado. Se eliminarán todos los datos del motor especificado.
 public void DeleteEngine(const std::string& engineId)  |  Elimina el motor de protección con el id. especificado. Se eliminarán todos los datos del motor especificado.
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Obtiene la configuración utilizada por [ProtectionProfile](class_mip_protectionprofile.md) durante su inicialización y a lo largo de su vigencia.

  
**Devuelve**: [configuración](class_mip_protectionprofile_settings.md) utilizada por [ProtectionProfile](class_mip_protectionprofile.md) durante su inicialización y a lo largo de su vigencia
  
### <a name="listenginesasync"></a>ListEnginesAsync
Inicia la operación de los motores de la lista.

Parámetros:  
* **context**: contexto de cliente que se pasará de manera opaca hacia los observadores.


Se llamará a [Profile::Observer](class_mip_protectionprofile_observer.md) una vez que la operación se complete correctamente o genere un error.
  
### <a name="listengines"></a>ListEngines
Muestra una lista de motores.

  
**Devuelve**: id. de motor almacenados en caché.
  
### <a name="addengineasync"></a>AddEngineAsync
Comienza a agregar un nuevo motor de protección al perfil.

Parámetros:  
* **settings**: el objeto [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) que especifica los parámetros del motor. 


* **context**: contexto de cliente que se pasará de manera opaca hacia los observadores.


Se llamará a [Profile::Observer](class_mip_protectionprofile_observer.md) una vez que la operación se complete correctamente o genere un error.
  
### <a name="protectionengine"></a>ProtectionEngine
Agrega un nuevo motor de protección al perfil.

Parámetros:  
* **settings**: el objeto [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) que especifica los parámetros del motor.



  
**Devuelve**: nuevos elementos [ProtectionEngine](class_mip_protectionengine.md) creados.
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
Inicia la eliminación del motor de protección con el id. especificado. Se eliminarán todos los datos del motor especificado.

Parámetros:  
* **id**: el id. del motor único. 


* **context**: contexto de cliente que se pasará de manera opaca hacia los observadores.


Se llamará a [Profile::Observer](class_mip_protectionprofile_observer.md) una vez que la operación se complete correctamente o genere un error.
  
### <a name="deleteengine"></a>DeleteEngine
Elimina el motor de protección con el id. especificado. Se eliminarán todos los datos del motor especificado.

Parámetros:  
* **id**: el id. del motor único.

