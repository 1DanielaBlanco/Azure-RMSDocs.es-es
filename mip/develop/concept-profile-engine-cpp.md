---
title: 'Conceptos: conceptos básicos en el SDK de MIP (perfil y motor)'
description: Este artículo le permitirá comprender los conceptos básicos del SDK, denominados perfil y motor, que se crean durante la inicialización de la aplicación.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 05a66dc7a00b976dfb9883f44b3c93a25b4b6975
ms.sourcegitcommit: 0d3b43c9cedbaeae65299ac372fbfb9ad66ce27f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/10/2019
ms.locfileid: "54183633"
---
# <a name="microsoft-information-protection-sdk---profile-and-engine-object-concepts"></a>SDK de Microsoft Information Protection: conceptos de los objetos de perfil y motor

## <a name="profiles"></a>Profiles

El perfil es la clase raíz de todas las operaciones en el SDK de MIP. Antes de utilizar cualquiera de las tres API, la aplicación cliente debe crear un perfil. Futuras operaciones se realizan mediante el perfil, o por otros objetos *agregado* al perfil.

Hay tres tipos de perfiles en el SDK de MIP:

- [`PolicyProfile`](reference/class_mip_policyprofile.md): La clase profile de la API de la directiva de MIP.
- [`ProtectionProfile`](reference/class_mip_protectionprofile.md): La clase de perfil para la API de protección de MIP.
- [`FileProfile`](reference/class_mip_fileprofile.md): La clase profile de la API de archivo de MIP.

La API que se utiliza en la aplicación consumidora determina qué clase de perfil se debe usar.

El perfil en sí proporciona las siguientes funciones:

- Define la ubicación de almacenamiento del estado del SDK. En los datos de estado, se incluyen los detalles del usuario, las directivas de usuario descargadas, los registros y los datos de telemetría.
- Define si es necesario cargar el estado en la memoria o tiene que persistir en el disco.
- Controla la autenticación al aceptar un objeto `mip::AuthDelegate`.
- Establece el identificador de la aplicación y el nombre descriptivo de la aplicación que usa el SDK.

### <a name="profile-settings"></a>Configuración del perfil

