---
title: "Código de ejemplo de iOS/OS X | Azure RMS"
description: "Este tema le presentará los elementos de código importantes para la versión de iOS/OS X de RMS SDK."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 7E12EBF2-5A19-4A8D-AA99-531B09DA256A
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: cd0d599ccd1e470e5e94904d04d58c32511704c7
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2017
---
# <a name="iosos-x-code-examples"></a>Código de ejemplo de iOS/OS X

Este tema le presentará los elementos de código importantes para la versión de iOS/OS X de RMS SDK.

**Nota**: en el código de ejemplo y las descripciones siguientes, utilizaremos el término MSIPC (protección de la información de Microsoft y Control de cliente) para hacer referencia al proceso del cliente.



## <a name="using-the-microsoft-rights-management-sdk-42---key-scenarios"></a>Uso de Microsoft Rights Management SDK 4.2: escenarios clave


A continuación se muestran ejemplos de código **Objective C** desde una aplicación de ejemplo más grande que representa los escenarios de desarrollo importantes para la orientación de este SDK. Estos muestran; uso del formato de archivo protegido de Microsoft que se reconoce como archivo protegido, el uso de formatos de archivo protegido personalizados y el uso de controles de interfaz de usuario personalizados.

### <a name="scenario-consume-an-rms-protected-file"></a>Escenario: consumo de un archivo protegido RMS


