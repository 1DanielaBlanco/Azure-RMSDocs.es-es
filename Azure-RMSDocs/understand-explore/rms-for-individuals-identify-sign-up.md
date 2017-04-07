---
title: "¿Los usuarios se suscribieron para obtener RMS para individuos? - AIP"
description: "Como administrador, ¿cómo sabes si tus usuarios se han registrado para RMS para usuarios? Puede usar cualquiera de los métodos descritos en este artículo, o bien una combinación de ellos."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a36c3d99-a794-4f7a-aafb-64a950f1fcf9
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 10dfa64146587fe816df6a555e0a3b43c1290c45
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="how-to-find-out-if-your-users-have-signed-up-for-rms-for-individuals"></a>Cómo averiguar si los usuarios se suscribieron para obtener RMS para usuarios

>*Se aplica a: Azure Information Protection*

Como administrador, ¿cómo sabes si tus usuarios se han registrado para RMS para usuarios? Puede usar uno de estos métodos o combinarlos según su criterio:

-   Pregunte a los usuarios cómo protegen archivos muy confidenciales, especialmente cuando colaboran con otras personas de fuera de la organización.

-   Si tiene una suscripción de Azure para su organización, use el cmdlet [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) para ver si algunos usuarios tienen asignada la licencia **RIGHTSMANAGEMENT_ADHOC**. Esta licencia procede de la suscripción a RMS para usuarios que se concedió a la organización, con un conjunto de unidades activas disponibles para que los usuarios utilicen el proceso de registro de autoservicio.

-   Use una solución de administración de sistemas, como System Center Configuration Manager, para inventariar el software instalado y el software en uso. Por ejemplo, busque **MSIP.App.exe**, que utiliza el cliente de Azure Information Protection, y **ipviewer.exe** para la aplicación Rights Management sharing. Puede descargar e instalar este cliente y esta aplicación de forma gratuita para identificar otras características que posteriormente puede usar para el inventario de software.

-   Manténgase atento a las extensiones de nombre de archivos creadas por el cliente de Azure Information Protection o por la aplicación Rights Management sharing. Las extensiones de nombre de archivo .pfile y .ppdf son el ejemplo más notorio, pero hay otros archivos que cambian su extensión de nombre de archivo cuando están protegidos de forma nativa por el servicio Rights Management. Para más información, vea [Tipos de archivo compatibles para protección](../rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection) en la guía para administradores del cliente de Azure Information Protection.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]