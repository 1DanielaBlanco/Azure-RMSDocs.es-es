---
# required metadata

title: Seguimiento de contenido | Azure RMS
description: Guía básica para la implementación del seguimiento de documentos
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: F5089765-9D94-452B-85E0-00D22675D847
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** El contenido de este SDK no es actual. Durante un breve periodo podrá encontrar la [versión actual](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx) de la documentación en MSDN. **
# Seguimiento de contenido

En este tema se abordan las instrucciones básicas para implementar el seguimiento de documentos con contenido protegido con Rights Management Services SDK 2.1.

El seguimiento de documentos es una característica del sistema Rights Management. Al agregar metadatos específicos durante el proceso de protección de documentos, se puede registrar un documento con el seguimiento de portal de servicio de seguimiento que ofrece varias opciones de seguimiento.

Use estas API para agregar o actualizar una licencia de contenido con metadatos de seguimiento de documentos.

-   [**IpcCreateLicenseMetadataHandle**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensemetadatahandle)
-   [**IpcSetLicenseMetadataProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicensemetadataproperty)

    Se espera que establezca todas las propiedades de metadatos. Aquí están, mostradas por tipo.

    Para más información, consulte [**Tipos de propiedades de metadatos de licencias**](/rights-management/sdk/2.1/api/win/license%20metadata%20property%20types#msipc_license_metadata_property_types).

    -   **IPC\_MD\_CONTENIDO\_RUTA DE ACCESO**

        Se usa para identificar el documento cuyo seguimiento se realiza. En aquellos casos en los que no sea posible especificar una ruta de acceso completa, basta con que proporcione el nombre de archivo.

    -   **IPC\_MD\_CONTENIDO\_NOMBRE**

        Se usa para identificar el nombre del documento cuyo seguimiento se realiza.

    -   **IPC\_MD\_NOTIFICACIÓN\_TIPO**

        Se usa para especificar cuándo se enviará la notificación. Para más información, consulte [**Tipo de notificación**](/rights-management/sdk/2.1/api/win/notification%20type#msipc_notification_type).

    -   **IPC\_MD\_NOTIFICACIÓN\_PREFERENCIA**

        Se usa para especificar el tipo de notificación. Para más información, consulte [**Preferencia de notificación**](/rights-management/sdk/2.1/api/win/constants#msipc_notification_preference).

    -   **IPC\_MD\_FECHA\_MODIFICADO**

        Se recomienda establecer esta fecha cada vez que el usuario hace clic en **Guardar**.

    -   **IPC\_MD\_FECHA\_CREADO**

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


## Temas relacionados


* [**Tipos de propiedades de metadatos de licencias**](/rights-management/sdk/2.1/api/win/license%20metadata%20property%20types#msipc_license_metadata_property_types)
* [**Preferencia de notificación**](/rights-management/sdk/2.1/api/win/constants#msipc_notification_preference)
* [**Tipo de notificación**](/rights-management/sdk/2.1/api/win/notification%20type#msipc_notification_type)
* [**IpcCreateLicenseMetadataHandle**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensemetadatahandle)
* [**IpcSetLicenseMetadataProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicensemetadataproperty)
* [**IpcSerializeLicenseWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcserializelicensemetadata)
* [**IpcfEncryptFileWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilewithmetadata)
* [**IpcfEncryptFileStreamWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilestreamwithmetadata)
* [**IpcRegisterLicense**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcregisterlicense)
 

 


<!--HONumber=Jun16_HO1-->


