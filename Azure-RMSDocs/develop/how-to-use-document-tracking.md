---
title: Cómo usar el seguimiento de documentos | Azure RMS
description: El uso de la característica de seguimiento de documentos requiere algunos conocimientos sencillos sobre la administración de los metadatos asociados y el registro en el servicio.
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 70E10936-7953-49B0-B0DC-A5E7C4772E60
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 1caac2301fd41930856e13b634ead28f7335728f
ms.sourcegitcommit: 93124ef58e471277c7793130f1a82af33dabcea9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/11/2018
ms.locfileid: "27764606"
---
# <a name="how-to-use-document-tracking"></a>Uso del seguimiento de documentos

El uso de la característica de seguimiento de documentos requiere algunos conocimientos sencillos sobre la administración de los metadatos asociados y el registro en el servicio.

## <a name="managing-document-tracking-metadata"></a>Administración de metadatos de seguimiento de documentos

Cada uno de los sistemas operativos que admite el seguimiento de documentos tiene implementaciones similares. Puede tratarse como conjunto de propiedades que representan los metadatos, un nuevo parámetro agregado a los métodos de creación de directiva de usuario y un método para registrar la directiva que se va a seguir con el servicio de seguimiento de documentos.

Funcionalmente, solo las propiedades **content name** y **notification type** son necesarias para el seguimiento de documentos.

La secuencia de pasos que se va a utilizar para configurar el seguimiento de documentos para una parte determinada del contenido es:

-   Cree un objeto de **metadatos de licencia** y establezca el **nombre de contenido** y el **tipo de notificación**. Estas son las únicas propiedades necesarias.
   - Android: [LicenseMetadata](https://msdn.microsoft.com/library/mt573675.aspx)
   -  iOS: [MSLicenseMetadata](https://msdn.microsoft.com/library/mt573683.aspx)

Elija el tipo de directiva, que puede ser plantilla o ad hoc:
- Para el seguimiento de documentos basado en plantillas, cree un objeto **user policy** pasando los metadatos de licencia como un parámetro.
  - Android: [UserPolicy.create](https://msdn.microsoft.com/library/dn790887.aspx)
  - iOS: [MSUserPolicy.userPolicyWithTemplateDescriptor](https://msdn.microsoft.com/library/dn790808.aspx)

- Para el seguimiento de documentos basado en ad hoc, establezca la propiedad **license metadata** en el objeto **policy descriptor**.
  - Android:  [PolicyDescriptor.setLicenseMetadata](https://msdn.microsoft.com/library/mt573698.aspx)
  - iOS: [MSPolicyDescriptor.licenseMetadata](https://msdn.microsoft.com/library/mt573693.aspx).

    **Nota**: solo se puede obtener acceso al objeto license metadata directamente durante el proceso de configuración del seguimiento de documentos para la directiva de usuario determinada. Una vez creado el objeto de directiva de usuario, no se puede acceder a los metadatos de la licencia asociados; es decir, el cambio de los valores de los metadatos de licencia no tiene ningún efecto.

     

-   Por último, llame al método de registro de la plataforma para el seguimiento de documentos.
  - Android: [UserPolicy.registerForDocTracking asynchronous](https://msdn.microsoft.com/library/mt573699.aspx) o [UserPolicy.registerForDocTracking synchronous](https://msdn.microsoft.com/library/mt631387.aspx)
  - iOS: [MSUserPolicy.registerForDocTracking](https://msdn.microsoft.com/library/mt573694.aspx)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]