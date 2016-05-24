---
# required metadata

title: Servidor de AD RMS | Azure RMS
description: El componente de servidor de Rights Management Services (RMS) se implementa mediante un conjunto de servicios web que se ejecutan en Microsoft Internet Information Services.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 17B05780-B0EF-4805-8304-52DCDEB3AADB
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Servidor de AD RMS

Este tema describe el propósito y las funciones del servidor de RMS.

El componente de servidor de Rights Management Services (RMS) se implementa mediante un conjunto de servicios web que se ejecutan en [Microsoft Internet Information Services](http://www.iis.net/overview) (IIS) También puede utilizar la implementación basada en la nube a través de RMS en Azure. Para más información sobre cómo utilizar el servicio de Azure Rights Management, consulte [Habilitación de la aplicación de servicio para que funcione con RMS basado en la nube](how-to-use-file-api-with-aadrm-cloud.md).

Para servidores locales a partir de Windows Server 2008, puede instalar y configurar el servicio de RMS agregándolo como un rol. Para instalar el servicio en los sistemas operativos anteriores, descárguelo del Centro de descarga de Microsoft en [Microsoft Windows Rights Management Services con Service Pack 2](http://www.microsoft.com/download/en/details.aspx?id=4909).

De los muchos servicios web instalados, los siguientes son importantes para el desarrollo de las aplicaciones.

**Administración**: hospeda el sitio web de administración que permite administrar RMS. El servicio se ejecuta en servidores de certificación raíz y en servidores de licencias. Puede usar la [API de scripting de Active Directory Rights Management Services ](https://msdn.microsoft.com/library/Bb968797) escribir scripts de administración.

**Certificación de cuentas**: crea certificados de equipo que identifican los equipos en la jerarquía de certificados de RMS y los certificados de cuenta de derechos que asocian los usuarios a equipos específicos. Para más información, consulte [Activación de un usuario](https://msdn.microsoft.com/library/Cc530378).

Este servicio se ejecuta en el servidor de certificación raíz.

**Licencias**: emite una licencia de usuario final que permite a los usuarios finales consumir el contenido protegido. El servicio se ejecuta en servidores de certificación raíz y en servidores de licencias.

**Publicación**: crea [Creación de una licencia de emisión](https://msdn.microsoft.com/library/Aa362355). El servicio se ejecuta en servidores de certificación raíz y en servidores de licencias.

**Certificación previa**: permite a un servidor solicitar un certificado de cuenta de derechos (RAC) en nombre del usuario. Un RAC utiliza el certificado de equipo de activación de RMS para enlazar las cuentas de usuario con equipos específicos o grupos de equipos y se utiliza para permitir a los consumidores utilizar contenido protegido. El servicio se ejecuta en servidores de certificación raíz y en servidores de licencias.

**Localizador de servicios**: proporciona la dirección URL de los servicios de publicación, licencias y certificación de cuenta a Active Directory para que los clientes de RMS los puedan detectar. El servicio se ejecuta en servidores de certificación raíz y en servidores de licencias.

 

## Temas relacionados ##
* [Información general](ad-rms-overview.md)
* [Servicios de Microsoft Internet Information Server](http://www.iis.net/overview)
* [Habilitación de la aplicación de servicio para que funcione con RMS basado en la nube](how-to-use-file-api-with-aadrm-cloud.md)
* [Microsoft Windows Rights Management Services con Service Pack 2](http://www.microsoft.com/download/en/details.aspx?id=4909)
* [API de scripting de Active Directory Rights Management Services](https://msdn.microsoft.com/library/Bb968797)
* [Activación de un equipo](https://msdn.microsoft.com/library/Cc530377)
* [Activación de un usuario](https://msdn.microsoft.com/library/Cc530378)
* [Creación de una licencia de emisión](https://msdn.microsoft.com/library/Aa362355)

 

 


<!--HONumber=Apr16_HO4-->


