---
title: "Preparación de Azure Rights Management | Azure RMS"
description: "Compruebe que tiene todo listo para habilitar e implementar Azure RMS, que incluye las cuentas de usuario y los grupos para la autenticación."
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ada00b6f6298e7d359c73eb38dfdac169eacb708
ms.openlocfilehash: c5f22b4050779193042f3e6e059d8ca84e94b390


---

# Preparación de Azure Rights Management

>*Se aplica a: Azure Rights Management, Office 365*

Después de haberse registrado para una suscripción en la nube y haber provisto a su organización de una cuenta para [!INCLUDE[o365_1](../includes/o365_1_md.md)] o Azure Active Directory, está preparado para habilitar el servicio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].

Sin embargo, antes de hacerlo, asegúrese de contar con lo siguiente:

-   Cuentas y grupos de usuarios en la nube que crea manualmente o que se crean y se sincronizan automáticamente desde los Servicios de dominio de Active Directory (AD DS).

    Al sincronizar sus cuentas y grupos locales, no es necesario sincronizar todos los atributos. Consulte una lista de los atributos que deben sincronizarse para Azure RMS en la sección [Azure RMS](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms) de la documentación de Azure Active Directory. Para que la implementación resulte más sencilla, recomendamos que use [Azure AD Connect](/active-directory/active-directory-aadconnectsync-whatis) para conectar sus directorios locales con Azure Active Directory, pero puede usar cualquier método de sincronización de directorios con el que se obtenga el mismo resultado.

-   Grupos habilitados para correo en la nube que usará con Rights Management. Pueden ser grupos integrados o creados manualmente que contengan usuarios que usarán Rights Management.

    Si tiene Exchange Online, puede crear y usar grupos habilitados para correo mediante el centro de administración de Exchange. Si tiene AD DS y va a sincronizar con Azure AD, puede crear y usar grupos habilitados para correo que sean grupos de seguridad o grupos de distribución.

## Habilitar Rights Management
De forma predeterminada, [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] está deshabilitado cuando registra su cuenta de [!INCLUDE[o365_2](../includes/o365_2_md.md)] o Azure AD. Para habilitar [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para su organización, debe activar el servicio. Para más información, consulte [Activación de Azure Rights Management](../deploy-use/activate-service.md).






<!--HONumber=Aug16_HO4-->


