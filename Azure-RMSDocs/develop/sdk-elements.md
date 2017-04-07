---
title: Archivos del entorno de desarrollo | Azure RMS
description: "En este tema se muestran los archivos del entorno de desarrollo y sus ubicaciones de instalación relativas en su equipo."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: B57AC6F3-733C-42A8-AF83-0E15FBF27C99
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 8f52c6b737603e8fd71b32c53991bb015f945abc
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="development-environment-files"></a>Archivos del entorno de desarrollo

En este tema se muestran los archivos del entorno de desarrollo y sus ubicaciones de instalación relativas en su equipo.

Rights Management Services SDK 2.1 incluye los siguientes archivos, instalados en su equipo en la ubicación predeterminada o bien en la que usted haya especificado: %MsipcSDKDir%.

|Archivo|Path|Descripción|
|----|----|-----------|
|ReadMe.htm| \ | Contiene un vínculo a la Ayuda de RMS y [notas de la versión](release-notes-rtm.md).|
|Isvtier5appsigningprivkey.dat|\bin|Contiene la clave privada utilizada a fin de generar un manifiesto para su uso durante el desarrollo de una aplicación habilitada para RMS.|
|Isvtier5appsigningpubkey.dat|\bin|Contiene la clave pública utilizada a fin de generar un manifiesto para su uso durante el desarrollo de una aplicación habilitada para RMS.|
|Isvtier5appsignsdk_client.xml|\bin|Se utiliza a fin de generar un manifiesto para su uso durante el desarrollo de una aplicación habilitada para RMS.|
|YourAppName.isv.mcf|\bin|Un archivo de configuración del manifiesto reutilizable que puede usar para generar un manifiesto durante el desarrollo de una aplicación habilitada para RMS.|
|Ipcsecproc_isv.dll|\bin\x86|DLL usada internamente, para las aplicaciones x86, por Active Directory Rights Management Services Client 2.1 cuando se trabaja en la jerarquía de ISV.|
|Ipcsecproc_ssp_isv.dll|\bin\x86|DLL usada internamente, para las aplicaciones x86, por AD RMS 2.1 cuando se trabaja en la jerarquía de ISV.|
|Ipcsecproc_isv.dll|\bin\x64|DLL usada internamente, para las aplicaciones x64, por AD RMS Client 2.1 cuando se trabaja en la jerarquía de ISV.|
|Ipcsecproc_ssp_isv.dll|\bin\x64|DLL usada internamente, para las aplicaciones x64, por AD RMS Client 2.1 cuando se trabaja en la jerarquía de ISV.|
|Msipc.h|\inc|Archivo de inclusión principal para RMS SDK 2.1.|
|Ipcprot.h|\inc|Contiene la interfaz pública exportada por RMS SDK 2.1.|
|Ipcbase.h|\inc|Contiene tipos básicos y funciones auxiliares exportados por RMS SDK 2.1.|
|Ipcerror.h|\inc|Contiene códigos de error públicos exportados por RMS SDK 2.1.|
|Ipcfile.h|\inc|Contiene las interfaces de API de archivo exportadas por RMS SDK 2.1.|
|Msipc.lib|\lib|Biblioteca con la que vincular cuando se usa RMS SDK 2.1 para crear aplicaciones x86.|
|Msipc_s.lib|\lib|Proporciona el punto de entrada para [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx) para las aplicaciones x86.|
|Msipc.lib|\lib\x64|Biblioteca con la que vincular cuando se usa RMS SDK 2.1 para crear aplicaciones x64.|
|Msipc_s.lib|\lib\x64|Proporciona el punto de entrada para [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx) para las aplicaciones x64.|
|Genmanifest.exe|\tools|Genera un manifiesto para su uso durante el desarrollo de una aplicación habilitada para RMS.|

[!INCLUDE[Commenting house rules](../includes/houserules.md)]