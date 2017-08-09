---
title: "Configuración para los clientes que usan aplicaciones de Office con Azure RMS desde AIP"
description: "Información e instrucciones para que los administradores puedan configurar las aplicaciones de Office para que funcionen con el servicio Azure Rights Management de Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ec269afe-4e87-4cc1-9144-5fbb594b412e
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 52b3942d7918ada46cbdd7b45ed3925817e75f45
ms.sourcegitcommit: 55a71f83947e7b178930aaa85a8716e993ffc063
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2017
---
# <a name="office-apps-configuration-for-clients-to-use-the-azure-rights-management-service"></a>Aplicaciones de Office: configuración para los clientes que usan el servicio Azure Rights Management

>*Se aplica a: Azure Information Protection, Office 365*


Use esta información para determinar lo que necesita hacer para que las aplicaciones de Office funcionen con el servicio Azure Rights Management desde Azure Information Protection.

## <a name="office-2016-and-office-2013"></a>Office 2016 y Office 2013
Dado que estas últimas versiones de Office son compatibles de forma nativa con el servicio Azure Rights Management, no es necesario configurar el equipo cliente para que admita las características de Information Rights Management (IRM) en aplicaciones como Word, Excel, PowerPoint, Outlook y Outlook en la Web. Lo único que deben hacer los usuarios es iniciar sesión en sus aplicaciones de Office con sus credenciales de [!INCLUDE[o365_1](../includes/o365_1_md.md)]. Después ya pueden proteger archivos y correos electrónicos, y usar archivos y correos electrónicos que hayan protegido otros usuarios.

No obstante, se recomienda complementar estas aplicaciones con el cliente de Azure Information Protection, para que los usuarios se beneficien del complemento de Office y de la compatibilidad con tipos de archivos adicionales. Para más información, vea [Cliente de Azure Information Protection: instalación y configuración de clientes](configure-client.md).

## <a name="office-2010"></a>Office 2010
Para que los equipos cliente puedan usar el servicio Azure Rights Management con Office 2010, deben tener el cliente de Azure Information Protection o la aplicación Rights Management sharing para Windows. No es preciso implementar ninguna otra configuración, los usuarios deben iniciar sesión con sus credenciales de [!INCLUDE[o365_1](../includes/o365_1_md.md)] y pueden proteger los archivos, así como usar los que hayan sido protegidos por otros usuarios.

Para más información sobre el cliente de Azure Information Protection, vea [Cliente de Azure Information Protection: instalación y configuración de clientes](configure-client.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
