---
title: "Ejemplos de código de Android | Azure RMS"
description: "Este tema le presentará los elementos de código importantes para la versión de Android de RMS SDK."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 58CC2E50-1E4D-4621-A947-25312C3FF519
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 847d19feaea442da66296565f0ffb5b0663ad170


---

# <a name="android-code-examples"></a>Código de ejemplo de Android

Este tema le presentará los elementos de código importantes para la versión de Android de RMS SDK.

**Nota**: en el código de ejemplo y las descripciones siguientes, utilizaremos el término MSIPC (protección de la información de Microsoft y Control de cliente) para hacer referencia al proceso del cliente.


## <a name="using-the-microsoft-rights-management-sdk-42---key-scenarios"></a>Uso de Microsoft Rights Management SDK 4.2: escenarios clave

A continuación se muestran ejemplos de código desde una aplicación de ejemplo más grande que representa los escenarios de desarrollo importantes para la orientación de este SDK. Estos muestran; uso del formato de archivo protegido de Microsoft que se reconoce como archivo protegido, el uso de formatos de archivo protegido personalizados y el uso de controles de interfaz de usuario personalizados.



La aplicación de ejemplo, *MSIPCSampleApp*, está disponible para su uso con este SDK para el sistema operativo Android. Consulte [rms ui sdk para android](https://github.com/AzureAD/rms-sdk-ui-for-android) en GitHub para obtener acceso a esta aplicación de ejemplo.

### <a name="scenario-consume-an-rms-protected-file"></a>Escenario: consumo de un archivo protegido RMS

-   **Paso 1**: Creación de [ProtectedFileInputStream](https://msdn.microsoft.com/library/dn790851.aspx)

    **Origen**: *MsipcAuthenticationCallback.java*

    **Descripción**: Cree instancias de un objeto [ProtectedFileInputStream](https://msdn.microsoft.com/library/dn790851.aspx) mediante un método de creación que implementa la autenticación de servicios con [AuthenticationRequestCallback](https://msdn.microsoft.com/library/dn758250.aspx) para obtener un token pasando una instancia de **AuthenticationRequestCallback**, como el parámetro *mRmsAuthCallback*, a la API de MSIPC. Consulte la llamada a [ProtectedFileInputStream.create](https://msdn.microsoft.com/library/dn790851.aspx) cerca del final de la siguiente sección de código de ejemplo.

        public void startContentConsumptionFromPtxtFileFormat(InputStream inputStream)
        {
            CreationCallback<ProtectedFileInputStream> protectedFileInputStreamCreationCallback =
              new CreationCallback<ProtectedFileInputStream>()
            {
                @Override
                public Context getContext()
                {
                   …
               }

                @Override
                public void onCancel()
                {
                   …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                   …
                }

                @Override
                public void onSuccess(ProtectedFileInputStream protectedFileInputStream)
                {
                   …
                   …
                    byte[] dataChunk = new byte[16384];
                    try
                    {
                        while ((nRead = protectedFileInputStream.read(dataChunk, 0,
                                dataChunk.length)) != -1)
                        {
                            …
                        }
                         …
                        protectedFileInputStream.close();
                    }
                    catch (IOException e)
                    {
                      …
                    }  
              }
            };
            try
            {
               …
                ProtectedFileInputStream.create(inputStream, null, mRmsAuthCallback,
                                                PolicyAcquisitionFlags.NONE,
                                                protectedFileInputStreamCreationCallback);
            }
            catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e)
            {
                …
            }
        }


-   **Paso 2**: Configuración de la autenticación mediante la biblioteca de autenticación de Active Directory (ADAL).

    **Origen**: *MsipcAuthenticationCallback.java*.

    **Descripción**: En este paso verá la ADAL usada para implementar un [AuthenticationRequestCallback](https://msdn.microsoft.com/library/dn758255.aspx) con los parámetros de autenticación de ejemplo. Para más información sobre el uso de ADAL, consulte la [biblioteca de autenticación de Azure AD (ADAL)](https://msdn.microsoft.com/library/jj573266.aspx).


        class MsipcAuthenticationCallback implements AuthenticationRequestCallback
        {

        …

        @Override
        public void getToken(Map<String, String> authenticationParametersMap,
                             final AuthenticationCompletionCallback authenticationCompletionCallbackToMsipc)
        {
            String authority = authenticationParametersMap.get("oauth2.authority");
            String resource = authenticationParametersMap.get("oauth2.resource");
            String userId = authenticationParametersMap.get("userId");
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
                            }

                            );
                      }


-   **Paso 3**: Comprobación de si existe el derecho de **edición** para este usuario con este contenido a través del método [UserPolicy.accessCheck](https://msdn.microsoft.comlibrary/dn790885.aspx).

    **Origen**: *TextEditorFragment.java*


         //check if user has edit rights and apply enforcements
                if (!mUserPolicy.accessCheck(EditableDocumentRights.Edit))
                {
                    mTextEditor.setFocusableInTouchMode(false);
                    mTextEditor.setFocusable(false);
                    mTextEditor.setEnabled(false);
                    …
                }


### <a name="scenario-create-a-new-protected-file-using-a-template"></a>Escenario: Creación de un nuevo archivo protegido mediante una plantilla

Este escenario comienza con la obtención de una lista de plantillas, la selección de la primera de ellas para crear una directiva y, a continuación, con la creación y escritura en el nuevo archivo protegido.

-   **Paso 1**: Obtención de una lista de plantillas a través de un objeto [TemplateDescriptor](https://msdn.microsoft.com/library/dn790871.aspx).

    **Origen**: *MsipcTaskFragment.java*



    CreationCallback<List<TemplateDescriptor>> getTemplatesCreationCallback = new CreationCallback<List<TemplateDescriptor>>() { @Override public Context getContext() { …
          }

          @Override
          public void onCancel()
          {
              …
          }

          @Override
          public void onFailure(ProtectionException e)
          {
              …
          }

          @Override
          public void onSuccess(List<TemplateDescriptor> templateDescriptors)
          {
             …
          }
      }; try { …
          mIAsyncControl = TemplateDescriptor.getTemplates(emailId, mRmsAuthCallback, getTemplatesCreationCallback); } catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e) { …
      }


-    **Paso 2**: Creación de [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) mediante la primera plantilla de la lista.

    **Origen**: *MsipcTaskFragment.java*



      CreationCallback<UserPolicy> userPolicyCreationCallback = new CreationCallback<UserPolicy>() { @Override public Context getContext() { …
          }

          @Override
          public void onCancel()
          {
              …
          }

          @Override
          public void onFailure(ProtectionException e)
          {
              …
          }

          @Override
          public void onSuccess(final UserPolicy item)
          {
              …
          }
      }; try { …
          mIAsyncControl = UserPolicy.create((TemplateDescriptor)selectedDescriptor, mEmailId, mRmsAuthCallback, UserPolicyCreationFlags.NONE, userPolicyCreationCallback); …
      } catch (InvalidParameterException e) { …
      }


-    **Paso 3**: Creación de [ProtectedFileOutputStream](https://msdn.microsoft.com/library/dn790855.aspx) y escritura del contenido en él.

    **Origen**: *MsipcTaskFragment.java*


    private void createPTxt(final byte[] contentToProtect) { …
            CreationCallback<ProtectedFileOutputStream> protectedFileOutputStreamCreationCallback = new CreationCallback<ProtectedFileOutputStream>() { @Override public Context getContext() { …
                }

                @Override
                public void onCancel()
                {
                 …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                 …
                }

                @Override
                public void onSuccess(ProtectedFileOutputStream protectedFileOutputStream)
                {
                    try
                    {
                        // write to this stream
                        protectedFileOutputStream.write(contentToProtect);
                        protectedFileOutputStream.flush();
                        protectedFileOutputStream.close();
                        …
                    }
                    catch (IOException e)
                    {
                        …
                    }
                }
            };
            try
            {
                File file = new File(filePath);
                outputStream = new FileOutputStream(file);
                mIAsyncControl = ProtectedFileOutputStream.create(outputStream, mUserPolicy, originalFileExtension,
                        protectedFileOutputStreamCreationCallback);
            }
            catch (FileNotFoundException e)
            {
                 …
            }
            catch (InvalidParameterException e)
            {
                 …
            }
        }



### <a name="scenario-open-a-custom-protected-file"></a>Escenario: Apertura de un archivo protegido personalizado

-   **Paso 1**: Creación de [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) a partir de *serializedContentPolicy*.

    **Origen**: *MsipcTaskFragment.java*


    CreationCallback<UserPolicy> userPolicyCreationCallbackFromSerializedContentPolicy = new CreationCallback<UserPolicy>() { @Override public void onSuccess(UserPolicy userPolicy) { …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                  …
                }

                @Override
                public void onCancel()
                {
                  …
                }

                @Override
                public Context getContext()
                {
                  …
                }
            };


    try {   ...

      // Leer serializedContentPolicyLength desde inputStream.
      long serializedContentPolicyLength = readUnsignedInt(inputStream);

      // Leer los bytes de PL del flujo de entrada con el tamaño de PL.
      byte[] serializedContentPolicy = new byte[(int)serializedContentPolicyLength]; inputStream.read(serializedContentPolicy);

      ...

      UserPolicy.acquire(serializedContentPolicy, null, mRmsAuthCallback, PolicyAcquisitionFlags.NONE,           userPolicyCreationCallbackFromSerializedContentPolicy); } catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e) {   ... } catch (IOException e) {   ... }



-    **Paso 2**: Creación de [CustomProtectedInputStream](https://msdn.microsoft.com/library/dn758271.aspx) con [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) del **paso 1**.

    **Origen**: *MsipcTaskFragment.java*



      CreationCallback<CustomProtectedInputStream> customProtectedInputStreamCreationCallback = new CreationCallback<CustomProtectedInputStream>() { @Override public Context getContext() { …
         }

         @Override
         public void onCancel()
         {
             …
         }

         @Override
         public void onFailure(ProtectionException e)
         {
             …
         }

         @Override
         public void onSuccess(CustomProtectedInputStream customProtectedInputStream)
         {
            …

             byte[] dataChunk = new byte[16384];
             try
             {
                 while ((nRead = customProtectedInputStream.read(dataChunk, 0, dataChunk.length)) != -1)
                 {
                      …
                 }
                  …
                 customProtectedInputStream.close();
             }
             catch (IOException e)
             {
                …
             }
             …
         }
     };

    try {  ...

      // Recuperar el tamaño del contenido cifrado.
      long encryptedContentLength = readUnsignedInt(inputStream);

      updateTaskStatus(new TaskStatus(TaskState.Starting, "Consuming content", true));

      CustomProtectedInputStream.create(userPolicy, inputStream,                                 encryptedContentLength,                                 customProtectedInputStreamCreationCallback); } catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e) {  ... } catch (IOException e) {  ... }


-    **Paso 3**: Lectura del contenido de [CustomProtectedInputStream](https://msdn.microsoft.com/library/dn758271.aspx) en *mDecryptedContent* y cierre.

    **Origen**: *MsipcTaskFragment.java*


    @Override public void onSuccess(CustomProtectedInputStream customProtectedInputStream) {  mUserPolicy = customProtectedInputStream.getUserPolicy();  ByteArrayOutputStream buffer = new ByteArrayOutputStream();

      int nRead;                      
      byte[] dataChunk = new byte[16384];

      try  {    while ((nRead = customProtectedInputStream.read(dataChunk, 0,                                                        dataChunk.length)) != -1)    {       buffer.write(dataChunk, 0, nRead);    }

        buffer.flush();    mDecryptedContent = new String(buffer.toByteArray(), Charset.forName("UTF-8"));

        buffer.close();    customProtectedInputStream.close();  }  catch (IOException e)  {    ...  } }


### <a name="scenario-create-a-custom-protected-file-using-a-custom-ad-hoc-policy"></a>Escenario: Creación de un archivo protegido personalizado mediante una directiva personalizada (ad hoc)

-   **Paso 1**: con una dirección de correo electrónico proporcionada por el usuario, creación de un descriptor de la directiva

    **Origen**: *MsipcTaskFragment.java*

    **Descripción**: En la práctica, los siguientes objetos se crearían con entradas de usuario desde la interfaz de dispositivo: [UserRights](https://msdn.microsoft.com/library/dn790911.aspx) y [PolicyDescriptor](https://msdn.microsoft.com/library/dn790843.aspx).



      // crear la lista userRights   UserRights userRights = new UserRights(Arrays.asList("consumer@domain.com"),     Arrays.asList( CommonRights.View, EditableDocumentRights.Print));   ArrayList<UserRights> usersRigthsList = new ArrayList<UserRights>();   usersRigthsList.add(userRights);

      // Crear PolicyDescriptor con la lista userRights   PolicyDescriptor policyDescriptor = PolicyDescriptor.createPolicyDescriptorFromUserRights(                                                          usersRigthsList);   policyDescriptor.setOfflineCacheLifetimeInDays(10);   policyDescriptor.setContentValidUntil(new Date());



-    **Paso 2**: Creación de [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) personalizado del descriptor de la directiva, *selectedDescriptor*.

    **Origen**: *MsipcTaskFragment.java*


       mIAsyncControl = UserPolicy.create((PolicyDescriptor)selectedDescriptor,                                          mEmailId, mRmsAuthCallback,                                          UserPolicyCreationFlags.NONE,                                          userPolicyCreationCallback);



-   **Paso 3**: Creación y escritura de contenido en [CustomProtectedOutputStream](https://msdn.microsoft.com/library/dn758274.aspx) y cierre.

    **Origen**: *MsipcTaskFragment.java*


    File file = new File(filePath); final OutputStream outputStream = new FileOutputStream(file); CreationCallback<CustomProtectedOutputStream> customProtectedOutputStreamCreationCallback = new CreationCallback<CustomProtectedOutputStream>() { @Override public Context getContext() { …
            }

            @Override
            public void onCancel()
            {
              …
            }

            @Override
            public void onFailure(ProtectionException e)
            {
              …
            }

            @Override
            public void onSuccess(CustomProtectedOutputStream protectedOutputStream)
            {
                try
                {
                    // write serializedContentPolicy
                    byte[] serializedContentPolicy = mUserPolicy.getSerializedContentPolicy();
                    writeLongAsUnsignedIntToStream(outputStream, serializedContentPolicy.length);
                    outputStream.write(serializedContentPolicy);
                    // write encrypted content
                    if (contentToProtect != null)
                    {
                        writeLongAsUnsignedIntToStream(outputStream,
                                CustomProtectedOutputStream.getEncryptedContentLength(contentToProtect.length,
                                        protectedOutputStream.getUserPolicy()));
                        protectedOutputStream.write(contentToProtect);
                        protectedOutputStream.flush();
                        protectedOutputStream.close();
                    }
                    else
                    {
                        outputStream.flush();
                        outputStream.close();
                    }
                    …
                }
                catch (IOException e)
                {
                  …
                }
            }
        };
        try
        {
            mIAsyncControl = CustomProtectedOutputStream.create(outputStream, mUserPolicy,
                    customProtectedOutputStreamCreationCallback);
        }
        catch (InvalidParameterException e)
        {
          …
        }

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


