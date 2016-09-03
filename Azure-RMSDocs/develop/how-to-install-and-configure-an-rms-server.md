---
title: "Cómo instalar, configurar y probar con un servidor RMS |Azure RMS"
description: "Instalar y configurar un servidor RMS para probar la aplicación con derechos habilitados."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 06/28/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 32C7F387-CF7E-4CE0-AFC9-4C63FE1E134A
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 5d2339ece646fc51410186d43facdea28ac8fdfe
ms.openlocfilehash: d046e7f6bbe867b6bc867483441bb0cc5c20df82


---

# Instalación, configuración y prueba con un servidor RMS

En este tema se explica cómo conectar con un servidor RMS o Azure RMS para probar la aplicación con derechos habilitados.
 
## Instrucciones

### Paso 1: Configurar el servidor RMS

Los siguientes pasos le guiarán en la configuración del servidor de RMS e incluyen:

-   Instalar el servidor
-   Inscribir el servidor

1.  **Instalar el servidor**

    Active Directory Rights Management Services (AD RMS) está formado por componentes de servidor y de cliente independientes. El componente de servidor se implementa como un conjunto de servicios web que pueden usarse para administrar una infraestructura de RMS y emitir licencias para los consumidores y editores de contenido, además de certificados para usuarios y equipos.

    A partir de Windows Server 2008, el sistema operativo incluye los componentes de cliente y servidor. Puede descargar los componentes de servidor para los sistemas operativos anteriores desde la ubicación siguiente.

    -   [RMS Server v1.0 SP2](http://go.microsoft.com/fwlink/p/?linkid=73722)

    Para configurar el componente de servidor en Windows Server 2008, debe instalar el rol de AD RMS. Si está desarrollando aplicaciones en un sistema operativo del servidor anterior, configure el registro después de instalar RMS Server v1.0 SP2, pero antes de aprovisionar el servicio de RMS.

2.  **Inscribir el servidor**

    Inscriba un servidor de Rights Management Services (RMS) para identificarlo en la jerarquía de preproducción o de producción. El proceso de inscripción deja un certificado emisor de licencias de servidor en el equipo servidor. Este certificado está ligado a una raíz de confianza de Microsoft. La manera de inscribir el servidor depende de la versión de RMS que se esté usando.

    -   **Inscripción automática**

        A partir de Windows Server 2008, es posible inscribir un servidor RMS en la jerarquía apropiada sin necesidad de enviar información a Microsoft. Cuando se instala el rol de RMS, también se instalan un certificado de inscripción automática y la clave privada. Estos se usan para crear automáticamente el certificado emisor de licencias de servidor. No se produce ningún intercambio de información con Microsoft.

    -   **Inscripción en línea**

        Si usa AD RMS v1.0 SP2, puede inscribir el servidor en línea. La inscripción tiene lugar en segundo plano durante el proceso de aprovisionamiento, pero es necesaria una conexión a Internet.

        **HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**1.0**\\**UddiProvider** = 0e3d9bb8-b765-4a68-a329-51548685fed3

3. **Prueba con el servidor RMS**

    Para realizar una prueba con un servidor RMS, configure la detección del lado servidor o del lado cliente para permitir que el cliente de Rights Management Services 2.1 pueda detectar y establecer comunicación con el servidor RMS.

    > [!Note]
    > La prueba con Azure RMS no requiere la configuración de detección.

  - En la detección del lado servidor, un administrador registra un punto de conexión de servicio (SCP) para el clúster raíz de RMS con Active Directory, y el cliente consulta a Active Directory para detectar el SCP y establecer una conexión con el servidor.
  - En la detección del lado cliente, la detección de servicios de RMS se configura en el Registro del equipo donde se ejecuta el cliente de RMS 2.1. En esta configuración, el cliente de RMS 2.1 apunta al servidor RMS que se va a usar. Cuando están presentes, no se realiza la detección del lado servidor.

  Para configurar la detección del lado cliente, se pueden establecer las siguientes claves del Registro de modo que apunten al servidor RMS. Para más información sobre cómo configurar la detección del lado del servicio, consulte [Notas de la implementación del cliente de RMS 2.0](https://technet.microsoft.com/library/jj159267(WS.10).aspx).

1. **EnterpriseCertification**
        HKEY_LOCAL_MACHINE        SOFTWARE          Microsoft            MSIPC              ServiceLocation                EnterpriseCertification

  **Valor**: (predeterminado): [**http|https**]://RMSClusterName/**_wmcs/Certification**

2. **EnterprisePublishing**
        HKEY_LOCAL_MACHINE        SOFTWARE          Microsoft            MSIPC              ServiceLocation                EnterprisePublishing **Valor**: (predeterminado): [**http|https**]://RMSClusterName/**_wmcs/Licensing**

>[!NOTE] 
> De forma predeterminada, estas claves no existen en el Registro y necesitan crearse.

>[!IMPORTANT] 
> Si está ejecutando una aplicación de 32 bits en una versión de Windows de 64 bits, establezca estas claves en la ubicación de claves siguiente:<p>
  ```    
  HKEY_LOCAL_MACHINE
    SOFTWARE
      Wow6432Node
        Microsoft
          MSIPC
            ```

 

 



<!--HONumber=Aug16_HO4-->


