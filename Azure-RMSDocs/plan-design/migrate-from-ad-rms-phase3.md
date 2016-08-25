---
title: "Migración desde AD RMS a Azure Rights Management - Fase 3 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 08/17/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8b039ad5-95a6-4c73-9c22-78c7b0e12cb7
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 437afd88efebd9719a3db98f8ab0ae07403053f7
ms.openlocfilehash: 6d3cb53fb199bb880a0e61d2b964f297e547a027


---

# Fase de migración 3: Configuración de servicios auxiliares

*Se aplica a: Active Directory Rights Management Services, Azure Rights Management*


Use la siguiente información para la fase 3 de migración desde AD RMS a Azure Rights Management (Azure RMS). Estos procedimientos incluyen los pasos 6 y 7 del tema [Migración desde AD RMS a Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).


## Paso 6. Configure la integración de IRM en Exchange Online.

Si ha importado anteriormente el TDP desde AD RMS a Exchange Online, debe quitarlo para evitar conflictos de plantillas y directivas después de haber migrado a Azure RMS. Para ello, use el cmdlet [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) de Exchange Online.

Si eligió una topología de clave de inquilino de Azure RMS de **administrada por Microsoft**:

-   Consulte la sección [Exchange Online: Configuración de IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration) en el artículo [Office 365: Configuración para clientes y servicios en línea](../deploy-use/configure-office365.md). Esta sección incluye la ejecución de comandos típicos que conectan con el servicio de Exchange Online, importan la clave de inquilino de Azure RMS y habilitan la funcionalidad IRM para Exchange Online. Después de completar estos pasos, tendrá la funcionalidad completa de RMS con Exchange Online.

Si ha elegido una topología de clave de inquilino de Azure RMS **administrada por el cliente (BYOK)**:

-   Habrá reducido la funcionalidad de RMS con Exchange Online, como se describe en el artículo [Precio y restricciones de BYOK](byok-price-restrictions.md).

## Paso 7. Implemente el conector RMS.
Si ha utilizado la funcionalidad Information Rights Management (IRM) de Exchange Server o SharePoint Server con AD RMS, primero debe deshabilitar IRM en estos servidores y quitar la configuración de AD RMS. A continuación, implemente el conector de Rights Management (RMS), que actúa como interfaz de comunicaciones (una retransmisión) entre los servidores locales y Azure RMS.

Por último, para este paso, si ha importado varios archivos de configuración de datos de AD RMS (.xml) en Azure RMS que se usaron para proteger los mensajes de correo electrónico, tendrá que editar de forma manual el Registro en los equipos de Exchange Server para redirigir todas las direcciones URL del dominio de publicación de confianza al conector RMS.

> [!NOTE]
> Antes de empezar, compruebe las versiones de los servidores locales que son compatibles con Azure RMS desde [Servidores locales compatibles con Azure RMS](../get-started/requirements-servers.md).

### Deshabilitar IRM en servidores de Exchange y quitar la configuración de AD RMS

1.  En cada servidor de Exchange, busque la carpeta siguiente y elimine todas las entradas de esa carpeta: \ProgramData\Microsoft\DRM\Server\S-1-5-18

