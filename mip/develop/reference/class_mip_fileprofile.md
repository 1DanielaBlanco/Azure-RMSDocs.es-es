---
title: clase mip::FileProfile
description: 'Documenta la clase MIP:: fileprofile de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 0210bc6b3bdf9ffdbe3f34c2c606997773d16b31
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651095"
---
# <a name="class-mipfileprofile"></a>clase mip::FileProfile 
La clase [FileProfile](class_mip_fileprofile.md) es la clase raíz para el uso de las operaciones de Microsoft Information Protection.
Una aplicación típica solo necesitará un perfil.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Devuelve la configuración del perfil.
pública ListEnginesAsync void (const std:: shared_ptr\<void\>& contexto)  |  Inicia la operación de los motores de la lista.
pública UnloadEngineAsync void (const std:: String & Id., const std:: shared_ptr\<void\>& contexto)  |  Inicia la descarga el motor de archivos con el identificador especificado.
pública AddEngineAsync void (const FileEngine::Settings & configuración, const std:: shared_ptr\<void\>& contexto)  |  Comienza a agregar un nuevo motor de archivos al perfil.
pública DeleteEngineAsync void (const std:: String & Id., const std:: shared_ptr\<void\>& contexto)  |  Inicia la eliminación del motor de archivos con el identificador especificado. Todos los datos para el perfil dado se eliminarán.
  
## <a name="members"></a>Miembros
  
### <a name="getsettings-function"></a>Función GetSettings
Devuelve la configuración del perfil.
  
### <a name="listenginesasync-function"></a>Función ListEnginesAsync
Inicia la operación de los motores de la lista.
Se llamará a [FileProfile::Observer](class_mip_fileprofile_observer.md) después de la realización correcta o de un error.
  
### <a name="unloadengineasync-function"></a>Función UnloadEngineAsync
Inicia la descarga el motor de archivos con el identificador especificado.
Se llamará a [FileProfile::Observer](class_mip_fileprofile_observer.md) después de la realización correcta o de un error.
  
### <a name="addengineasync-function"></a>Función AddEngineAsync
Comienza a agregar un nuevo motor de archivos al perfil.
Se llamará a [FileProfile::Observer](class_mip_fileprofile_observer.md) después de la realización correcta o de un error.
  
### <a name="deleteengineasync-function"></a>Función DeleteEngineAsync
Inicia la eliminación del motor de archivos con el identificador especificado. Todos los datos para el perfil dado se eliminarán.
Se llamará a [FileProfile::Observer](class_mip_fileprofile_observer.md) después de la realización correcta o de un error.