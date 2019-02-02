---
title: clase mip::FileHandler::Observer
description: 'Documenta la clase MIP:: filehandler de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 33f8a9c0d90d7f64295d469004c36a4c4cc80338
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650636"
---
# <a name="class-mipfilehandlerobserver"></a>clase mip::FileHandler::Observer 
Interfaz de [Observer](class_mip_filehandler_observer.md) para que los clientes obtengan eventos de notificaciones relacionados con el controlador de archivos.
Todos los errores que se heredan de [mip::Error](class_mip_error.md). El cliente no debe volver a llamar al motor en el subproceso que llama al observador.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
OnCreateFileHandlerSuccess de void virtual pública (const std:: shared_ptr\<FileHandler\>& fileHandler, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando el controlador se ha creado correctamente.
OnCreateFileHandlerFailure de void virtual pública (std::exception_ptr const & error, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando se producen errores al crear el controlador.
OnClassifySuccess de void virtual pública (const std:: vector\<std:: shared_ptr\<acción\>\>& acciones, const std:: shared_ptr\<void\>& contexto)  |  Se le llama cuando clasificar correcto.
OnClassifyFailure de void virtual pública (std::exception_ptr const & error, const std:: shared_ptr\<void\>& contexto)  |  Se le llama cuando clasificar error.
public virtual void OnGetDecryptedTemporaryFileSuccess(const std::string& decryptedFilePath, const std::shared_ptr\<void\>& context)  |  Se llama cuando se obtenga el éxito de descifrado de archivo temporal.
OnGetDecryptedTemporaryFileFailure de void virtual pública (std::exception_ptr const & error, const std:: shared_ptr\<void\>& contexto)  |  Se llama al obtener el archivo temporal descifrado no se pudo.
OnCommitSuccess de void virtual pública (bool confirmado, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando se realizó correctamente la confirmación de los cambios en el archivo.
OnCommitFailure de void virtual pública (std::exception_ptr const & error, const std:: shared_ptr\<void\>& contexto)  |  Se llama cuando se producen errores al confirmar los cambios en el archivo.
  
## <a name="members"></a>Miembros
  
### <a name="oncreatefilehandlersuccess-function"></a>Función OnCreateFileHandlerSuccess
Se llama cuando el controlador se ha creado correctamente.
  
### <a name="oncreatefilehandlerfailure-function"></a>Función OnCreateFileHandlerFailure
Se llama cuando se producen errores al crear el controlador.
  
### <a name="onclassifysuccess-function"></a>Función OnClassifySuccess
Se le llama cuando clasificar correcto.
  
### <a name="onclassifyfailure-function"></a>Función OnClassifyFailure
Se le llama cuando clasificar error.
  
### <a name="ongetdecryptedtemporaryfilesuccess-function"></a>Función OnGetDecryptedTemporaryFileSuccess
Se llama cuando se obtenga el éxito de descifrado de archivo temporal.
  
### <a name="ongetdecryptedtemporaryfilefailure-function"></a>Función OnGetDecryptedTemporaryFileFailure
Se llama al obtener el archivo temporal descifrado no se pudo.
  
### <a name="oncommitsuccess-function"></a>Función OnCommitSuccess
Se llama cuando se realizó correctamente la confirmación de los cambios en el archivo.
  
### <a name="oncommitfailure-function"></a>Función OnCommitFailure
Se llama cuando se producen errores al confirmar los cambios en el archivo.