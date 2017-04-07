---
title: "Cómo incorporar derechos de propiedad explícitos | Azure RMS"
description: "La aplicación debe agregar explícitamente derechos de propietario al crear una licencia desde cero."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: EF43FAC4-ABB4-459D-B173-972B5716F816
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: d7365dc91139d9edc38a52ba66319946470873d5
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="how-to-add-explicit-owner-rights"></a>Incorporación de derechos de propiedad explícitos

La aplicación debe agregar explícitamente derechos "Owner" al crear una licencia desde cero mediante [IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx).

## <a name="prerequisites"></a>Requisitos previos

Cuando la aplicación está creando un controlador de licencia utilizando [IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx), debe conceder al propietario todos los derechos explícitamente.

>[!NOTE] 
> Si configura un usuario como "propietario" con [IpcSetLicenseProperty](https://msdn.microsoft.com/library/hh535271.aspx) con la propiedad **IPC\_LI\_OWNER**, no se le concederán todos los permisos.

En el ejemplo de código siguiente solo se muestran los pasos necesarios para crear y agregar derechos específicos a una licencia determinada.

## <a name="instructions"></a>Instrucciones
 
## <a name="step-1-example-scenario"></a>Paso 1: escenario de ejemplo

En este ejemplo, se agregan los derechos necesarios a una licencia creada con [IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx). El ejemplo muestra la creación y asignación de los derechos de la licencia a través de una lista de derechos.

Estos usuarios se agregan los dos derechos siguientes:

-   Permisos de *lectura* asignados a joe@contoso.com
-   Permisos *completos* asignados a mary\_kay@contoso.com

        // Create User Rights structure
        IPC_USER_RIGHTS ownerRightForOwner = {0};

        // Create rights
        LPCWSTR rgwszOwnerRights[1] = {IPC_GENERIC_ALL};

        // Assign values to members of Rights structure
        ownerRightForOwner.User.dwType = IPC_USER_TYPE_IPC;
        ownerRightForOwner.User.wszID = IPC_USER_ID_OWNER;
        ownerRightForOwner.rgwszRights = rgwszOwnerRights;
        ownerRightForOwner.cRights = 1;

        // Create User Rights structure for Joe with Read permissions
        IPC_USER_RIGHTS joeReadRight = {0};
        LPCWSTR rgwszReadRights[1] = {IPC_GENERIC_READ};

        // Assign values to members of Rights structure for Joe
        joeReadRight.User.dwType = IPC_USER_TYPE_EMAIL;
        joeReadRight.User.wszID = "joe@contoso.com";
        joeReadRight.rgwszRights = rgwszReadRights;
        joeReadRight.cRights = 1;

        // Create User Rights structure for Mary Kay with Full permissions
        IPC_USER_RIGHTS mary_kayFullRight = {0};
        LPCWSTR rgwszFullRights[1] = {IPC_GENERIC_ALL};

        // Assign values to members of Rights structure for Mary Kay
        mary_kayFullRight.User.dwType = IPC_USER_TYPE_EMAIL;
        mary_kayFullRight.User.wszID = L"mary_kay@contoso.com";
        mary_kayFullRight.rgwszRights = rgwszFullRights;
        mary_kayFullRight.cRights = 1;

        // Create User Rights List and assign the above rights
        size_t uNoOfUserRights = 3;
        PIPC_USER_RIGHTS_LIST pUserRightsList = NULL;
        pUserRightsList = reinterpret_cast<PIPC_USER_RIGHTS_LIST>
        (new BYTE[ sizeof(IPC_USER_RIGHTS_LIST) + uNoOfUserRights * sizeof(IPC_USER_RIGHTS)]);

        if(pUserRightsList == NULL)
        {
          // Handle error
        }

        // Assign values to members of Rights List structure for Joe and Mary Kay
        (*pUserRightsList).cbSize = sizeof(IPC_USER_RIGHTS_LIST);
        (*pUserRightsList).cUserRights = uNoOfUserRights;
        (*pUserRightsList).rgUserRights[0] = ownerRightForOwner;
        (*pUserRightsList).rgUserRights[1] = joeReadRight;
        (*pUserRightsList).rgUserRights[2] = mary_kayFullRight;

        // Set the Rights List property on the license via its handle
        // hLicense is a license handle created with IpcCreateLicenseFromScratch
        hr = IpcSetLicenseProperty(hLicense, FALSE, IPC_LI_USER_RIGHTS_LIST, pUserRightsList);

        if(FAILED(hr))
        {
          // Handle the error
        }



## <a name="related-topics"></a>Temas relacionados

- [Notas para el desarrollador](developer-notes.md)
- [IpcSetLicenseProperty](https://msdn.microsoft.com/library/hh535271.aspx)
- [IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]