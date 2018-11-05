---
title: 'Conceptos: observadores de API de protección en el SDK de MIP.'
description: El SDK de MIP está diseñado para ser casi completamente asincrónico. Este artículo le ayudará a comprender cómo se implementan y se usan los observadores de API de protección para el asincronismo.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 35c0fb8eb358c5872ab378755d303425cc8e80a4
ms.sourcegitcommit: 2c4e72120213407516a49286368f9b2860505f56
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2018
ms.locfileid: "50236822"
---
# <a name="microsoft-information-protection-sdk---protection-api-observers"></a>SDK de Microsoft Information Protection: observadores de API de protección

La API de protección contiene tres clases de observador. Los miembros observador son virtuales y se pueden reemplazar para controlar las devoluciones de llamada para las operaciones asincrónicas.

- [Perfil de protección: `mip::ProtectionProfile::Observer`](reference/class_mip_ProtectionProfile_observer.md)
- [Motor de protección: `mip::ProtectionEngine::Observer`](reference/class_mip_ProtectionEngine_observer.md)
- [Controlador de protección: `mip::ProtectionHandler::Observer`](reference/class_mip_Protectionhandler_observer.md)

Cuando se completa una operación asincrónica, se llama a la función miembro `OnXxx()` correspondiente al resultado. Algunos ejemplos son `OnLoadSuccess()`, `OnLoadFailure()` y `OnAddEngineSuccess()` para `mip::ProtectionProfile::Observer`.

En los ejemplos siguientes, se muestra el modelo de patrón de promesa o futuro, que también se usa en los ejemplos del SDK; también se puede ampliar para implementar el comportamiento deseado de la devolución de llamada. 

## <a name="protectionprofile-observer-implementation"></a>Implementación del observador de ProtectionProfile

En el ejemplo siguiente, hemos creado una clase, `ProtectionProfileObserverImpl`, que se deriva de `mip::ProtectionProfile::Observer`. Se han reemplazado las funciones de miembro para usar el patrón de promesa o futuro utilizado a lo largo de los ejemplos.

### <a name="protectionprofileobserverimpl-class-declaration"></a>Declaración de clase ProtectionProfileObserverImpl

En el encabezado, definimos `ProtectionProfileObserverImpl`, que deriva de `mip::ProtectionProfile::Observer`, y después reemplazamos cada una de las funciones miembro.

```cpp
//ProtectionProfileObserverImpl.h
class ProtectionProfileObserverImpl final : public mip::ProtectionProfile::Observer {
public:
  ProtectionProfileObserverImpl() { }
  void OnLoadSuccess(const shared_ptr<mip::ProtectionProfile>& profile, const shared_ptr<void>& context) override;
  void OnLoadFailure(const exception_ptr& error, const shared_ptr<void>& context) override;
  void OnAddEngineSuccess(const shared_ptr<mip::ProtectionEngine>& engine, const shared_ptr<void>& context) override;
  void OnAddEngineError(const exception_ptr& error, const shared_ptr<void>& context) override;
};
```

### <a name="protectionprofileobserverimpl-implementation"></a>Implementación de ProtectionProfileObserverImpl

En la propia implementación, simplemente definimos una acción que se realizará para cada función miembro del observador.

Cada miembro acepta dos parámetros. El primero es un puntero compartido a la clase que controlamos en la función. `ProtectionObserver::OnLoadSuccess` espera recibir `mip::ProtectionProtection`, `ProtectionObserver::OnAddEngineSuccess` espera `mip::ProtectionEngine`.

El segundo es un puntero compartido al *contexto*. En nuestra implementación, el contexto es una referencia a `std::promise`, pasado como `shared_ptr<void>`. La primera línea de la función convierte esto a `std::promise` y, después, se almacena en un objeto denominado `promise`.

Por último, para preparar el futuro, se establece `promise->set_value()` y se pasa el objeto `mip::ProtectionProtection`.

