---
# required metadata

title: Condiciones de error comunes y soluciones | Azure RMS
description: Este tema incluye los mensajes de error más comunes que pueden surgir al usar las herramientas de desarrollador de RMS SDK 2.1.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: A5B95EB8-3528-4CFF-86FC-166613A5F4A3
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Condiciones de error comunes y soluciones
Este tema incluye los mensajes de error más comunes que pueden surgir al usar las herramientas de desarrollador de Rights Management Services SDK 2.1. También proporciona una acción recomendada para corregir el error, si procede.

**Importante**: Para el procesamiento de la condición de error, utilice siempre una llamada a [IpcGetErrorMessageText](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgeterrormessagetext) justo después de que se produzca un error en una llamada a la API del SDK, a fin de obtener información completa sobre la naturaleza del error.

 

## Error y acción ##
La lista siguiente contiene una lista de constantes de error, su descripción asociada y una acción recomendada para tratar la condición de error.

**ERROR** - *IPCERROR_DEBUGGER_DETECTED*: se ha detectado un depurador por RMS SDK 2.1

**ACCIÓN**: la versión para programadores de RMS SDK 2.1 no comprueba la presencia de un depurador. Si es posible, depure la aplicación con esta versión de RMS SDK 2.1.
Si debe depurar la versión de producción de RMS SDK 2.1, siga las instrucciones que se presentan a continuación.

Algunas funciones de RMS SDK 2.1 están diseñadas para producir un error en un depurador:
- [IpcGetKey</strong>](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
- [IpcGetTemplateList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
- [IpcGetTemplateIssuerList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist)

Para depurar código con base en estas llamadas de función, debe interrumpir el proceso y adjuntar un depurador una vez que se hayan completado dichas llamadas de función. Uno de los métodos para ello es usar una instrucción assert para interrumpir el depurador. La macro ASSERTE se incluye en el encabezado *Crtdbg.h*.
Para más información sobre \_ASSERTE, consulte [_ASSERT, _ASSERTE (Macros)](https://msdn.microsoft.com/en-us/library/ezb1wyez.aspx).

**ERROR** - *IPCERROR_BROKEN_CERT_CHAIN*: la cadena de certificados no coincide.

**ACCIÓN**: asegúrese de que la clave de la jerarquía contiene el valor correcto con base en la clave utilizada para firmar el manifiesto de aplicación de AD RMS.
Estas son las claves de firma y sus valores asociados (jerarquía **DWORD**):
- ISV: 1
- Producción: 0 o ausencia de valor

**ERROR** - *IPCERROR_MACHINE_CERT_NOT_TRUSTED*: está usando una aplicación firmada con la clave de firma de ISV, pero está intentando comunicarse con un servidor AD RMS de producción, o viceversa.

- Si utiliza la versión del desarrollador del servidor de AD RMS, asegúrese de que utiliza la clave de firma de ISV para firmar la aplicación.
- Si utiliza la versión de producción del servidor de AD RMS, asegúrese de que utiliza la clave de firma de producción para firmar la aplicación.

**ERROR** - *IPCERROR_APPLICATION_AUTH_ERROR_MANIFEST*: el manifiesto de aplicación no es válido. Esto puede deberse a que una vez que se volvió a generar el archivo binario (aplicación), no se hizo lo mismo con el manifiesto.

**ACCIÓN**: asegúrese de que vuelve a generar el manifiesto de aplicación cada vez que vuelva a generar la aplicación.

## Temas relacionados ##
* [Notas para el desarrollador](developer-notes.md)
* [IpcGetKey](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
* [IpcGetTemplateList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
* [IpcGetTemplateIssuerList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist)
* [_ASSERT, _ASSERTE (Macros)](https://msdn.microsoft.com/en-us/library/ezb1wyez.aspx)
 

 


<!--HONumber=Apr16_HO4-->


