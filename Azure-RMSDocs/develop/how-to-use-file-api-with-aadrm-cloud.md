---
# required metadata

title: Habilitar la aplicación de servicio para que funcione con RMS basado en la nube | Azure RMS
description: En este tema se describe cómo configurar la aplicación de servicio para que use Azure Rights Management.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1f726c6a-68a5-421f-8ed9-9cbb051c205b

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
# Habilitar la aplicación de servicio para que funcione con RMS basado en la nube

En este tema se describe cómo configurar la aplicación de servicio para que use Azure Rights Management. Para más información, vea [Getting started with Azure Rights Management](https://technet.microsoft.com/en-us/library/jj585016.aspx) (Introducción a Azure Rights Management).

**Importante**  
Este es un procedimiento recomendado para una primera prueba de la aplicación de Rights Management Services SDK 2.1 en el entorno de preproducción de RMS y en un servidor RMS. Luego, si quiere que su cliente tenga la posibilidad de usar la aplicación con el servicio de Azure RMS, pruébela con ese entorno.

Para usar la aplicación de servicio de RMS SDK 2.1 con Azure RMS, debe pedir un inquilino de Azure RMS, si aún no lo tiene. Envíe un correo electrónico a <rmcstbeta@microsoft.com> con su solicitud de inquilino.

## Requisitos previos

-   RMS SDK 2.1 debe estar instalado y configurado. Para más información, vea [Introducción a RMS SDK 2.1](getting-started-with-ad-rms-2-0.md).
-   [Cree una identidad de servicio a través de ACS](https://msdn.microsoft.com/en-us/library/gg185924.aspx) mediante la opción de clave simétrica (o a través de otros medios) y registre la información de clave de ese proceso.

## Conectarse al servicio de administración de permisos de Azure

-   Llame a [**IpcInitialize**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize).
-   Establezca [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty).


    int mode = IPC_API_MODE_SERVER;
    IpcSetGlobalProperty(IPC_EI_API_MODE, &(mode));


**Nota**  Para más información, vea [Establecer el modo de seguridad de API](setting-the-api-security-mode-api-mode.md)

     

-   En los pasos siguientes se realiza la configuración para crear una instancia de una estructura [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx) con el miembro **pcCredential** ([**IPC\_CREDENTIAL**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential)) relleno con información de conexión de Azure Rights Management Service.
-   Use la información obtenida en la creación de la identidad de servicio de clave simétrica (vea los requisitos previos mencionados anteriormente en este tema) para establecer los parámetros **wszServicePrincipal**, **wszBposTenantId** y **cbKey** cuando cree una instancia de una estructura [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key).

**Nota**   Debido a una condición existente en nuestro servicio de detección, las credenciales de clave simétrica solo se aceptan si está en Norteamérica. Por lo tanto, si se encuentra en otra región, deberá especificar directamente las URL de inquilino. Esto se hace mediante el parámetro [**IPC\_CONNECTION\_INFO**](/rights-management/sdk/2.1/api/win/ipc_connection_info#msipc_ipc_connection_info) de [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist) o [**IpcGetTemplateIssuerList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist).

## Generar una clave simétrica y recopilar la información necesaria

### Instrucciones para generar una clave simétrica

-   Instale el [ayudante para el inicio de sesión de Microsoft Online](http://go.microsoft.com/fwlink/p/?LinkID=286152).
-   Instale el [módulo de Azure AD para PowerShell](https://bposast.vo.msecnd.net/MSOPMW/8073.4/amd64/AdministrationConfig-en.msi).

**Nota**  Debe ser administrador de inquilinos para poder usar los cmdlets de PowerShell.


-   Inicie PowerShell y ejecute los comandos siguientes para generar una clave.
            `Import-Module MSOnline`
            `Connect-MsolService` (escriba sus credenciales de administrador)
            `New-MsolServicePrincipal` (escriba un nombre para mostrar)
-   Una vez generada la clave simétrica, se mostrará la propia clave e información como **AppPrincipalId**.



    The following symmetric key was created as one was not supplied
    ZYbF/lTtwE28qplQofCpi2syWd11D83+A3DRlb2Jnv8=

    DisplayName : RMSTestApp
    ServicePrincipalNames : {7d9c1f38-600c-4b4d-8249-22427f016963}
    ObjectId : 0ee53770-ec86-409e-8939-6d8239880518
    AppPrincipalId : 7d9c1f38-600c-4b4d-8249-22427f016963



### Instrucciones para conocer **TenantBposId** y **Urls**

-   Instale el [módulo de Azure RMS para PowerShell](https://technet.microsoft.com/en-us/library/jj585012.aspx).
-   Inicie PowerShell y ejecute los comandos siguientes para obtener la configuración de RMS del inquilino.

    `Import-Module aadrm`

    `Connect-AadrmService` (escriba sus credenciales de administrador)

    `Get-AadrmConfiguration`


-   Cree una instancia de [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key) y configure algunos miembros.

    // Crear una estructura de claves.
    IPC_CREDENTIAL_SYMMETRIC_KEY symKey = {0};

    // Configure cada miembro con la información de la creación del servicio.
    symKey.wszBase64Key = "su clave principal del servicio";
    symKey.wszAppPrincipalId = "su identificador principal de la aplicación";
    symKey.wszBposTenantId = "su identificador de inquilino";


Para más información, vea [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key).

-   Cree una instancia de una estructura [**IPC\_CREDENTIAL**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential) que contenga su instancia de [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key).

**Nota**  Los miembros *conectionInfo* se establecen con las direcciones URL de la llamada anterior a `Get-AadrmConfiguration` y se anotan aquí con esos nombres de campo.

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
    Llame a [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist) pasando la misma instancia de [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx).


    PCIPC_TIL pTemplates = NULL;
    IPC_TEMPLATE_ISSUER templateIssuer = (pTemplateIssuerList->aTi)[0];

    hr = IpcGetTemplateList(&(templateIssuer.connectionInfo),
           IPC_GTL_FLAG_FORCE_DOWNLOAD,
           0,
           &promptCtx,
           NULL,
           &pTemplates);


-   Con la plantilla que se incluye anteriormente en este tema, llame a [**IpcfEncrcyptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile), pasando la misma instancia de [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx).

Ejemplo de uso de [**IpcfEncrcyptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile):

    LPCWSTR wszContentTemplateId = pTemplates->aTi[0].wszID;
    hr = IpcfEncryptFile(wszInputFilePath,
           wszContentTemplateId,
           IPCF_EF_TEMPLATE_ID,
           IPC_EF_FLAG_KEY_NO_PERSIST,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

Ejemplo de uso de [**IpcfDecryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile):

    hr = IpcfDecryptFile(wszInputFilePath,
           IPCF_DF_FLAG_DEFAULT,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

Ha completado todos los pasos necesarios para que la aplicación pueda usar Azure Rights Management.

### Temas relacionados

* [Conceptos de desarrollador](ad-rms-concepts-nav.md)
* [Introducción a Azure Rights Management](https://technet.microsoft.com/en-us/library/jj585016.aspx)
* [Introducción a RMS SDK 2.1](getting-started-with-ad-rms-2-0.md)
* [Crear una identidad de servicio a través de ACS](https://msdn.microsoft.com/en-us/library/gg185924.aspx)
* [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty)
* [**IpcInitialize**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)
* [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx)
* [**IPC\_CREDENTIAL**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential)
* [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key)
* [**IpcGetTemplateIssuerList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist)
* [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
* [**IpcfDecryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile)
* [**IpcfEncrcyptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile)
* [**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)
* [**IpcCreateLicenseFromTemplateID**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromtemplateid)
 

 


<!--HONumber=Apr16_HO3-->


