---
title: 'Conceptos: el objeto del motor de la API de protección'
description: Este artículo le ayudará a comprender los conceptos básicos sobre el objeto del motor de protección que se crea durante la inicialización de aplicaciones.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: da0c50de6a818fcd8beda0483696ba433ce22149
ms.sourcegitcommit: 823a14784f4b34288f221e3b3cb41bbd1d5ef3a6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/29/2018
ms.locfileid: "47453323"
---
# <a name="microsoft-information-protection-sdk---protection-api-engine-concepts"></a>SDK de Microsoft Information Protection: conceptos del motor de la API de protección

## <a name="implementation-add-a-protection-engine"></a>Implementación: agregar un motor de protección

En la API de archivo, la clase `mip::ProtectionProfile` es la clase raíz de todas las operaciones del SDK. Después de crear el perfil, ya podemos agregar un motor al perfil.

En el ejemplo siguiente, se muestra cómo usar un único motor para un único usuario autenticado.

### <a name="implementation-create-protection-engine-settings"></a>Implementación: crear la configuración del motor de protección

De forma similar a un perfil, el motor también necesita un objeto de configuración, `mip::ProtectionEngine::Settings`. Este objeto almacena el identificador único del motor, los datos de cliente personalizables que pueden usarse para depurar o para telemetría y, opcionalmente, la configuración regional.

Aquí, creamos un objeto `ProtectionEngine::Settings` llamado *engineSettings*. 

```cpp
ProtectionEngine::Settings engineSettings("UniqueID", "");
```

**Nota**: Si usa este método para crear el objeto de configuración de protección, también tendrá que establecer de forma manual el elemento CloudEndpointBaseUrl en https://api.aadrm.com.

Le recomendamos que el primer parámetro (**id**) sea algo que permita al motor conectarse fácilmente al usuario asociado **o** a un objeto `mip::Identity`. Para inicializar la configuración con `mip::Identity`:

```cpp
ProtectionEngine::Settings engineSettings(mip::Identity("Bob@Contoso.com", "");
```

Aunque suele pasarse en una variable para identificarlas, en lugar de codificarlas de forma rígida.

### <a name="implementation-add-the-protection-engine"></a>Implementación: agregar el motor de protección

Para agregar el motor, volveremos al patrón de promesa o futuro usado para cargar el perfil. En lugar de crear la promesa para `mip::ProtectionProfile`, usaremos `mip::ProtectionEngine`.

```cpp

  //auto profile will be std::shared_ptr<mip::ProtectionProfile>
  auto profile = profileFuture.get();

  //Create the ProtectionEngine::Settings object
  ProtectionEngine::Settings engineSettings("UniqueID", "");

  //Create a promise for std::shared_ptr<mip::ProtectionEngine>
  auto enginePromise = std::make_shared<std::promise<std::shared_ptr<mip::ProtectionEngine>>>();

  //Instantiate the future from the promise
  auto engineFuture = enginePromise->get_future();

  //Add the engine using AddEngineAsync, passing in the engine settings and the promise
  profile->AddEngineAsync(engineSettings, enginePromise);

  //get the future value and store in std::shared_ptr<mip::ProtectionEngine>
  auto engine = engineFuture.get();
```

El resultado final del código anterior es que hemos agregado correctamente al perfil un motor para el usuario autenticado.

## <a name="implementation-list-templates"></a>Implementación: lista de plantillas

Después de agregar el motor, ahora se puede mostrar una lista de todas las plantillas de confidencialidad disponibles para el usuario autenticado mediante una llamada a `engine->GetTemplatesAsync()`. 

`GetTemplatesAsync()` obtendrá la lista de identificadores de plantilla. El resultado se almacena en un vector de `std::shared_ptr<std::string>`.

### <a name="implementation-listsensitivitytemplates"></a>Implementation: ListSensitivityTemplates()

```cpp
auto loadPromise = std::make_shared<std::promise<shared_ptr<vector<string>>>>();
std::future<std::shared_ptr<std::vector<std::string>>> loadFuture = loadPromise->get_future();
mEngine->GetTemplatesAsync(engineObserver, loadPromise);
auto templates = loadFuture.get();
```

### <a name="implementation-print-the-template-ids"></a>Implementación: imprimir los identificadores de plantilla

```cpp
//Iterate through all template IDs in the vector
for (const auto& temp : *templates) {
  cout << "Template:" << "\n\tId: " << temp << endl;
}
```

Imprimir los nombres es una forma sencilla de mostrar que hemos extraído correctamente la directiva del servicio y hemos podido obtener las plantillas. Para aplicar la plantilla, se necesita el identificador de plantilla.

La asignación de plantillas a las etiquetas solo se puede realizar mediante la API de directiva si se examina el resultado de `ComputeActions()`.

## <a name="next-steps"></a>Pasos siguientes

Después de cargar el perfil y agregar el motor, ya tenemos plantillas y podemos agregar un controlador para empezar a leer, escribir o eliminar etiquetas de los archivos. Vea [Conceptos del controlador de protección](concept-handler-protection-cpp.md).