---
title: 'Conceptos: controladores de protección en el SDK de MIP.'
description: Este artículo lo ayudará a comprender cómo se crean y se utilizan los controladores de la API de Protection para llamar a operaciones.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a087f1bdef5a010718c67fbdca938ecbb62e5faa
ms.sourcegitcommit: 823a14784f4b34288f221e3b3cb41bbd1d5ef3a6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/29/2018
ms.locfileid: "47453501"
---
# <a name="microsoft-information-protection-sdk---protection-handler-concepts"></a>SDK de Microsoft Information Protection: conceptos del controlador de Protection

En la API de Protection del SDK de MIP, `mip::ProtectionHandler` expone las funciones para cifrar y descifrar los búferes y flujos protegidos, realizar comprobaciones de acceso, obtener la licencia de publicación y obtener los atributos de la información protegida. 

## <a name="requirements"></a>Requisitos

Para crear un objeto `ProtectionHandler` con el fin trabajar con un archivo concreto, se requiere lo siguiente:

- Una función `ProtectionProfile`
- Una función `ProtectionEngine` agregada a `ProtectionProfile`
- Una clase que herede `mip::ProtectionHandler::Observer`, al igual que el patrón descrito [aquí]().
- Un objeto `mip::ProtectionDescriptor` o licencia de publicación

## <a name="create-a-protection-handler"></a>Creación de un controlador de protección

Los objetos `mip::ProtectionHandler` se crean proporcionando un elemento `ProtectionDescriptor` o una licencia de publicación serializada a uno de los dos funciones `ProtectionEngine`. El descriptor de protección debe generarse para proteger la información de texto simple que ya no tiene una licencia de publicación. La **licencia de publicación** se usará al descifrar el contenido ya protegido o al proteger contenido donde ya se ha creado la licencia. No se puede descifrar contenido protegido sin la licencia de publicación asociada.

`mip::ProtectionEngine` expone dos funciones para crear una función `ProtectionHandler`. Los parámetros son los mismos, a excepción del controlador o la licencia de publicación como primer parámetro.

- `mip::ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync`
  - Requiere `ProtectionDescriptor` como primer parámetro.
- `mip::ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync`
  - Necesita una licencia de publicación serializada, almacenada en `std::vector<unint8_t>` como primer parámetro.

### <a name="create-from-descriptor"></a>Creación a partir del descriptor

Si protege el contenido que aún no se ha protegido, o bien si aplica el nuevo grupo de protección al contenido, lo que implica que se haya descifrado, debe crearse un objeto `mip::ProtectionDescriptor`. Una vez creado, se pasa a `mip::ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync()` y el resultado se devuelve a través de `mip::ProtectionHandler::Observer`.

```cpp
auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<ProtectionHandler>>>();
auto handlerFuture = handlerPromise->get_future();
auto observer = std::make_shared<ProtectionHandlerObserverImpl>();

//Refer to ProtectionDescriptor docs for details on creating the descriptor
auto descriptor = CreateProtectionDescriptor(); //Stub function

mEngine->CreateProtectionHandlerFromDescriptorAsync(
    descriptor,
    mip::ProtectionHandlerCreationOptions::None,
    observer,
    handlerPromise);

auto handler = handlerFuture.get();
```

Después de crear correctamente el objeto `ProtectionHandler`, se pueden realizar operaciones de archivo (get/set/delete/commit).

### <a name="create-from-publishing-license"></a>Creación a partir de la licencia de publicación

En este ejemplo se da por supuesto que la licencia de publicación ya se ha leído desde algún origen y está almacenada en `std::vector<uint8_t> serializedPublishingLicense`.

```cpp

//TODO: Implement GetPublishingLicense()
//Snip implies that function reads PL from source file, database, stream, etc.
std::vector<uint8_t> serializedPublishingLicense = GetPublishingLicense(filePath);

auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<ProtectionHandler>>>();
auto handlerFuture = handlerPromise->get_future();

shared_ptr<ProtectionHandlerObserverImpl> handleObserver =
    std::make_shared<ProtectionHandlerObserverImpl>();

mEngine->CreateProtectionHandlerFromPublishingLicenseAsync(
    serializedPublishingLicense,
    mip::ProtectionHandlerCreationOptions::None,
    handleObserver,
    handlerPromise);

auto handler = handlerFuture.get();
```

