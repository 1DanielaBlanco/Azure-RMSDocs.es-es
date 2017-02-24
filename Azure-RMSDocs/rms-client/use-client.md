---
title: El cliente| Azure Information Protection
description: "Microsoft Azure Information Protection proporciona una solución cliente/servidor que ayuda a proteger los datos de la organización. El cliente (el cliente de Azure Information Protection o el cliente de Rights Management) se integra con aplicaciones que ejecuta en equipos y dispositivos móviles."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a6fa85be-f92a-4e00-9efc-9dbfd4dfbfcb
ROBOTS: noindex,nofollow
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 190b5d2a25dc9479aa2ba34fd884795e0de40238
ms.openlocfilehash: f52f3e04f41e33828bd9a9c5c1aad3ef460b2d23


---

# <a name="the-client-side-of-azure-information-protection"></a>El lado cliente de Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 8.1, Windows 8, Windows 7 SP1*

Azure Information Protection proporciona una solución cliente/servidor que ayuda a proteger los documentos y correos electrónicos de la organización:

- El cliente puede ser el cliente de Azure Information Protection o el cliente de Rights Management, y se integra con aplicaciones que ejecuta en equipos y dispositivos móviles. 

- El servicio se encuentra en la nube (Azure Information Protection, que usa el servicio Azure Rights Management para la protección de datos) o local (Active Directory Rights Management Services). 

El cliente de Azure Information Protection admite la clasificación y el etiquetado, además de protección. Este cliente se integra con las aplicaciones de Office y debe instalarse de manera independiente.

El cliente de Rights Management (RMS) se instala automáticamente con algunas aplicaciones, como aplicaciones de Office, el cliente de Azure Information Protection y las aplicaciones habilitadas para RMS de proveedores de software. En cambio, también puede instalarse por sí mismo, en cuyo caso es compatible con diversos escenarios, como desarrolladores que quieren integrar la protección de Rights Management en las aplicaciones de línea de negocio.

Use la siguiente documentación si necesita obtener más información sobre la implementación y el uso de estos clientes, que se pueden usar con Azure Information Protection y Active Directory Rights Management Services para ayudar a proteger los datos de su organización:

- [Cliente de Azure Information Protection](AIP-client.md)

- [Notas de la implementación del cliente RMS](client-deployment-notes.md)

- [Protección de RMS con la infraestructura de clasificación de archivos (FCI) de Windows Server](configure-fci.md)

- [Aplicación Rights Management sharing para Windows](sharing-app-windows.md)

Tenga en cuenta que la aplicación Rights Management sharing para Windows y la herramienta de protección de RMS ahora se reemplaza por el cliente de Azure Information Protection. 


## <a name="see-also"></a>Consulte también
[Comparación de Azure Information Protection y AD RMS](../understand-explore/compare-azure-rms-ad-rms.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Feb17_HO2-->


