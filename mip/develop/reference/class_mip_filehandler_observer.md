---
title: clase mip FileHandler Observer
description: Referencia de la clase mip FileHandler Observer
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a587107afc2b8963d64c31ad47af81761bf2b9f8
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446205"
---
# <a name="class-mipfilehandlerobserver"></a>clase mip::FileHandler::Observer 
Interfaz de [Observer](class_mip_filehandler_observer.md) para que los clientes obtengan eventos de notificaciones relacionados con el controlador de archivos.
Todos los errores que se heredan de [mip::Error](class_mip_error.md). El cliente no debe volver a llamar al motor en el subproceso que llama al observador.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public virtual void OnCreateFileHandlerSuccess(const std::shared_ptr<FileHandler>& fileHandler, const std::shared_ptr<void>& context)  |  Se llama cuando el controlador se ha creado correctamente.
public virtual void OnCreateFileHandlerFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando se producen errores al crear el controlador.
public virtual void OnGetLabelSuccess(const std::shared_ptr<ContentLabel>& label, const std::shared_ptr<void>& context)  |  Se llama cuando la etiqueta se recupera correctamente.
public virtual void OnGetLabelFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando se producen errores al recuperar la etiqueta.
public virtual void OnGetProtectionSuccess(const std::shared_ptr<ProtectionHandler>& protectionHandler, const std::shared_ptr<void>& context)  |  Se llama cuando la directiva de protección se recupera correctamente.
public virtual void OnGetProtectionFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando se producen errores al recuperar la directiva de protección.
public virtual void OnCommitSuccess(bool committed, const std::shared_ptr<void>& context)  |  Se llama cuando se realizó correctamente la confirmación de los cambios en el archivo.
public virtual void OnCommitFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando se producen errores al confirmar los cambios en el archivo.
  
## <a name="members"></a>Miembros
  
### <a name="oncreatefilehandlersuccess"></a>OnCreateFileHandlerSuccess
Se llama cuando el controlador se ha creado correctamente.
  
### <a name="oncreatefilehandlerfailure"></a>OnCreateFileHandlerFailure
Se llama cuando se producen errores al crear el controlador.
  
### <a name="ongetlabelsuccess"></a>OnGetLabelSuccess
Se llama cuando la etiqueta se recupera correctamente.
  
### <a name="ongetlabelfailure"></a>OnGetLabelFailure
Se llama cuando se producen errores al recuperar la etiqueta.
  
### <a name="ongetprotectionsuccess"></a>OnGetProtectionSuccess
Se llama cuando la directiva de protección se recupera correctamente.
  
### <a name="ongetprotectionfailure"></a>OnGetProtectionFailure
Se llama cuando se producen errores al recuperar la directiva de protección.
  
### <a name="oncommitsuccess"></a>OnCommitSuccess
Se llama cuando se realizó correctamente la confirmación de los cambios en el archivo.
  
### <a name="oncommitfailure"></a>OnCommitFailure
Se llama cuando se producen errores al confirmar los cambios en el archivo.