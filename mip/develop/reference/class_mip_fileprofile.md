---
title: clase mip::FileProfile
description: 'Documenta la clase MIP:: fileprofile de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: f6578d4bb3a8926b38b02b06ca2ca525dc524582
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56256335"
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
