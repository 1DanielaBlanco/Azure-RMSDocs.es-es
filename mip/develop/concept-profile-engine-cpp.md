---
title: 'Conceptos: conceptos básicos en el SDK de MIP (perfil y motor)'
description: Este artículo le permitirá comprender los conceptos básicos del SDK, denominados perfil y motor, que se crean durante la inicialización de la aplicación.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 6f11944e7cceed39423af2a8104ce044d1f6eec6
ms.sourcegitcommit: 823a14784f4b34288f221e3b3cb41bbd1d5ef3a6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/29/2018
ms.locfileid: "47453425"
---
# <a name="microsoft-information-protection-sdk---profile-and-engine-object-concepts"></a>SDK de Microsoft Information Protection: conceptos de los objetos de perfil y motor

## <a name="profiles"></a>Profiles

El perfil es la clase raíz de todas las operaciones en el SDK de MIP. Antes de usar cualquiera de las tres API, es necesario que la aplicación cliente cree un perfil. Todas las operaciones futuras se realizarán con el perfil o con otros objetos *agregados* al perfil.

Hay tres tipos de perfiles en el SDK de MIP:

- [`PolicyProfile`](reference/class_mip_policyprofile.md): la clase de perfil para la API de directiva de MIP.
- [`ProtectionProfile`](reference/class_mip_protectionprofile.md): la clase de perfil para la API de protección de MIP.
- [`FileProfile`](reference/class_mip_fileprofile.md): la clase de perfil para la API de archivo de MIP.

Las API usada en la aplicación determinará la clase de perfil que se usará.

El perfil en sí proporciona las siguientes funciones:

- Define la ubicación de almacenamiento del estado del SDK. En los datos de estado, se incluyen los detalles del usuario, las directivas de usuario descargadas, los registros y los datos de telemetría.
- Define si es necesario cargar el estado en la memoria o tiene que persistir en el disco.
- Controla la autenticación al aceptar un objeto `mip::AuthDelegate`.
- Establece el identificador de la aplicación y el nombre descriptivo de la aplicación que usa el SDK.

### <a name="profile-settings"></a>Configuración de perfil

- `Path`: ruta del archivo donde se almacenan los datos de registro, telemetría y otros estados persistentes.
- `useInMemoryStorage`: un operador booleano que define si el estado tiene que almacenarse en memoria o en el disco.
- `authDelegate`: un puntero compartido de la clase `mip::AuthDelegate`. 
- `consentDelegate`: un puntero compartido de la clase `mip::ConsentDelegate`. 
- `observer`: un puntero compartido a la implementación `Observer` del perfil (en `PolicyProfile`, `ProtectionProfile` y `EngineProfile`).
- `applicationInfo`: un objeto `mip::ApplicationInfo`. Información sobre la aplicación que usa el SDK.

## <a name="engines"></a>Motores

En las API de protección, perfil y archivo, los motores proporcionan una interfaz para las operaciones realizadas en nombre de una identidad específica. Se agregará un motor al objeto de perfil por cada usuario que inicie sesión en la aplicación. Todas las operaciones realizadas en el motor estarán en el contexto de esa identidad.

Hay tres clases de motor en el SDK, una para cada API. En la lista siguiente, se muestran las clases de motor y algunas de las funciones asociadas a estas:

- [`mip::ProtectionEngine`]
- [`mip::PolicyEngine`](reference/class_mip_policyengine.md)
  - `ListSensitivityLabels()`: obtiene la lista de etiquetas para el motor cargado.
  - `GetSensitivityLabel()`: obtiene la etiqueta a partir del contenido existente.
  - `ComputeActions()`: si se proporciona con un identificador de etiqueta y metadatos opcionales, devuelve la lista de acciones que tienen que producirse para un elemento específico.
- [`mip::FileEngine`](reference/class_mip_fileengine.md)
  - `ListSensitivityLabels()`: obtiene la lista de etiquetas para el motor cargado.
  - `CreateFileHandler()`: crea `mip::FileHandler` para una secuencia o un archivo específico.

