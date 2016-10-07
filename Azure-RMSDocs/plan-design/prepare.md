---
title: "Preparación para la protección de Azure Rights Management | Azure Information Protection"
description: "Compruebe que tiene todo preparado para empezar a usar el servicio Azure Rights Management, con el que su organización podrá proteger documentos y correos electrónicos."
author: cabailey
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
ms.sourcegitcommit: 46db6ef6f65a06c42909252cf99884cc5eaaefe4
ms.openlocfilehash: 5a3df821c70b8cd308f8fb8cc94ee0cff069a3d9


---

# Preparación de Azure Information Protection

>*Se aplica a: Azure Information Protection, Office 365*

Antes de implementar Azure Information Protection para su organización, asegúrese de que tiene preparado lo siguiente:

-   Cuentas y grupos de usuarios en la nube que crea manualmente o que se crean y se sincronizan automáticamente desde los Servicios de dominio de Active Directory (AD DS).

    Al sincronizar sus cuentas y grupos locales, no es necesario sincronizar todos los atributos. Para ver una lista de los atributos que es necesario sincronizar para el servicio Azure Rights Management usado por Azure Information Protection, vea la [sección Azure RMS](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms) de la documentación de Azure Active Directory. Para que la implementación resulte más sencilla, recomendamos que use [Azure AD Connect](/active-directory/active-directory-aadconnectsync-whatis) para conectar sus directorios locales con Azure Active Directory, pero puede usar cualquier método de sincronización de directorios con el que se obtenga el mismo resultado.

-   Grupos habilitados para correo en la nube que usará con Azure Information Protection. Pueden ser grupos integrados o grupos creados de forma manual que contengan usuarios que usarán documentos y correos electrónicos protegidos.

    Si tiene Exchange Online, puede crear y usar grupos habilitados para correo mediante el centro de administración de Exchange. Si tiene AD DS y va a sincronizar con Azure AD, puede crear y usar grupos habilitados para correo que sean grupos de seguridad o grupos de distribución.

## Activar el servicio Rights Management para la protección de datos
Cuando esté preparado para empezar a proteger documentos y correos electrónicos, active el servicio Rights Management para habilitar esta tecnología. Para más información, consulte [Activación de Azure Rights Management](../deploy-use/activate-service.md).






<!--HONumber=Sep16_HO4-->


