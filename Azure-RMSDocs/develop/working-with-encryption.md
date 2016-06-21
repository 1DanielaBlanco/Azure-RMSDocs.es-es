---
# required metadata

title: Cómo trabajar con la configuración de cifrado | Azure RMS
description: En este artículo se le orienta a los paquetes de cifrado
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: B1D2C227-F43D-4B18-9956-767B35145792
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Trabajo con la configuración de cifrado

En este tema se le brinda información relacionada con los paquetes de cifrado y se muestran algunos recortes de código para su uso.

## Compatibilidad con AES 256, el nuevo valor predeterminado

No se requiere ningún código adicional para usar cifrado basado en *AES 256*, ya que es el nuevo valor predeterminado, siempre y cuando use en su compilación la actualización de marzo de 2015 o posterior de RMS SDK 2.1. Le animamos a considerar seriamente la actualización de sus aplicaciones a esta versión para disfrutar de las ventajas de seguridad adicionales de *AES 256*.

> [!IMPORTANT]
> La compatibilidad con el uso de los archivos protegidos con *AES 256* existe desde [la versión de octubre de 2014](release-notes-rtm.md). Si ejecuta aplicaciones compiladas con una versión del SDK anterior a octubre de 2014, esta actualización no permitirá seguir usando la aplicación. Asegúrese de que los clientes de las aplicaciones que está compilando ya usen el SDK actualizado o estén dispuestos a actualizar de inmediato a la versión más reciente de la aplicación.

 
## Compatibilidad con el cifrado API

A partir de la [actualización de marzo de 2015](release-notes-rtm.md), hemos incorporado en nuestra API y sus paquetes de cifrado asociado las tres marcas siguientes:

-   IPC\_ENCRYPTION\_PACKAGE\_AES256\_CBC4K
-   IPC\_ENCRYPTION\_PACKAGE \_AES128\_CBC4K
-   IPC\_ENCRYPTION\_PACKAGE \_AES128\_ECB (también conocido como modo de algoritmos desusados)

Las marcas de paquete de cifrado (véase [**Preferred encryption (cifrado preferido)**](/rights-management/sdk/2.1/api/win/constants#msipc_preferred_encryption)), pueden usarse junto con la nueva marca de propiedad de la licencia **IPC\_LI\_PREFERRED\_ENCRYPTION\_PACKAGE**.

Los siguientes son algunos fragmentos de código simple que muestran cómo utilizar la nueva propiedad de la licencia.

## Algoritmos desusados

La marca **IPC\_LI\_DEPRECATED\_ENCRYPTION\_ALGORITHMS** dejará de exponerse en la API. Esto significa que las aplicaciones futuras ya no se compilarán si hacen referencia a esta marca, pero las ya desarrolladas con ella seguirán funcionando dado que respetaremos la marca de forma privada en el código de la API.

Todavía será posible beneficiarse de la antigua marca de algoritmos de cifrado desusados si se cambia una marca. Consulte los fragmentos de código siguientes para obtener ejemplos.

## Protección de archivos con AES 256 CBC4K

No se requieren cambios en el código, *AES 256* CBC4K es el valor predeterminado.

    C++

    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID,
                                    0,
                                    NULL,
                                    &amp;pLicenseHandle);


## Protección de archivos con AES-128 CBC4K

    C++

    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID,
                                    0,
                                    NULL,
                                    &amp;pLicenseHandle);

    DWORD dwEncryptionMode = IPC_ENCRYPTION_PACKAGE_AES128_CBC4K;

    hr = IpcSetLicenseProperty(pLicenseHandle,
                           false,
                           IPC_LI_PREFERRED_ENCRYPTION_PACKAGE,
                           &amp;dwEncryptionMode);


## Protección de archivos con AES-128 ECB (algoritmos desusados)

Este ejemplo también muestra la nueva forma de admitir *algoritmos desusados*.

    C++
    
    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID,
                                    0,
                                    NULL,
                                    &amp;pLicenseHandle);

    DWORD dwEncryptionMode = IPC_ENCRYPTION_PACKAGE_AES128_ECB;

    hr = IpcSetLicenseProperty(pLicenseHandle,
                           false,
                           IPC_LI_PREFERRED_ENCRYPTION_PACKAGE,
                           &amp;dwEncryptionMode);

 

 


<!--HONumber=Jun16_HO2-->


