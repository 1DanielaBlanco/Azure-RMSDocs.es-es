---
title: clase mip::ProtectionProfile
description: 'Documenta la clase MIP:: protectionprofile de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 14df005d62b753c871c2c03604be6276edc61493
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56254703"
---
# <a name="class-mipprotectionprofile"></a>clase mip::ProtectionProfile 
[ProtectionProfile](class_mip_protectionprofile.md) es la clase raíz para realizar las operaciones de protección.
Una aplicación tiene que crear una clase [ProtectionProfile](class_mip_protectionprofile.md) antes de realizar cualquier operación de protección.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Obtiene la configuración utilizada por [ProtectionProfile](class_mip_protectionprofile.md) durante su inicialización y a lo largo de su vigencia.
pública ListEnginesAsync void (const std:: shared_ptr\<void\>& contexto)  |  Inicia la operación de los motores de la lista.
Public std:: vector\<std:: String\> ListEngines()  |  Muestra una lista de motores.
pública AddEngineAsync void (const ProtectionEngine::Settings & configuración, const std:: shared_ptr\<void\>& contexto)  |  Comienza a agregar un nuevo motor de protección al perfil.
Public std:: shared_ptr\<ProtectionEngine\> AddEngine (ProtectionEngine::Settings const & configuración)  |  Agrega un nuevo motor de protección al perfil.
pública DeleteEngineAsync void (const std:: String & engineId, const std:: shared_ptr\<void\>& contexto)  |  Inicia la eliminación del motor de protección con el id. especificado. Se eliminarán todos los datos del motor especificado.
public void DeleteEngine(const std::string& engineId)  |  Elimina el motor de protección con el id. especificado. Se eliminarán todos los datos del motor especificado.
  
## <a name="members"></a>Miembros
  
### <a name="getsettings-function"></a>Función GetSettings
Obtiene la configuración utilizada por [ProtectionProfile](class_mip_protectionprofile.md) durante su inicialización y a lo largo de su vigencia.

  
**Devuelve**: La [configuración](class_mip_protectionprofile_settings.md) utilizada por [ProtectionProfile](class_mip_protectionprofile.md) durante su inicialización y a lo largo de su vigencia
  
### <a name="listenginesasync-function"></a>Función ListEnginesAsync
Inicia la operación de los motores de la lista.

Parámetros:  
* **context**: Contexto de cliente que se pasarán a los observadores de manera opaca


Se llamará a [Profile::Observer](class_mip_protectionprofile_observer.md) una vez que la operación se complete correctamente o genere un error.
  
### <a name="listengines-function"></a>Función ListEngines
Muestra una lista de motores.

  
**Devuelve**: Motor en caché los identificadores
  
### <a name="addengineasync-function"></a>Función AddEngineAsync
Comienza a agregar un nuevo motor de protección al perfil.

Parámetros:  
* **settings**: el objeto [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) que especifica los parámetros del motor. 


* **context**: Contexto de cliente que se pasarán a los observadores de manera opaca


Se llamará a [Profile::Observer](class_mip_protectionprofile_observer.md) una vez que la operación se complete correctamente o genere un error.
  
### <a name="addengine-function"></a>Función AddEngine
Agrega un nuevo motor de protección al perfil.

Parámetros:  
* **settings**: el objeto [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) que especifica los parámetros del motor.



  
**Devuelve**: Recién creado [ProtectionEngine](class_mip_protectionengine.md)
  
### <a name="deleteengineasync-function"></a>Función DeleteEngineAsync
Inicia la eliminación del motor de protección con el id. especificado. Se eliminarán todos los datos del motor especificado.

Parámetros:  
* **id**: el id. del motor único. 


* **context**: Contexto de cliente que se pasarán a los observadores de manera opaca


Se llamará a [Profile::Observer](class_mip_protectionprofile_observer.md) una vez que la operación se complete correctamente o genere un error.
  
### <a name="deleteengine-function"></a>Función DeleteEngine
Elimina el motor de protección con el id. especificado. Se eliminarán todos los datos del motor especificado.

Parámetros:  
* **id**: el id. del motor único.

