---
# required metadata

title: Términos | Azure RMS
description: Colección de definiciones de terminología específicas de Rights Management Services.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 6f53c7e5-bbe2-4619-83b0-cdc620b3af14

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# Términos

Colección de definiciones de terminología específicas de Rights Management Services.

**Algoritmo en desuso**  
Ajuste modal que implementa un esquema de protección de contenido anterior, haciendo referencia específicamente al modo de cifrado de la guía electrónica (ECB). En este SDK, el ajuste le permite generar licencias compatibles con la biblioteca MSDRM que se usa en el [AD Rights Management Services SDK](https://msdn.microsoft.com/en-us/library/windows/desktop/cc530379.aspx).

Puede que este ajuste haga que la aplicación proteja el contenido de una manera que no cumple con los estándares de sus clientes para protección de contenido.

Este ajuste impedirá que la aplicación se beneficie de las mejoras criptográficas agregadas a Microsoft Rights Management SDK 3.0 o versión posterior.

**Formato de archivo protegido de Microsoft**

También llamado formato PFile, es el formato de archivo predeterminado de AD RMS y funciona como estándar en todas las aplicaciones habilitadas para RMS.

El formato PFile es transparente para el desarrollador de la aplicación ya que se integra en la forma en que está diseñado Microsoft Rights Management SDK 4.2.

 

 





<!--HONumber=Apr16_HO3-->


