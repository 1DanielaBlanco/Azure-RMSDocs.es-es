---
title: Servidor de AD RMS | Azure RMS
description: El componente de servidor de Rights Management Services (RMS) se implementa mediante un conjunto de servicios web que se ejecutan en Microsoft Internet Information Services.
keywords: ''
author: bryanla
ms.author: bryanla
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 17B05780-B0EF-4805-8304-52DCDEB3AADB
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 224139de1e23ace70923aefe508e5d6ccb2969b8
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56251115"
---
# <a name="server"></a>Servidor de

En este tema se describe el propósito y las funciones del servidor RMS para Azure y Windows Server.

**Azure RMS**: para obtener información sobre cómo usar Azure Rights Management Services, consulte [Enable your service application to work with cloud based RMS](how-to-use-file-api-with-aadrm-cloud.md) (Habilitación de la aplicación de servicio para que funcione con RMS basado en la nube).

> [!IMPORTANT] 
> Se recomienda que desarrolle y pruebe la aplicación a través de Azure RMS.

**Windows Server**: para RMS en servidores locales a partir de Windows Server 2008, puede instalar y configurar el servicio de RMS agregándolo como un rol. Para instalar el servicio en los sistemas operativos anteriores, descárguelo del Centro de descarga de Microsoft en [Microsoft Windows Rights Management Services con Service Pack 2](https://www.microsoft.com/download/details.aspx?id=4909).

De los muchos servicios web instalados, los siguientes son importantes para el desarrollo de aplicaciones para el servidor RMS en Windows Server.

| Servicio | Descripción |
|---------|-------------|
| Administration | Hospeda el sitio web de administración que permite administrar RMS. El servicio se ejecuta en servidores de certificación raíz y en servidores de licencias. Puede usar la API de scripting de Active Directory Rights Management Services para escribir scripts de administración.|
| Certificación de cuenta |Crea certificados de equipo que identifican los equipos en la jerarquía de certificados de RMS y los certificados de cuenta de derechos que asocian los usuarios a equipos específicos. Para obtener más información, consulte Activación de un equipo y Activación de un usuario.<p><p>Este servicio se ejecuta en el servidor de certificación raíz. |
|Licencias | Emite una *licencia de usuario final*. El servicio se ejecuta en servidores de certificación raíz y en servidores de licencias.|
|Publicando | Crea una *licencia de emisión* que define las directivas que se pueden enumerar en una licencia de usuario final. Para obtener más información, vea [Creating an Issuance License](https://msdn.microsoft.com/library/Aa362355) (Creación de una licencia de emisión).<p><p>El servicio se ejecuta en servidores de certificación raíz y en servidores de licencias.|
|Certificación previa | Permite a un servidor solicitar un *certificado de cuenta de derechos* en nombre de un usuario. El servicio se ejecuta en servidores de certificación raíz y en servidores de licencias.|
|Localizador de servicios | Proporciona la dirección URL de los servicios de publicación, licencias y certificación de cuenta a Active Directory para que los clientes de RMS los puedan detectar. El servicio se ejecuta en servidores de certificación raíz y en servidores de licencias.|

## <a name="related-topics"></a>Temas relacionados ##
* [Información general](ad-rms-overview.md)
* [Microsoft Internet Information Services](https://www.iis.net/overview)
* [Habilitación de la aplicación de servicio para que funcione con RMS basado en la nube](how-to-use-file-api-with-aadrm-cloud.md)
* [Microsoft Windows Rights Management Services con Service Pack 2](https://www.microsoft.com/download/details.aspx?id=4909)
* [API de scripting de Active Directory Rights Management Services](https://msdn.microsoft.com/library/Bb968797)
* [Activación de un equipo](https://msdn.microsoft.com/library/Cc530377)
* [Activación de un usuario](https://msdn.microsoft.com/library/Cc530378)
* [Creación de una licencia de emisión](https://msdn.microsoft.com/library/Aa362355)
