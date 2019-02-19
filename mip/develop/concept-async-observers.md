---
title: 'Conceptos: observadores en el SDK de MIP.'
description: El SDK de MIP está diseñado para ser casi completamente asincrónico. Este artículo le ayudará a comprender cómo se implementan y usan los observadores de la API de archivo para la asincronía.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 9ee7e0bcf7fdd42bb989067adf1037ac8d371cad
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259667"
---
# <a name="microsoft-information-protection-sdk---observer-concepts"></a>SDK de Microsoft Information Protection: conceptos de observador

El SDK de MIP está diseñado para ser casi completamente asincrónico. Por ejemplo, cualquier operación que dé como resultado una E/S de archivo o de red se realiza de forma asincrónica. Para controlar las notificaciones de eventos de estos eventos asincrónicos, el SDK usa el [patrón del observador](https://wikipedia.org/wiki/Observer_pattern). 

## <a name="implementation-overview"></a>Información general sobre la implementación

Al crear un objeto que realizará una operación asincrónica, es necesario implementar una clase `Observer`. Los observadores recibirán los eventos de notificación relacionados con las distintas operaciones asincrónicas en el SDK de MIP y proporcionarán el resultado al autor de la llamada.

Las funciones de cada clase `Observer` son virtuales y se reemplazan por el modelo asincrónico preferido. El SDK implementa el patrón del observador de notificación de eventos mediante `std::promise` y `std::future`.

Cada observador específico de la clase contiene un conjunto de funciones de operación correcta y con errores para el resultado de una operación asincrónica. Las funciones de *operación correcta* devuelven el objeto asociado a la operación. Las funciones de *error*/** devuelven una excepción que contiene detalles sobre el motivo por el que la operación no se ha completado correctamente.

Por ejemplo, `FileProfile` admite las dos operaciones siguientes: 

- Agrega un nuevo motor al perfil mediante `FileProfile::AddEngineAsync`. 
- Puede descargar un motor desde el perfil mediante `FileProfile::UnloadEngineAsync`.

Como las dos funciones de `Observer` se implementan mediante una operación asincrónica, puede darse por hecho que hay **cuatro** métodos de `Observer` asociados a `FileProfile`: 

- `FileProfileObserver::OnAddEngineSuccess()`
- `FileProfileObserver::OnAddEngineError()`
- `FileProfileObserver::OnUnloadEngineSuccess`
- `FileProfileObserver::OnUnloadEngineError()`  

## <a name="mip-sdk-observer-classes"></a>Clases del observador del SDK de MIP

La API de archivo del SDK de MIP contiene dos observadores:

* `mip::FileProfile::Observer`
* `mip::FileHandler::Observer`

La API de directiva del SDK de MIP contiene un único observador:

* `mip::Profile::Observer`

La API de protección del SDK de MIP contiene tres observadores:

* `mip::ProtectionProfile::Observer`
* `mip::ProtectionEngine::Observer`
* `mip::ProtectionHandler::Observer`

## <a name="next-steps"></a>Pasos siguientes

Obtenga más información sobre cómo las distintas API implementan y usan los observadores:

* [Observadores de la API de archivo (C++)](concept-async-observers-file-cpp.md)
* [Observadores de la API de directiva (C++)](concept-async-observers-policy-cpp.md)
* [Observadores de la API de protección (C++)](concept-async-observers-protection-cpp.md)
