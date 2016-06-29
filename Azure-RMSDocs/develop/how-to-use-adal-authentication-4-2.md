---
# required metadata

title: Usar el Portal de Azure para configurar la autenticación de RMS | Azure RMS
description: Describe el proceso para la autenticación con AAL
keywords: authentication, RMS, ADAL
author: bruceperlerms
manager: mbaldwin
ms.date: 06/14/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 2680b399-febb-4bd6-b844-ac3d1e69aca4

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Usar el Portal de Azure para configurar la autenticación de RMS

Autenticación con Azure RMS para una aplicación que use Azure Active Directory Authentication Library (ADAL).

Usar este método requiere que la aplicación administre su propia autenticación de OAuth. Con este método, el cliente de RMS realizará una devolución de llamada definida por la aplicación cuando sea necesaria la autenticación.

## Configuración mediante el Portal de Azure
Para comenzar, siga esta guía para la configuración a través del Portal de Azure, [Configure Azure RMS for ADAL authentication (Configuración de Azure RMS para la autenticación ADAL)](adal-auth.md). Asegúrese de copiar y guardar el *Identificador de cliente* y el *URI de redirección* de este proceso para usarlos posteriormente.

## Ejemplo de código
Aquí se muestra un recorte de código del ejemplo más grande del código de cliente móvil para habilitar Azure ADAL. Para obtener más información, vea el ejemplo completo en [MSIPCSampleApp](https://github.com/AzureAD/rms-sdk-ui-for-android/tree/master/samples/MsipcSampleApp).

       /**
       * Instantiates a new rms authentication callback.
       *
       * @param parentActivity the parent activity
       * @throws NoSuchAlgorithmException the no such algorithm exception
       * @throws InvalidKeySpecException the invalid key spec exception
       * @throws UnsupportedEncodingException the unsupported encoding exception
       */

       public MsipcAuthenticationCallback(Activity parentActivity) throws NoSuchAlgorithmException, InvalidKeySpecException, UnsupportedEncodingException
       {
         mParentActivity = parentActivity;
         setADALKeyStore();

         /**
         * Note: Following values of are client_id and redirect_uri are for demo purpose only.
         * Your values will come from the preceeding Azure Portal process.
         */
         mClientId = "com.microsoft.rightsmanagement.sampleapp";
         mRedirectURI = mClientId + "://authorize";
       }


## Temas relacionados

- [MSIPCSampleApp](https://github.com/AzureAD/rms-sdk-ui-for-android/tree/master/samples/MsipcSampleApp)
- [Configuración de Azure RMS para la autenticación ADAL](adal-auth.md)


<!--HONumber=Jun16_HO2-->


