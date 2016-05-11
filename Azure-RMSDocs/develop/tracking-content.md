---
# required metadata

title: Seguimiento de contenido | Azure RMS
description:
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ca08e01f-690d-46f4-ae0f-a880cc29dabc

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿# Seguimiento de contenido

\[Parte de la información está relacionada con productos preliminares que pueden sufrir cambios sustanciales en su versión comercial. Microsoft no otorga ninguna garantía, ni expresa ni implícita, con respecto a la información suministrada aquí. \]

En este tema se abordan las instrucciones básicas para implementar el seguimiento de documentos con contenido protegido con Rights Management Services SDK 2.1.

El seguimiento de documentos es una característica del sistema Rights Management. Al agregar metadatos específicos durante el proceso de protección de documentos, se puede registrar un documento con el seguimiento de portal de servicio de seguimiento que ofrece varias opciones de seguimiento.

Use estas API para agregar o actualizar una licencia de contenido con metadatos de seguimiento de documentos.

-   [**IpcCreateLicenseMetadataHandle**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensemetadatahandle)
-   [**IpcSetLicenseMetadataProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicensemetadataproperty)

    Se espera que establezca todas las propiedades de metadatos. Aquí están, mostradas por tipo.

    Para más información, consulte [**Tipos de propiedades de metadatos de licencias**](/rights-management/sdk/2.1/api/win/license%20metadata%20property%20types#msipc_license_metadata_property_types).

    -   **IPC\_MD\_CONTENT\_PATH**

        Se usa para identificar el documento cuyo seguimiento se realiza. En aquellos casos en los que no sea posible especificar una ruta de acceso completa, basta con que proporcione el nombre de archivo.

    -   **IPC\_MD\_CONTENT\_NAME**

        Se usa para identificar el nombre del documento cuyo seguimiento se realiza.

    -   **IPC\_MD\_NOTIFICATION\_TYPE**

        Se usa para especificar cuándo se enviará la notificación. Para más información, consulte [**Tipo de notificación**](/rights-management/sdk/2.1/api/win/notification%20type#msipc_notification_type).

    -   **IPC\_MD\_NOTIFICATION\_PREFERENCE**

        Se usa para especificar el tipo de notificación. Para más información, consulte [**Preferencia de notificación**](/rights-management/sdk/2.1/api/win/constants#msipc_notification_preference).

    -   **IPC\_MD\_DATE\_MODIFIED**

        Se recomienda establecer esta fecha cada vez que el usuario hace clic en **Guardar**.

    -   **IPC\_MD\_DATE\_CREATED**

        Fecha de creación del archivo.

-   [**IpcSerializeLicenseWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcserializelicensemetadata)

De estas API, use la adecuada para agregar los metadatos al archivo o la secuencia.

-   [**IpcfEncryptFileWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilewithmetadata)
-   [**IpcfEncryptFileStreamWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilestreamwithmetadata)

Por último, use esta API para registrar el documento cuyo seguimiento se realiza en el sistema de seguimiento.

-   [**IpcRegisterLicense**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcregisterlicense)

El siguiente es un fragmento de código que muestra un ejemplo de cómo establecer metadatos de seguimiento de documentos y la llamada al registro en el sistema de seguimiento.



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

    LOGSTATUS_EX(L&quot;Encrypt file with official template...&quot;);

    hr =IpcfEncryptFileWithMetadata(  wszWorkingFile.c_str(),
                                       m_wszTestTemplateID.c_str(),
                                       IPCF_EF_TEMPLATE_ID,
                                       0,
                                       NULL,
                                       NULL,
                                       &amp;md,
                                       &amp;wszOutputFile);

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


### Temas relacionados


* [**Tipos de propiedades de metadatos de licencias**](/rights-management/sdk/2.1/api/win/license%20metadata%20property%20types#msipc_license_metadata_property_types)
* [**Preferencia de notificación**](/rights-management/sdk/2.1/api/win/constants#msipc_notification_preference)
* [**Tipo de notificación**](/rights-management/sdk/2.1/api/win/notification%20type#msipc_notification_type)
* [**IpcCreateLicenseMetadataHandle**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensemetadatahandle)
* [**IpcSetLicenseMetadataProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicensemetadataproperty)
* [**IpcSerializeLicenseWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcserializelicensemetadata)
* [**IpcfEncryptFileWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilewithmetadata)
* [**IpcfEncryptFileStreamWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilestreamwithmetadata)
* [**IpcRegisterLicense**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcregisterlicense)
 

 


<!--HONumber=Apr16_HO3-->


