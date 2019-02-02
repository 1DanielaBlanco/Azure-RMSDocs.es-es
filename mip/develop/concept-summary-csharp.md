---
title: SDK de Microsoft Information Protection C# información general de contenedor
description: Una introducción rápida sobre cómo empezar a trabajar con el contenedor de .NET SDK de MIP y las diferencias entre el contenedor de .NET y el SDK de C++.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 01/04/2019
ms.author: tommos
ms.openlocfilehash: ec1d2083449f1cb4ffccb086f71a7085a9251604
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651986"
---
# <a name="getting-started-with-the-microsoft-information-protection-net-wrapper"></a>Introducción a con el contenedor de .NET de Microsoft Information Protection

El contenedor de .NET Microsoft SDK de protección de información permite a los desarrolladores integrar la experiencia de Microsoft Information Protection en sus propias aplicaciones y servicios. El SDK clasificación, etiquetado y protección características ayuda a asegurarse de que la información está clasificada, etiquetados y protegidos independientemente de dónde desplaza. 

El contenedor administrado y todas las dependencias se pueden instalar a través de NuGet en Visual Studio.

## <a name="supported-platforms"></a>Plataformas compatibles

El contenedor de .NET de protección de información Microsoft es compatible con las siguientes plataformas. NET:

* .NET standard 2.0
* .NET 4.0

## <a name="installing-the-package"></a>Instalación del paquete

Desde la consola de administrador de paquetes en Visual Studio 2017, instale el paquete mediante la ejecución:

`install-package Microsoft.InformationProtection.File`

No hay paquetes adicionales son necesarios. Todas las bibliotecas de terceros se incluyen y se copiará en la carpeta de salida en la compilación.

## <a name="wrapper-details"></a>Detalles de contenedor

El contenedor de .NET es un [SWIG](https://swig.org/) contenedor administrado generado. El contenedor usa las bibliotecas de C++ compiladas desde el SDK de Microsoft Information Protection. Estos archivos DLL son los mismos archivos DLL que se incluyen con la versión del SDK de C++.

## <a name="concept-overlap"></a>Superposición de concepto

Hay algunas diferencias fundamentales entre la versión del SDK de C++ y el contenedor administrado.

* El contenedor de .NET no requiere el uso de observadores para operaciones asincrónicas. Las operaciones asincrónicas se implementan a través de la [modelo asincrónico basado en tareas](https://docs.microsoft.com/en-us/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap).
* El contenedor de .NET requieren a los delegados que forman parte del SDK de C++: AuthDelegate y ConsentDelegate. Estos delegados se implementan a través de las interfaces `IAuthDelegate` y `IConsentDelegate`

## <a name="next-steps"></a>Pasos siguientes

A continuación, revise [inicio rápido: inicialización de Microsoft Information Protection (MIP) SDK C# ](quick-app-initialization-csharp.md) para empezar a trabajar en la creación de una aplicación de consola básica, habilitado de MIP.
