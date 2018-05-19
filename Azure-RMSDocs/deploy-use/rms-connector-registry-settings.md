---
title: Configuración del Registro para el conector de Rights Management - AIP
description: Información sobre la configuración del registro de servidores mediante el conector RMS. El método recomendado para configurar estos servidores es utilizar la herramienta de configuración del servidor del conector Microsoft RMS.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/16/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ed3e9a3d-0f7c-4abc-9d0b-aa3b18403d39
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 9334a781378ffdbe76dd9fe9d78f5db5913766d1
ms.sourcegitcommit: 373e05ff0c411d29cc5b61c36edaf5a203becc14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/17/2018
---
# <a name="registry-setting-for-the-rights-management-connector"></a>Configuración del Registro para el conector de Rights Management

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2*


Use las tablas de las secciones siguientes solamente si quiere agregar o comprobar de forma manual la configuración del Registro en los servidores que ejecutan Exchange, SharePoint o Windows Server. La configuración del Registro configura los servidores para usar el [conector RMS](deploy-rms-connector.md). El método recomendado para configurar estos servidores es utilizar la herramienta de configuración del servidor del conector RMS de Microsoft.

Instrucciones para cuando use esta configuración:

-   *\<YourTenantURL>* es la dirección URL del servicio Azure Rights Management para su inquilino de Azure Information Protection. Para encontrar este valor:

    1.  Ejecute el cmdlet [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) para el servicio Azure Rights Management. Si aún no ha instalado el módulo de Windows PowerShell para Azure RMS, vea [Instalación del módulo de PowerShell para AADRM](install-powershell.md).

    2.  En la salida, identifique el valor **LicensingIntranetDistributionPointUrl** .

        Por ejemplo: **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

    3.  En el valor, quite **/_wmcs/licensing** de esta cadena. La cadena restante es la dirección URL del servicio Azure Rights Management. En nuestro ejemplo, la dirección URL del servicio Azure Rights Management sería el valor siguiente:

        **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**
        
        Para comprobar que tiene el valor correcto, ejecute el siguiente comando de PowerShell:
        
            (Get-AadrmConfiguration).LicensingIntranetDistributionPointUrl -match "https:\/\/[0-9A-Za-z\.-]*" | Out-Null; $matches[0]

-   *\<ConnectorFQDN>* es el nombre de equilibrio de carga que ha definido en DNS para el conector. Por ejemplo, **rmsconnector.contoso.com**.

-   Use el prefijo HTTPS para la URL del conector si ha configurado el conector para usar HTTPS para comunicarte con tus servidores locales. Para obtener más información, vea la sección [Configuración del conector RMS para usar HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https) de las instrucciones generales. La dirección URL del servicio Azure Rights Management siempre usa HTTPS.


## <a name="exchange-2016-or-exchange-2013-registry-settings"></a>Configuración del Registro de Exchange 2016 o Exchange 2013

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**Tipo:** Reg_SZ

**Valor:** Default

**Datos:** https://*\<YourTenantURL>*/_wmcs/certification

---

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valor:** Default

**Datos:** https://*\<YourTenantURL>*/_wmcs/Licensing

---

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\CertificationServerRedirection

**Tipo:** Reg_SZ

**Valor:** https://*\<YourTenantURL>*


**Datos:** Una de las siguientes, en función de si usas HTTP o HTTPS desde tu servidor Exchange al conector RMS:

- http://*<\ConnectorFQDN>*

- https://*<\ConnectorFQDN>*

---

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**Tipo:** Reg_SZ

**Valor:** https://*<\YourTenantURL>*


**Datos:** Una de las siguientes, en función de si usas HTTP o HTTPS desde tu servidor Exchange al conector RMS:

- http://*<\ConnectorFQDN>*

- https://*<\ConnectorFQDN>*


## <a name="exchange-2010-registry-settings"></a>Configuración del Registro de Exchange 2010

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**Tipo:** Reg_SZ

**Valor:** Default

**Datos:** https://*<\YourTenantURL>*/_wmcs/certification

---

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valor:** Default

**Datos:** https://*<\YourTenantURL>*/_wmcs/Licensing

---

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\CertificationServerRedirection

**Tipo:** Reg_SZ

**Valor:** https://*<\YourTenantURL>*

**Datos:** Una de las siguientes, en función de si usas HTTP o HTTPS desde tu servidor Exchange al conector RMS:

- http://*<\ConnectorFQDN>*

- https://*<\ConnectorFQDN>*

---

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Tipo:** Reg_SZ

**Valor:** https://*<\YourTenantURL>*

**Datos:** Una de las siguientes, en función de si usas HTTP o HTTPS desde tu servidor Exchange al conector RMS:

- http://*<\ConnectorFQDN>*

- https://*<\ConnectorFQDN>*


## <a name="sharepoint-2016-or-sharepoint-2013-registry-settings"></a>Configuración del Registro de SharePoint 2016 o SharePoint 2013

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\LicensingRedirection

**Tipo:** Reg_SZ

**Valor:** https://*<\YourTenantURL>*/_wmcs/licensing


**Datos:** Una de las siguientes, en función de si usa HTTP o HTTPS desde su servidor SharePoint al conector RMS:

- http://*<\ConnectorFQDN>*/_wmcs/licensing

- https://*<\ConnectorFQDN>*/_wmcs/licensing

---

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification

**Tipo:** Reg_SZ

**Valor:** Default

**Datos:** Una de las siguientes, en función de si usa HTTP o HTTPS desde su servidor SharePoint al conector RMS:

- http://*<\ConnectorFQDN>*/_wmcs/certification

- https://*<\ConnectorFQDN>*/_wmcs/certification

---

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valor:** Default


**Datos:** Una de las siguientes, en función de si usa HTTP o HTTPS desde su servidor SharePoint al conector RMS:

- http://*<\ConnectorFQDN>*/_wmcs/licensing

- https://*<\ConnectorFQDN>*/_wmcs/licensing




## <a name="file-server-and-file-classification-infrastructure-registry-settings"></a>Configuración del Registro del servidor de archivos y de la Infraestructura de la clasificación de archivos

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valor:** Default

**Datos:** http://*<\ConnectorFQDN>*/_wmcs/licensing

---

**Ruta de acceso del Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

**Tipo:** Reg_SZ

**Valor:** Default

**Datos:** http://*<\ConnectorFQDN>*/_wmcs/certification


Vuelta a [Implementación del conector de Azure Rights Management](deploy-rms-connector.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]