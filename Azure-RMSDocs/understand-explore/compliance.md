---
title: "Información y cumplimiento para Azure Information Protection"
description: "Información complementaria para Azure Information Protection, que incluye información legal, de cumplimiento y SLA."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/20/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: b3a7127b-6d24-4439-bc4e-2a0a325e8ea3
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ef0b40db5dbbb66d7cbf45028862576a58886051
ms.sourcegitcommit: 240378d216e386ad760460c50b7a664099c669e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2018
---
# <a name="compliance-and-supporting-information-for-azure-information-protection"></a>Información complementaria y de cumplimiento para Azure Information Protection

Azure Information Protection admite otros servicios y también se basa en otros servicios. Si está buscando información relacionada con Azure Information Protection pero no sobre cómo usar el servicio, compruebe los recursos siguientes:

## <a name="suitability-for-different-countries"></a>Idoneidad para distintos países

Dada la variabilidad entre las leyes y las regulaciones de los países, los distintos escenarios y casos de uso, así como las diferentes necesidades de cada sector empresarial, deberá consultar con un asesor jurídico para saber si Azure Information Protection es apto para su país.

Aquí tiene alguna información pertinente que puede ayudar a su asesor jurídico a tomar una determinación:

- Azure Information Protection usa AES 256 y AES 128 para cifrar los documentos. [Más información](../understand-explore/how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)

- Todas las claves de cifrado utilizadas con Azure Information Protection están protegidas con una clave raíz específica del cliente que usa RSA 2048 bits. No obstante, RSA 1024 también se admite para versiones anteriores. [Más información](../understand-explore/how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)

- Las claves raíz específicas del cliente son administradas por Microsoft o aprovisionadas por el cliente en un HSM de Thales mediante "[Bring Your Own Key](../plan-design/plan-implement-tenant-key.md)" (BYOK). En caso de que el contenido se vea afectado por requisitos que indican que no debe protegerse con un clave en la nube, Azure Information Protection admite también funcionalidad limitada con una clave local mediante "[Hold Your Own Key](../deploy-use/configure-adrms-restrictions.md)" (HYOK).

- El servicio Azure Information Protection se hospeda en centros de datos regionales repartidos por todo el mundo. Las claves y las directivas de Azure Information Protection siempre permanecen dentro de la región en la que se implementó originalmente.
 
- Azure Information Protection no transmite el contenido de los documentos de los clientes al servicio Azure Information Protection. Las operaciones de cifrado y descifrado de contenido se realizan localmente en el dispositivo cliente. O bien, para la representación basada en servicios, estas operaciones se ejecutan dentro del servicio que procesa el contenido. [Más información](../understand-explore/how-does-it-work.md)

## <a name="legal-and-privacy"></a>Información legal y privacidad

- Para información contractual de Microsoft Azure: [Contrato de Microsoft Azure](http://azure.microsoft.com/support/legal/subscription-agreement/)

- Para información de privacidad de Microsoft Azure: [Declaración de privacidad de Microsoft Azure](http://azure.microsoft.com/support/legal/privacy-statement/)

## <a name="security-compliance-and-auditing"></a>Seguridad, cumplimiento y auditoría

Consulte la sección [Security, compliance, and regulatory requirements](../understand-explore/azure-rms-problems-it-solves.md#security-compliance-and-regulatory-requirements) (Requisitos de seguridad, normativos y regulatorios) del artículo [What problems does Azure RMS solve?](../understand-explore/azure-rms-problems-it-solves.md) (¿Qué problemas resuelve Azure RMS?) para obtener información sobre las certificaciones específicas del servicio de Azure Rights Management. Además:

- Para certificaciones externas de Azure Information Protection: [Centro de confianza de Microsoft Azure](http://azure.microsoft.com/support/trust-center/)

- Para obtener información sobre FIPS 140: [Validación conforme a FIPS 140](https://technet.microsoft.com/library/security/cc750357.aspx)

Para obtener información técnica detallada acerca de cómo funciona la tecnología de protección, consulte ¿[Cómo funciona Azure RMS?](../understand-explore/how-does-it-work.md) 

## <a name="service-level-agreements"></a>Contratos de nivel de servicio

- Contrato de nivel de servicio para Azure Information Protection, por región seleccionada: [Descargar de la página de búsqueda de licencias de productos](http://microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&amp;DocumentTypeId=37)

    - Por ejemplo, haga clic en **OnlineSvcsConsolidatedSLA(WW)(English)(March2016)** para descargar el contrato de nivel de servicio de marzo de 2016 para Norteamérica.

-   Contrato de nivel de servicio para Azure Active Directory: [Contratos de nivel de servicio](http://azure.microsoft.com/support/legal/sla/)

## <a name="documentation"></a>Documentación

- Documentación de Azure Active Directory: [Azure Active Directory](/active-directory/)

- Biblioteca de Office 365: [Office 365](http://technet.microsoft.com/library/dn127064%28v=office.14%29.aspx)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
