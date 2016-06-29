---
# required metadata

title: Instrucciones&#58; Obtener un id. de la aplicación de Azure | Azure RMS
description: La creación de una aplicación habilitada para RMS con Microsoft Rights Management SDK 4.2 requiere la creación a su vez de un acuerdo con el equipo de RMS.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0fe9dc-bc91-4018-b28d-2db293a3eaa2
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Procedimiento para obtener un identificador de aplicación de Azure

La creación de una aplicación habilitada para RMS con Microsoft Rights Management SDK 4.2 requiere la creación a su vez de un acuerdo con el equipo de RMS.

## Información general

La creación y publicación de una aplicación habilitada para RMS con MS RMS SDK 4.2 requiere también la creación a su vez de un acuerdo de uso de servicios con el equipo de RMS. Este acuerdo, también conocido como Rights Management License Agreement (RMLA), le guía para respetar el contrato para la protección de contenido que mantendrá en nombre del usuario o propietario del contenido por los comportamientos (adherencia a reglas de negocios) de su aplicación. Como creador de una aplicación habilitada para RMS, su contrato con el equipo de RMS se aplicará por la existencia de un "id. de la aplicación de Azure" que representa este acuerdo y permite a su aplicación conectarse al servicio de Autenticación de Azure AD.

## Procesar

Use los pasos siguientes para crear el id. de su aplicación y firme su acuerdo de uso con el equipo de RMS.

-   Siga las instrucciones del tema [Creación de un id. de la aplicación en Azure](https://msdn.microsoft.com/en-us/library/azure/dn132599.aspx) para crear el id. de su aplicación.
-   Escriba al equipo de RMS para iniciar su proceso de RMLA, enviando el "id. de la aplicación" a <askipteam@microsoft.com>..
-   Firme RMLA y devuélvalo al equipo de RMS.
-   Ahora que ha firmado RMLA, debe pasar el id. de la aplicación al llamar a la biblioteca de autenticación a través del parámetro *clientID*.

    Este es el aspecto que presenta la llamada de autenticación en nuestro tema [iOS/OS X code examples](ios-os-x-code-examples.md) (Ejemplos de código iOS/OS X).


    // Recuperar token mediante ADAL
        [context acquireTokenWithResource:authenticationParameters.resource
                                 clientId:appClientId
                              redirectUri:redirectURI
                                   userId:authenticationParameters.userId
                          completionBlock:^(ADAuthenticationResult *result)



**Nota**  Si el equipo de RMS no recibe su RMLA firmado en un plazo de 60 días, su aplicación no podrá autenticarse con el sistema de autenticación de Azure.

 

 

 


<!--HONumber=Apr16_HO4-->


