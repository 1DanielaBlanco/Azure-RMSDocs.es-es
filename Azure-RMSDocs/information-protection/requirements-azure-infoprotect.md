---
title: Requirements for Azure Information Protection (Requisitos de Azure Information Protection) | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/21/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: aa4353e5-c5b0-47f6-a6f9-87d13e8f075f
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: eee30e1dca8013aa6d66c55ffa7385da956db4e8
ms.openlocfilehash: f87ec26f5d950ca7a5ca894d8adece8a523f1728


---

# Requirements for Azure Information Protection (Requisitos de Azure Information Protection)

*Se aplica a: Azure Information Protection (versión preliminar)*


Para evaluar la versión preliminar de Azure Information Protection, asegúrese de cumplir los siguientes requisitos previos. 

|Requisito|Más información|
|---------------|--------------------|
|Una suscripción de nube que incluya Azure RMS|Su organización debe tener una suscripción en la nube que admita Rights Management.<br /><br />Para obtener más información, así como vínculos a versiones gratuitas de prueba, vea [Suscripciones en la nube que son compatibles con Azure RMS](../get-started/requirements-subscriptions.md).|
|Directorio de Azure AD|Su organización debe tener un directorio de Azure AD que admita la autenticación de usuario para Azure RMS y Azure Information Protection. Además, si desea usar sus cuentas de usuario desde su directorio local (AD DS), también deberá configurar la integración de directorios.<br /><br />Multi-Factor Authentication (MFA) es compatible con Azure RMS si tiene el software cliente necesario y la infraestructura de MFA configurada correctamente.<br /><br />Para obtener más información, vea [Directorio de Azure AD](../get-started/requirements-azure-ad.md), donde la información de Azure RMS también se aplica a Azure Information Protection.|
|Dispositivos cliente|Los siguientes dispositivos cliente son compatibles con esta versión preliminar:<br /><br />- Windows 10 (x86 y x64)<br /><br />- Windows 8.1 (x86 y x64)<br /><br />- Windows 8 (x86 y x64)<br /><br />- Windows 7 Service Pack 1 (x86 y x64)<br /><br />Versión mínima de Microsoft .NET Framework: **4.6.1** Para obtener más información sobre esta versión y las opciones para descargarla, vea [Microsoft .NET Framework 4.6.1 is available on Windows Update and WSUS](https://blogs.msdn.microsoft.com/dotnet/2016/01/26/microsoft-net-framework-4-6-1-is-available-on-windows-update-and-wsus/) (Microsoft .NET Framework 4.6.1 está disponible en Windows Update y WSUS) en .NET Blog.<br /><br />Al proteger los datos, se pueden consumir con los mismos dispositivos (Windows, Mac, iOS, Android...), compatibles con Azure Rights Management. Para obtener más información sobre estos dispositivos y las versiones compatibles, vea [Requisitos de Azure RMS: dispositivos cliente que son compatibles con Azure RMS](../get-started/requirements-client-devices.md).|
|Aplicaciones|Para la versión preliminar y según la disponibilidad general, Azure Information Protection admite el etiquetado y la protección de archivos y correos electrónicos creados con las siguientes aplicaciones de Office: **Word**, **Excel**, **PowerPoint** y **Outlook** desde los siguientes paquetes de Office:<br /><br />- Office 2016<br /><br />- Office 2013 con el Service Pack 1<br /><br />- Office 2010<br /><br />Después de la disponibilidad general, busque un anuncio en [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) (Blog de seguridad y movilidad empresarial) en el que se indique cuándo admitirá Azure Information Protection tipos de archivo adicionales, como PDF, audio, vídeo y archivos de imagen.|
|Infraestructura compatible con la conectividad a Internet y dependiente de los servicios en la nube|Si tiene un firewall o dispositivos de red de intervención similares que deban configurarse para permitir conexiones específicas, vea la información de **Azure Rights Management (RMS)** en la sección [Portal de Office 365 e infraestructura compartida](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#BKMK_Portal-identity) del siguiente artículo de Office: [URL de Office 365 e intervalos de direcciones IP](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).<br /><br />Además:<br /><br />-Debe permitir el tráfico HTTPS en el TCP 443 a **rmsibizaapiprod.cloudapp.net**.<br /><br />- No termine la conexión TLS de cliente a servicio (por ejemplo, para realizar una inspección de los paquetes). <br /><br />- Si usa un proxy web que precisa de autenticación, debe configurarlo para usar autenticación integrada de Windows con las credenciales de inicio de sesión de Active Directory del usuario.|

## Pasos siguientes

Si cumple estos requisitos, pruebe nuestra demostración autodidacta para configurar y experimentar con Azure Information Protection: [Tutorial de inicio rápido de Azure Information Protection](infoprotect-quick-start-tutorial.md).




<!--HONumber=Jul16_HO3-->


