---
title: "Preparación para la protección de Azure Rights Management | Azure Information Protection"
description: "Compruebe que tiene todo preparado para empezar a usar el servicio Azure Rights Management, con el que su organización podrá proteger documentos y correos electrónicos."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: b0c5596feec3f61ad25fe47416a1383f453bdc6b


---

# <a name="preparing-for-azure-information-protection"></a>Preparación de Azure Information Protection

>*Se aplica a: Azure Information Protection, Office 365*

Antes de implementar Azure Information Protection para su organización, asegúrese de que tiene preparado lo siguiente:

-   Cuentas y grupos de usuarios en la nube que crea manualmente o que se crean y se sincronizan automáticamente desde los Servicios de dominio de Active Directory (AD DS).

    Al sincronizar sus cuentas y grupos locales, no es necesario sincronizar todos los atributos. Para ver una lista de los atributos que es necesario sincronizar para el servicio Azure Rights Management usado por Azure Information Protection, vea la [sección Azure RMS](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms) de la documentación de Azure Active Directory. Para que la implementación resulte más sencilla, recomendamos que use [Azure AD Connect](/active-directory/active-directory-aadconnectsync-whatis) para conectar sus directorios locales con Azure Active Directory, pero puede usar cualquier método de sincronización de directorios con el que se obtenga el mismo resultado.

-   Grupos habilitados para correo en la nube que usará con Azure Information Protection. Pueden ser grupos integrados o grupos creados de forma manual que contengan usuarios que usarán documentos y correos electrónicos protegidos.

    Si tiene Exchange Online, puede crear y usar grupos habilitados para correo mediante el centro de administración de Exchange. Si tiene AD DS y va a sincronizar con Azure AD, puede crear y usar grupos habilitados para correo que sean grupos de seguridad o grupos de distribución.

## <a name="activate-the-rights-management-service-for-data-protection"></a>Activar el servicio Rights Management para la protección de datos
Cuando esté preparado para empezar a proteger documentos y correos electrónicos, active el servicio Rights Management para habilitar esta tecnología. Para más información, consulte [Activación de Azure Rights Management](../deploy-use/activate-service.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]





<!--HONumber=Jan17_HO4-->


