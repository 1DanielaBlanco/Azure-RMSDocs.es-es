---
title: 'Conceptos: auditoría en la API de archivos del SDK de Microsoft Information Protection'
description: Este artículo le ayudará a entender a utilizar el SDK de Microsoft Information Protection para enviar eventos de auditoría de la API de archivos a Azure Information Protection Analytics.
services: information-protection
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 11/01/2018
ms.author: tommos
ms.openlocfilehash: f091cfd220ac8886a6bf26903deb7b97062cffd7
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56258596"
---
# <a name="auditing-in-the-mip-sdk-file-api"></a>Auditorías en la API de archivos del SDK de MIP

El portal de administración de Azure Information Protection proporciona acceso a informes de administrador. Estos informes proporcionan visibilidad en las etiquetas que aplican los usuarios, ya sea manual o automáticamente, en cualquier aplicación o servicio que tenga integrado el SDK de MIP. Los asociados de desarrollo que utilicen el SDK podrán habilitar esta funcionalidad fácilmente, de manera que la información de sus aplicaciones se muestre en los informes de cliente.

## <a name="event-types"></a>Tipos de evento

Hay tres tipos de eventos que se pueden enviar con el SDK a Azure Information Protection Analytics: los **eventos de latido**, los **eventos de detección** y los **eventos de cambio**.

### <a name="heartbeat-events"></a>Eventos de latido

Los eventos de latido se generan automáticamente para todas las aplicaciones que tengan integrada la API de archivos. Los eventos de latido incluyen:

* TenantId
* Hora de generación
* Nombre principal de usuario
* Nombre de la máquina en la que se ha generado la auditoría
* Nombre del proceso
* Plataforma
* Identificador de aplicación: corresponde al identificador de aplicación de Azure AD.

Estos eventos son útiles para detectar aplicaciones en toda su empresa que utilicen el SDK de Microsoft Information Protection.

### <a name="discovery-events"></a>Eventos de detección

Los eventos de detección proporcionan datos sobre la información etiquetada que lee o utiliza la API de archivos. Estos eventos son útiles porque muestran los dispositivos, la ubicación y los usuarios que acceden a la información en toda una organización.

Estos eventos se envían a Azure Information Protection Analytics estableciendo el parámetro `AuditDiscoveryEnabled` en true al crear un elemento `mip::FileHandler`. Además, se proporciona un identificador de contenido que identifica el archivo con algún formato legible. Se recomienda utilizar la ruta de archivo para este identificador.

En el siguiente ejemplo se crea un elemento `mip::FileHandler` con la detección de auditoría habilitada. Se llama al método `CreateFileHandler()` en el elemento `mip::FileEngine` y `AuditDiscoveryEnabled` se establece en true. Una vez que el elemento `FileHanlder` lee la etiqueta, se genera una auditoría de detección.

```cpp
// Create FileHandler with discovery enabled
auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
auto handlerFuture = handlerPromise->get_future();
fileEngine->CreateFileHandlerAsync(filePath, contentId, mip::ContentState::REST, true /*AuditDiscoveryEnabled*/, make_shared<FileHandlerObserver>(), createFileHandlerPromise);
auto handler = handlerFuture.get();

// Read label. This generates the discovery audit.
auto label = handler->GetLabel();
```

### <a name="change-events"></a>Eventos de cambio

Los eventos de cambio proporcionan información sobre el archivo, la etiqueta que se ha aplicado o cambiado y cualquier justificación que proporcione el usuario. Los eventos de cambio se generan al llamar a `NotifyCommitSuccessful()` en el elemento `mip::FileHandler` una vez que se ha confirmado correctamente un cambio en un archivo.

```cpp
// Create labeling options, set label
string contentId = "C:\users\myuser\Documents\MyPlan.docx";
mip::LabelingOptions labelingOptions(mip::AssignmentMethod::PRIVILEGED, mip::ActionSource::MANUAL);
handler->SetLabel(labelId, labelingOptions);
auto commitPromise = std::make_shared<std::promise<bool>>();
auto commitFuture = commitPromise->get_future();

// CommitAsync() returns a bool. If the change was successful, call NotifyCommitSuccessful().
fileHandler->CommitAsync(outputFile, commitPromise);
if(commitFuture.get()) {

    // Submit audit event.
    handler->NotifyCommitSuccessful(contentId);
}
```

## <a name="audit-dashboard"></a>Panel de auditoría

Los eventos enviados a la canalización de auditoría de Azure Information Protection se mostrarán en los informes en https://portal.azure.com. Azure Information Protection Analytics se encuentra en versión preliminar pública y las características y funcionalidades están sujetas a cambios.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre la experiencia de auditoría de Azure Information Protection, eche un vistazo a la [entrada de blog sobre el anuncio de la versión preliminar en Tech Community](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854).
