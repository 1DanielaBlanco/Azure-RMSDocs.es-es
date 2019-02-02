---
title: Versión del SDK de Microsoft Information Protection (MIP) historial de versiones y directiva de soporte técnico
description: Guía de inicio rápido donde se muestra cómo escribir la lógica de inicialización para aplicaciones cliente del SDK de Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 01/08/2019
ms.author: bryanla
manager: mbaldwin
ms.openlocfilehash: c385c43ac7d7c0a505c05cc24a4beeef34a76af7
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55652020"
---
# <a name="microsoft-information-protection-mip-sdk-version-release-history-and-support-policy"></a>Versión del SDK de Microsoft Information Protection (MIP) historial de versiones y directiva de soporte técnico

## <a name="servicing"></a>Mantenimiento 

Cada versión de disponibilidad general (GA) se admite durante seis meses después de la próxima versión de GA es la versión. La documentación no puede incluir información sobre las versiones no admitidas. Solo se aplican correcciones y funcionalidades nuevas a la última versión de GA.

Las versiones preliminares no deben implementarse en producción. En su lugar, use la última versión preliminar para probar nuevas funcionalidades o correcciones que se incluyen en la próxima versión de GA. Se admite solo la versión preliminar más reciente.

## <a name="release-history"></a>Historial de versiones

Use la siguiente información para ver el contenido nuevo o modificado en una versión compatible. La versión más reciente aparece en primer lugar. 

> [!NOTE]
> Revisiones secundarias no se enumeran por si experimenta un problema con el SDK, que se recomienda que compruebe si se ha corregido con la última versión de GA. Si el problema continúa, compruebe la versión preliminar actual.
>  
> Para obtener soporte técnico, visite la [foro de Stack Overflow Microsoft Information Protection](https://stackoverflow.com/questions/tagged/microsoft-information-protection). 

## <a name="version-110"></a>Versión 1.1.0

**Fecha de lanzamiento**: TBD

Esta versión incluye compatibilidad con las siguientes plataformas:

  - .NET
  - SDK (directiva de API) de iOS
  - SDK de Android (directiva de API y la API de protección)

**Nuevas características**

- Soporte técnico ADRMS
- Las operaciones de API de protección son verdaderamente asincrónicas (Win32), lo que permite operaciones simultáneas de cifrar o descifrar sin bloqueo
  - Ahora se pueden invocar las devoluciones de llamada de aplicación (AuthDelegate, HTTPDelegate, etc.) en *cualquier* subproceso en segundo plano
- Ahora se pueden leer las propiedades de etiqueta personalizada establecidas por los administradores de TI mediante mip::Label::GetCustomSettings
- Ahora se puede recuperar la licencia serializada de publicación directamente desde un archivo sin realizar operaciones HTTP a través de mip::FileHandler::GetSerializedPublishingLicense
- Las aplicaciones se le notifica si una operación HTTP es necesario para completar la creación de un MIP:: fileengine/MIP:: policyengine a través de mip::FileProfile::Observer::OnAddPolicyEngineStarting / mip::PolicyProfile::Observer::OnAddEngineStarting
- Detección de si el contenido protegido tiene una fecha de expiración o no se ha simplificado con comodidad método mip::ProtectionDescriptor::DoesContentExpire
- Clasificación:
  - Tipos de sensibilidad (expresiones de regex para CC de #, passport #, etc.) se puede adquirir de servicio de control de código fuente
    - Habilitar característica estableciendo mip::FileEngine::Settings / mip::PolicyEngine::Settings marca
    - Leer los tipos de mip::FileEngine::ListSensitivityTypes / mip::PolicyEngine::ListSensitivityTypes
  - Resultados de la clasificación de las utilidades de escáner de documento externo pueden enviarse a MIP para impulsar etiquetas recomendado o necesarios en función del contenido del documento
    - Pasar los resultados a MIP mediante mip::FileExecutionState::GetClassificationResults / mip::ExecutionState::GetClassificationResults
    - MIP::ApplyLabelAction y mip::RecommendLabelAction pueden devolver mip::PolicyEngine::ComputeActions cuando los resultados de la clasificación coincide con una regla de directiva que indica las etiquetas necesarias o recomendadas

- Nuevos requisitos:
  - Aplica el rellenado de mip::ApplicationInfo de campos de identificador/nombre/versión al crear MIP:: fileprofile, mip::PolicyProfile y MIP:: protectionprofile
  - Las aplicaciones deben implementar la nueva interfaz mip::FileExecutionState al crear mip::FileHandlers
  
- Excepciones actualizadas:
  - MIP::NoAuthTokenError que se produce si AuthDelegate la aplicación devuelve un token vacío (debido a la cancelación)
    - Se aplica a la creación de:
      - mip::FileEngine
      - mip::FileHandler
      - mip::PolicyEngine
      - mip::ProtectionHandler
  - se produce si el inquilino no está configurado para las etiquetas de MIP::NoPolicyError
    - Se aplica a la creación de:
      - mip::FileEngine
      - mip::PolicyEngine
  - MIP::ServiceDisabledError que se produce si el servicio de RMS está deshabilitado para un usuario o dispositivo o plataforma/inquilino específico
    - Se aplica a la creación de:
      - mip::FileHandler
      - mip::ProtectionHandler
  - MIP::NoPermissionsError que se produce si un usuario no tiene derechos para descifrar un documento o el contenido ha expirado
    - Se aplica a la creación de:
      - mip::FileHandler
      - mip::ProtectionHandler

**Correcciones**:

TBD

## <a name="next-steps"></a>Pasos siguientes

- Consulte [problemas y preguntas más frecuentes de SDK de MIP](faqs-known-issues.md) para obtener información sobre las plataformas compatibles y mucho más.
- Consulte [configuración e instalación del SDK de MIP](setup-configure-mip.md) para obtener información sobre cómo empezar a trabajar con el SDK de MIP.