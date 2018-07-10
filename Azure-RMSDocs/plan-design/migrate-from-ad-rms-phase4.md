---
title: 'Migración de AD RMS-Azure Information Protection: fase 4'
description: Fase 4 de la migración desde AD RMS a Azure Information Protection, donde se describen los pasos del 8 al 9 de la migración de AD RMS a Azure Information Protection
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/20/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8b039ad5-95a6-4c73-9c22-78c7b0e12cb7
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 254e3ecc1292d2b9db0e291f9c45af343f3ccb9c
ms.sourcegitcommit: 93e83ed71250e408e11fb098551e486282494013
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/22/2018
ms.locfileid: "36324310"
---
# <a name="migration-phase-4---supporting-services-configuration"></a>Fase 4 de la migración: configuración de servicios auxiliares

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Use la información siguiente para la fase 4 de la migración desde AD RMS a Azure Information Protection. En estos procedimientos se describen los pasos 8 y 9 de la [Migración desde AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).



## <a name="step-8-configure-irm-integration-for-exchange-online"></a>Paso 8. Configure la integración de IRM en Exchange Online.

> [!IMPORTANT]
> Ya que no se puede controlar qué destinatarios eligen los usuarios migrados para los correos electrónicos protegidos, debe asegurarse de que todos los usuarios y grupos habilitados para el correo electrónico de su organización tengan una cuenta en Azure AD que se pueda usar para Azure Information Protection. [Más información](prepare.md)

Independientemente de la topología de claves de inquilino de Azure Information Protection que haya elegido, siga estos pasos:

1. Para que Exchange Online pueda descifrar los correos electrónicos que están protegidos por AD RMS, necesita saber que la dirección URL de AD RMS para el clúster se corresponde con la clave que está disponible en el inquilino. Esto se hace con el registro SRV de DNS para el clúster de AD RMS que también se usa para volver a configurar los clientes de Office a fin de usar Azure Information Protection. Si no ha creado el registro SRV de DNS para volver a configurar el cliente en el paso 7, créelo ahora para que se admita en Exchange Online. [Instrucciones](migrate-from-ad-rms-phase3.md#client-reconfiguration-by-using-dns-redirection)
    
    Cuando este registro de DNS está en su lugar, los usuarios con Outlook en los clientes de correo electrónico y en la web podrán ver los correos electrónicos protegidos con AD RMS en esas aplicaciones, y Exchange podrá usar la clave importada desde AD RMS para descifrar, indexar y proteger el contenido que se ha protegido por AD RMS, así como escribir notas.  

2. Ejecute el comando [Get-IRMConfiguration](https://technet.microsoft.com/library/dd776120(v=exchg.160\).aspx) de Exchange Online. Si necesita ayuda para ejecutar este comando, consulte las instrucciones detalladas de [Exchange Online: Configuración de IRM](/..deploy-use/configure-office365.md#exchange-online-irm-configuration).
    
    En la salida, compruebe si **AzureRMSLicensingEnabled** está establecido en **True**:
    
    - Si AzureRMSLicensingEnabled está establecido en **True**, no es necesario configurar nada más en este paso. 
    
    - Si AzureRMSLicensingEnabled está establecido en **False**, ejecute los comandos de [Set up new Office 365 Message Encryption capabilities built on top of Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e) (Configuración de nuevas funcionalidades del cifrado de mensajes de Office 365 basadas en Azure Information Protection). 

## <a name="step-9-configure-irm-integration-for-exchange-server-and-sharepoint-server"></a>Step 9. Configuración de la integración de IRM para Exchange Server y SharePoint Server

Si ha usado la función Information Rights Management (IRM) de Exchange Server o SharePoint Server con AD RMS, deberá implementar el conector de Rights Management (RMS), que actúa como interfaz de comunicaciones (retransmisión) entre los servidores locales y el servicio de protección de Azure Information Protection.

En este paso se describe cómo instalar y configurar el conector, deshabilitar IRM para Exchange y SharePoint y configurar estos servidores para usar el conector. Por último, si ha importado archivos de configuración de datos de AD RMS (.xml) en Azure Information Protection que se habían usado para proteger los mensajes de correo electrónico, tendrá que editar de forma manual el Registro en los equipos de Exchange Server para redirigir todas las direcciones URL del dominio de publicación de confianza al conector RMS.

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
        $list += "<Your Tenant URL>/_wmcs/licensing"
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

Para todos los servidores de Exchange, agregue los siguientes valores del Registro a LicenseServerRedirection, según las versiones de Exchange:

---

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