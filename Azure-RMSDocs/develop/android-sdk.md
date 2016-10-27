---
title: "Configuración de Android | Azure RMS"
description: "Las aplicaciones de Android pueden usar Microsoft Rights Management SDK 4.2 para habilitar la protección de información integrada en sus aplicaciones."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 986f6932-159b-4791-bd1a-7640a83ee792
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: 90c8c97c720c624ba8f1ca7703b6c79a66f77d08


---

# Configuración de Android

Las aplicaciones de Android pueden usar Microsoft Rights Management SDK 4.2 para habilitar la protección de información integrada en sus aplicaciones mediante Azure Active Directory Rights Management (AAD RM).

Este tema sirve de guía por el proceso de configuración del entorno para crear sus propias aplicaciones.

-   [Requisitos previos](#prerequisites)
-   [Opcional](#optional)
-   [Configuración del entorno de desarrollo](#configuring-your-development-environment)
-   [Consulte también](#see-also)

## Requisitos previos

Se recomienda tener el siguiente software en el sistema de desarrollo:

-   Sistema operativo Windows u OS X para ejecutar el entorno de desarrollo [Eclipse](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).
-   En esta guía se da por hecho que se está usando un SDK de Eclipse con una versión a partir de Eclipse Juno 4.2 y, además, que se está usando una instalación predeterminada.
-   Java a partir de Java 1.6.
-   [Complemento Herramientas para desarrolladores de Android (ADT)](http://developer.android.com/sdk/installing/index.html). NOTA: puede que se le pida reiniciar Eclipse para completar la instalación.

     

-   El paquete MS RMS SDK 4.2 para Android. Para más información, vea [Get started](get-started.md) (Introducción).

    Este SDK se puede usar para desarrollar para Android 4.0.3 (nivel de API 15) y versiones posteriores.

-   Biblioteca de autenticación: se recomienda usar la [biblioteca de autenticación de Azure AD (ADAL)](https://msdn.microsoft.com/library/jj573266.aspx). Con todo, también puede usar otras bibliotecas de autenticación que admiten OAuth 2.0.

    Para más información, vea [ADAL for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android) (ADAL para Android).

    **Nota:** si la aplicación no usa la biblioteca ADAL como biblioteca de autenticación OAuth 2.0, conviene revisar estas directrices sobre Android: [Some SecureRandom Thoughts](http://android-developers.blogspot.com/2013/08/some-securerandom-thoughts.html) (Algunas consideraciones sobre SecureRandom).

     

Lea el tema de [novedades](release-notes.md) para más información sobre actualizaciones, notas de la versión y preguntas más frecuentes de la API.

## Opcional

Nuestra biblioteca de interfaz de usuario proporciona una interfaz de usuario reutilizable para operaciones de consumo y protección, dirigida a desarrolladores que no quieren crear su propia interfaz de usuario personalizada: [UI Library and Sample app for Android](https://github.com/AzureAD/rms-sdk-ui-for-android) (Biblioteca de interfaz de usuario y aplicación de ejemplo para Android).

## Configurar el entorno de desarrollo

**Nota sobre la versión preliminar de MS RMS SDK 4.2:** en esta versión preliminar, las capturas de pantalla no se han actualizado para reflejar el cambio en los nombres de las rutas de acceso de com/microsoft a com/microsoft/rightsmanagment. El texto sí se ha actualizado.

 
-   Abra el entorno de desarrollo de Eclipse.
-   Para crear un proyecto de aplicación de Android, en el menú **File** (Archivo), haga clic en **New** (Nuevo) y en **Project** (Proyecto) y, después, seleccione **Android Application Project** (Proyecto de aplicación de Android).

    ![Cree una nueva aplicación de Android.](../media/Android-setup-01c.png)

-   Escriba el nombre de aplicación. El nombre de proyecto y el nombre de paquete se rellenarán según este nombre de aplicación.
-   Haga clic en **Next** (Siguiente) y seleccione dónde quiere crear el área de trabajo.

    ![Escriba el nombre de aplicación.](../media/Android-setup-02a.jpg)

-   Haga clic en **Next** (Siguiente) y seleccione un icono para la aplicación.

    ![Seleccione un icono para la aplicación.](../media/Android-setup-03.png)

-   Haga clic en **Next** (Siguiente) y seleccione **Blank Activity** (Actividad en blanco) para crear la actividad.

    ![Cree la actividad.](../media/Android-setup-04.png)

-   Haga clic en **Next** (Siguiente) e indique un nombre para la actividad. Puede dejar *MainActivity* como nombre predeterminado con un nombre de diseño de *activity\_main*.

    ![Indique un nombre para la actividad.](../media/Android-setup-05a.jpg)

-   Haga clic en **Finalizar**.

    ![Finalice la creación.](../media/Android-setup-06.jpg)

-   El proyecto se crea, junto con la clase de actividad principal *MainActivity.java*.

**Referencia al SDK**

-   Vaya a la carpeta donde ha extraído *adrms\_android\_sdk.zip*. En la carpeta "SDK > com > microsoft > rightsmanagement", asegúrese de que los archivos *.classpath*, *.project* y *project.properties* no están marcados como de solo lectura.
-   Para poder hacer referencia al SDK, hay que importarlo al área de trabajo.

    En Eclipse, haga clic en **File** (Archivo). En el menú **File** (Archivo), haga clic en **Import** (Importar). En el cuadro de diálogo **Import** (Importar), seleccione **Android / Existing Android Code into Workspace** (Android/Código de Android existente a área de trabajo).

    ![Impórtelo al área de trabajo.](../media/Android-setup-07.png)

-   Haga clic en **Siguiente**. Seleccione la carpeta donde ha extraído *adrms\_android\_sdk.zip*. El SDK debe aparecer en la lista como **com.microsoft.rightsmanagement**.

    ![Desplácese para seleccionar la carpeta.](../media/Android-setup-08c.jpg)

-   Cuando haga clic en **Finish** (Finalizar), el proyecto del SDK aparecerá como un elemento relacionado de la aplicación creada anteriormente.

    ![El proyecto del SDK aparece como un elemento relacionado de la aplicación.](../media/Android-setup-09.jpg)

-   Haga clic con el botón derecho en el icono **Project** (Proyecto) para ver las propiedades del proyecto.
-   Vaya a la pestaña **Android**.
-   Haga clic en **Add** (Agregar) y, después, seleccione la biblioteca *com.microsoft.rightsmanagement* en el área de trabajo.

    ![Agregue la biblioteca.](../media/Android-setup-10b.jpg)

-   Haga clic en **Aceptar**.

    Como MS RMS SDK 4.2 se conecta a AAD RM, la aplicación debe tener los permisos **INTERNET** y **ACCESS\_NETWORK\_STATE**. Para ello, abra el archivo *AndroidManifest.xml* en la raíz del proyecto.

    Para agregar los permisos, haga clic en **Add** (Agregar) y, luego, seleccione **Uses Permissions** (Permisos de uso).

    ![Agregue permisos.](../media/Android-setup-11d.jpg)

-   Para comprobar que el paso del manifiesto es correcto, abra el manifiesto en un editor de texto. Asegúrese de que aparecen las siguientes líneas:


    <uses-sdk      android:minSdkVersion="15"      android:targetSdkVersion="19"/> <uses-permission android:name="android.permission.INTERNET"/> <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/> <uses-permission/>


**Note** The SDK uses the *android.support.v4*

-   Ya está listo para crear sus propias aplicaciones Android.

### Véase también

[Introducción](get-started.md)

[Novedades](release-notes.md)

[Conceptos y términos de desarrollador](core-concepts.md)

[Referencia de API de Android](https://msdn.microsoft.com/library/dn758245.aspx)

 

 



<!--HONumber=Sep16_HO5-->


