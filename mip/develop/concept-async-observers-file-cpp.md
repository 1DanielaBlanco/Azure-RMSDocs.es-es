---
title: 'Conceptos: observadores de la API de archivos en el SDK de MIP.'
description: El SDK de MIP está diseñado para ser casi completamente asincrónico. Este artículo le ayudará a comprender cómo se implementan y usan los observadores de la API de archivos para la asincronía.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: aec8fd7df79fe44503887e22dc7e6a110407f98a
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259554"
---
# <a name="microsoft-information-protection-sdk---file-api-observers"></a>SDK de Microsoft Information Protection: observadores de API de archivos

La API de archivos contiene dos clases de observador. Los miembros del observador son virtuales y pueden invalidarse para controlar devoluciones de llamada de eventos.

- [`mip::FileProfile::Observer`](reference/class_mip_fileprofile_observer.md)
- [`mip::FileHandler::Observer`](reference/class_mip_filehandler_observer.md)

Cuando se completa una operación asincrónica, se llama a la función miembro `OnXxx()` correspondiente al resultado. Algunos ejemplos son `OnLoadSuccess()`, `OnLoadFailure()` y `OnAddEngineSuccess()` para `mip::FileProfile::Observer`.

En los ejemplos siguientes, se muestra el modelo de patrón de promesa o futuro, que también se usa en los ejemplos del SDK; también se puede ampliar para implementar el comportamiento deseado de la devolución de llamada. 

## <a name="file-profile-observer-implementation"></a>Implementación del observador del perfil de archivos

En el ejemplo siguiente, hemos creado una clase, `ProfileObserver`, que se deriva de `mip::FileProfile::Observer`. Se han reemplazado las funciones miembro para usar el patrón de promesa o futuro usado en los ejemplos.

**Tenga en cuenta**: Los siguientes ejemplos se implementan parcialmente y no incluyen invalidaciones para el `mip::FileEngine` relacionados con los observadores.

### <a name="profileobserverh"></a>profile_observer.h

En el encabezado, definimos `ProfileObserver`, que deriva de `mip::FileProfile::Observer`, y después reemplazamos cada una de las funciones miembro.

```cpp
class ProfileObserver final : public mip::FileProfile::Observer {
public:
ProfileObserver() { }
  void OnLoadSuccess(const std::shared_ptr<mip::FileProfile>& profile, const std::shared_ptr<void>& context) override;
  void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
  //TODO: Implement mip::FileEngine related observers.
};
```

### <a name="profileobservercpp"></a>profile_observer.cpp

En la propia implementación, definimos una acción que se realizará para cada función miembro del observador.

Cada miembro acepta dos parámetros. El primero es un puntero compartido a la clase que controlamos en la función. `ProfileObserver::OnLoadSuccess` espera recibir `mip::FileProfile`. `ProfileObserver::OnAddEngineSuccess` espera `mip::FileEngine`.

El segundo es un puntero compartido al *contexto*. En nuestra implementación, el contexto es una referencia a `std::promise`, pasado por referencia como `std::shared_ptr<void>`. La primera línea de la función convierte esto a `std::promise` y, después, se almacena en un objeto denominado `promise`.

Por último, para preparar el futuro, se establece `promise->set_value()` y se pasa el objeto `mip::FileProfile`.

```cpp
#include "profile_observer.h"
#include <future>

//Called when FileProfile is successfully loaded
void ProfileObserver::OnLoadSuccess(const std::shared_ptr<mip::FileProfile>& profile, const std::shared_ptr<void>& context) {
  //cast context to promise
  auto promise = 
  std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileProfile>>>(context);
  //set promise value to profile
  promise->set_value(profile);
}

//Called when FileProfile fails to load
void ProfileObserver::OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) {
  auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileProfile>>>(context);
  promise->set_exception(error);
}

//TODO: Implement mip::FileEngine related observers.
```

Cuando se crean instancias de cualquier clase SDK o se usa una función que realiza operaciones asincrónicas, se pasa la implementación del observador al constructor de la configuración o la propia función asincrónica. Al crear una instancia del objeto `mip::FileProfile::Settings`, el constructor adopta `mip::FileProfile::Observer` como uno de los parámetros. En el ejemplo siguiente, se muestra un elemento `ProfileObserver` personalizado que se usa en un constructor `mip::FileProfile::Settings`.

## <a name="filehandler-observer-implementation"></a>Implementación de FileHandler Observer

De forma similar al observador de perfil, `mip::FileHandler` implementa una clase `mip::FileHandler::Observers` para controlar notificaciones de eventos asincrónicas durante operaciones con archivos. La implementación es similar a la que se ha detallado anteriormente. `FileHandlerObserver` se define parcialmente a continuación. 

### <a name="filehandlerobserverh"></a>file_handler_observer.h

```cpp
#include "mip/file/file_handler.h"

class FileHandlerObserver final : public mip::FileHandler::Observer {
public:
  void OnCreateFileHandlerSuccess(
      const std::shared_ptr<mip::FileHandler>& fileHandler,
      const std::shared_ptr<void>& context) override;

  void OnCreateFileHandlerFailure(
      const std::exception_ptr& error,
      const std::shared_ptr<void>& context) override;

  //TODO: override remaining member functions inherited from mip::FileHandler::Observer
};
```

### <a name="filehandlerobservercpp"></a>file_handler_observer.cpp

En este ejemplo, se muestran solo las dos primeras funciones, pero en el resto de las funciones se usa un patrón similar a estas y a `ProfileObserver`.

```cpp
#include "file_handler_observer.h"

void FileHandlerObserver::OnCreateFileHandlerSuccess(const std::shared_ptr<mip::FileHandler>& fileHandler, const std::shared_ptr<void>& context) {
    auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileHandler>>>(context);
    promise->set_value(fileHandler);
}

void FileHandlerObserver::OnCreateFileHandlerFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) {
    auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileHandler>>>(context);
    promise->set_exception(error);
}

//TODO: override remaining member functions inherited from mip::FileHandler::Observer
```

