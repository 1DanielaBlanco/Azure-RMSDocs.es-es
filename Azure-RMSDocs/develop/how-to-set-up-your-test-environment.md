---
# required metadata

title: Prueba de la aplicación | Azure RMS
description: Instrucciones sobre cómo configurar la aplicación para las pruebas.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: E480D8D6-F070-43D1-B2B0-6921459C3437
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Prueba de la aplicación

Este tema contiene instrucciones sobre cómo configurar la prueba de la aplicación.

## Instrucciones

### Paso 1: configuración para la prueba

Puede realizar la prueba con Azure RMS o un servidor RMS que se ejecute en Windows Server. Se recomienda que comience la prueba en Azure RMS y después, si es necesario para la implementación, realice la prueba con el servidor RMS.

1. Para realizar la prueba con Azure RMS, vea [Uso de la autenticación ADAL](how-to-use-adal-authentication.md).
2. Para realizar la prueba con el servidor RMS, consulte [Instalación y configuración de un servidor RMS](how-to-install-and-configure-an-rms-server.md).
3. A continuación se describe cómo instalar Developer Runtime.

   Debe tener el cliente de Rights Management Services 2.1 instalado en el equipo en el que va a probar la aplicación.
   - Si va a probar la aplicación en un equipo que no sea el equipo de desarrollo, puede instalar el cliente de RMS 2.1 en ese equipo desde la [página de descarga del cliente de AD RMS](http://www.microsoft.com/en-us/download/details.aspx?id=38396).
   - Si va a probar la aplicación en el equipo de desarrollo, necesita tener instalado Rights Management Services SDK 2.1. A estas alturas, el cliente de RMS 2.1 ya se habrá instalado en modo silencioso.

    Para más información sobre cómo instalar RMS SDK 2.1, vea [Instalar el SDK](create-your-first-rights-aware-application.md).

## Comentarios

Las instrucciones de este tema no son exhaustivas. Para obtener información detallada sobre cómo configurar el cliente de RMS 2.1, vea [RMS Client 2.1 Deployment Notes](https://technet.microsoft.com/en-us/library/jj159267(WS.10).aspx) (Notas de implementación del cliente de RMS 2.1).

### Temas relacionados

* [Instalación y configuración de un servidor RMS](how-to-install-and-configure-an-rms-server.md)
* [Uso de la autenticación ADAL](how-to-use-adal-authentication,md)
* [Instalar el SDK](create-your-first-rights-aware-application.md)
* [Notas de implementación del cliente de RMS 2.1](https://technet.microsoft.com/en-us/library/jj159267(WS.10).aspx)
 

 


<!--HONumber=Jun16_HO2-->


