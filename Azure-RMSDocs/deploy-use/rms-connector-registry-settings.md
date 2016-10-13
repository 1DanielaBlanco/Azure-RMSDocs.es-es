---
title: "Configuración del Registro para el conector RMS | Azure Information Protection"
description: "Información sobre la configuración del registro de servidores mediante el conector RMS. El método recomendado para configurar estos servidores es utilizar la herramienta de configuración del servidor del conector Microsoft RMS."
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ed3e9a3d-0f7c-4abc-9d0b-aa3b18403d39
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d5b6a1fc3fa0a19f3a6b65aa7b8815eda7432cd7
ms.openlocfilehash: 1dd1b26735732f4bef8cf73a566b0f26b7610a82


---


# Configuración del Registro para el conector de Rights Management

>*Se aplica a: Azure Information Protection, Office 365*


Use las tablas de las secciones siguientes solamente si quiere agregar o comprobar manualmente las configuraciones de registro en los servidores que ejecutan Exchange, SharePoint o Windows Server, lo que configura los servidores para usar el [conector RMS](deploy-rms-connector.md). El método recomendado para configurar estos servidores es utilizar la herramienta de configuración del servidor del conector RMS de Microsoft.

Instrucciones para cuando use esta configuración:

-   *MicrosoftRMSURL* es la URL del servicio de Microsoft RMS de tu organización. Para encontrar este valor:

    1.  Ejecute el cmdlet [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) para Azure RMS. Si aún no ha instalado el módulo de Windows PowerShell para Azure RMS, consulte [Instalación de Windows PowerShell para Azure Rights Management](install-powershell.md).

    2.  En la salida, identifique el valor **LicensingIntranetDistributionPointUrl** .

        Por ejemplo: **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

    3.  En el valor, quite **/_wmcs/licensing** de esta cadena. La cadena resultante es su URL de Microsoft RMS. En nuestro ejemplo, la URL de Microsoft RMS sería el valor siguiente:

        **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

-   *ConnectorFQDN* es el nombre de equilibrio de carga que definió en DNS para el conector. Por ejemplo, **rmsconnector.contoso.com**.

-   Use el prefijo HTTPS para la URL del conector si ha configurado el conector para usar HTTPS para comunicarte con tus servidores locales. Para obtener más información, vea la sección [Configuración del conector RMS para usar HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https) de las instrucciones generales. Las URL de Microsoft RMS usan siempre HTTPS.


## Configuración del Registro de Exchange 2016 o Exchange 2013

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**Tipo:** Reg_SZ

**Valor:** Default

**Datos:** https://*MicrosoftRMSURL*/_wmcs/certification

---

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valor:** Default

**Datos:** https://*MicrosoftRMSURL*/_wmcs/Licensing

---

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\CertificationServerRedirection

**Tipo:** Reg_SZ

**Valor:** https://*MicrosoftRMSURL*


**Datos:** Una de las siguientes, en función de si usas HTTP o HTTPS desde tu servidor Exchange al conector RMS:

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*

---

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**Tipo:** Reg_SZ

**Valor:** https://*MicrosoftRMSURL*


**Datos:** Una de las siguientes, en función de si usas HTTP o HTTPS desde tu servidor Exchange al conector RMS:

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*


## Configuración del Registro de Exchange 2010

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**Tipo:** Reg_SZ

**Valor:** Default

**Datos:** https://*MicrosoftRMSURL*/_wmcs/certification

---

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valor:** Default

**Datos:** https://*MicrosoftRMSURL*/_wmcs/Licensing

---

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\CertificationServerRedirection

**Tipo:** Reg_SZ

**Valor:** https://*MicrosoftRMSURL*

**Datos:** Una de las siguientes, en función de si usas HTTP o HTTPS desde tu servidor Exchange al conector RMS:

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*

---

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Tipo:** Reg_SZ

**Valor:** https://*MicrosoftRMSURL*

**Datos:** Una de las siguientes, en función de si usas HTTP o HTTPS desde tu servidor Exchange al conector RMS:

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*


## Configuración del Registro de SharePoint 2016 o SharePoint 2013

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\LicensingRedirection

**Tipo:** Reg_SZ

**Valor:** https://*MicrosoftRMSURL*/_wmcs/licensing


**Datos:** Una de las siguientes, en función de si usa HTTP o HTTPS desde su servidor SharePoint al conector RMS:

- http://*ConnectorFQDN*/_wmcs/licensing

- https://*ConnectorFQDN*/_wmcs/licensing

---

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification

**Tipo:** Reg_SZ

**Valor:** Default

**Datos:** Una de las siguientes, en función de si usa HTTP o HTTPS desde su servidor SharePoint al conector RMS:

- http://*ConnectorFQDN*/_wmcs/certification

- https://*ConnectorFQDN*/_wmcs/certification

---

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valor:** Default


**Datos:** Una de las siguientes, en función de si usa HTTP o HTTPS desde su servidor SharePoint al conector RMS:

- http://*ConnectorFQDN*/_wmcs/licensing

- https://*ConnectorFQDN*/_wmcs/licensing




## Configuración del Registro del servidor de archivos y de la Infraestructura de la clasificación de archivos

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valor:** Default

**Datos:** http://*ConnectorFQDN*/_wmcs/licensing

---

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

**Tipo:** Reg_SZ

**Valor:** Default

**Datos:** http://*ConnectorFQDN*/_wmcs/certification


Vuelta a [Implementación del conector de Azure Rights Management](deploy-rms-connector.md)


<!--HONumber=Sep16_HO4-->


