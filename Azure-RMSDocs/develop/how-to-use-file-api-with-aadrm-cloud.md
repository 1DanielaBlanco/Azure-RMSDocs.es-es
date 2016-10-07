---
title: "Cómo habilitar la aplicación de servicio para que funcione con RMS basado en la nube | Azure RMS"
description: "En este tema se describe cómo configurar la aplicación de servicio para que use Azure Rights Management."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: EA1457D1-282F-4CF3-A23C-46793D2C2F32
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: 1e95ce00c96fb0ee0d53ce4865a566a00cf62076


---

# Habilitación de la aplicación de servicio para que funcione con RMS basado en la nube

En este tema se describe cómo configurar la aplicación de servicio para que use Azure Rights Management. Para más información, consulte [Introducción a Azure Rights Management](https://technet.microsoft.com/library/jj585016.aspx).

**Importante**  
Para usar la aplicación de servicio de Rights Management Services SDK 2.1 con Azure RMS, debe crear sus propios inquilinos. Para más información, consulte [Requisitos de Azure RMS: Suscripciones en la nube que son compatibles con Azure RMS](../get-started/requirements-subscriptions.md)

## Requisitos previos

-   RMS SDK 2.1 debe estar instalado y configurado. Para más información, vea [Introducción a RMS SDK 2.1](getting-started-with-ad-rms-2-0.md).
-   [Cree una identidad de servicio a través de ACS](https://msdn.microsoft.com/en-us/library/gg185924.aspx) mediante la opción de clave simétrica (o a través de otros medios) y registre la información de clave de ese proceso.

## Conectarse al servicio de administración de permisos de Azure

-   Llame a [**IpcInitialize**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcinitialize).
-   Establezca [**IpcSetGlobalProperty**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty).

        C++
        int mode = IPC_API_MODE_SERVER;
        IpcSetGlobalProperty(IPC_EI_API_MODE, &(mode));


  **Nota**  Para más información, vea [Establecer el modo de seguridad de API](setting-the-api-security-mode-api-mode.md)

     
-   En los pasos siguientes se realiza la configuración para crear una instancia de una estructura [**IPC\_PROMPT\_CTX**](/information-protection/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx) con el miembro **pcCredential** ([**IPC\_CREDENTIAL**](/information-protection/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential)) rellenado con información de conexión de Azure Rights Management Service.
-   Use la información obtenida en la creación de la identidad de servicio de clave simétrica (consulte los requisitos previos enumerados anteriormente en este mismo tema) para establecer los parámetros **wszServicePrincipal**, **wszBposTenantId** y **cbKey** cuando cree una instancia de una estructura [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/information-protection/sdk/2.1/api/win/ipc_credential_symmetric_key#msipc_ipc_credential_symmetric_key).

**Nota** Debido a una condición existente en nuestro servicio de detección, las credenciales de clave simétrica solo se aceptan si está en Norteamérica. Por lo tanto, si se encuentra en otra región, deberá especificar directamente las URL de inquilino. Esto se hace mediante el parámetro [**IPC\_CONNECTION\_INFO**](/information-protection/sdk/2.1/api/win/ipc_connection_info#msipc_ipc_connection_info) de [**IpcGetTemplateList**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist) o [**IpcGetTemplateIssuerList**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist).

## Generar una clave simétrica y recopilar la información necesaria

### Instrucciones para generar una clave simétrica

-   Instale el [ayudante para el inicio de sesión de Microsoft Online](http://go.microsoft.com/fwlink/p/?LinkID=286152).
-   Instale el [módulo de Azure AD para PowerShell](https://bposast.vo.msecnd.net/MSOPMW/8073.4/amd64/AdministrationConfig-en.msi).

**Nota**  Debe ser administrador de inquilinos para poder usar los cmdlets de PowerShell.

-   Inicie Powershell y ejecute los comandos siguientes para generar una clave         `Import-Module MSOnline`
            `Connect-MsolService` (escriba las credenciales de administrador)         `New-MsolServicePrincipal` (escriba un nombre para mostrar)
-   Una vez generada la clave simétrica, se mostrará la propia clave e información como **AppPrincipalId**.


    Se creó la siguiente clave simétrica porque no se proporcionó ninguna ZYbF/lTtwE28qplQofCpi2syWd11D83+A3DRlb2Jnv8=

    DisplayName : RMSTestApp ServicePrincipalNames : {7d9c1f38-600c-4b4d-8249-22427f016963} ObjectId : 0ee53770-ec86-409e-8939-6d8239880518 AppPrincipalId : 7d9c1f38-600c-4b4d-8249-22427f016963


### Instrucciones para conocer **TenantBposId** y **Urls**

-   Instale el [módulo de Azure RMS para PowerShell](https://technet.microsoft.com/en-us/library/jj585012.aspx).
-   Inicie PowerShell y ejecute los comandos siguientes para obtener la configuración de RMS del inquilino.

    `Import-Module aadrm`

    `Connect-AadrmService` (escriba sus credenciales de administrador)

    `Get-AadrmConfiguration`


-   Cree una instancia de [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/information-protection/sdk/2.1/api/win/ipc_credential_symmetric_key#msipc_ipc_credential_symmetric_key) y configure algunos miembros.

    // Crear una estructura de claves.
    IPC_CREDENTIAL_SYMMETRIC_KEY symKey = {0};

    // Configure cada miembro con la información de la creación del servicio.
    symKey.wszBase64Key = "su clave principal del servicio"; symKey.wszAppPrincipalId = "su identificador principal de la aplicación"; symKey.wszBposTenantId = "su identificador de inquilino";


Para más información, consulte [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/information-protection/sdk/2.1/api/win/ipc_credential_symmetric_key#msipc_ipc_credential_symmetric_key).

-   Cree una instancia de una estructura [**IPC\_CREDENTIAL**](/information-protection/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential) que contenga la instancia de [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/information-protection/sdk/2.1/api/win/ipc_credential_symmetric_key#msipc_ipc_credential_symmetric_key).

**Nota** Los miembros *connectionInfo* se establecen con las direcciones URL de la llamada anterior a `Get-AadrmConfiguration` y se anotan aquí con esos nombres de campo.

    // Create a credential structure.
    IPC_CREDENTIAL cred = {0};

    IPC_CONNECTION_INFO connectionInfo = {0};
    connectionInfo.wszIntranetUrl = LicensingIntranetDistributionPointUrl;
    connectionInfo.wszExtranetUrl = LicensingExtranetDistributionPointUrl;

    // Set each member.
    cred.dwType = IPC_CREDENTIAL_TYPE_SYMMETRIC_KEY;
    cred.pcCertContext = (PCCERT_CONTEXT)&symKey;

    // Create your prompt control.
    IPC_PROMPT_CTX promptCtx = {0};

    // Set each member.
    promptCtx.cbSize = sizeof(IPC_PROMPT_CTX);
    promptCtx.hwndParent = NULL;
    promptCtx.dwflags = IPC_PROMPT_FLAG_SILENT;
    promptCtx.hCancelEvent = NULL;
    promptCtx.pcCredential = &cred;

### Identificar una plantilla y cifrar

-   Seleccione una plantilla para el cifrado.
    Llame a [**IpcGetTemplateList**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist) pasando la misma instancia de [**IPC\_PROMPT\_CTX**](/information-protection/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx).


    PCIPC_TIL pTemplates = NULL; IPC_TEMPLATE_ISSUER templateIssuer = (pTemplateIssuerList->aTi)[0];

    hr = IpcGetTemplateList(&(templateIssuer.connectionInfo),        IPC_GTL_FLAG_FORCE_DOWNLOAD,        0,        &promptCtx,        NULL,        &pTemplates);


-   Con la plantilla que se incluye anteriormente en este tema, llame a [**IpcfEncrcyptFile**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcfencryptfile) pasando la misma instancia de [**IPC\_PROMPT\_CTX**](/information-protection/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx).

Ejemplo de uso de [**IpcfEncrcyptFile**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcfencryptfile):

    LPCWSTR wszContentTemplateId = pTemplates->aTi[0].wszID;
    hr = IpcfEncryptFile(wszInputFilePath,
           wszContentTemplateId,
           IPCF_EF_TEMPLATE_ID,
           IPC_EF_FLAG_KEY_NO_PERSIST,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

Ejemplo de uso de [**IpcfDecryptFile**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile):

    hr = IpcfDecryptFile(wszInputFilePath,
           IPCF_DF_FLAG_DEFAULT,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

Ha completado todos los pasos necesarios para que la aplicación pueda usar Azure Rights Management.

## Temas relacionados

* [Introducción a Azure Rights Management](https://technet.microsoft.com/en-us/library/jj585016.aspx)
* [Introducción a RMS SDK 2.1](getting-started-with-ad-rms-2-0.md)
* [Crear una identidad de servicio a través de ACS](https://msdn.microsoft.com/en-us/library/gg185924.aspx)
* [**IpcSetGlobalProperty**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty)
* [**IpcInitialize**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcinitialize)
* [**IPC\_PROMPT\_CTX**](/information-protection/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx)
* [**IPC\_CREDENTIAL**](/information-protection/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential)
* [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/information-protection/sdk/2.1/api/win/ipc_credential_symmetric_key#msipc_ipc_credential_symmetric_key)
* [**IpcGetTemplateIssuerList**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist)
* [**IpcGetTemplateList**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
* [**IpcfDecryptFile**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile)
* [**IpcfEncrcyptFile**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcfencryptfile)
* [**IpcCreateLicenseFromScratch**](/information-protection/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)
* [**IpcCreateLicenseFromTemplateID**](/information-protection/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromtemplateid)
 

 



<!--HONumber=Sep16_HO5-->