2.  Desde uno de los servidores de Exchange, use el cmdlet [Set_IRMConfiguration](http://technet.microsoft.com/library/dd979792.aspx) de Exchange para deshabilitar primero las características de IRM para los mensajes enviados a destinatarios internos:

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

3.  A continuación, utilice el mismo cmdlet para deshabilitar las características de IRM para los mensajes enviados a destinatarios externos:

    ```
    Set-IRMConfiguration -ExternalLicensingEnabled $false
    ```

4.  A continuación, use el mismo cmdlet para deshabilitar IRM en Microsoft Office Outlook Web App y en Microsoft Exchange ActiveSync:

    ```
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  Por último, use el mismo cmdlet para borrar los certificados almacenados en la memoria caché:

    ```
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  En cada Exchange Server, restablezca ahora IIS, por ejemplo, mediante la ejecución de un símbolo del sistema como administrador y escriba **iisreset**.

### Deshabilitar IRM en servidores de SharePoint y quitar la configuración de AD RMS

1.  Asegúrese de que no hay ningún documento desprotegido desde bibliotecas protegidas con RMS. Si hay, quedarán inaccesibles al final de este procedimiento.

2.  En el sitio web de Administración central de SharePoint, en la sección **Inicio rápido** , haga clic en **Seguridad**.

3.  En la página **Seguridad** , en la página **Directiva de información** , haga clic en **Configurar Information Rights Management**.

4.  En la página **Information Rights Management** , en la sección **Information Rights Management** , seleccione **No use IRM en este servidor**y luego haga clic en **Aceptar**.

5.  En cada uno de los equipos de SharePoint Server, elimine el contenido de la carpeta \ProgramData\Microsoft\MSIPC\Server\*&lt;SID de la cuenta que ejecuta SharePoint Server&gt;*.

#### Instalar y configurar el conector RMS

-   Siga las instrucciones del artículo [Implementación del conector de Azure Rights Management](../deploy-use/deploy-rms-connector.md).

#### En Exchange solo y varios TPD: Editar el registro

-   En cada Exchange Server, agregue de forma manual las siguientes claves del Registro por cada archivo de datos de configuración (.xml) adicional que haya importado para redirigir las direcciones URL de dominios de publicación de confianza al conector RMS. Estas entradas del Registro son específicas para la migración y no se agregan mediante la herramienta de configuración de servidor para el conector RMS de Microsoft.

    Al realizar estas modificaciones del registro, utilice las siguientes instrucciones:

    -   Reemplace *ConnectorFQDN* por el nombre que definió en el DNS para el conector. Por ejemplo, **rmsconnector.contoso.com**.

    -   Use el prefijo HTTP o HTTPS para la dirección URL del conector, en función de si ha configurado el conector para usar HTTP o HTTPS para comunicarse con los servidores locales.

Para Exchange 2013 - 1 Editor del registro 1:


**Ruta de acceso del registro:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**Tipo:**

Reg_SZ

**Valor:**

https://<AD RMS Intranet Licensing URL>/_wmcs/licensing

**Datos:**

Una de las siguientes, en función de si usas HTTP o HTTPS desde tu servidor Exchange al conector RMS:

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorName>/_wmcs/licensing


---

Para Exchange 2013 - Editor del registro 2:

**Ruta de acceso del registro:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection 


**Tipo:**

Reg_SZ

**Valor:**

https://<AD RMS Extranet Licensing URL>/_wmcs/licensing


**Datos:**

Una de las siguientes, en función de si usas HTTP o HTTPS desde tu servidor Exchange al conector RMS:

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorFQDN>/_wmcs/licensing

---

Para Exchange 2010 - Editor del registro 1:



**Ruta de acceso del registro:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Tipo:**

Reg_SZ

**Valor:**

https://<AD RMS Intranet Licensing URL>/_wmcs/licensing

**Datos:**

Una de las siguientes, en función de si usas HTTP o HTTPS desde tu servidor Exchange al conector RMS:

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorName>/_wmcs/licensing


---

Para Exchange 2010 - Editor del registro 2:


**Ruta de acceso del registro:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection
 

**Tipo:**

Reg_SZ

**Valor:**

https://<AD RMS Extranet Licensing URL>/_wmcs/licensing


**Datos:**

Una de las siguientes, en función de si usas HTTP o HTTPS desde tu servidor Exchange al conector RMS:

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorFQDN>/_wmcs/licensing

---

Después de completar estos procedimientos, asegúrese de leer la sección **Pasos siguientes** del artículo [Implementación del conector de Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## Pasos siguientes
Para continuar con la migración, vaya a [Fase 4: Tareas posteriores a la migración](migrate-from-ad-rms-phase4.md).


<!--HONumber=Aug16_HO3-->


