---
title: Prueba de la aplicación | Azure RMS
description: Instrucciones sobre cómo configurar la aplicación para las pruebas.
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: E480D8D6-F070-43D1-B2B0-6921459C3437
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 481922859e14009e345a38853c15e51b065d5387
ms.sourcegitcommit: 1cd4edd4ba1eb5e10cb61628029213eda316783a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53266382"
---
# <a name="testing-your-application"></a>Prueba de la aplicación

Aquí aprenderá a preparar la prueba de la aplicación.

## <a name="instructions"></a>Instrucciones

Puede hacer la prueba con Azure RMS o con un servidor RMS que se ejecute en Windows Server.  Empiece la prueba con Azure RMS y siga con el servidor RMS (si es necesario para su implementación).

- Para realizar la prueba con Azure RMS, vea [Uso de la autenticación ADAL](how-to-use-adal-authentication.md).
- Para realizar la prueba con el servidor RMS, consulte [Instalación y configuración de un servidor RMS](how-to-install-and-configure-an-rms-server.md).
- Para instalar Developer Runtime:

   Debe tener el cliente de Rights Management Services 2.1 instalado en el equipo en el que va a probar la aplicación.
   - Para probar la aplicación en un equipo que no sea el equipo de desarrollo, instale el cliente de RMS 2.1 en ese equipo desde la [página de descarga del cliente de AD RMS](https://www.microsoft.com/download/details.aspx?id=38396).
   - El equipo de desarrollo debe tener Rights Management Services SDK 2.1, instalado previamente.

   Para obtener ayuda sobre cómo instalar RMS SDK 2.1, vea [Instalar el SDK](install-the-rms-sdk.md).

## <a name="remarks"></a>Comentarios

Esta guía no es exhaustiva. Para aprender a configurar el cliente de RMS 2.1, vea [Notas de la implementación del cliente de RMS 2.1](https://technet.microsoft.com/library/jj159267(WS.10).aspx).

## <a name="related-topics"></a>Temas relacionados

* [Instalación y configuración de un servidor RMS](how-to-install-and-configure-an-rms-server.md)
* [Uso de la autenticación ADAL](how-to-use-adal-authentication.md)
* [Instalar el SDK](install-the-rms-sdk.md)
* [Notas de implementación del cliente de RMS 2.1](https://technet.microsoft.com/library/jj159267(WS.10).aspx)

