---
# required metadata

title: Cómo establecer el modo de seguridad de API | Azure RMS
description: Elija el modo de seguridad que ejecuta la aplicación de la API de archivo.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3B088F14-81C5-4C78-8DED-F5F153353EE0
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Establecimiento del modo de seguridad de API

Puede elegir el modo de seguridad en que se ejecuta la aplicación de la API de archivo con la función [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty).

A fin de inicializar la aplicación para su ejecución en *modo servidor*, llame a la función [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) y establezca el modo de seguridad en [**IPC\_API\_MODE\_SERVER**](/rights-management/sdk/2.1/api/win/api%20mode%20values#msipc_api_mode_values_IPC_API_MODE_SERVER). De forma predeterminada, la aplicación se ejecutará en *modo cliente*, **IPC\_API\_MODE\_CLIENT**.

Para más información sobre el *modo servidor*, consulte [Tipos de aplicación](application-types.md).

**Importante**  El modo de seguridad debe establecerse antes de que se llame a cualquier otra función de Rights Management Services SDK 2.1. Una vez establecido el modo de seguridad, no podrá cambiarse para el proceso en vigor.

## Temas relacionados

* [Tipos de aplicación](application-types.md)
* [**Valores del modo de API**](/rights-management/sdk/2.1/api/win/api%20mode%20values#msipc_api_mode_values_IPC_API_MODE_SERVER)
* [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty)
 

 


<!--HONumber=Jun16_HO2-->