### <a name="engine-states"></a>Estados del motor

Un motor puede tener uno de estos dos estados:

- `CREATED`: al crearse, indica que el SDK tiene información de estado local suficiente después de llamar a los servicios de back-end necesarios.
- `LOADED`: el SDK ha creado las estructuras de datos necesarias para que el motor sea operativo.

Es necesario crear y cargar un motor para realizar cualquier operación. La clase `Profile` expone varios métodos de administración de motores: `AddEngineAsync`, `RemoveEngineAsync` y `UnloadEngineAsync`.

En la tabla siguiente, se describen los posibles estados del motor y qué método puede cambiar ese estado.

|         | NONE              | CREATED           | LOADED         |
|---------|-------------------|-------------------|----------------|
| NONE    |                   |                   | AddEngineAsync |
| CREATED | DeleteEngineAsync |                   | AddEngineAsync |
| LOADED  | DeleteEngineAsync | UnloadEngineAsync |                |

### <a name="engine-id"></a>Id. de motor

Cada motor tiene un identificador único (`id`) que se usa en todas las operaciones de administración de motores. La aplicación puede proporcionar un elemento `id`, o bien el SDK generará un nuevo identificador único (si la aplicación no proporciona ninguno). El resto de las propiedades del motor (por ejemplo, la dirección de correo electrónico en la información de la identidad) son cargas opacas del SDK. El SDK NO realiza ninguna lógica para garantizar que el resto de las propiedades sean únicas, ni aplica otras restricciones.

### <a name="engine-management-methods"></a>Métodos de administración de motores

Como se ha indicado anteriormente, existen tres métodos de administración de motores en el SDK: `AddEngineAsync`, `DeleteEngineAsync` y `UnloadEngineAsync`.

#### <a name="addengineasync"></a>AddEngineAsync

Este método carga un motor existente o crea uno (si aún no existe en el estado local).

Si la aplicación no proporciona un elemento `id`, `AddEngineAsync` genera un nuevo elemento `id`. Después, comprueba si ya existe un motor con ese elemento `id` en el estado local. Si existe, carga ese motor. Si el motor *no* existe en el estado local, se crea un motor (para hacerlo, se llama a las API y los servicios de back-end necesarios).

En ambos casos, si el método es correcto, el motor se cargará y estará listo para su uso.

#### <a name="deleteengineasync"></a>DeleteEngineAsync

Elimina el motor con el elemento `id` especificado. Se eliminan todos los seguimientos del motor del estado local.

#### <a name="unloadengineasync"></a>UnloadEngineAsync

Descarga las estructuras de datos en memoria para el motor con el elemento `id` especificado. El estado local de este motor seguirá estando intacto y se puede volver a cargar con `AddEngineAsync`.

Este método permite que la aplicación determine el uso de memoria mediante la descarga de los motores que no vayan a usarse.

## <a name="next-steps"></a>Pasos siguientes

- Ahora, obtenga más información sobre [Conceptos de autenticación](concept-authentication-cpp.md) y [Observadores](concept-async-observers.md). MIP ofrece un modelo de autenticación extensible, mientras que los observadores se usan para proporcionar notificaciones de eventos para eventos asincrónicos. Ambos son fundamentales y se aplican a todos los conjuntos de API de MIP.
- Después, revise los conceptos del motor y el perfil para las API de protección, directiva y archivo.
  - [Conceptos del perfil de la API de archivo](concept-profile-engine-file-profile-cpp.md)
  - [Conceptos del motor de la API de archivo](concept-profile-engine-file-engine-cpp.md)
  - [Conceptos del perfil de la API de directiva](concept-profile-engine-file-profile-cpp.md)
  - [Conceptos del motor de la API de directiva](concept-profile-engine-file-engine-cpp.md)
  - [Conceptos del perfil de la API de protección](concept-profile-engine-file-profile-cpp.md)
  - [Conceptos del motor de la API de protección](concept-profile-engine-file-engine-cpp.md)  
