---
title: 'Conceptos: auditoría en la API de directivas del SDK de Microsoft Information Protection'
description: Este artículo le ayudará a entender a utilizar el SDK de Microsoft Information Protection para enviar eventos de auditoría de la API de directivas a Azure Information Protection Analytics.
services: information-protection
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/07/2018
ms.author: tommos
ms.openlocfilehash: c660a5f58acd87ff9047a21fea26cc2732667493
ms.sourcegitcommit: 05fdaf43f74013eecb5886b95b09dd5e00670753
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2018
ms.locfileid: "51297846"
---
# <a name="auditing-in-the-mip-sdk"></a>Auditorías en el SDK de MIP

El portal de administración de Azure Information Protection proporciona acceso a informes de administrador. Estos informes proporcionan visibilidad en las etiquetas que aplican los usuarios, ya sea manual o automáticamente, en cualquier aplicación que tenga integrado el SDK de MIP. Los asociados de desarrollo que hagan uso del SDK podrán habilitar esta funcionalidad fácilmente, de manera que la información de sus aplicaciones se muestre en los informes de cliente.

## <a name="event-types"></a>Tipos de evento

Hay tres tipos de eventos que se pueden enviar con el SDK a Azure Information Protection Analytics: los **eventos de latido**, los **eventos de detección** y los **eventos de cambio**.

### <a name="heartbeat-events"></a>Eventos de latido

Los eventos de latido se generan automáticamente para todas las aplicaciones que tengan integrada la API de directivas. Los eventos de latido incluyen:

* TenantId
* Hora de generación
* Nombre principal de usuario
* Nombre de la máquina en la que se ha generado la auditoría
* Nombre del proceso
* Plataforma
* Identificador de aplicación: corresponde al identificador de aplicación de Azure AD.

Estos eventos son útiles para detectar aplicaciones en toda su empresa que utilicen el SDK de Microsoft Information Protection.

### <a name="discovery-events"></a>Eventos de detección

Los eventos de detección proporcionan datos sobre la información etiquetada que lee o utiliza la API de directivas. Estos eventos son útiles porque muestran los dispositivos, la ubicación y los usuarios que acceden a la información en toda una organización.

Los eventos de detección se generan en la API de directivas estableciendo un indicador booleano al crear el objeto `mip::PolicyHandler` con `mip::PolicyEngine`. En el ejemplo siguiente, el valor de **isAuditDiscoveryEnabled** está establecido en true. Si se pasa `mip::ExecutionState` a `ComputeActions()` o `GetSensitivityLabel()` (con información de metadatos e identificador de contenido existentes), dicha información de detección se enviará a Azure Information Protection Analytics.

La auditoría de detección se genera una vez que la aplicación llama a `ComputeActions()` o `GetSensitivityLabel()` y proporciona `mip::ExecutionState`. Este evento se genera solo una vez por cada controlador.

Consulte la documentación de los conceptos `mip::ExecutionState` para obtener más información detallada sobre el estado de ejecución.

```cpp
// Create PolicyHandler, passing in true for isAuditDiscoveryEnabled
auto handler = mEngine->CreatePolicyHandler(true);

// Returns vector of mip::Action and generates discovery event.
auto actions = handler->ComputeActions(*state);

//Or, get the label for a given state
auto label = handler->GetSensitivityLabel(*state);
```

En la práctica, **isAuditDiscoveryEnabled** debe ser `true` durante la construcción de `mip::PolicyHandler` para que la información de acceso a los archivos se dirija a Azure Information Protection Analytics.

## <a name="change-event"></a>Evento de cambio

Los eventos de cambio proporcionan información sobre el archivo, la etiqueta que se ha aplicado o cambiado y cualquier justificación que proporcione el usuario. Los eventos de cambio se generan al llamar a `NotifyCommittedActions()` en `mip::PolicyHandler`. La llamada se hace una vez confirmado correctamente un cambio en un archivo, con lo que se pasa el elemento `mip::ExecutionState` que se ha utilizado para calcular las acciones.

> Si la aplicación no puede llamar a esta función, no llegará ningún evento a Azure Information Protection Analytics.

```cpp
handler->NotifyCommittedActions(*state);
```

## <a name="audit-dashboard"></a>Panel de auditoría

Los eventos enviados a la canalización de auditoría de Azure Information Protection se mostrarán en los informes en https://portal.azure.com. Azure Information Protection Analytics se encuentra en versión preliminar pública y las características y funcionalidades están sujetas a cambios.

## <a name="next-steps"></a>Pasos siguientes

Consulte la [entrada de blog sobre el anuncio de la versión preliminar en Tech Community](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854) para obtener más información sobre la experiencia de auditoría de Azure Information Protection.

