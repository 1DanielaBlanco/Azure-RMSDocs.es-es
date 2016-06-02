---
# required metadata

title: Autenticación de ADAL de la aplicación habilitada para RMS | Azure RMS
description: Describe el proceso para la autenticación con AAL
keywords: authentication, RMS, ADAL
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f89f59b7-33d1-4ab3-bb64-1e9bda269935

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Autenticación de ADAL de la aplicación habilitada para RMS

La autenticación con Azure RMS de la aplicación mediante Azure ADAL ahora forma parte del cliente de RMS 2.1.

Si actualiza la aplicación para que use la autenticación de ADAL en lugar del Ayudante para el inicio de sesión de Microsoft Online, usted y sus clientes podrán:

- Usar Multi-Factor Authentication.
- Instalar el cliente de RMS 2.1 sin necesidad de tener privilegios administrativos en el equipo.
- Certificar la aplicación para Windows 10

## Dos enfoques para la autenticación

En este tema se describen dos métodos de autenticación con sus ejemplos de código correspondientes.

- **Autenticación interna**: autenticación de OAuth administrada por RMS SDK. Use este método si quiere que el cliente de RMS muestre un mensaje de autenticación de ADAL cuando sea necesaria la autenticación. Para obtener más información sobre cómo configurar la aplicación, consulte la sección "Autenticación interna".

> [!NOTE] Si la aplicación usa actualmente AD RMS SDK 2.1 con el Ayudante para el inicio de sesión, se recomienda que use el método de autenticación interna como ruta de acceso de la migración de la aplicación.

- **Autenticación externa**: autenticación de OAuth administrada por la aplicación. Use este método si quiere que la aplicación administre su propia autenticación de OAuth. Con este método, el cliente de RMS realizará una devolución de llamada definida por la aplicación cuando sea necesaria la autenticación. Para obtener un ejemplo detallado, consulte "Autenticación externa" al final de este tema.

> [!NOTE] La autenticación externa no permite cambiar los usuarios; el cliente de RMS usa siempre el usuario predeterminado para un inquilino de RMS determinado.

### Autenticación interna

Necesitará lo siguiente:

