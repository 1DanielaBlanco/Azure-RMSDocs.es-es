---
title: "Migración de AD RMS-Azure Information Protection: fase 4"
description: "Fase 4 de la migración desde AD RMS a Azure Information Protection, donde se describen los pasos del 8 al 9 de la migración de AD RMS a Azure Information Protection"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/18/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8b039ad5-95a6-4c73-9c22-78c7b0e12cb7
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 4157148c0109317851ed2f128a5ae74603d82af2
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2017
---
# <a name="migration-phase-4---supporting-services-configuration"></a>Fase 4 de la migración: configuración de servicios auxiliares

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Office 365*


Use la información siguiente para la fase 4 de la migración desde AD RMS a Azure Information Protection. En estos procedimientos se describen los pasos 8 y 9 de la [Migración desde AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).



## <a name="step-8-configure-irm-integration-for-exchange-online"></a>Paso 8. Configure la integración de IRM en Exchange Online.

Si ha importado anteriormente el TDP desde AD RMS a Exchange Online, necesita quitarlo para evitar conflictos de plantillas y directivas después de realizar la migración a Azure Information Protection. Para ello, use el cmdlet [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) de Exchange Online.

Si ha elegido una topología de claves de inquilino de Azure Information Protection **administrada por Microsoft**:

1. Siga las instrucciones de la sección [Exchange Online: Configuración de IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration) en el artículo [Office 365: Configuración para clientes y servicios en línea](../deploy-use/configure-office365.md). En esta sección se incluye la ejecución de comandos típicos que establecen una conexión con el servicio de Exchange Online, importan la clave de inquilino desde Azure Information Protection y habilitan la función de IRM para Exchange Online. Después de completar estos pasos, tendrá la función de protección completa de Azure Rights Management con Exchange Online.

2. Además de la configuración estándar para habilitar IRM para Exchange Online, ejecute los siguientes comandos de PowerShell para asegurarse de que los usuarios puedan leer correos electrónicos enviados mediante la protección de AD RMS.

    Sustituya su nombre de dominio de organización por *\<suempresa.dominio>*.

        $irmConfig = Get-IRMConfiguration
        $list = $irmConfig.LicensingLocation
        $list += "https://adrms.<yourcompany.domain>/_wmcs/licensing"
        Set-IRMConfiguration -LicensingLocation $list
        Set-IRMConfiguration -internallicensingenabled $false
        Set-IRMConfiguration -internallicensingenabled $true


Si ha elegido una topología de claves de inquilino de Azure Information Protection **administrada por el cliente (BYOK)**:

-   Habrá reducido las funciones de protección de Rights Management con Exchange Online, como se describe en el artículo [Precio y restricciones de BYOK](byok-price-restrictions.md).


## <a name="step-9-configure-irm-integration-for-exchange-server-and-sharepoint-server"></a>Step 9. Configuración de la integración de IRM para Exchange Server y SharePoint Server

Si ha usado la función Information Rights Management (IRM) de Exchange Server o SharePoint Server con AD RMS, deberá implementar el conector de Rights Management (RMS), que actúa como interfaz de comunicaciones (retransmisión) entre los servidores locales y el servicio de protección de Azure Information Protection.

En estos pasos se describe cómo instalar y configurar el conector, deshabilitar IRM para Exchange y SharePoint y configurar estos servidores para usar el conector. Por último, si ha importado archivos de configuración de datos de AD RMS (.xml) en Azure Information Protection que se habían usado para proteger los mensajes de correo electrónico, tendrá que editar de forma manual el Registro en los equipos de Exchange Server para redirigir todas las direcciones URL del dominio de publicación de confianza al conector RMS.

> [!NOTE]
> Antes de empezar, compruebe las versiones de los servidores locales que son compatibles con el servicio Azure Rights Management desde [On-premises servers that support Azure RMS](../get-started/requirements-servers.md) (Servidores locales compatibles con Azure RMS).

### <a name="install-and-configure-the-rms-connector"></a>Instalar y configurar el conector RMS

Siga las instrucciones del artículo [Implementación del conector de Azure Rights Management](../deploy-use/deploy-rms-connector.md) y realice los pasos del 1 al 4. Aún no empiece el paso 5 de las instrucciones del conector. 

### <a name="disable-irm-on-exchange-servers-and-remove-ad-rms-configuration"></a>Deshabilitar IRM en servidores de Exchange y quitar la configuración de AD RMS

1.  En cada servidor de Exchange, busque la carpeta siguiente y elimine todas las entradas de esa carpeta: **\ProgramData\Microsoft\DRM\Server\S-1-5-18**.

2. Desde uno de los servidores de Exchange, ejecute los siguientes comandos de PowerShell para asegurarse de que los usuarios puedan leer los correos electrónicos que se protegen mediante Azure Rights Management.

    Antes de ejecutar estos comandos, sustituya su propia dirección URL de servicio de Azure Rights Management por *\<la dirección URL del inquilino>*.

        $irmConfig = Get-IRMConfiguration
        $list = $irmConfig.LicensingLocation 
        $list + "<Your Tenant URL>/_wmcs/licensing"
        Set-IRMConfiguration -LicensingLocation $list

