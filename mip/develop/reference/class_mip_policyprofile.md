---
title: Clase mip::PolicyProfile
description: Documenta la clase mip::policyprofile de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: c97f6335159f99c97ff68e233ed7d357242bedb3
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651163"
---
# <a name="class-mippolicyprofile"></a>Clase mip::PolicyProfile 
[PolicyProfile](class_mip_policyprofile.md) es la clase raíz para el uso de las operaciones de Microsoft Information Protection. Una aplicación típica solo necesitará un elemento [PolicyProfile](class_mip_policyprofile.md), pero puede crear varios perfiles si es necesario.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Obtiene la configuración establecida en el perfil.
pública ListEnginesAsync void (const std:: shared_ptr\<void\>& contexto)  |  Inicia la operación de los motores de la lista.
pública UnloadEngineAsync void (const std:: String & Id., const std:: shared_ptr\<void\>& contexto)  |  Inicia la descarga el motor de directivas con el identificador especificado.
pública AddEngineAsync void (const PolicyEngine::Settings & configuración, const std:: shared_ptr\<void\>& contexto)  |  Comienza a agregar un nuevo motor de directivas al perfil.
pública DeleteEngineAsync void (const std:: String & Id., const std:: shared_ptr\<void\>& contexto)  |  Inicia la eliminación del motor de directivas con el identificador especificado. Todos los datos para el perfil dado se eliminarán.
  
## <a name="members"></a>Miembros
  
### <a name="getsettings-function"></a>Función GetSettings
Obtiene la configuración establecida en el perfil.

  
**Devuelve**: Configuración establecida en el perfil.
  
### <a name="listenginesasync-function"></a>Función ListEnginesAsync
Inicia la operación de los motores de la lista.

Parámetros:  
* **context**: un parámetro que se pasará en las funciones de observador. 


Se llamará a [PolicyProfile::Observer](class_mip_policyprofile_observer.md) después de la realización correcta o de un error.
  
### <a name="unloadengineasync-function"></a>Función UnloadEngineAsync
Inicia la descarga el motor de directivas con el identificador especificado.

Parámetros:  
* **id**: el id. del motor único. 


* **context**: un parámetro que se desviará de forma opaca a las funciones de observador. 


Se llamará a [PolicyProfile::Observer](class_mip_policyprofile_observer.md) después de la realización correcta o de un error.
  
### <a name="addengineasync-function"></a>Función AddEngineAsync
Comienza a agregar un nuevo motor de directivas al perfil.

Parámetros:  
* **settings**: el objeto [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md) que especifica la configuración del motor. 


* **context**: un parámetro que se desviará a las funciones de observador. 


Se llamará a [PolicyProfile::Observer](class_mip_policyprofile_observer.md) después de la realización correcta o de un error.
  
### <a name="deleteengineasync-function"></a>Función DeleteEngineAsync
Inicia la eliminación del motor de directivas con el identificador especificado. Todos los datos para el perfil dado se eliminarán.

Parámetros:  
* **id**: el id. del motor único. 


* **context**: un parámetro que se pasará en las funciones de observador. 


Se llamará a [PolicyProfile::Observer](class_mip_policyprofile_observer.md) después de la realización correcta o de un error.