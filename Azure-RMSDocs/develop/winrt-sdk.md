---
# required metadata

title: Programa de instalación de la Tienda Windows | Azure RMS
description: Las aplicaciones de la Tienda Windows pueden usar Microsoft Rights Management SDK 4.2 para habilitar la protección de información integrada en la aplicación.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 2720aa0e-0d37-469f-be99-678bf95a9c51
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Programa de instalación de la Tienda Windows

Las aplicaciones de la Tienda Windows pueden usar Microsoft Rights Management SDK 4.2 para habilitar la protección de información integrada en sus aplicaciones mediante Azure Active Directory Rights Management (AAD RM).

Este tema sirve de guía por el proceso de configuración del entorno para crear sus propias aplicaciones.

-   [Requisitos previos](#prerequisites)
-   [Opcional](#optional)
-   [Configuración del entorno de desarrollo](#configuring-your-development-environment)
-   [Véase también](#see-also)

## Requisitos previos


Debe tener el siguiente software en el sistema de desarrollo:

-   El sistema operativo [Windows 8.1](http://windows.microsoft.com/en-US/windows-8/meet)
-   El [Windows SDK para Windows 8.1](https://msdn.microsoft.com/en-us/windows/desktop/bg162891.aspx)
-   Microsoft [Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview) o superior, o Visual Studio Express 2012, que se incluye en Windows SDK para Windows 8.0/8.1.
-   El paquete de Microsoft RMS SDK 4.2 para aplicaciones de la Tienda Windows. Para más información, consulte [Get started](get-started.md) (Introducción).
-   Biblioteca de autenticación: se recomienda que utilice la [biblioteca de autenticación de Azure AD](https://msdn.microsoft.com/en-us/library/jj573266.aspx), aunque se pueden usar otras bibliotecas de autenticación.

Lea el tema de [novedades](release-notes.md) para más información sobre actualizaciones, información de dispositivos y entornos, notas de la versión y preguntas más frecuentes de la API.

## Opcional

Nuestra biblioteca de UI proporciona una interfaz de usuario reutilizable para operaciones de consumo y protección a aquellos desarrolladores que no quieren crear su propia interfaz de usuario personalizada: [UI Library for Windows Store apps](https://github.com/AzureAD/rms-sdk-ui-for-windowsstore) (Biblioteca de UI para aplicaciones de la Tienda Windows). También proporcionamos una aplicación de ejemplo de la aplicación de la Tienda Windows: [RMS Sample application for Windows Store](https://github.com/AzureADSamples/rms-samples-for-windowsstore) (aplicación de ejemplo de RMS para la Tienda Windows).

## Configuración del entorno de desarrollo


-   Abra Visual Studio.
-   Haga clic en **Archivo**, **Nuevo** y a continuación haga clic en **Proyecto**.
-   En el cuadro de diálogo **Nuevo proyecto**, haga clic en **Visual C#** y seleccione **Aplicación vacía (Windows)**; a continuación, haga clic en **Aceptar**.

    ![Crear proyecto](../media/winrtsetup-newproj.png)

-   En el **Explorador de soluciones**, haga clic en el proyecto y seleccione **Agregar referencia** para abrir el cuadro de diálogo **Agregar referencia**.

    ![Agregar referencia](../media/winrtsetup-addref.png)

-   En el cuadro de diálogo **Agregar referencia**, haga clic en **Examinar** y seleccione el archivo *Microsoft.RightsManagement.dll* que se encuentra en la carpeta en la que extrajo el paquete del SDK.
-   **Aplicaciones administradas**: para la creación de una aplicación administrada, tendrá que agregar esta referencia; seleccione **Windows 8.1**-&gt;**Extensiones** y active la casilla de **Windows Visual C++ Runtime Package for Windows** (Paquete de Windows Visual C++ en tiempo de ejecución para Windows).

    ![Agregar extensiones](../media/winrtsetup-refmngr.png)

-   **Adición de funciones**: la aplicación necesitará la funcionalidad de "Internet (cliente y servidor)" para usar el SDK. Para agregar esta funcionalidad a la aplicación, abra el archivo *Package.appxmanifest* en el proyecto y navegue hasta la pestaña **Capacidades**.

Ya está listo para crear sus propias aplicaciones nuevas de la Tienda Windows.

### Véase también

[Introducción](get-started.md)

[Novedades](release-notes.md)

[Conceptos y términos para desarrolladores](core-concepts.md)

[Windows 8](http://windows.microsoft.com/en-US/windows-8/meet)

[Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview)

[Referencia de la API de Windows](/rights-management/sdk/4.2/api/winrt/Microsoft.RightsManagement)


<!--HONumber=May16_HO2-->