3.  Ahora, deshabilite las características de IRM para los mensajes enviados a destinatarios internos:

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

4. Después, use el mismo cmdlet para deshabilitar IRM en Microsoft Office Outlook Web App y en Microsoft Exchange ActiveSync:

    ```
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  Por último, use el mismo cmdlet para borrar los certificados almacenados en la memoria caché:

    ```
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  En cada Exchange Server, restablezca ahora IIS, por ejemplo, mediante la ejecución de un símbolo del sistema como administrador y escriba **iisreset**.

### <a name="disable-irm-on-sharepoint-servers-and-remove-ad-rms-configuration"></a>Deshabilitar IRM en servidores de SharePoint y quitar la configuración de AD RMS

1.  Asegúrese de que no hay ningún documento desprotegido desde bibliotecas protegidas con RMS. Si hay, quedarán inaccesibles al final de este procedimiento.

2.  En el sitio web de Administración central de SharePoint, en la sección **Inicio rápido** , haga clic en **Seguridad**.

3.  En la página **Seguridad** , en la página **Directiva de información** , haga clic en **Configurar Information Rights Management**.

4.  En la página **Information Rights Management** , en la sección **Information Rights Management** , seleccione **No use IRM en este servidor**y luego haga clic en **Aceptar**.

5.  En cada uno de los equipos de SharePoint Server, elimine el contenido de la carpeta \ProgramData\Microsoft\MSIPC\Server\\<*SID de la cuenta que ejecuta SharePoint Server>*.

### <a name="configure-exchange-and-sharepoint-to-use-the-connector"></a>Configuración de Exchange y SharePoint para que usen el conector

1. Vuelva a las instrucciones para implementar el conector RMS: [Paso 5: configuración de servidores para que usen el conector RMS](../deploy-use/configure-servers-rms-connector.md)

    Si solo tiene SharePoint Server, vaya directamente a [Pasos siguientes](#next-steps) para continuar con la migración. 

2. En cada Exchange Server, agregue de forma manual las claves del Registro en la sección siguiente por cada archivo de datos de configuración (.xml) que haya importado para redirigir las direcciones URL de dominios de publicación de confianza al conector RMS. Estas entradas del Registro son específicas para la migración y no se agregan mediante la herramienta de configuración de servidor para el conector RMS de Microsoft.

    Al realizar estas modificaciones del registro, utilice las siguientes instrucciones:

    -   Reemplace *FQDN de conector* por el nombre que haya definido en el DNS del conector. Por ejemplo, **rmsconnector.contoso.com**.

    -   Use el prefijo HTTP o HTTPS para la dirección URL del conector, en función de si ha configurado el conector para usar HTTP o HTTPS para comunicarse con los servidores locales.

#### <a name="registry-edits-for-exchange"></a>Modificaciones del Registro para Exchange

Para todos los servidores de Exchange, quite los valores del Registro que ha agregado para LicenseServerRedirection durante la fase de preparación. Estos valores se han agregado en las rutas de acceso siguientes:

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection


Para Exchange 2013 y Exchange 2016 (modificación del Registro 1):


**Ruta de acceso del Registro:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**Tipo:** Reg_SZ

**Valor:** https://\<Dirección URL de licencias de intranet de AD RMS\>/_wmcs/licensing

**Datos:**

Una de las siguientes, en función de si usas HTTP o HTTPS desde tu servidor Exchange al conector RMS:

- http://\<FQDN de conector\>/_wmcs/licensing

- https://\<FQDN de conector\>/_wmcs/licensing


---

Para Exchange 2013 - Editor del registro 2:

**Ruta de acceso del Registro:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection 

**Tipo:** Reg_SZ

**Valor:** https://\<Dirección URL de licencias de extranet de AD RMS\>/_wmcs/licensing

**Datos:**

Una de las siguientes, en función de si usas HTTP o HTTPS desde tu servidor Exchange al conector RMS:

- http://\<FQDN de conector\>/_wmcs/licensing

- https://\<FQDN de conector\>/_wmcs/licensing

---

Para Exchange 2010 - Editor del registro 1:


**Ruta de acceso del Registro:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Tipo:** Reg_SZ

**Valor:** https://\<Dirección URL de licencias de intranet de AD RMS\>/_wmcs/licensing

**Datos:**

Una de las siguientes, en función de si usas HTTP o HTTPS desde tu servidor Exchange al conector RMS:

- http://\<FQDN de conector\>/_wmcs/licensing

- https://\<Nombre conector\>/_wmcs/licensing


---

Para Exchange 2010 - Editor del registro 2:


**Ruta de acceso del Registro:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Tipo:** Reg_SZ

**Valor:** https://\<Dirección URL de licencias de extranet de AD RMS\>/_wmcs/licensing

**Datos:**

Una de las siguientes, en función de si usas HTTP o HTTPS desde tu servidor Exchange al conector RMS:

- http://\<FQDN de conector\>/_wmcs/licensing

- https://\<FQDN de conector\>/_wmcs/licensing

---


## <a name="next-steps"></a>Pasos siguientes
Para continuar con la migración, vaya a [Fase 5: tareas posteriores a la migración](migrate-from-ad-rms-phase5.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]