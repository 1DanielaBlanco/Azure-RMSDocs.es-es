---
# required metadata

title: Instalar y configurar el servidor | Azure RMS
description: Instalar y configurar un servidor RMS para probar la aplicación con derechos habilitados.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 32C7F387-CF7E-4CE0-AFC9-4C63FE1E134A
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Instalar y configurar el servidor

En este tema se explica cómo instalar y configurar un servidor RMS para probar la aplicación con derechos habilitados.

**Importante**  Si está probando su aplicación ejecutándola en el entorno 1-box RMS ISV, no es necesario instalar un servidor RMS porque ya hay uno instalado y configurado en el entorno de 1 cuadro.
Para más información sobre el entorno 1-box AD RMS ISV, vea [Set up the test environment](how-to-set-up-your-test-environment.md) (Configurar el entorno de prueba).

 

## Instrucciones

### Paso 1: Configurar el servidor RMS

Los siguientes pasos le guiarán en la configuración del servidor de RMS e incluyen:

-   Configurar el registro
-   Instalar el servidor
-   Inscribir el servidor

1.  **Configurar el registro**

    Para especificar que está usando la jerarquía de certificados de preproducción, establezca los siguientes valores del registro.

    **Nota**  Si usa Windows Server 2008 R2 o Windows Server 2008, establezca los valores del registro antes de instalar el servicio de AD RMS.

    Si usa AD RMS en Windows Server 2008 R2, debe establecer el siguiente valor **REG\_DWORD**. Sustituya este valor por 0 (cero) para cambiar a la jerarquía de producción.

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**Hierarchy** = 0x00000001

    Si usa AD RMS en Windows Server 2008 R2 y otro servicio de AD RMS ya está implementado en Active Directory como un servicio de preproducción, agregue el siguiente valor de cadena vacía en el registro.

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**GICURL** = ""

    Si usa AD RMS en Windows Server 2008, debe establecer el siguiente valor **REG\_DWORD**. Sustituya este valor por 0 (cero) para cambiar a la jerarquía de producción.

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**2.0**\\**Hierarchy** = 0x00000001

    Si usa AD RMS en Windows Server 2008 y otro servicio de AD RMS ya está implementado en Active Directory como un servicio de preproducción, agregue el siguiente valor de cadena vacía en el registro.

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**2.0**\\**GICURL** = ""

2.  **Instalar el servidor**

    Active Directory Rights Management Services (AD RMS) está formado por componentes de servidor y de cliente independientes. El componente de servidor se implementa como un conjunto de servicios web que pueden usarse para administrar una infraestructura de RMS y emitir licencias para los consumidores y editores de contenido, además de certificados para usuarios y equipos.

    A partir de Windows Server 2008, el sistema operativo incluye los componentes de cliente y servidor. Puede descargar los componentes de servidor para los sistemas operativos anteriores desde la ubicación siguiente.

    -   [RMS Server v1.0 SP2](http://go.microsoft.com/fwlink/p/?linkid=73722)

    Para configurar el componente de servidor en Windows Server 2008, debe instalar el rol de AD RMS. Pero antes de hacerlo, debe configurar el registro para especificar que se va a usar la jerarquía de certificados de preproducción en lugar de la jerarquía de producción. Si, en cambio, está desarrollando aplicaciones en un sistema operativo del servidor anterior, configure el registro después de instalar RMS Server v1.0 SP2 pero antes de aprovisionar el servicio de RMS.

    Para más información, vea el paso 1, "Configurar el registro".

3.  **Inscribir el servidor**

    Inscriba un servidor de Rights Management Services (RMS) para identificarlo en la jerarquía de preproducción o de producción. El proceso de inscripción deja un certificado emisor de licencias de servidor en el equipo servidor. Este certificado está ligado a una raíz de confianza de Microsoft. La manera de inscribir el servidor depende de la versión de RMS que se esté usando.

    -   **Inscripción automática**

        A partir de Windows Server 2008, es posible inscribir un servidor RMS en la jerarquía apropiada sin necesidad de enviar información a Microsoft. Cuando se instala el rol de RMS, también se instalan un certificado de inscripción automática y la clave privada. Estos se usan para crear automáticamente el certificado emisor de licencias de servidor. No se produce ningún intercambio de información con Microsoft.

    -   **Inscripción en línea** Si usa AD RMS v1.0 SP2, puede inscribir el servidor en línea. La inscripción tiene lugar en segundo plano durante el proceso de aprovisionamiento, pero es necesaria una conexión a Internet y debe especificarse el valor del registro adecuado para identificar en qué jerarquía se va a inscribir el servidor. Para inscribirse en la jerarquía de preproducción, agregue el siguiente valor **REG\_SZ** y aprovisione el servidor. Para inscribirse en la jerarquía de producción, agregue este valor y aprovisione el servidor.

        Para más información, vea el paso 1, "Configurar el registro".

        **HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**1.0**\\**UddiProvider** = 0e3d9bb8-b765-4a68-a329-51548685fed3

## Temas relacionados

* [Procedimiento](how-to-use-msipc.md)
 

 





<!--HONumber=Apr16_HO4-->


