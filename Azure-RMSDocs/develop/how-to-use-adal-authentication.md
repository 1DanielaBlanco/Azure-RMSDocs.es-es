---
title: "Autenticación de ADAL de la aplicación habilitada para RMS | Azure RMS"
description: "Describe el proceso para la autenticación con AAL"
keywords: "autenticación, RMS, ADAL"
author: bruceperlerms
manager: mbaldwin
ms.date: 06/28/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f89f59b7-33d1-4ab3-bb64-1e9bda269935
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 5d2339ece646fc51410186d43facdea28ac8fdfe
ms.openlocfilehash: a2da0e0aedde09cbd834f731d1ddc25f9062336e


---

# Uso de la autenticación ADAL

Autenticación con Azure RMS para una aplicación que use la biblioteca de autenticación de Azure Active Directory (ADAL).

Si actualiza la aplicación para que use la autenticación de ADAL en lugar del Ayudante para el inicio de sesión de Microsoft Online, usted y sus clientes podrán:

- Usar Multi-Factor Authentication.
- Instalar el cliente de RMS 2.1 sin necesidad de tener privilegios administrativos en el equipo.
- Certificar la aplicación para Windows 10

## Dos enfoques para la autenticación

En este tema se describen dos métodos de autenticación con sus ejemplos de código correspondientes.

- **Autenticación interna**: autenticación de OAuth administrada por RMS SDK.

  Use este método si quiere que el cliente de RMS muestre un mensaje de autenticación de ADAL cuando sea necesaria la autenticación. Para obtener más información sobre cómo configurar la aplicación, consulte la sección "Autenticación interna".

  > [!Note] 
  > Si la aplicación usa actualmente AD RMS SDK 2.1 con el Ayudante para el inicio de sesión, se recomienda que use el método de autenticación interna como ruta de acceso de la migración de la aplicación.

- **Autenticación externa**: autenticación de OAuth administrada por la aplicación.

  Use este método si quiere que la aplicación administre su propia autenticación de OAuth. Con este método, el cliente de RMS realizará una devolución de llamada definida por la aplicación cuando sea necesaria la autenticación. Para obtener un ejemplo detallado, consulte "Autenticación externa" al final de este tema.

  > [!Note] 
  > La autenticación externa no permite cambiar los usuarios; el cliente de RMS usa siempre el usuario predeterminado para un inquilino de RMS determinado.

## Autenticación interna

1. Siga los pasos de configuración de Azure indicados en [Configuración de Azure RMS para la autenticación ADAL](adal-auth.md) y después vaya al paso siguiente para la inicialización de aplicaciones.
2. Ahora ya puede configurar la aplicación para que use la autenticación de ADAL interna proporcionada por RMS SDK 2.1.

Para configurar el cliente de RMS, agregue una llamada a [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) justo después de llamar a [IpcInitialize](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize) para configurar el cliente de RMS. Use como ejemplo el fragmento de código siguiente.

      C++
      IpcInitialize();

      IPC_AAD_APPLICATION_ID applicationId = { 0 };
      applicationId.cbSize = sizeof(IPC_AAD_APPLICATION_ID);
      applicationId.wszClientId = L"GUID-provided-by-AAD-for-your-app-(no-brackets)";
      applicationId.wszRedirectUri = L"RedirectionUriWeProvidedAADForOurApp://authorize";
      HRESULT hr = IpcSetGlobalProperty(IPC_EI_APPLICATION_ID, &applicationId);
      if (FAILED(hr)) {
        //Handle the error
      }

## Autenticación externa

Use este código como ejemplo sobre cómo administrar sus propios tokens de autenticación.
C++ extern HRESULT GetADALToken(LPVOID pContext, const IPC_NAME_VALUE_LIST& Parameters, __out wstring wstrToken) throw();

      HRESULT GetLicenseKey(PCIPC_BUFFER pvLicense, __in LPVOID pContextForAdal, __out IPC_KEY_HANDLE &hKey)
      {
          IPC_OAUTH2_CALLBACK pfGetADALToken =
          [](LPVOID pvContext, PIPC_NAME_VALUE_LIST pParameters, IPC_AUTH_TOKEN_HANDLE* phAuthToken) -> HRESULT
          {
              wstring wstrToken;
              HRESULT hr = GetADALToken(pvContext, *pParameters, wstrToken);
              return SUCCEEDED(hr) ? IpcCreateOAuth2Token(wstrToken.c_str(), OUT phAuthToken) : hr;
          };

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
          credentialContext.pcOAuth2 = &callbackCredentialContext;

          IPC_PROMPT_CTX promptContext =
          {
              sizeof(IPC_PROMPT_CTX),
              NULL,
              IPC_PROMPT_FLAG_SILENT | IPC_PROMPT_FLAG_HAS_USER_CONSENT,
              NULL,
              &credentialContext
          };

          hKey = 0L;
          return IpcGetKey(pvLicense, 0, &promptContext, NULL, &hKey);
      }

## Temas relacionados

* [Tipos de datos](/rights-management/sdk/2.1/api/win/data%20types)
* [Propiedades del entorno](/rights-management/sdk/2.1/api/win/environment%20properties#msipc_environment_properties)
* [IpcCreateOAuth2Token](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreateoauth2token)
* [IpcGetKey](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
* [IpcInitialize](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)
* [IPC_CREDENTIAL](/rights-management/sdk/2.1/api/win/IPC_CREDENTIAL)
* [IPC_NAME_VALUE_LIST](/rights-management/sdk/2.1/api/win/IPC_NAME_VALUE_LIST)
* [IPC_OAUTH2_CALLBACK_INFO](/rights-management/sdk/2.1/api/win/ipc_oauth2_callback_info#msipc_ipc_oath2_callback_info)
* [IPC_PROMPT_CTX](/rights-management/sdk/2.1/api/win/IPC_PROMPT_CTX)
* [IPC_AAD_APPLICATION_ID](/rights-management/sdk/2.1/api/win/ipc_aad_application_id#msipc_ipc_aad_application_id)



<!--HONumber=Aug16_HO4-->