- **Paso 1**: Creación de un objeto [MSProtectedData](https://msdn.microsoft.com/library/dn758348.aspx).

 **Descripción**: Cree una instancia del objeto [MSProtectedData](https://msdn.microsoft.com/library/dn758348.aspx) mediante la creación de un método que implementa la autenticación de servicios con [MSAuthenticationCallback](https://msdn.microsoft.com/library/dn758312.aspx) para obtener un token pasando una instancia de **MSAuthenticationCallback**, como el parámetro *authenticationCallback*, a la API de MSIPC. Consulte la llamada a [MSProtectedData protectedDataWithProtectedFile](https://msdn.microsoft.com/library/dn758351.aspx) en la siguiente sección de código de ejemplo.

        + (void)consumePtxtFile:(NSString *)path authenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            // userId can be provided as a hint for authentication
            [MSProtectedData protectedDataWithProtectedFile:path
                                                 userId:nil
                                 authenticationCallback:authenticationCallback
                                                options:Default
                                        completionBlock:^(MSProtectedData *data, NSError *error)
            {
                //Read the content from the ProtectedData, this will decrypt the data
                NSData *content = [data retrieveData];
            }];
        }

- **Paso 2**: Configuración de la autenticación mediante la biblioteca de autenticación de Active Directory (ADAL).

  **Descripción**: En este paso verá la ADAL usada para implementar un [MSAuthenticationCallback](https://msdn.microsoft.com/library/dn758312.aspx) con los parámetros de autenticación de ejemplo. Para más información sobre el uso de ADAL, consulte la biblioteca de autenticación de Azure AD (AAL).

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
          ADAuthenticationContext* context = [
              ADAuthenticationContext authenticationContextWithAuthority:authenticationParameters.authority
                                                                error:&error
          ];
          NSString *appClientId = @”com.microsoft.sampleapp”;
          NSURL *redirectURI = [NSURL URLWithString:@"local://authorize"];
          // Retrieve token using ADAL
          [context acquireTokenWithResource:authenticationParameters.resource
                                 clientId:appClientId
                              redirectUri:redirectURI
                                   userId:authenticationParameters.userId
                          completionBlock:^(ADAuthenticationResult *result) {
                              if (result.status != AD_SUCCEEDED)
                              {
                                  NSLog(@"Auth Failed");
                                  completionBlock(nil, result.error);
                              }
                              else
                              {
                                  completionBlock(result.accessToken, result.error);
                              }
                          }];
       }

-   **Paso 3**: Comprobación de si existe el derecho de edición para este usuario con este contenido a través del método [MSUserPolicy accessCheck](https://msdn.microsoft.com/library/dn790789.aspx) de un objeto [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx).

        - (void)accessCheckWithProtectedData:(MSProtectedData *)protectedData
        {
            //check if user has edit rights and apply enforcements
            if (!protectedData.userPolicy.accessCheck(EditableDocumentRights.Edit))
            {
                // enforce on the UI
                textEditor.focusableInTouchMode = NO;
                textEditor.focusable = NO;
                textEditor.enabled = NO;
            }
        }

### <a name="scenario-create-a-new-protected-file-using-a-template"></a>Escenario: Creación de un nuevo archivo protegido mediante una plantilla

Este escenario comienza con la obtención de una lista de plantillas, [MSTemplateDescriptor](https://msdn.microsoft.com/library/dn790785.aspx), la selección de la primera de ellas para crear una directiva y, después, la creación y escritura en el nuevo archivo protegido.

-   **Paso 1**: Obtención de una lista de las plantillas

        + (void)templateListUsageWithAuthenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            [MSTemplateDescriptor templateListWithUserId:@"user@domain.com"
                            authenticationCallback:authenticationCallback
                                   completionBlock:^(NSArray/*MSTemplateDescriptor*/ *templates, NSError *error)
                                   {
                                     // use templates array of MSTemplateDescriptor (Note: will be nil on error)
                                   }];
        }

-   **Paso 2**: Creación de [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx) mediante la primera plantilla de la lista.

        + (void)userPolicyCreationFromTemplateWithAuthenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            [MSUserPolicy userPolicyWithTemplateDescriptor:[templates objectAtIndex:0]
                                            userId:@"user@domain.com"
                                     signedAppData:nil
                            authenticationCallback:authenticationCallback
                                           options:None
                                   completionBlock:^(MSUserPolicy *userPolicy, NSError *error)
            {
            // use userPolicy (Note: will be nil on error)
            }];
        }

-   **Paso 3**: Creación de [MSMutableProtectedData](https://msdn.microsoft.com/library/dn758325.aspx) y escritura de contenido en ellos.

        + (void)createPtxtWithUserPolicy:(MSUserPolicy *)userPolicy contentToProtect:(NSData *)contentToProtect
        {
            // create an MSMutableProtectedData to write content
            [contentToProtect protectedDataInFile:filePath
                        originalFileExtension:kDefaultTextFileExtension
                               withUserPolicy:userPolicy
                              completionBlock:^(MSMutableProtectedData *data, NSError *error)
            {
             // use data (Note: will be nil on error)
            }];
        }

### <a name="scenario-open-a-custom-protected-file"></a>Escenario: Apertura de un archivo protegido personalizado


-   **Paso 1**: Creación de [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx) a partir de una *serializedContentPolicy*.

        + (void)userPolicyWith:(NSData *)protectedData
        authenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            // Read header information from protectedData and extract the  PL
            /*-------------------------------------------
            | PL length | PL | ContetSizeLength |
            -------------------------------------------*/
            NSUInteger serializedPolicySize;
            NSMutableData *serializedPolicy;
            [protectedData getBytes:&serializedPolicySize length:sizeof(serializedPolicySize)];
            [protectedData getBytes:[serializedPolicy mutableBytes] length:serializedPolicySize];

            // Get the user policy , this is an async method as it hits the REST service
            // for content key and usage restrictions
            // userId provided as a hint for authentication
            [MSUserPolicy userPolicyWithSerializedPolicy:serializedPolicy
                                              userId:@"user@domain.com"
                              authenticationCallback:authenticationCallback
                                             options:Default
                                     completionBlock:^(MSUserPolicy *userPolicy,
                                                       NSError *error)
            {

            }];
         }

-   **Paso 2**: Creación de [MSCustomProtectedData](https://msdn.microsoft.com/library/dn758321.aspx) mediante [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx) del **paso 1** y lectura a partir de él.

        + (void)customProtectedDataWith:(NSData *)protectedData
        {
            // Read header information from protectedData and extract the  protectedContentSize
            /*-------------------------------------------
            | PL length | PL | ContetSizeLength |
            -------------------------------------------*/
            NSUInteger protectedContentSize;
            [protectedData getBytes:&protectedContentSize
                         length:sizeof(protectedContentSize)];

            // Create the MSCustomProtector used for decrypting the content
            // The content start position is the header length
            [MSCustomProtectedData customProtectedDataWithPolicy:userPolicy
                                               protectedData:protectedData
                                        contentStartPosition:sizeof(NSUInteger) + serializedPolicySize
                                                 contentSize:protectedContentSize
                                             completionBlock:^(MSCustomProtectedData *customProtector,
                                                               NSError *error)
            {
             //Read the content from the custom protector, this will decrypt the data
             NSData *content = [customProtector retrieveData];
             NSLog(@"%@", content);
            }];
         }

### <a name="scenario-create-a-custom-protected-file-using-a-custom-ad-hoc-policy"></a>Escenario: Creación de un archivo protegido personalizado mediante una directiva personalizada (ad hoc)


-   **Paso 1**: con una dirección de correo electrónico proporcionada por el usuario, creación de un descriptor de la directiva

    **Descripción**: En la práctica, los siguientes objetos se crearían con entradas de usuario desde la interfaz de dispositivo: [MSUserRights](https://msdn.microsoft.com/en-us/library/dn790811.aspx) y [MSPolicyDescriptor](https://msdn.microsoft.com/library/dn758339.aspx).

        + (void)policyDescriptor
        {
            MSUserRights *userRights = [[MSUserRights alloc] initWithUsers:[NSArray arrayWithObjects: @"user1@domain.com", @"user2@domain.com", nil] rights:[MSEmailRights all]];

            MSPolicyDescriptor *policyDescriptor = [[MSPolicyDescriptor alloc] initWithUserRights:[NSArray arrayWithObjects:userRights, nil]];
            policyDescriptor.contentValidUntil = [[NSDate alloc] initWithTimeIntervalSinceNow:NSTimeIntervalSince1970 + 3600.0];
            policyDescriptor.offlineCacheLifetimeInDays = 10;
        }

-   **Paso 2**: Creación de [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx) personalizado del descriptor de la directiva, *selectedDescriptor*.

        + (void)userPolicyWithPolicyDescriptor:(MSPolicyDescriptor *)policyDescriptor
        {
            [MSUserPolicy userPolicyWithPolicyDescriptor:policyDescriptor
                                          userId:@"user@domain.com"
                          authenticationCallback:authenticationCallback
                                         options:None
                                 completionBlock:^(MSUserPolicy *userPolicy, NSError *error)
            {
              // use userPolicy (Note: will be nil on error)
            }];
        }

-   **Paso 3**: Creación y escritura de contenido en [MSMutableCustomProtectedData](https://msdn.microsoft.com/library/dn758321.aspx) y cierre.

        + (void)mutableCustomProtectedData:(NSMutableData *)backingData policy:(MSUserPolicy *)policy contentToProtect:(NSString *)contentToProtect
        {
            //Get the serializedPolicy from a given policy
            NSData *serializedPolicy = [policy serializedPolicy];

            // Write header information to backing data including the PL
            // ------------------------------------
            // | PL length | PL | ContetSizeLength |
            // -------------------------------------
            NSUInteger serializedPolicyLength = [serializedPolicy length];
            [backingData appendData:[NSData dataWithBytes:&serializedPolicyLength length:sizeof(serializedPolicyLength)]];
            [backingData appendData:serializedPolicy];
            NSUInteger protectedContentLength = [MSCustomProtectedData getEncryptedContentLengthWithPolicy:policy contentLength:unprotectedData.length];
            [backingData appendData:[NSData dataWithBytes:&protectedContentLength length:sizeof(protectedContentLength)]];

            NSUInteger headerLength = sizeof(serializedPolicyLength) + serializedPolicyLength + sizeof(protectedContentLength);

            // Create the MSMutableCustomProtector used for encrypting content
            // The content start position is the current length of the backing data
            // The encryptedContentSize content size is 0 since there is no content yet
            [MSMutableCustomProtectedData customProtectorWithUserPolicy:policy
                                                        backingData:backingData
                                             protectedContentOffset:headerLength
                                                    completionBlock:^(MSMutableCustomProtectedData *customProtector,
                                                                      NSError *error)
            {
                //Append data to the custom protector, this will encrypt the data and write it to the backing data
                [customProtector appendData:[contentToProtect dataUsingEncoding:NSUTF8StringEncoding] error:&error];

                //close the custom protector so it will flush and finalise encryption
                [customProtector close:&error];

            }];
          }

[!INCLUDE[Commenting house rules](../includes/houserules.md)]