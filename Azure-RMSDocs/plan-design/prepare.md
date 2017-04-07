---
title: "Preparación para la protección de Azure Rights Management - AIP"
description: "Compruebe que tiene todo preparado para empezar a usar el servicio Azure Rights Management, con el que su organización podrá proteger documentos y correos electrónicos."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/28/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 4b074f9a9a3d72b4d1ab5810b69e92b4792b0711
ms.sourcegitcommit: 16fec44713c7064959ebb520b9f0857744fecce9
translationtype: HT
---
# <a name="preparing-for-azure-information-protection"></a>Preparación de Azure Information Protection

>*Se aplica a: Azure Information Protection, Office 365*

Antes de implementar Azure Information Protection para su organización, asegúrese de que tiene preparado lo siguiente:

-   Cuentas y grupos de usuarios en la nube que crea manualmente o que se crean y se sincronizan automáticamente desde los Servicios de dominio de Active Directory (AD DS).

    Al sincronizar sus cuentas y grupos locales, no es necesario sincronizar todos los atributos. Para ver una lista de los atributos que es necesario sincronizar para el servicio Azure Rights Management usado por Azure Information Protection, vea la [sección Azure RMS](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms) de la documentación de Azure Active Directory. Para que la implementación resulte más sencilla, recomendamos que use [Azure AD Connect](/active-directory/active-directory-aadconnectsync-whatis) para conectar sus directorios locales con Azure Active Directory, pero puede usar cualquier método de sincronización de directorios con el que se obtenga el mismo resultado.

-   Grupos habilitados para correo en la nube que usará con Azure Information Protection. Pueden ser grupos integrados o grupos creados de forma manual que contengan usuarios que usarán documentos y correos electrónicos protegidos.

    Si tiene Exchange Online, puede crear y usar grupos habilitados para correo mediante el centro de administración de Exchange. Si tiene AD DS y va a sincronizar con Azure AD, puede crear y usar grupos habilitados para correo que sean grupos de seguridad o grupos de distribución.

### <a name="group-membership-caching"></a>Caché de pertenencia al grupo

Por motivos de rendimiento, el servicio Azure Rights Management almacena en caché la pertenencia al grupo. Esto significa que cualquier cambio realizado en la pertenencia al grupo puede tardar hasta tres horas en aplicarse y este período está sujeto a cambios. No olvide incluir este retraso en los cambios o pruebas que realice cuando use grupos en la configuración del servicio Azure Rights Management, como la configuración de [plantillas personalizadas](../deploy-use/configure-custom-templates.md) o al usar un grupo para la [característica de superusuario](../deploy-use/configure-super-users.md). 

### <a name="considerations-if-email-addresses-change"></a>Consideraciones si las direcciones de correo electrónico cambian

Al configurar los derechos de uso para usuarios o grupos y seleccionarlos por su nombre para mostrar, la selección se guarda y usa la dirección de correo electrónico de ese objeto. Si posteriormente la dirección de correo electrónico cambia, la autorización de los usuarios seleccionados no se realizará correctamente.

Si las direcciones de correo electrónico cambian, se recomienda agregar la dirección de correo electrónico antigua como una dirección de correo electrónico de proxy (también conocida como un alias o dirección de correo electrónico alternativa) para el usuario o grupo, por lo que se conservan los derechos de uso que se asignaron previamente. Si no puede hacerlo, debe quitar el usuario o grupo de la configuración y seleccionarlo de nuevo para guardar la dirección de correo electrónico actualizada, de forma que el contenido recién protegido use la nueva dirección de correo electrónico.

Las plantillas de administración de derechos personalizadas son un ejemplo de dónde puede seleccionar usuarios o grupos mediante el nombre para mostrar para asignar derechos de uso. Los usuarios también pueden seleccionar usuarios y grupos por su nombre para mostrar cuando configuran permisos personalizados con el cliente de Azure Information Protection.

## <a name="activate-the-rights-management-service-for-data-protection"></a>Activar el servicio Rights Management para la protección de datos
Cuando esté preparado para empezar a proteger documentos y correos electrónicos, active el servicio Rights Management para habilitar esta tecnología. Para más información, consulte [Activación de Azure Rights Management](../deploy-use/activate-service.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