- Una [suscripción de Microsoft Azure](https://azure.microsoft.com/en-us/) (una evaluación gratuita es suficiente).
- Una suscripción de Microsoft Azure Rights Management (una cuenta gratuita de [RMS para usuarios](https://technet.microsoft.com/en-us/library/dn592127.aspx) es suficiente).

> [!NOTE] Pregúntele al administrador de TI si dispone de una suscripción a Microsoft Azure Rights Management y solicítele que realice los pasos siguientes. Si la organización no tiene una suscripción, pídale al administrador de TI que cree una. Además, el administrador de TI debe suscribirse con una cuenta profesional o educativa, en lugar de con una cuenta de Microsoft (es decir, Hotmail).

Después de suscribirse a Microsoft Azure:

- Inicie sesión en el [Portal de administración de Azure](https://manage.windowsazure.com) para la organización mediante una cuenta con privilegios administrativos.

![Inicio de sesión de Azure](../media/AzurePortalLogin.png)

- Desplácese hacia abajo hasta la aplicación de **Active Directory** en el lado izquierdo del portal.

![Seleccione Active Directory](../media/AzureADPick.png)

- Si todavía no ha creado un directorio, elija el botón **Nuevo** en la esquina inferior izquierda del portal.

![Seleccione NUEVO](../media/AzureNewBtn.png)

- Seleccione la pestaña **Rights Management** y asegúrese de que el **Estado de Rights Management** sea **Activo**, **Desconocido** o **No autorizado**. Si el estado es **Inactivo**, elija el botón **Activar** situado en la parte inferior central del portal y confirme la selección.

![Elija ACTIVAR](../media/RMTab.png)

- Ahora cree una *Aplicación nativa* en su directorio. Para ello, seleccione su directorio y elija Aplicaciones.

![Seleccione APLICACIONES](../media/CreateNativeApp.png)

- Después, elija el botón **AGREGAR** situado en la parte inferior central del portal.

![Seleccione AGREGAR](../media/AddAppBtn.png)

- En el símbolo del sistema, elija **Agregar una aplicación que mi organización está desarrollando**.

![Seleccione Agregar una aplicación que mi organización está desarrollando](../media/AddAnAppPick.png)

- Asígnele un nombre a la aplicación. Para ello, seleccione **APLICACIÓN DE CLIENTE NATIVO** y elija el botón **Siguiente**.

![Asígnele un nombre a la aplicación](../media/TellUsInput.png)

- Agregue un identificador URI de redireccionamiento y elija Siguiente. El identificador URI de redireccionamiento debe ser un identificador URI válido y único para su directorio. Por ejemplo, podría usar algo parecido a `com.mycompany.myapplication://authorize`.

![Agregue un identificador URI de redireccionamiento](../media/RedirectURI.png)

- Seleccione la aplicación en el directorio y elija **CONFIGURAR**.

![Elija CONFIGURAR](../media/ConfigYourApp.png)

>[!NOTE] Copie el **ID. DE CLIENTE** y el **IDENTIFICADOR URI DE REDIRECCIONAMIENTO** y consérvelos para usarlos cuando configure el cliente de RMS.

- Vaya a la parte inferior de los ajustes de configuración de la aplicación y elija el botón **Agregar aplicación**, situado bajo **permisos para otras aplicaciones**.

![Seleccione Agregar aplicación](../media/PermissionsToOtherBtn.png)

- Ahora, agregue el GUID `00000012-0000-0000-c000-000000000000` al cuadro de edición **EMPEZANDO POR** y elija el botón de comprobación.

![Agregue el GUID](../media/AddGUID.png)

- Elija el botón de signo más (+) situado junto a **Microsoft Rights Management**.

![Seleccione el botón +](../media/ChoosePlusBtn.png)

- Ahora, seleccione la marca de verificación que se encuentra en la esquina inferior izquierda del cuadro de diálogo.

![Seleccione la marca de verificación](../media/ChooseCheck.png)

- Ahora ya puede agregar una dependencia a la aplicación para Azure RMS. Para agregar la dependencia, seleccione la nueva entrada **Microsoft Rights Management Services** situada bajo **permisos para otras aplicaciones** y elija la casilla **Create and access protected content for users** (Creación y acceso a contenido protegido para los usuarios) en el cuadro desplegable **Permisos delegados:**.

![Configuración de permisos](../media/AddDependency.png)

- Guarde la aplicación para conservar los cambios. Para ello, elija el icono **GUARDAR** ubicado en la parte inferior central del portal.

![Seleccione GUARDAR](../media/SaveApplication.png)

- Ahora ya puede configurar la aplicación para que use la autenticación de ADAL interna proporcionada por RMS SDK 2.1. Para configurar el cliente de RMS, agregue una llamada a [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/IpcSetGlobalProperty) justo después de llamar a [IpcInitialize](/rights-management/sdk/2.1/api/win/IpcInitialize) para configurar el cliente de RMS. Use como ejemplo el fragmento de código siguiente.


    IpcInitialize();

    IPC_AAD_APPLICATION_ID applicationId = { 0 };   applicationId.cbSize = sizeof(IPC_AAD_APPLICATION_ID);   applicationId.wszClientId = L"GUID-provided-by-AAD-for-your-app-(no-brackets)";   applicationId.wszRedirectUri = L"RedirectionUriWeProvidedAADForOurApp://authorize";

    HRESULT hr = IpcSetGlobalProperty(IPC_EI_APPLICATION_ID, &amp;applicationId);

    if (FAILED(hr)) {    //Handle the error   }

### Autenticación externa

- Use este código como ejemplo sobre cómo administrar sus propios tokens de autenticación.


    extern HRESULT GetADALToken(LPVOID pContext, const IPC_NAME_VALUE_LIST&amp; Parameters, __out wstring wstrToken) throw();

    HRESULT GetLicenseKey(PCIPC_BUFFER pvLicense, __in LPVOID pContextForAdal, __out IPC_KEY_HANDLE &amp;hKey)   {     IPC_OAUTH2_CALLBACK pfGetADALToken =         [](LPVOID pvContext, PIPC_NAME_VALUE_LIST pParameters, IPC_AUTH_TOKEN_HANDLE* phAuthToken) -&gt; HRESULT     {         wstring wstrToken;         HRESULT hr = GetADALToken(pvContext, *pParameters, wstrToken);         return SUCCEEDED(hr) ? IpcCreateOAuth2Token(wstrToken.c_str(), OUT phAuthToken) : hr;     };

      IPC_OAUTH2_CALLBACK_INFO callbackCredentialContext =
      {
          sizeof(IPC_OAUTH2_CALLBACK_INFO),
          pfGetADALToken,
          pContextForAdal
      };

      IPC_CREDENTIAL credentialContext =
      {
          IPC_CREDENTIAL_TYPE_OAUTH2,
          NULL
      };
      credentialContext.pcOAuth2 = &amp;callbackCredentialContext;

      IPC_PROMPT_CTX promptContext =
      {
        sizeof(IPC_PROMPT_CTX),
        NULL,
        IPC_PROMPT_FLAG_SILENT | IPC_PROMPT_FLAG_HAS_USER_CONSENT,
        NULL,
        &amp;credentialContext
      };

      hKey = 0L;
      return IpcGetKey(pvLicense, 0, &amp;promptContext, NULL, &amp;hKey);
  }

### Temas relacionados
- [Tipos de datos](/rights-management/sdk/2.1/api/win/Data%20types)
- [Propiedades del entorno](/rights-management/sdk/2.1/api/win/Environment%20properties)
- [IpcCreateOAuth2Token](/rights-management/sdk/2.1/api/win/IpcCreateOAuth2Token)
- [IpcGetKey](/rights-management/sdk/2.1/api/win/IpcGetKey)
- [IpcInitialize](/rights-management/sdk/2.1/api/win/IpcInitialize)
- [IPC_CREDENTIAL](/rights-management/sdk/2.1/api/win/IPC\_CREDENTIAL)
- [IPC_NAME_VALUE_LIST](/rights-management/sdk/2.1/api/win/IPC\_NAME\_VALUE\_LIST)
- [IPC_OAUTH2_CALLBACK_INFO](/rights-management/sdk/2.1/api/win/IPC\_OAUTH2\_CALLBACK\_INFO)
- [IPC_PROMPT_CTX](/rights-management/sdk/2.1/api/win/IPC\_PROMPT\_CTX)
- [IPC_AAD_APPLICATION_ID](/rights-management/sdk/2.1/api/win/IPC\_AAD\_APPLICATION\_ID)


<!--HONumber=May16_HO2-->


