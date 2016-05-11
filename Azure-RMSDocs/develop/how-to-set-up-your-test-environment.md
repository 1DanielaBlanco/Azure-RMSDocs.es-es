---
# required metadata

title: Configuración del entorno de pruebas | Azure RMS
description: Puede probar la aplicación con derechos habilitados con diferentes opciones de servidor.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4d32682c-754d-4e30-977d-95b08e0662cc

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
# Configuración del entorno de pruebas

Puede probar la aplicación con derechos habilitados con diferentes opciones de servidor.

**Importante**  Este es un procedimiento recomendado para una primera prueba de la aplicación de Rights Management Services SDK 2.1 con el entorno de preproducción de AD RMS y en un servidor AD RMS. Luego, si quiere que su cliente tenga la posibilidad de usar la aplicación con el servicio de Azure RMS, pruébela con ese entorno. Para más información, consulte [Enable your service application to work with cloud based RMS](how-to-use-file-api-with-aadrm-cloud.md) (Permitir que la aplicación de servicio funcione con RMS en la nube).

 

### Requisitos previos

-   [Instalar el SDK](create-your-first-rights-aware-application.md)

Instrucciones

### Paso 1: Configurar su entorno de pruebas

Para probar la aplicación con derechos habilitados, debe ejecutarla en un servidor RMS configurado para preproducción. Un servidor RMS de preproducción usa la jerarquía de certificados ISV y preproducción para cifrar y descifrar archivos.

Para más información sobre la jerarquía de certificados de AD RMS, consulte [Understanding certificate chains](understanding-certificate-chains.md) (Descripción de cadenas de certificados).

Hay dos opciones disponibles para probar la aplicación en un servidor RMS:

-   **Puede ejecutar la aplicación en el entorno ISV de AD RMS de 1 cuadro**. Si está ejecutando Windows Server 2012, Windows Server 2008 R2 o Windows Server 2008 y tiene Hyper-V instalado, puede implementar el entorno ISV de AD RMS de 1 cuadro creando una máquina virtual mediante VHD de 1 cuadro de AD RMS. El entorno ISV de AD RMS de 1 cuadro proporciona un servidor RMS configurado para preproducción y también tiene Active Directory Rights Management Services Client 2.1 instalado. La configuración de registro para el cliente y servidor RMS ya está definida. Para probar la aplicación, se ejecútela en la máquina virtual en el que se implementa el entorno de cuadro 1.
-   **Puede ejecutar la aplicación en un servidor RMS configurado para preproducción y que se implemente en la red**. En este caso, también debe instalar y configurar el Cliente 2.1 de AD RMS en el equipo donde se ejecutará la aplicación. Para obtener información sobre cómo hacer esto, consulte [Configure client](how-to-configure-the-ad-rms-client-2-0.md) (Configuración del cliente). Para obtener información sobre cómo implementar un servidor RMS y configurarlo para preproducción, consulte [Install and configure the server](how-to-install-and-configure-an-rms-server.md) (Instalación y configuración del servidor).

### Temas relacionados

* [Procedimiento](how-to-use-msipc.md)
* [Página de descarga colateral del seminario web de AD RMS SDK](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)
* [Configuración del cliente](how-to-configure-the-ad-rms-client-2-0.md)
* [Instalar el SDK](create-your-first-rights-aware-application.md)
* [Instalación y configuración del servidor](how-to-install-and-configure-an-rms-server.md)
* [Descripción de cadenas de certificados](understanding-certificate-chains.md)
 

 





<!--HONumber=Apr16_HO3-->


