---
# required metadata

title: Introducción | Azure RMS
description: La plataforma RMS SDK 2.1 permite a los desarrolladores crear aplicaciones que aprovechan la protección de la información de RMS.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 728113C9-FCF9-4280-BE1D-6AF5C15E449E
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** El contenido de este SDK no es actual. Durante un breve periodo podrá encontrar la [versión actual](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx) de la documentación en MSDN. **
# Introducción

La plataforma Rights Management Services SDK 2.1 permite a los desarrolladores crear aplicaciones que aprovechan la protección de la información de RMS. La plataforma controla prácticas de seguridad complejas como la administración de claves, el procesamiento de cifrado y descifrado, y ofrece una API simplificada para el desarrollo sencillo de aplicaciones.

## Introducción a RMS SDK 2.1

Lea estas secciones (abajo):

-   ¿Por qué usar RMS SDK 2.1 para proteger el contenido?
-   Principios básicos

Pruebe a utilizar RMS SDK 2.1 siguiendo las guías de estos temas:

-   [Instalar el SDK](create-your-first-rights-aware-application.md)
-   [Prueba de la aplicación con derechos habilitados](running-your-first-application.md)
-   [IPCHelloWorld: una aplicación de ejemplo](how-to-build-your-first-application.md)

Cuando haya empezado, revise algunos de nuestros otros [ejemplos de RMS](samples.md). Después, manténgase informado a través de nuestro [Rincón del desarrollador de RMS](http://blogs.msdn.com/b/rms/).

### ¿Por qué usar RMS SDK 2.1 para proteger el contenido?

Para los desarrolladores que deseen agregar compatibilidad con RMS a sus aplicaciones nuevas y existentes, el RMS SDK 2.1 ayuda a que sea más fácil:

-   Crear aplicaciones compatibles con RMS manejables, compatibles y robustas.
-   Cifrar datos de usuario de forma persistente. Los datos permanecen cifrados sin tener en cuenta el entorno, el dispositivo o el sistema operativo.
-   Exigir un conjunto completo de restricciones de uso, como evitar capturas de pantalla de sus datos confidenciales.
-   Admitir directivas de protección administradas por la empresa.
-   Admitir nuevos mecanismos de autenticación y algoritmos de cifrado a medida que están disponibles.

El RMS SDK 2.1 es compatible con diversas plataformas de cliente y servidor importantes. Para más información, vea [Supported platforms](supported-platforms.md) (Plataformas admitidas).

## Principios básicos

**Simplicidad**: Se han analizado patrones de uso y comentarios para el AD RMS SDK 1.0 y esos datos se han utilizado para simplificar o automatizar las tareas de programación más difíciles. Las aplicaciones de RMS creadas mediante el RMS SDK 2.1 normalmente requieren entre 5 y 10 veces menos líneas de código de RMS que las aplicaciones de RMS escritas mediante AD RMS SDK 1.0.
**Escribir una vez**: Las aplicaciones RMS SDK 2.1 no necesitan un cambio en el código o una recompilación para funcionar con las características de RMS más recientes. Las nuevas características de RMS pasan a estar disponibles en la aplicación existente cuando se agregan al servidor RMS.
**Coherencia**: RMS SDK 2.1 facilita la escritura de aplicaciones que respetan constantemente distintas configuraciones de RMS. También reduce considerablemente la cantidad de interfaz de usuario de RMS, ya que el desarrollador de la aplicación, necesita crear, fomentando una apariencia coherente y reduciendo la necesidad de educación del usuario.

## Temas relacionados

* [Ejemplos de AD RMS](samples.md)
* [Rincón del desarrollador de AD RMS](http://blogs.msdn.com/b/rms/)
* [Instalar el SDK](create-your-first-rights-aware-application.md)
* [IPCHelloWorld: una aplicación de ejemplo](how-to-build-your-first-application.md)
* [Información general](ad-rms-overview.md)
* [Plataformas compatibles](supported-platforms.md)
* [Prueba de la aplicación con derechos habilitados](running-your-first-application.md)
 

 





<!--HONumber=Jun16_HO1-->


