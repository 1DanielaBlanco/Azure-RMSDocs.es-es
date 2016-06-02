---
# required metadata

title: Procedimiento para&#58;usar el seguimiento de documentos | Azure RMS
description: El uso de la característica de seguimiento de documentos requiere algunos conocimientos sencillos sobre la administración de los metadatos asociados y el registro en el servicio.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 70E10936-7953-49B0-B0DC-A5E7C4772E60
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Uso del seguimiento de documentos

El uso de la característica de seguimiento de documentos requiere algunos conocimientos sencillos sobre la administración de los metadatos asociados y el registro en el servicio.

## Administración de metadatos de seguimiento de documentos

Cada uno de los sistemas operativos que admite el seguimiento de documentos tiene implementaciones similares. Puede tratarse como conjunto de propiedades que representan los metadatos, un nuevo parámetro agregado a los métodos de creación de directiva de usuario y un método para registrar la directiva que se va a seguir con el servicio de seguimiento de documentos.

Funcionalmente, solo las propiedades **content name** y **notification type** son necesarias para el seguimiento de documentos.

La secuencia de pasos que se va a utilizar para configurar el seguimiento de documentos para una parte determinada del contenido es:

-   Cree un objeto **license metadata**.

    Consulte [**LicenseMetadata**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_licensemetadata_interface_java) o [**MSLicenseMetadata**](/rights-management/sdk/4.2/api/iOS/mslicensemetadata#msipcthin2_mslicensemetadata_class_objc) para más información.

-   Establezca las propiedades **content name** y **notification type**. Estas son las únicas propiedades necesarias.

    Para más información, consulte los métodos de acceso de la propiedad para la clase de metadatos de licencia apropiada de la plataforma, ya sea [**LicenseMetadata**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_licensemetadata_interface_java) o [**MSLicenseMetadata**](/rights-management/sdk/4.2/api/iOS/mslicensemetadata#msipcthin2_mslicensemetadata_class_objc).

-   Por tipo de directiva; plantilla o ad hoc:

    -   Para el seguimiento de documentos basado en plantillas, cree un objeto **user policy** pasando los metadatos de licencia como un parámetro.

        Para más información, consulte [**UserPolicy.create**](/rights-management/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_class_java) y [**MSUserPolicy.userPolicyWithTemplateDescriptor**](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_templatedescriptor_property_objc).

    -   Para el seguimiento de documentos basado en ad hoc, establezca la propiedad **license metadata** en el objeto **policy descriptor**.

        Para obtener más información, consulte [**PolicyDescriptor.getLicenseMetadata**](/rights-management/sdk/4.2/api/android/policydescriptor#msipcthin2_policydescriptor_interface_java), [**PolicyDescriptor.setLicenseMetadata**](/rights-management/sdk/4.2/api/android/policydescriptor#msipcthin2_policydescriptor_setlicensemetadata_java) y [**MSPolicyDescriptor.licenseMetadata**](/rights-management/sdk/4.2/api/iOS/mspolicydescriptor#msipcthin2_mspolicydescriptor_licensemetadata_property_objc).

    **Nota**: solo se puede obtener acceso al objeto license metadata directamente durante el proceso de configuración del seguimiento de documentos para la directiva de usuario determinada. Una vez creado el objeto user policy, no se puede obtener acceso a los metadatos de la licencia asociados, es decir, el cambio de los valores de los metadatos de licencia no tiene ningún efecto.

     

-   Llame al método de registro de la plataforma para el seguimiento de documentos.

    Consulte [**MSUserPolicy.registerForDocTracking**](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_registerfordoctracking_userid_authenticationcallback_completionblock_method_objc) o [**UserPolicy.registerForDocTracking**](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_registerfordoctracking_userid_authenticationcallback_completionblock_method_objc).

 

 





<!--HONumber=Apr16_HO4-->


