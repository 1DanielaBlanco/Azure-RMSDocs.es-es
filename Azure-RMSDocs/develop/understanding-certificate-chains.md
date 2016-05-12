---
# required metadata

title: Descripción de cadenas de certificados | Azure RMS
description:
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 14694cb0-adc4-4c2f-aff5-22aa132777df

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿# Descripción de cadenas de certificados

Desarrollar una aplicación habilitada para derechos requiere un par de claves públicas y una cadena de certificados que remita a un certificado de Microsoft en la raíz de confianza.

## Tipos de certificado

Todas las licencias y los certificados utilizados en un entorno de Rights Management Services (RMS) constan de una cadena de certificados que remiten a un certificado de entidad emisora (CA) de Microsoft. Microsoft proporciona dos cadenas en la que se puede anidar una licencia o un certificado, una cadena de certificados de preproducción y una cadena de producción. Se recomienda usar la jerarquía de preproducción al desarrollar una aplicación para que sea posible trabajar sin firmar un *contrato de licencia de producción* con Microsoft. Tenga en cuenta que también debe configurarse el servidor RMS para preproducción.

Antes de publicar la aplicación, debe cambiar a una cadena de producción. El contenido protegido por un certificado de preproducción es menos seguro que un certificado de producción.

Las claves pública y privada y el certificado de preproducción se incluyen con el SDK de los siguientes archivos ubicados en la carpeta `%MsipcSDKDir%\Bin`.

- **ISVTier5AppSigningPrivKey.dat** contiene la clave privada utilizada para firmar un manifiesto para su uso durante el desarrollo de aplicaciones.
- **ISVTier5AppSigningPubKey.dat** contiene la clave pública firmada en la jerarquía de certificados de preproducción.
- **ISVTier5AppSignSDK_Client.xml** contiene el certificado de preproducción utilizado para generar un manifiesto para su uso durante el desarrollo de aplicaciones.

 

El certificado y la clave privada se usan para crear y firmar un manifiesto que identifica los archivos que pueden o deben cargarse en el espacio de procesos de la aplicación y aquellos que no deben cargarse. A continuación, la plataforma carga el manifiesto.

Independientemente de que haya utilizado un certificado de preproducción durante el desarrollo de aplicaciones, cuando esté listo para publicar la aplicación, debe generar un nuevo par de claves, adquirir un certificado de producción de Microsoft y usar la nueva clave privada y el certificado para crear y firmar un manifiesto de aplicación.

Para más información sobre cómo trabajar con cadenas de certificados y la firma de la aplicación, consulte [Cambio al entorno de producción](switching-to-the-production-environment.md).

### Temas relacionados

* [Conceptos para desarrolladores](ad-rms-concepts-nav.md)
* [Cambio al entorno de producción](switching-to-the-production-environment.md)
 

 


<!--HONumber=Apr16_HO3-->

