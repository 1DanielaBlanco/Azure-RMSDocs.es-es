---
title: "Usar el Portal de Azure para configurar la autenticación de RMS | Azure RMS"
description: "Describe el proceso para la autenticación con AAL"
keywords: "autenticación, RMS, ADAL"
author: bruceperlerms
manager: mbaldwin
ms.date: 06/14/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 2680b399-febb-4bd6-b844-ac3d1e69aca4
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 5d2339ece646fc51410186d43facdea28ac8fdfe
ms.openlocfilehash: cf247d4c3ffc751ac143f2bed0d69acf87afb941


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



<!--HONumber=Aug16_HO4-->


