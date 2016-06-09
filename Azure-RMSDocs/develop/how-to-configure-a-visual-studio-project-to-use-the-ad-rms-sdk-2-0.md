---
# required metadata

title: Configuración de Visual Studio | Azure RMS
description: Instrucciones sobre cómo configurar un proyecto de Visual Studio para usar RMS SDK 2.1.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 396A2C19-3A00-4E9A-9088-198A48B15289
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configuración de Visual Studio

Este tema contiene instrucciones sobre cómo configurar un proyecto de Visual Studio para usar Rights Management Services SDK 2.1.

## Requisitos previos

-   [Instalar el SDK](install-the-rms-sdk.md)

**Instrucciones**

### Paso 1: Configurar un proyecto de Visual Studio para usar RMS SDK 2.1

Estas instrucciones son específicas de Microsoft Visual Studio 2010. Si usa una versión diferente de Microsoft Visual Studio, los cuadros de diálogo de configuración pueden aparecer ligeramente diferentes.

Estas instrucciones se aplican a la creación de una aplicación nativa de 32 bits.

1.  Agregue el directorio de inclusión de RMS SDK 2.1 a su proyecto de Visual Studio 2010.

    En **Propiedades de configuración**, seleccione **Directorios de VC ++** y agregue el directorio de inclusión de RMS SDK 2.1, **$(MSIPCSDKDIR)\\inc**, al campo **Directorios de inclusión**.

    ![Campo Directorios de inclusión de Propiedades de configuración](../media/include_directories.png)

2.  Agregue el directorio de bibliotecas de RMS SDK 2.1 a su proyecto de Visual Studio 2010.

    En **Propiedades de configuración** seleccione **Directorios de VC ++** y agregue el directorio de bibliotecas de RMS SDK 2.1 al campo **Directorios de bibliotecas**.

    -   Para Win32, use **$(MSIPCSDKDIR)\\lib**
    -   Para x64, use **$(MSIPCSDKDIR)\\lib\\x64**

    ![Campo Directorios de bibliotecas de Propiedades de configuración](../media/library_directories.png)

3.  Agregue los archivos de biblioteca de RMS SDK 2.1 como dependencias de Visual Studio 2010.

    En **Enlazador**, seleccione **Entrada** y agregue los archivos de biblioteca de RMS SDK 2.1, **Msipc.lib** y **Msipc\_s.lib**, al campo **Dependencias adicionales**.

    ![Campo Dependencias de biblioteca del enlazador](../media/additional_dependencies.png)

4.  Agregue la biblioteca de vínculos dinámicos (DLL) de RMS SDK 2.1 como un archivo DLL de carga retrasada.

    Bajo **Enlazador**, seleccione **Entrada** y agregue el archivo DLL de RMS SDK 2.1, **Msipc.dll**, al campo **Archivos DLL de carga retrasada**.

    ![Campo de bibliotecas de carga retrasada del enlazador](../media/delay_loaded.png)

5.  Cree la información de versión para el binario resultante.

    En el **Explorador de soluciones** seleccione **Archivos de recursos** y agregue el nombre binario al campo **OriginalFileName**.

    ![Campo Archivos de recursos del Explorador de soluciones](../media/original_file_name.png)

## Temas relacionados

* [Instalar el SDK](install-the-rms-sdk.md)
 

 


<!--HONumber=Jun16_HO2-->


