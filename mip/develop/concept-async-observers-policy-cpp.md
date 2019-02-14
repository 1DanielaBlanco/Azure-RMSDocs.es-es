---
title: 'Conceptos: observadores de API de directiva en el SDK de MIP.'
description: El SDK de MIP está diseñado para ser casi completamente asincrónico. Este artículo le ayudará a comprender cómo se implementan y se usan los observadores de API de directiva para el asincronismo.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: d822a8ea57def13d2f04ac1c18b22ff629e413ad
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56251183"
---
# <a name="microsoft-information-protection-sdk---policy-api-observers"></a>SDK de Microsoft Information Protection: observadores de API de directiva

El SDK de API de directiva contiene una clase de observador. Los miembros observador son virtuales y se deben reemplazar para controlar las devoluciones de llamada para las operaciones asincrónicas.

- [`mip::PolicyProfile::Observer`](reference/class_mip_policyprofile_observer.md)

Cuando se completa una operación asincrónica, se llama a la función miembro `OnXxx()` correspondiente al resultado. Algunos ejemplos son `OnLoadSuccess()`, `OnLoadFailure()` y `OnAddEngineSuccess()` para `mip::Profile::Observer`.

En los ejemplos siguientes, se muestra el modelo de patrón de promesa o futuro, que también se usa en los ejemplos del SDK; también se puede ampliar para implementar el comportamiento deseado de la devolución de llamada. 

## <a name="profile-observer-implementation"></a>Implementación del observador del perfil

En el ejemplo siguiente, hemos creado una clase, `ProfileObserver`, que se deriva de `mip::Profile::Observer`. Se han reemplazado las funciones miembro para usar el patrón de promesa o futuro usado en los ejemplos.

**Tenga en cuenta**: Los siguientes ejemplos se implementan parcialmente y no incluyen invalidaciones para el `mip::ProfileEngine` relacionados con los observadores.

### <a name="profileobserverh"></a>profile_observer.h

En el encabezado, definimos `ProfileObserver`, que deriva de `mip::Profile::Observer`, y después reemplazamos cada una de las funciones miembro.

```cpp
class ProfileObserver final : public mip::Profile::Observer {
public:
ProfileObserver() { }
  void OnLoadSuccess(const std::shared_ptr<mip::Profile>& profile, const std::shared_ptr<void>& context) override;
  void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
  //TODO: Implement remaining members
};
```

### <a name="profileobservercpp"></a>profile_observer.cpp

En la propia implementación, definimos una acción que se realizará para cada función miembro del observador.

Cada miembro acepta dos parámetros. El primero es un puntero compartido a la clase controlada por la función. `ProfileObserver::OnLoadSuccess` espera recibir `mip::Profile`. `ProfileObserver::OnAddEngineSuccess` espera `mip::ProfileEngine`.

El segundo es un puntero compartido al *contexto*. En nuestra implementación, el contexto es una referencia a `std::promise`, pasado como `shared_ptr<void>`. La primera línea de la función convierte esto a `std::promise` y, después, se almacena en un objeto denominado `promise`.

Por último, para preparar el futuro, se establece `promise->set_value()` y se pasa el objeto `mip::Profile`.

```cpp
#include "profile_observer.h"
#include <future>

//Called when Profile is successfully loaded
void ProfileObserver::OnLoadSuccess(const std::shared_ptr<mip::Profile>& profile, const std::shared_ptr<void>& context) {
  //cast context to promise
  auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::Profile>>>(context);
  //set promise value to profile
  promise->set_value(profile);
}

//Called when Profile fails to load
void ProfileObserver::OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) {
  auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::Profile>>>(context);
  promise->set_exception(error);
}

//TODO: Implement remaining observer members
```

Al realizar cualquier operación asincrónica, la implementación del observador se pasa al constructor de la configuración o a la función asincrónica en sí. 

