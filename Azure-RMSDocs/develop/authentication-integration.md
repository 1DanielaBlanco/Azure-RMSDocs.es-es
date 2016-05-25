---
# required metadata

title: Procedimiento para agregar autenticación a la aplicación | Azure RMS
description: Se describen los conceptos básicos de la autenticación de usuario de la aplicación habilitada para RMS.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 200D9B23-F35D-4165-9AC4-C482A5CE1D28
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Procedimiento para agregar autenticación a la aplicación

En este tema se describen los conceptos básicos de la autenticación de usuario de la aplicación habilitada para RMS.

## ¿Qué es la autenticación del usuario?
La autenticación de usuario es un paso esencial para establecer la comunicación entre la aplicación del dispositivo y la infraestructura de RMS. En este proceso de autenticación se usa el protocolo OAuth 2.0 estándar, donde son necesarios los siguientes datos sobre el usuario actual y su solicitud de autenticación: **authority**, **resource** e **userId**.

**Nota:** el ámbito no se usa actualmente, pero no se descarta, de modo que está reservado para un futuro uso.

 

**Devolución de llamada de autenticación de usuario:** Microsoft Rights Management SDK 4.2 usará su implementación de una devolución de llamada de autenticación cuando no proporcione un token de acceso, cuando el token de acceso deba actualizarse o cuando el token de acceso haya expirado.

Cada una de las API de RMS de la plataforma tiene una devolución de llamada que se debe implementar para permitir la autenticación del usuario.

