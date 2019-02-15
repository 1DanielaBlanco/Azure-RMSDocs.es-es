---
title: Introducción | Azure RMS
description: La plataforma RMS SDK 2.1 permite a los desarrolladores crear aplicaciones que aprovechan la protección de la información de RMS.
keywords: ''
author: bryanla
ms.author: bryanla
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 728113C9-FCF9-4280-BE1D-6AF5C15E449E
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: c81c033529a3b711776d34086f411d64a8582296
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56256556"
---
# <a name="getting-started"></a>Introducción

La plataforma Rights Management Services SDK 2.1 permite a los desarrolladores crear aplicaciones que aprovechan la protección de la información de RMS a través de un servidor RMS o Azure RMS. La plataforma controla prácticas de seguridad complejas como la administración de claves, el procesamiento de cifrado y descifrado, y ofrece una API simplificada para el desarrollo sencillo de aplicaciones.

## <a name="get-started-with-rmssdk21"></a>Introducción a RMS SDK 2.1

Este tema le guiará a través del proceso de configuración y ejecución de su aplicación con derechos habilitados en un entorno de prueba. Los temas siguientes describen cómo configurar el entorno de desarrollo y se muestran de forma que sugieren un orden en el que podría realizar las tareas.

## <a name="in-this-sections"></a>En esta sección

| Tema | Descripción |
|-------|-------------|
| [Notas de la versión](release-notes-rtm.md) | Este tema contiene información importante sobre esta versión y versiones anteriores de RMS SDK 2.1.|
| [Instalar el SDK](install-the-rms-sdk.md) | Este tema le guiará en el proceso de instalación de las herramientas para desarrolladores.|
| [Configurar Visual Studio](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md) | Este tema contiene instrucciones sobre cómo configurar un proyecto de Visual Studio para usar RMS SDK 2.1.|
| [Desarrollo de la aplicación](developing-your-application.md) | Este tema contiene instrucciones esenciales sobre los principales aspectos de una aplicación habilitada para RMS y puede servir como base para el desarrollo de su propia aplicación.|
| [Prueba de la aplicación](how-to-set-up-your-test-environment.md) |Este tema contiene instrucciones sobre cómo configurar la prueba de la aplicación.|
| [Implementación en el entorno de producción](deploying-your-application.md) |En este tema se describen las opciones de implementación de la aplicación con derechos habilitados.|


Pruebe a usar RMS SDK 2.1 siguiendo las guías de estos temas:

- [Instalar el SDK](install-the-rms-sdk.md)
- [Configurar Visual Studio](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md)
- [Desarrollo de la aplicación](developing-your-application.md)
- [Prueba de la aplicación](how-to-set-up-your-test-environment.md)
- [Implementación en el entorno de producción](deploying-your-application.md)

### <a name="why-use-rmssdk21-for-protecting-your-content"></a>¿Por qué usar RMS SDK 2.1 para proteger el contenido?

Para los desarrolladores que quieran agregar compatibilidad con RMS a sus aplicaciones nuevas y existentes, el RMS SDK 2.1 hace que sea más fácil:

-   Crear aplicaciones compatibles con RMS manejables, compatibles y robustas.
-   Cifrar datos de usuario de forma persistente. Los datos permanecen cifrados sin tener en cuenta el entorno, el dispositivo o el sistema operativo.
-   Exigir un conjunto completo de restricciones de uso, como evitar capturas de pantalla de sus datos confidenciales.
-   Admitir directivas de protección administradas por la empresa.
-   Admitir nuevos mecanismos de autenticación y algoritmos de cifrado a medida que están disponibles.

El RMS SDK 2.1 es compatible con diversas plataformas de cliente y servidor importantes. Para más información, vea [Supported platforms](supported-platforms.md) (Plataformas admitidas).

## <a name="core-principles"></a>Principios básicos

**Simplicidad**: Se han analizado patrones de uso y comentarios para el AD RMS SDK 1.0 y esos datos se han utilizado para simplificar o automatizar las tareas de programación más difíciles. Las aplicaciones de RMS creadas mediante el RMS SDK 2.1 normalmente requieren entre 5 y 10 veces menos líneas de código de RMS que las aplicaciones de RMS escritas mediante AD RMS SDK 1.0.
**Escribir una vez**: Las aplicaciones RMS SDK 2.1 no necesitan un cambio en el código o una recompilación para funcionar con las características de RMS más recientes. Las nuevas características de RMS pasan a estar disponibles en la aplicación existente cuando se agregan al servidor RMS.
**Coherencia**: RMS SDK 2.1 facilita la escritura de aplicaciones que respetan constantemente distintas configuraciones de RMS. También reduce considerablemente la cantidad de interfaz de usuario de RMS, ya que el desarrollador de la aplicación, necesita crear, fomentando una apariencia coherente y reduciendo la necesidad de educación del usuario.

## <a name="related-topics"></a>Temas relacionados

* [Guía de desarrolladores de RMS](developers-guide.md)
