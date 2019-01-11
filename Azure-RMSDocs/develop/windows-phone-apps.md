---
title: Programa de instalación de Windows Phone | Azure RMS
description: Las aplicaciones de Windows Phone pueden usar Microsoft Rights Management SDK 4.2 para habilitar la protección de información integrada en la aplicación.
keywords: ''
author: bryanla
ms.author: bryanla
manager: mbaldwin
ms.date: 12/10/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: e25a446e-b977-4736-9c65-7711171fb0e1
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 711b19631cc191f7a182602d3e05556f97072ee4
ms.sourcegitcommit: bd2b31dd97c8ae08c28b0f5688517110a726e3a1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2019
ms.locfileid: "54071724"
---
# <a name="windows-phone-setup"></a>Programa de instalación de Windows Phone


Las aplicaciones de Windows Phone pueden usar Microsoft Rights Management SDK 4.2 para habilitar la protección de información integrada en sus aplicaciones mediante Azure Active Directory Rights Management (AAD RM).

Este tema sirve de guía por el proceso de configuración del entorno para crear sus propias aplicaciones.

-   [Requisitos previos](#prerequisites)
-   [Configurar el entorno de desarrollo](#configuring-your-development-environment)
-   [Ver también](#see-also)

## <a name="prerequisites"></a>Requisitos previos


Debe tener el siguiente software en el sistema de desarrollo:

-   El sistema operativo [Windows 8.1](https://windows.microsoft.com/windows-8/meet)
-   [Herramientas de desarrollo de Windows Phone 8.1 (SDK)](https://developer.microsoft.com/windows/downloads/sdk-archive)
-   Microsoft [Visual Studio 2012](https://visualstudio.microsoft.com/vs/older-downloads/) o superior, o Visual Studio Express 2012, que se incluye en el Windows Phone SDK 8.0/8.1
-   El paquete de Microsoft RMS SDK 4.2 para Windows Phone. Para más información, vea [Get started](get-started.md) (Introducción).
-   Biblioteca de autenticación: se recomienda que use la [biblioteca de autenticación de Azure AD](https://msdn.microsoft.com/library/jj573266.aspx), aunque se pueden usar otras bibliotecas de autenticación.

Lea el tema de [novedades](release-notes.md) para más información sobre actualizaciones, información de dispositivos y entornos, notas de la versión y preguntas más frecuentes de la API.

Revise la información de la guía de [desarrollo de Windows Phone](https://msdn.microsoft.com/library/windowsphone/develop/ff402535.aspx) en el centro de desarrollo de Windows Phone.

## <a name="configuring-your-development-environment"></a>Configuración del entorno de desarrollo


-   Abra *Visual Studio*.
-   Haga clic en **Archivo**. En el menú **Archivo**, haga clic en **Nuevo** y, después, en **Proyecto**.
-   En el cuadro de diálogo **Nuevo proyecto**, seleccione **Visual C\#**, **Aplicación vacía (Windows Phone)** y después haga clic en **Aceptar**.

    ![Crear proyecto](../media/wpsetup-newproj.png)

-   En el Explorador de soluciones, haga clic en el proyecto y seleccione **Agregar referencia** para abrir el cuadro de diálogo **Agregar referencia**.

    ![Agregar referencia](../media/wpsetup-addref.png)

-   Haga clic en **Examinar** en la parte inferior izquierda del cuadro de diálogo **Agregar referencia** y seleccione el archivo *Microsoft.RightsManagement.dll* que se encuentra en la carpeta en la que extrajo el paquete del SDK.
-   **Aplicaciones administradas**: para la creación de una aplicación administrada, tendrá que agregar esta referencia; seleccione **Windows 8.1**-&gt;**Extensiones** y active la casilla de **Windows Visual C++ Runtime Package for Windows** (Paquete de Windows Visual C++ en tiempo de ejecución para Windows).

    ![Agregar extensiones](../media/wpsetup-refmngr.png)

-   **Adición de funciones**: la aplicación necesitará la funcionalidad de "Internet (cliente y servidor)" para usar el SDK. Para agregar esta funcionalidad a la aplicación, abra el archivo *Package.appxmanifest* en el proyecto y navegue hasta la pestaña **Capacidades**.

Ya está listo para crear sus propias aplicaciones nuevas de Windows Phone.

### <a name="see-also"></a>Consulte también

[Introducción](get-started.md)

[Novedades](release-notes.md)

[Conceptos principales](core-concepts.md)

[Desarrollo de Windows Phone](https://msdn.microsoft.com/library/windowsphone/develop/ff402535.aspx)

[Referencia de la API de Windows](https://msdn.microsoft.com/library/dn891914.aspx)

[Visual Studio 2012](https://visualstudio.microsoft.com/vs/older-downloads/)

[Windows Phone SDK](https://developer.microsoft.com/windows/downloads/sdk-archive)
