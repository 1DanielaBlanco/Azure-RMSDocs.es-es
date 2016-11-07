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
ms.sourcegitcommit: 7df62371ba4a2eea0227c731cf90b3454993f533
ms.openlocfilehash: 28b85313e278455391040797ea2886bd9247abe2


---

# <a name="howto-enable-your-service-application-to-work-with-cloud-based-rms"></a>Habilitación de la aplicación de servicio para que funcione con RMS basado en la nube

En este tema se describe cómo configurar la aplicación de servicio para que use Azure Rights Management. Para más información, consulte [Introducción a Azure Rights Management](https://technet.microsoft.com/library/jj585016.aspx).

**Importante**  
Para usar la aplicación de servicio de Rights Management Services SDK 2.1 con Azure RMS, debe crear sus propios inquilinos. Para más información, consulte [Requisitos de Azure RMS: Suscripciones en la nube que son compatibles con Azure RMS](../get-started/requirements-subscriptions.md)

## <a name="prerequisites"></a>Requisitos previos

-   RMS SDK 2.1 debe estar instalado y configurado. Para más información, vea [Introducción a RMS SDK 2.1](getting-started-with-ad-rms-2-0.md).
-   [Cree una identidad de servicio a través de ACS](https://msdn.microsoft.com/en-us/library/gg185924.aspx) mediante la opción de clave simétrica (o a través de otros medios) y registre la información de clave de ese proceso.

## <a name="connecting-to-the-azure-rights-management-service"></a>Conectarse al servicio de administración de permisos de Azure

-   Llame a [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx).
-   Establezca [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx).

        C++
        int mode = IPC_API_MODE_SERVER;
        IpcSetGlobalProperty(IPC_EI_API_MODE, &(mode));


  **Nota**  Para más información, vea [Establecer el modo de seguridad de API](setting-the-api-security-mode-api-mode.md)

     
-   En los pasos siguientes se efectúa la configuración para crear una instancia de una estructura [IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx) con el miembro *pcCredential* ([IPC\_CREDENTIAL](https://msdn.microsoft.com/library/hh535275.aspx)) rellenado con información de conexión de Azure Rights Management Service.
-   Use la información obtenida en la creación de la identidad de servicio de clave simétrica (consulte los requisitos previos enumerados anteriormente en este mismo tema) para establecer los parámetros *wszServicePrincipal*, *wszBposTenantId* y *cbKey* cuando cree una instancia de una estructura [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx).

**Nota**: Debido a una condición existente en nuestro servicio de detección, las credenciales de clave simétrica solo se aceptan si está en Norteamérica. Por lo tanto, si se encuentra en otra región, deberá especificar directamente las URL de inquilino. Esto se hace mediante el parámetro *pConnectionInfo*, tipo [IPC\_CONNECTION\_INFO](https://msdn.microsoft.com/library/hh535274.aspx), en las funciones [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx) o [IpcGetTemplateIssuerList](https://msdn.microsoft.com/library/hh535266.aspx).

## <a name="generate-a-symmetric-key-and-collect-the-needed-information"></a>Generar una clave simétrica y recopilar la información necesaria

### <a name="instructions-to-generate-a-symmetric-key"></a>Instrucciones para generar una clave simétrica

-   Instale el [ayudante para el inicio de sesión de Microsoft Online](http://go.microsoft.com/fwlink/p/?LinkID=286152).
-   Instale el [módulo de Azure AD para PowerShell](https://bposast.vo.msecnd.net/MSOPMW/8073.4/amd64/AdministrationConfig-en.msi).

**Nota**: Debe ser administrador de inquilinos para poder usar los cmdlet de PowerShell.

- Inicie PowerShell y ejecute los comandos siguientes para generar una clave.

    `Import-Module MSOnline`

    `Connect-MsolService` (escriba sus credenciales de administrador)

    `New-MsolServicePrincipal` (escriba un nombre para mostrar)

- Una vez generada la clave simétrica, mostrará información sobre la clave (la propia clave y *AppPrincipalId*).

      The following symmetric key was created as one was not supplied
      ZYbF/lTtwE28qplQofCpi2syWd11D83+A3DRlb2Jnv8=

      DisplayName : RMSTestApp
      ServicePrincipalNames : {7d9c1f38-600c-4b4d-8249-22427f016963}
      ObjectId : 0ee53770-ec86-409e-8939-6d8239880518
      AppPrincipalId : 7d9c1f38-600c-4b4d-8249-22427f016963


### <a name="instructions-to-find-out-tenantbposid-and-urls"></a>Instrucciones para conocer **TenantBposId** y **Urls**

-   Instale el [módulo de Azure RMS para PowerShell](https://technet.microsoft.com/en-us/library/jj585012.aspx).
-   Inicie PowerShell y ejecute los comandos siguientes para obtener la configuración de RMS del inquilino.

    `Import-Module aadrm`

    `Connect-AadrmService` (escriba sus credenciales de administrador)

    `Get-AadrmConfiguration`


- Cree una instancia de [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx) y configure algunos miembros.

      // Create a key structure.
      IPC_CREDENTIAL_SYMMETRIC_KEY symKey = {0};

      // Set each member with information from service creation.
      symKey.wszBase64Key = "your service principal key";
      symKey.wszAppPrincipalId = "your app principal identifier";
      symKey.wszBposTenantId = "your tenant identifier";


Para obtener más información, consulte [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx).

-   Cree una instancia de una estructura [IPC\_CREDENTIAL](https://msdn.microsoft.com/library/hh535275.aspx) que contenga la instancia de [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx).

**Nota**: Los miembros *connectionInfo* se establecen con las direcciones URL de la llamada anterior a `Get-AadrmConfiguration` y se anotan aquí con esos nombres de campo.

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

### <a name="identify-a-template-and-then-encrypt"></a>Identificar una plantilla y cifrar

-   Seleccione una plantilla para el cifrado.
    Llame a [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx) pasando la misma instancia de [IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx).


    PCIPC_TIL pTemplates = NULL; IPC_TEMPLATE_ISSUER templateIssuer = (pTemplateIssuerList->aTi)[0];

    hr = IpcGetTemplateList(&(templateIssuer.connectionInfo),        IPC_GTL_FLAG_FORCE_DOWNLOAD,        0,        &promptCtx,        NULL,        &pTemplates);


-   Con la plantilla que se incluye anteriormente en este tema, llame a [IpcfEncrcyptFile](https://msdn.microsoft.com/library/dn133059.aspx) pasando la misma instancia de [IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx).

Ejemplo de uso de [IpcfEncrcyptFile](https://msdn.microsoft.com/library/dn133059.aspx):

    LPCWSTR wszContentTemplateId = pTemplates->aTi[0].wszID;
    hr = IpcfEncryptFile(wszInputFilePath,
           wszContentTemplateId,
           IPCF_EF_TEMPLATE_ID,
           IPC_EF_FLAG_KEY_NO_PERSIST,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

Ejemplo de uso de [IpcfDecryptFile](https://msdn.microsoft.com/library/dn133058.aspx):

    hr = IpcfDecryptFile(wszInputFilePath,
           IPCF_DF_FLAG_DEFAULT,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

Ha completado todos los pasos necesarios para que la aplicación pueda usar Azure Rights Management.

## <a name="related-topics"></a>Temas relacionados

* [Introducción a Azure Rights Management](https://technet.microsoft.com/en-us/library/jj585016.aspx)
* [Introducción a RMS SDK 2.1](getting-started-with-ad-rms-2-0.md)
* [Crear una identidad de servicio a través de ACS](https://msdn.microsoft.com/en-us/library/gg185924.aspx)
* [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx)
* [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx)
* [IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx)
* [IPC\_CREDENTIAL](https://msdn.microsoft.com/library/hh535275.aspx)
* [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx)
* [IpcGetTemplateIssuerList](https://msdn.microsoft.com/library/hh535266.aspx)
* [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx)
* [IpcfDecryptFile](https://msdn.microsoft.com/library/dn133058.aspx)
* [IpcfEncrcyptFile](https://msdn.microsoft.com/library/dn133059.aspx)
* [IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx)
* [IpcCreateLicenseFromTemplateID](https://msdn.microsoft.com/library/hh535257.aspx)
 

 



<!--HONumber=Nov16_HO1-->


