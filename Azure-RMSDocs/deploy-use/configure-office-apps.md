---
title: "Aplicaciones de Office: Configuración para clientes | Azure Information Protection"
description: "Información e instrucciones para que los administradores puedan configurar las aplicaciones de Office para que funcionen con el servicio Azure Rights Management de Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ec269afe-4e87-4cc1-9144-5fbb594b412e
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: a471dd917aab193ddfe5a58cbfa4f5082e6a049d


---

# <a name="office-apps-configuration-for-clients"></a>Aplicaciones de Office: configuración para clientes

>*Se aplica a: Azure Information Protection, Office 365*


Use esta información para determinar lo que necesita hacer para que las aplicaciones de Office usadas por los usuarios finales funcionen con el servicio Azure Rights Management de Azure Information Protection.

## <a name="office-2016-and-office-2013"></a>Office 2016 y Office 2013
Dado que estas últimas versiones de Office son compatibles de forma nativa con el servicio Azure Rights Management, no es necesario configurar el equipo cliente para que admita las características de Information Rights Management (IRM) en aplicaciones como Word, Excel, PowerPoint, Outlook y Outlook Web App. Todo lo que tienen que hacer los usuarios es iniciar sesión en sus aplicaciones Office con sus credenciales de [!INCLUDE[o365_1](../includes/o365_1_md.md)] y pueden proteger archivos y correos electrónicos, así como usar los que hayan sido protegidos por otros usuarios.

Sin embargo, se recomienda que complemente estas aplicaciones con la aplicación de uso compartido Rights Management, para que los usuarios obtengan los beneficios del complemento de Office. Para más información, consulte la sección [Aplicación de uso compartido Rights Management: Instalación y configuración para clientes](configure-sharing-app.md) de este tema.

## <a name="office-2010"></a>Office 2010
Para que los equipos cliente puedan usar el servicio Azure Rights Management con Office 2010, es necesario instalar la aplicación Rights Management sharing para Windows. No es preciso implementar ninguna otra configuración, los usuarios deben iniciar sesión con sus credenciales de [!INCLUDE[o365_1](../includes/o365_1_md.md)] y pueden proteger los archivos, así como usar los que hayan sido protegidos por otros usuarios.

Para más información acerca de la aplicación de Rights Management sharing, consulte la sección [Aplicación de uso compartido Rights Management Instalación y configuración para clientes](configure-sharing-app.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



<!--HONumber=Jan17_HO4-->


