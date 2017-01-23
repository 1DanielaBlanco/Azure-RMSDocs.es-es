---
title: "Procedimiento para habilitar la revocación y el seguimiento de documentos | Azure RMS"
description: "Guía básica para implementar el seguimiento de documentos, así como código de ejemplo para las actualizaciones de metadatos y un botón Hacer seguimiento de uso para la aplicación."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: F5089765-9D94-452B-85E0-00D22675D847
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
experimental: true
experiment_id: priyamo-test-20160729
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 1e1bf622bfae4d2cca3b30798dbf6cb5c794e24a


---

# <a name="how-to-enable-document-tracking-and-revocation"></a>Habilitación de la revocación y el seguimiento de documentos

En este tema se abordan las instrucciones básicas para implementar el seguimiento de documentos, así como código de ejemplo para las actualizaciones de metadatos y para la creación de un botón **Hacer seguimiento de uso** para la aplicación.

## <a name="steps-to-implement-document-tracking"></a>Pasos para implementar el seguimiento de documentos

Los pasos 1 y 2 permiten que se realice un seguimiento del documento. El paso 3 permite que los usuarios de la aplicación lleguen al sitio de seguimiento de documentos para realizar un seguimiento de los documentos protegidos y revocarlos.

1. Incorporación de metadatos de seguimiento de documentos
2. Registro del documento con el servicio de RMS
3. Incorporación del botón Hacer seguimiento de uso a la aplicación

A continuación se indican los detalles de implementación de estos pasos.

## <a name="1-add-document-tracking-metadata"></a>1. Incorporación de metadatos de seguimiento de documentos

El seguimiento de documentos es una característica del sistema Rights Management. Al agregar metadatos específicos durante el proceso de protección de documentos, se puede registrar un documento con el seguimiento de portal de servicio de seguimiento que ofrece varias opciones de seguimiento.

Use estas API para agregar o actualizar una licencia de contenido con metadatos de seguimiento de documentos.


Funcionalmente, solo las propiedades **content name** y **notification type** son necesarias para el seguimiento de documentos.


