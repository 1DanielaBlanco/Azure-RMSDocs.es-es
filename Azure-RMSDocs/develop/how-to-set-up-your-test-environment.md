---
title: "Prueba de la aplicación | Azure RMS"
description: "Instrucciones sobre cómo configurar la aplicación para las pruebas."
keywords: 
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: E480D8D6-F070-43D1-B2B0-6921459C3437
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: c1705015efbe038b577c63286813bc560e62b148
ms.sourcegitcommit: 93124ef58e471277c7793130f1a82af33dabcea9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/11/2018
---
# <a name="testing-your-application"></a>Prueba de la aplicación

Este tema contiene instrucciones sobre cómo configurar la prueba de la aplicación.

## <a name="instructions"></a>Instrucciones

### <a name="step-1-setup-for-testing"></a>Paso 1: configuración para la prueba

Puede realizar la prueba con Azure RMS o un servidor RMS que se ejecute en Windows Server. Se recomienda que comience la prueba en Azure RMS y después, si es necesario para la implementación, realice la prueba con el servidor RMS.

1. Para realizar la prueba con Azure RMS, vea [Uso de la autenticación ADAL](how-to-use-adal-authentication.md).
2. Para realizar la prueba con el servidor RMS, consulte [Instalación y configuración de un servidor RMS](how-to-install-and-configure-an-rms-server.md).
3. A continuación se describe cómo instalar Developer Runtime.

   Debe tener el cliente de Rights Management Services 2.1 instalado en el equipo en el que va a probar la aplicación.
   - Si va a probar la aplicación en un equipo que no sea el equipo de desarrollo, puede instalar el cliente de RMS 2.1 en ese equipo desde la [página de descarga del cliente de AD RMS](http://www.microsoft.com/en-us/download/details.aspx?id=38396).
   - Si va a probar la aplicación en el equipo de desarrollo, necesita tener instalado Rights Management Services SDK 2.1. A estas alturas, el cliente de RMS 2.1 ya se habrá instalado en modo silencioso.

    Para más información sobre cómo instalar RMS SDK 2.1, consulte [Instalar el SDK](install-the-rms-sdk.md).

## <a name="remarks"></a>Comentarios

Las instrucciones de este tema no son exhaustivas. Para obtener información detallada sobre cómo configurar el cliente de RMS 2.1, vea [RMS Client 2.1 Deployment Notes](https://technet.microsoft.com/en-us/library/jj159267(WS.10).aspx) (Notas de implementación del cliente de RMS 2.1).

### <a name="related-topics"></a>Temas relacionados

* [Instalación y configuración de un servidor RMS](how-to-install-and-configure-an-rms-server.md)
* [Uso de la autenticación ADAL](how-to-use-adal-authentication.md)
* [Instalar el SDK](install-the-rms-sdk.md)
* [Notas de implementación del cliente de RMS 2.1](https://technet.microsoft.com/en-us/library/jj159267(WS.10).aspx)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]