- `Path`: Ruta de acceso de archivo en el registro, telemetría y otras se almacena el estado persistente.
- `useInMemoryStorage`: Un valor booleano que define si el estado debe almacenarse en memoria, o en el disco.
- `authDelegate`: Un puntero compartido de la clase `mip::AuthDelegate`. 
- `consentDelegate`: Un puntero compartido de la clase [ `mip::ConsentDelegate` ](reference/class_consentdelegate.md). 
- `observer`: Un puntero compartido para el perfil `Observer` implementación (en [ `PolicyProfile` ](reference/class_mip_policyprofile_observer.md), [ `ProtectionProfile` ](reference/class_mip_protectionprofile_observer.md), y [ `FileProfile` ](reference/class_mip_fileprofile_observer.md)).
- `applicationInfo`: Un [ `mip::ApplicationInfo` ](reference/mip-enums-and-structs.md#structures) objeto. Información acerca de la aplicación que consume el SDK, que coincide con el nombre y el Id. de registro de aplicación de Azure Active Directory.

## <a name="engines"></a>Motores

Los motores de archivo, el perfil y la API de protección de proporcionan una interfaz para las operaciones realizadas en nombre de una identidad específica. Uno de los motores se agrega al objeto de perfil, para cada usuario que inicia sesión en la aplicación. Todas las operaciones realizadas por el motor están en el contexto de esa identidad.

Hay tres clases de motor en el SDK, una para cada API. En la lista siguiente, se muestran las clases de motor y algunas de las funciones asociadas a estas:

- [`mip::ProtectionEngine`](reference/class_mip_protectionengine.md)
- [`mip::PolicyEngine`](reference/class_mip_policyengine.md)
  - `ListSensitivityLabels()`: Obtiene la lista de etiquetas para el motor cargado.
  - `GetSensitivityLabel()`: Obtiene la etiqueta del contenido existente.
  - `ComputeActions()`: Con un identificador de etiqueta y opcionales de los metadatos, devuelve la lista de acciones que debe producirse en un elemento específico.
- [`mip::FileEngine`](reference/class_mip_fileengine.md)
  - `ListSensitivityLabels()`: Obtiene la lista de etiquetas para el motor cargado.
  - `CreateFileHandler()`: Crea un `mip::FileHandler` para un archivo o flujo concreto.

### <a name="engine-states"></a>Estados del motor

Un motor puede tener uno de estos dos estados:

- `CREATED`: Crea indica que el SDK tiene suficiente información de estado local después de llamar a los servicios de back-end necesario.
- `LOADED`: El SDK ha creado las estructuras de datos necesarios para el motor para que sea operativa.

Es necesario crear y cargar un motor para realizar cualquier operación. La clase `Profile` expone varios métodos de administración de motores: `AddEngineAsync`, `RemoveEngineAsync` y `UnloadEngineAsync`.

La tabla siguiente describen los Estados posibles de motor y los métodos que pueden cambiar ese estado:

|         | NINGUNO              | CREADO           | LOADED         |
|---------|-------------------|-------------------|----------------|
| NINGUNO    |                   |                   | AddEngineAsync |
| CREADO | DeleteEngineAsync |                   | AddEngineAsync |
| LOADED  | DeleteEngineAsync | UnloadEngineAsync |                |

### <a name="engine-id"></a>Identificador de motor

Cada motor tiene un identificador único (`id`) que se usa en todas las operaciones de administración de motores. La aplicación puede proporcionar un `id`, o el SDK puede generar uno, si no se proporciona por la aplicación. El resto de las propiedades del motor (por ejemplo, la dirección de correo electrónico en la información de la identidad) son cargas opacas del SDK. El SDK NO realiza ninguna lógica para garantizar que el resto de las propiedades sean únicas, ni aplica otras restricciones.

### <a name="engine-management-methods"></a>Métodos de administración de motores

Como se mencionó anteriormente, existen tres métodos de administración de motor en el SDK: `AddEngineAsync`, `DeleteEngineAsync`, y `UnloadEngineAsync`.

#### <a name="addengineasync"></a>AddEngineAsync

Este método carga un motor existente o crea uno si aún no existe en el estado local.

Si la aplicación no proporciona un elemento `id`, `AddEngineAsync` genera un nuevo elemento `id`. Después, comprueba si ya existe un motor con ese elemento `id` en el estado local. Si existe, carga ese motor. Si el motor *no* existe en el estado local, se crea un motor (para hacerlo, se llama a las API y los servicios de back-end necesarios).

En ambos casos, si el método es correcto, el motor se cargará y estará listo para su uso.

#### <a name="deleteengineasync"></a>DeleteEngineAsync

Elimina el motor con el elemento `id` especificado. Se eliminan todos los seguimientos del motor del estado local.

#### <a name="unloadengineasync"></a>UnloadEngineAsync

Descarga las estructuras de datos en memoria para el motor con el elemento `id` especificado. El estado local de este motor seguirá estando intacto y se puede volver a cargar con `AddEngineAsync`.

Este método permite que la aplicación sea prudente sobre el uso de memoria, los motores de descarga que no se espera que se usará en breve.

## <a name="next-steps"></a>Pasos siguientes

- Ahora, obtenga más información sobre [Conceptos de autenticación](concept-authentication-cpp.md) y [Observadores](concept-async-observers.md). MIP ofrece un modelo de autenticación extensible, mientras que los observadores se usan para proporcionar notificaciones de eventos para eventos asincrónicos. Ambos son fundamentales y se aplican a todos los conjuntos de API de MIP.
- Después, revise los conceptos del motor y el perfil para las API de protección, directiva y archivo.
  - [Conceptos del perfil de la API de archivo](concept-profile-engine-file-profile-cpp.md)
  - [Conceptos del motor de la API de archivo](concept-profile-engine-file-engine-cpp.md)
  - [Conceptos del perfil de la API de directiva](concept-profile-engine-file-profile-cpp.md)
  - [Conceptos del motor de la API de directiva](concept-profile-engine-file-engine-cpp.md)
  - [Conceptos del perfil de la API de protección](concept-profile-engine-file-profile-cpp.md)
  - [Conceptos del motor de la API de protección](concept-profile-engine-file-engine-cpp.md)  