```cpp
//protection_observers.cpp

void ProtectionProfileObserverImpl::OnLoadSuccess(
  const shared_ptr<mip::ProtectionProfile>& profile,
  const shared_ptr<void>& context) {
  auto loadPromise = static_cast<promise<shared_ptr<mip::ProtectionProfile>>*>(context.get());
  loadPromise->set_value(profile);
};

void ProtectionProfileObserverImpl::OnLoadFailure(const exception_ptr& error, const shared_ptr<void>& context) {
  auto loadPromise = static_cast<promise<shared_ptr<mip::ProtectionProfile>>*>(context.get());
  loadPromise->set_exception(error);
};

void ProtectionProfileObserverImpl::OnAddEngineSuccess(
  const shared_ptr<mip::ProtectionEngine>& engine,
  const shared_ptr<void>& context) {
  auto addEnginePromise = static_cast<promise<shared_ptr<mip::ProtectionEngine>>*>(context.get());
  addEnginePromise->set_value(engine);
};

void ProtectionProfileObserverImpl::OnAddEngineError(
  const exception_ptr& error,
  const shared_ptr<void>& context) {
  auto addEnginePromise = static_cast<promise<shared_ptr<mip::ProtectionEngine>>*>(context.get());
  addEnginePromise->set_exception(error);
};
```

Cuando se crean instancias de cualquier clase SDK o se usa una función que realiza operaciones asincrónicas, se pasa la implementación del observador al constructor de la configuración o la propia función asincrónica. Al crear una instancia del objeto `mip::ProtectionProfile::Settings`, el constructor adopta `mip::ProtectionProfile::Observer` como uno de los parámetros. En el ejemplo siguiente, se muestra un elemento `ProtectionProfileObserverImpl` personalizado que se usa en un constructor `mip::ProtectionProfile::Settings`.

## <a name="protectionhandler-observer-implementation"></a>Implementación del observador ProtectionHandler

De forma parecida al observador de protección, `mip::ProtectionHandler` implementa una clase `mip::ProtectionHandler::Observer` para controlar las notificaciones de eventos asincrónicos durante las operaciones de protección. La implementación es similar a la que se ha detallado anteriormente. `ProtectionHandlerObserverImpl` se define parcialmente a continuación. La implementación completa puede encontrarse en nuestro [repositorio GitHub de ejemplo](https://azure.microsoft.com/resources/samples/?sort=0&term=mip+sdk).

### <a name="protectionhandlerobserverimpl-class-declaration"></a>Declaración de clase ProtectionHandlerObserverImpl

```cpp
//protection_observers.h

class ProtectionHandlerObserverImpl final : public mip::ProtectionHandler::Observer {
public:
  ProtectionHandlerObserverImpl() { }
  void OnCreateProtectionHandlerSuccess(const shared_ptr<mip::ProtectionHandler>& protectionHandler, const shared_ptr<void>& context) override;
  void OnCreateProtectionHandlerError(const exception_ptr& error, const shared_ptr<void>& context) override;
};
```

### <a name="protectionhandlerobserverimpl-partial-implementation"></a>Implementación parcial de ProtectionHandlerObserverImpl

Este ejemplo muestra simplemente las dos primeras funciones, pero las funciones restantes usan un patrón similar a estas y a `ProtectionObserver`.

```cpp
//protection_observers.cpp

void ProtectionHandlerObserverImpl::OnCreateProtectionHandlerSuccess(
  const shared_ptr<mip::ProtectionHandler>& protectionHandler,
  const shared_ptr<void>& context) {
  auto createProtectionHandlerPromise = static_cast<promise<shared_ptr<mip::ProtectionHandler>>*>(context.get());
  createProtectionHandlerPromise->set_value(protectionHandler);
};

void ProtectionHandlerObserverImpl::OnCreateProtectionHandlerError(
  const exception_ptr& error,
  const shared_ptr<void>& context) {
  auto createProtectionHandlerPromise = static_cast<promise<shared_ptr<mip::ProtectionHandler>>*>(context.get());
  createProtectionHandlerPromise->set_exception(error);
};
```

