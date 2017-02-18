---
title: "Terminología de desarrollador AIP | Microsoft Docs"
description: "Colección de definiciones de terminología de desarrollador específicas de Rights Management Services."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: adb1f868-0da7-431b-83d1-86f41c2da4ae
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9c0977c57ea8e85b6750fe1f5a063059ee343db9
ms.openlocfilehash: 4ecf686d8e7e26909c8bda4a2d0df7fc61f413bb


---

# <a name="terms"></a>Términos

Colección de definiciones de terminología de desarrollador específicas de Azure Information Protection.

**Algoritmo en desuso**  
Ajuste modal que implementa un esquema de protección de contenido anterior, haciendo referencia específicamente al modo de cifrado de la guía electrónica (ECB). En este SDK, la configuración le permite generar licencias compatibles con la biblioteca MSDRM que se usa en el [AD Rights Management Services SDK](https://msdn.microsoft.com/library/windows/desktop/cc530379.aspx).

Puede que este ajuste haga que la aplicación proteja el contenido de una manera que no cumple con los estándares de sus clientes para protección de contenido.

Este ajuste impedirá que la aplicación se beneficie de las mejoras criptográficas agregadas a Microsoft Rights Management SDK 3.0 o versión posterior.

**Formato de archivo protegido de Microsoft**

También llamado formato PFile, es el formato de archivo predeterminado de AD RMS y funciona como estándar en todas las aplicaciones habilitadas para RMS.

El formato PFile es transparente para el desarrollador de la aplicación ya que se integra en la forma en que está diseñado Microsoft Rights Management SDK 4.2.


[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