-   La API de Android usa las interfaces [**AuthenticationRequestCallback**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_authenticationrequestcallback_interface_java) y [**AuthenticationCompletionCallback**](/rights-management/sdk/4.2/api/android/authenticationcompletioncallback#msipcthin2_authenticationcompletioncallback_interface_java).
-   La API de iOS/OS X usa el protocolo [**MSAuthenticationCallback**](/rights-management/sdk/4.2/api/iOS/iOS#msipcthin2_msauthenticationcallback_protocol_objc).
-   La API de WinPhone usa la interfaz [**IAuthenticationCallback**](/rights-management/sdk/4.2/api/winrt/Microsoft.RightsManagement#msipcthin2_iauthenticationcallback).
-   La API de Linux usa la interfaz [IAuthenticationCallback](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1IAuthenticationCallback.html).

## ¿Qué biblioteca hay que usar para la autenticación?

Para implementar la devolución de llamada de autenticación, debe descargar una biblioteca adecuada y configurar el entorno de desarrollo para que la use. Encontrará las bibliotecas de ADAL en GitHub para cada una de las plataformas correspondientes. Los siguientes recursos contienen instrucciones para configurar el entorno y usar la biblioteca.

-   [Biblioteca de autenticación de Azure Active Directory (ADAL) para iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [Biblioteca de autenticación de Azure Active Directory (ADAL) para Mac](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [Biblioteca de autenticación de Azure Active Directory (ADAL) para Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)
-   [Biblioteca de autenticación de Azure Active Directory (ADAL) para dotnet](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)
-   En cuanto al SDK de Linux, la biblioteca de ADAL viene empaquetada con el origen del SDK, disponible en [Github](https://github.com/AzureAD/rms-sdk-for-cpp).

**Nota:** se recomienda usar una de las bibliotecas de autenticación de Active Directory (ADAL) anteriores, aunque use otras bibliotecas de autenticación.

## Entradas de autenticación con una biblioteca de autenticación de Azure Active Directory (ADAL)

Una ADAL necesita varios parámetros para autenticar correctamente a un usuario en Azure RMS (o AD RMS). Estos son los parámetros de OAuth 2.0 estándar que se suelen necesitar de cualquier aplicación de Azure AD, así como de aplicaciones habilitadas para RMS. Encontrará las directrices actuales de uso de ADAL en el archivo README de los repositorios de Github correspondientes mencionados anteriormente.

Estos parámetros e instrucciones son necesarios para los flujos de trabajo de RMS:

-   **Autoridad:**dirección URL del punto de conexión de autenticación, normalmente AAD o ADFS. Este parámetro se suministra a la aplicación a través de la devolución de llamada de autenticación de RMS SDK.
-   **Recurso:** dirección URL o URI de la aplicación de servicio a la que se intenta tener acceso, normalmente Azure RMS o AD RMS. Este parámetro se suministra a la aplicación a través de la devolución de llamada de autenticación de RMS SDK.
-   **Identificador de usuario:** UPN (normalmente, la dirección de correo) del usuario que quiere tener acceso a la aplicación. Este parámetro puede estar vacío si aún no se conoce el usuario. También se usa para almacenar en caché el token de usuario o para pedir un token de la memoria caché. Se suele usar también como "pista" para preguntar al usuario.
-   **Identificador de cliente:** identificador de la aplicación cliente. Debe ser un identificador de aplicación de Azure AD válido. Para más información, vea How to: Get an Azure Application ID (Procedimiento para obtener un identificador de aplicación de Azure).
-   **URI de redirección:** proporciona la biblioteca de autenticación con un destino de URI para el código de autenticación. Tenga en cuenta que en iOS y Android se necesitan formatos específicos, que encontrará detallados en los archivos README de los repositorios de GitHub correspondientes de ADAL.

    Android: `msauth://packagename/Base64UrlencodedSignature`

    iOS: `<app-scheme>://<bundle-id>`

**Nota:** si la aplicación no respeta estas directrices, probablemente los flujos de trabajo de Azure RMS y Azure AD no funcionen y sean incompatibles con Microsoft.com. Es más, se corre el riesgo de infringir el contrato de licencia de Rights Management si se usa un identificador de cliente no válido en una aplicación de producción.

## ¿Qué apariencia debe tener una implementación de devolución de llamada de autenticación?

**Ejemplos de código de autenticación:** este SDK tiene código de ejemplo que muestra el uso de las devoluciones de llamada de autenticación. Para su comodidad, estos ejemplos de código se muestran aquí, así como en cada uno de los siguientes temas vinculados.

**Autenticación de usuario de Android:** para más información, en [Android code examples](android-code.md) (Ejemplos de código Android), vea el **paso 2** del primer escenario sobre cómo consumir un archivo protegido de RMS.


    class MsipcAuthenticationCallback implements AuthenticationRequestCallback
    {
    ...

    @Override
    public void getToken(Map<String, String> authenticationParametersMap,
                         final AuthenticationCompletionCallback authenticationCompletionCallbackToMsipc)
    {
        String authority = authenticationParametersMap.get("oauth2.authority");
        String resource = authenticationParametersMap.get("oauth2.resource");
        String userId = authenticationParametersMap.get("userId");
        mClientId = “12345678-ABCD-ABCD-ABCD-ABCDEFGHIJ”; // get your registered Azure AD application ID here
        mRedirectUri = “urn:ietf:wg:oauth:2.0:oob”;
        final String userHint = (userId == null)? "" : userId;
        AuthenticationContext authenticationContext = App.getInstance().getAuthenticationContext();
        if (authenticationContext == null || !authenticationContext.getAuthority().equalsIgnoreCase(authority))
        {
            try
            {
                authenticationContext = new AuthenticationContext(App.getInstance().getApplicationContext(), authority, …);
                App.getInstance().setAuthenticationContext(authenticationContext);
            }
            catch (NoSuchAlgorithmException e)
            {
                …
                authenticationCompletionCallbackToMsipc.onFailure();
            }
            catch (NoSuchPaddingException e)
            {
                …
                authenticationCompletionCallbackToMsipc.onFailure();
            }
       }
        App.getInstance().getAuthenticationContext().acquireToken(mParentActivity, resource, mClientId, mRedirectURI, userId, mPromptBehavior,
                       "&USERNAME=" + userHint, new AuthenticationCallback<AuthenticationResult>()
                        {
                            @Override
                            public void onError(Exception exc)
                            {
                                …
                                if (exc instanceof AuthenticationCancelError)
                                {
                                     …
                                    authenticationCompletionCallbackToMsipc.onCancel();
                                }
                                else
                                {
                                     …
                                    authenticationCompletionCallbackToMsipc.onFailure();
                                }
                            }

                            @Override
                            public void onSuccess(AuthenticationResult result)
                            {
                                …
                                if (result == null || result.getAccessToken() == null
                                        || result.getAccessToken().isEmpty())
                                {
                                     …
                                }
                                else
                                {
                                    // request is successful
                                    …
                                    authenticationCompletionCallbackToMsipc.onSuccess(result.getAccessToken());
                                }
                            }
                        });
                         }


**Autenticación de usuario de iOS/OS X:** para más información, en [iOS/OS X code examples](ios-os-x-code-examples.md) (Ejemplos de código de iOS/OS X),

vea el **paso 2** del primer escenario sobre cómo consumir un archivo protegido de RMS.


    // AuthenticationCallback holds the necessary information to retrieve an access token.
    @interface MsipcAuthenticationCallback : NSObject<MSAuthenticationCallback>

    @end

    @implementation MsipcAuthenticationCallback

    - (void)accessTokenWithAuthenticationParameters:
         (MSAuthenticationParameters *)authenticationParameters
                                completionBlock:
         (void(^)(NSString *accessToken, NSError *error))completionBlock
    {
    ADAuthenticationError *error;
    ADAuthenticationContext* context = [ADAuthenticationContext authenticationContextWithAuthority:authenticationParameters.authority error:&error];

    NSString *appClientId = @”12345678-ABCD-ABCD-ABCD-ABCDEFGHIJ”;

    // get your registered Azure AD application ID here

    NSURL *redirectURI = [NSURL URLWithString:@”ms-sample://com.microsoft.sampleapp”];

    // get your <app-scheme>://<bundle-id> here
    // Retrieve token using ADAL
    [context acquireTokenWithResource:authenticationParameters.resource
                             clientId:appClientId
                          redirectUri:redirectURI
                               userId:authenticationParameters.userId
                      completionBlock:^(ADAuthenticationResult *result)
                      {
                          if (result.status != AD_SUCCEEDED)
                          {
                              NSLog(@"Auth Failed");
                              completionBlock(nil, result.error);
                          }
                          else
                          {
                              completionBlock(result.accessToken, result.error);
                          }
                      }

        ];
    }



**Autenticación de usuario de Linux/C++:** para más información, vea [Linux code examples](linux-c-code-examples.md) (Ejemplos de código de Linux).



    // Class Header
    class AuthCallback : public IAuthenticationCallback {
    private:

      std::shared_ptr<rmsauth::FileCache> FileCachePtr;
      std::string clientId_;
      std::string redirectUrl_;

      public:

      AuthCallback(const std::string& clientId,
               const std::string& redirectUrl);
      virtual std::string GetToken(shared_ptr<AuthenticationParameters>& ap) override;
    };

    class ConsentCallback : public IConsentCallback {
      public:

      virtual ConsentList Consents(ConsentList& consents) override;
    };

    // Class Implementation
    AuthCallback::AuthCallback(const string& clientId, const string& redirectUrl)
    : clientId_(clientId), redirectUrl_(redirectUrl) {
      FileCachePtr = std::make_shared<FileCache>();
    }

    string AuthCallback::GetToken(shared_ptr<AuthenticationParameters>& ap)
    {
      string redirect =
      ap->Scope().empty() ? redirectUrl_ : ap->Scope();

      try
      {
        if (redirect.empty()) {
        throw rmscore::exceptions::RMSInvalidArgumentException(
              "redirect Url is empty");
      }

      if (clientId_.empty()) {
      throw rmscore::exceptions::RMSInvalidArgumentException("client Id is empty");
      }

      AuthenticationContext authContext(
        ap->Authority(), AuthorityValidationType::False, FileCachePtr);

      auto result = authContext.acquireToken(ap->Resource(),
                                           clientId_, redirect,
                                           PromptBehavior::Auto,
                                           ap->UserId());
      return result->accessToken();
      }

      catch (const rmsauth::Exception& ex)
      {
        // out logs
        throw;
      }
    }



 

 


<!--HONumber=Apr16_HO4-->


