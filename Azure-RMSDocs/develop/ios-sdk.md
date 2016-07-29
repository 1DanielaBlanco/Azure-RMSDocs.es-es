---
title: "Configuración de iOS y OS X | Azure RMS"
description: "Las aplicaciones de iOS y OS X pueden usar RMS SDK 4.2 para habilitar la protección de información integrada en sus aplicaciones mediante el AAD RM."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: b31e5b72-e65e-450a-b1b8-d46e81e9fb34
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 79397c82d9478cbd55630a376fe2d12f3873ebc4
ms.openlocfilehash: ae1af4a1cddc904fd4800f1a3900e3c7c4d073ed


---

# Configuración de iOS y OS X

Las aplicaciones de iOS y OS X pueden usar Microsoft Rights Management SDK 4.2 para habilitar la protección de información integrada en sus aplicaciones mediante Azure Active Directory Rights Management (AAD RM).

Este tema sirve de guía por el proceso de configuración del entorno para crear sus propias aplicaciones.

**Nota**  Este SDK no admite iPod Touch.


-   [Requisitos previos](#prerequisites)
-   [Opcional](#optional)
-   [Configuración del entorno de desarrollo](#configuring-your-development-environment)
-   [Véase también](#see-also)

## Requisitos previos

Se recomienda tener el siguiente software en el sistema de desarrollo:

-   OS X es necesario para todo el desarrollo de iOS.
-   Xcode versión 6.0 y posteriores

    Xcode está disponible a través de la [Mac App Store](https://developer.apple.com/technologies/mac/).

-   El paquete de Microsoft RMS SDK 4.2 para iOS y OS X. Para más información, vea [Introducción](get-started.md).

    Este SDK se puede usar para desarrollar aplicaciones para iOS 7.0 y OS X 10.8 y versiones posteriores.

-   Biblioteca de autenticación: se recomienda usar la [biblioteca de autenticación de Azure AD (ADAL)](https://msdn.microsoft.com/library/jj573266.aspx). Con todo, también puede usar otras bibliotecas de autenticación que admiten OAuth 2.0.

    Para más información, vea [ADAL para iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios) o [ADAL para OS X](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/tree/OSXUniversal).

Lea el tema de [novedades](release-notes.md) para más información sobre actualizaciones, notas de la versión y preguntas más frecuentes de la API.

## Opcional

Nuestra biblioteca de interfaz de usuario proporciona una interfaz de usuario reutilizable para operaciones de consumo y protección, dirigida a desarrolladores que no quieren crear su propia interfaz de usuario personalizada: [UI Library and Sample app for iOS](https://github.com/AzureAD/rms-sdk-ui-for-ios) (Biblioteca de interfaz de usuario y aplicación de ejemplo para iOS).

## Configuración del entorno de desarrollo

-   Para crear un proyecto nuevo, abra el menú **Archivo** y haga clic en **Nuevo** y luego en **Proyecto**.
-   Seleccione **Single View Application** (Aplicación de vista única).

    ![Crear un nuevo proyecto](../media/iOS-Project.png)

-   Escriba un nombre y un identificador para el nuevo proyecto.

    ![Asígnele un nombre al proyecto](../media/iOS-project-options.png)

-   Haga clic en **Siguiente** y seleccione la ubicación para el proyecto.
-   Para agregar el marco **MSRightsManagement** para marcos de trabajo de iOS, arrastre la carpeta .framework desde la carpeta de instalación del SDK hasta la sección **Frameworks** (Marcos) del **Project Navigator** (Navegador de proyectos).

    ![Establezca una ubicación](../media/ios-add-dependencies-01a.png)

-   Seleccione el botón de opción **Create groups for any added folders** (Crear grupos para las carpetas agregadas) y desactive la casilla **Copy items into destination group's folder (if needed)** (Copiar elementos en la carpeta del grupo de destino [si es necesario]).

    En lugar de crear una copia, esta acción mantiene la referencia a la carpeta de instalación del SDK.

    ![Establezca la referencia a la carpeta de instalación del SDK](../media/iOS-create-groups.png)

-   Para agregar el MS RMS SDK 4.2 para la agrupación de recursos, arrastre el archivo MSRightsManagementResources.bundle desde la carpeta MSRightsManagement.framework/Resources hasta la sección **Frameworks** (Marcos) de Project Navigator (Navegador de proyectos).

    ![Agregue la agrupación de recursos](../media/iOS-add-resource-bundle-02a.png)

-   Al igual que hizo cuando copió el marco, seleccione el botón de opción **Create groups for any added folders** (Crear grupos para las carpetas agregadas) y desactive la casilla **Copy items into destination group's folder (if needed)** (Copiar elementos en la carpeta del grupo de destino [si es necesario]).
-   El SDK se basa en otros marcos, como: **CoreData**, **MessageUI**, **SystemConfiguration**, **Libresolv** y **Security**. Para agregar estos marcos, navegue a la sección **Linked Frameworks and Libraries** (Marcos y bibliotecas vinculados) del panel **Summary** (Resumen) del destino y expanda esa sección para agregarlos.

    Los marcos **UIKit** y **Foundation** son obligatorios y, por lo general, están presentes de forma predeterminada.

    ![Agregue recursos](../media/iOS-add-libraries.png)

-   Agregue la marca **-ObjC** a **Other Linker Flags** (Otras marcas de vinculador) en **Build Settings** (Configuración de compilación) de destino.

    ![Agregue la configuración de compilación](../media/iOS-linker-flags.png)

-   El **Project Navigator** (Navegador de proyectos) debería tener ahora un aspecto similar al de este árbol.

    ![Revise el proyecto](../media/iOS-verify-setup-01a.png)

-   Ya está listo para crear sus propias aplicaciones iOS/OS X.

### Véase también

* [Introducción](get-started.md)

* [Novedades](release-notes.md)

* [Conceptos y términos de desarrollador](core-concepts.md)

* [Referencia de la API de iOS/OS X](/rights-management/sdk/4.2/api/ios/ios)

 

 






<!--HONumber=Jul16_HO4-->