- [IpcCreateLicenseMetadataHandle](https://msdn.microsoft.com/library/dn974050.aspx)
- [IpcSetLicenseMetadataProperty](https://msdn.microsoft.com/library/dn974059.aspx)

  Se espera que establezca todas las propiedades de metadatos. Aquí están, mostradas por tipo.

  Para obtener más información, consulte [License metadata property types](https://msdn.microsoft.com/library/dn974062.aspx) (Tipos de propiedades de metadatos de licencias).

  - **IPC_MD_CONTENT_PATH**

    Se usa para identificar el documento cuyo seguimiento se realiza. En aquellos casos en los que no sea posible especificar una ruta de acceso completa, basta con que proporcione el nombre de archivo.

  - **IPC_MD_CONTENT_NAME**

    Se usa para identificar el nombre del documento cuyo seguimiento se realiza.

  - **IPC_MD_NOTIFICATION_TYPE**

    Se usa para especificar cuándo se enviará la notificación. Para obtener más información, consulte Tipo de notificación.

  - **IPC_MD_NOTIFICATION_PREFERENCE**

    Se usa para especificar el tipo de notificación. Para obtener más información, consulte Preferencia de notificación.

  - **IPC_MD_DATE_MODIFIED**

    Se recomienda establecer esta fecha cada vez que el usuario hace clic en Guardar.

  - **IPC_MD_DATE_CREATED**

    Se usa para establecer la fecha de creación del archivo.

- [IpcSerializeLicenseWithMetadata](https://msdn.microsoft.com/library/dn974058.aspx)

De estas API, use la adecuada para agregar los metadatos al archivo o la secuencia.

- [IpcfEncryptFileWithMetadata](https://msdn.microsoft.com/library/dn974052.aspx)
- [IpcfEncryptFileStreamWithMetadata](https://msdn.microsoft.com/library/dn974051.aspx)

Por último, use esta API para registrar el documento cuyo seguimiento se realiza en el sistema de seguimiento.

- [IpcRegisterLicense](https://msdn.microsoft.com/library/dn974057.aspx)


## <a name="2-register-the-document-with-the-rms-service"></a>2. Registro del documento con el servicio de RMS

El siguiente es un fragmento de código que muestra un ejemplo de cómo establecer metadatos de seguimiento de documentos y la llamada al registro en el sistema de seguimiento.

      C++
      HRESULT hr = S_OK;
      LPCWSTR wszOutputFile = NULL;
      wstring wszWorkingFile;
      IPC_LICENSE_METADATA md = {0};

      md.cbSize = sizeof(IPC_LICENSE_METADATA);
      md.dwNotificationType = IPCD_CT_NOTIFICATION_TYPE_ENABLED;
      md.dwNotificationPreference = IPCD_CT_NOTIFICATION_PREF_DIGEST;
      //file origination date, current time for this example
      md.ftDateCreated = GetCurrentTime();
      md.ftDateModified = GetCurrentTime();

      LOGSTATUS_EX(L"Encrypt file with official template...");

      hr =IpcfEncryptFileWithMetadata( wszWorkingFile.c_str(),
                               m_wszTestTemplateID.c_str(),
                               IPCF_EF_TEMPLATE_ID,
                               0,
                               NULL,
                               NULL,
                               &md,
                               &wszOutputFile);

     /* This will contain the serialized license */
     PIPC_BUFFER pSerializedLicense;

     /* the context to use for the call */
     PCIPC_PROMPT_CTX pContext;

     wstring wstrContentName(“MyDocument.txt”);
     bool sendLicenseRegistrationNotificationEmail = FALSE;

     hr = IpcRegisterLicense( pSerializedLicense,
                        0,
                        pContext,
                        wstrContentName.c_str(),
                        sendLicenseRegistrationNotificationEmail);

## <a name="add-a-track-usage-button-to-your-app"></a>Incorporación del botón **Hacer seguimiento de uso** a la aplicación

Agregar a la aplicación un elemento de interfaz de usuario **Hacer seguimiento de uso** es tan sencillo como usar uno de los siguientes formatos de dirección URL:

- Mediante el identificador de contenido
  - Obtenga el identificador de contenido mediante [IpcGetLicenseProperty](https://msdn.microsoft.com/library/hh535265.aspx) o [IpcGetSerializedLicenseProperty](https://msdn.microsoft.com/library/hh995038.aspx) si la licencia está serializada y use la propiedad de la licencia **IPC_LI_CONTENT_ID**. Para obtener más información, vea [License property types](https://msdn.microsoft.com/library/hh535287.aspx) (Tipos de propiedades de licencias).
  - Con los metadatos **ContentId** e **Issuer**, use el siguiente formato: `https://track.azurerms.com/#/{ContentId}/{Issuer}`

    Ejemplo: `https://track.azurerms.com/#/summary/05405df5-8ad6-4905-9f15-fc2ecbd8d0f7/janedoe@microsoft.com`

- Si no tiene acceso a esos metadatos (es decir, si está examinando la versión no protegida del documento), puede usar **Content_Name** en el formato siguiente: `https://track.azurerms.com/#/?q={ContentName}`

  Ejemplo: https://track.azurerms.com/#/?q=Secret!.txt

El cliente solo tiene que abrir un explorador con la dirección URL apropiada. El portal de seguimiento de documentos de RMS controlará la autenticación y los redireccionamientos necesarios.

## <a name="related-topics"></a>Temas relacionados

* [Tipos de propiedades de metadatos de licencias](https://msdn.microsoft.com/library/dn974062.aspx)
* [Preferencia de notificación](https://msdn.microsoft.com/library/dn974063.aspx)
* [Tipo de notificación](https://msdn.microsoft.com/library/dn974064.aspx)
* [IpcCreateLicenseMetadataHandle](https://msdn.microsoft.com/library/dn974050.aspx)
* [IpcSetLicenseMetadataProperty](https://msdn.microsoft.com/library/dn974059.aspx)
* [IpcSerializeLicenseWithMetadata](https://msdn.microsoft.com/library/dn974058.aspx)
* [IpcfEncryptFileWithMetadata](https://msdn.microsoft.com/library/dn974052.aspx)
* [IpcfEncryptFileStreamWithMetadata](https://msdn.microsoft.com/library/dn974051.aspx)
* [IpcRegisterLicense](https://msdn.microsoft.com/library/dn974057.aspx)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO1-->


