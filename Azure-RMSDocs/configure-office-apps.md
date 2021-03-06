---
title: Configuración para los clientes que usan aplicaciones de Office con Azure RMS desde AIP
description: Información e instrucciones para que los administradores puedan configurar las aplicaciones de Office para que funcionen con el servicio Azure Rights Management de Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/01/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ec269afe-4e87-4cc1-9144-5fbb594b412e
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 87baf8f7bccd4f99b1beefc8a7ede9c7b38c77cd
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56255094"
---
# <a name="office-apps-configuration-for-clients-to-use-the-azure-rights-management-service"></a>Aplicaciones de Office: configuración para los clientes que usan el servicio Azure Rights Management

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Use esta información para determinar lo que necesita hacer para que las aplicaciones de Office funcionen con el servicio Azure Rights Management desde Azure Information Protection.

## <a name="office2016-and-office-2013"></a>Office 2016 y Office 2013
Dado que estas últimas versiones de Office son compatibles de forma nativa con el servicio Azure Rights Management, no es necesario configurar el equipo cliente para que admita las características de Information Rights Management (IRM) en aplicaciones como Word, Excel, PowerPoint, Outlook y Outlook en la Web. Lo único que deben hacer los usuarios es iniciar sesión en sus aplicaciones de Office con sus credenciales de Office 365. Después ya pueden proteger archivos y correos electrónicos, y usar archivos y correos electrónicos que hayan protegido otros usuarios.

No obstante, se recomienda complementar estas aplicaciones con el cliente de Azure Information Protection, para que los usuarios se beneficien del complemento de Office y de la compatibilidad con tipos de archivos adicionales. Para más información, vea [Cliente de Azure Information Protection: instalación y configuración de clientes](configure-client.md).

## <a name="office2010"></a>Office 2010
Para que los equipos cliente puedan usar el servicio Azure Rights Management con Office 2010, deben tener el cliente de Azure Information Protection. No es preciso implementar ninguna otra configuración, los usuarios deben iniciar sesión con sus credenciales de Office 365 y pueden proteger los archivos, así como usar los que hayan sido protegidos por otros usuarios.

Para más información sobre el cliente de Azure Information Protection, vea [Cliente de Azure Information Protection: instalación y configuración de clientes](configure-client.md).

