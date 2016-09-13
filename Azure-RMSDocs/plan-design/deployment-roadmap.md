---
title: "Mapa de ruta de implementación de Azure Rights Management | Azure RMS"
description: "Use estos pasos para prepararse para la implementación y administración de Azure Rights Management (Azure RMS) en la organización."
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ada00b6f6298e7d359c73eb38dfdac169eacb708
ms.openlocfilehash: 06f07ad5c8c0f0e1f8511051a84af0b1f8e35647


---

# Mapa de ruta de implementación de Azure Rights Management

>*Se aplica a: Azure Rights Management, Office 365*

Use los siguientes pasos para prepararse para la implementación y administre Azure Rights Management (Azure RMS) en su organización.

Sin embargo, si solo quiere probar rápidamente Azure RMS por su cuenta, en lugar de implementarlo en un entorno de producción, consulte [Quick start tutorial for Azure Rights Management](../get-started/quick-start-tutorial.md) (Tutorial de inicio rápido de Azure Rights Management).

Para obtener una lista de escenarios específicos y los pasos de configuración asociados, así como documentación para el usuario final, consulte la [Guía de implementación rápida de Azure Rights Management](../get-started/rapid-deployment-guide.md).

> [!IMPORTANT]
> Antes de realizar los siguientes pasos, asegúrese de que ha examinado los [requisitos para Azure Rights Management](../get-started/requirements-azure-rms.md).

## Paso 1: Confirme que tiene una suscripción que incluye Azure Rights Management.
Hay más de un tipo de suscripción que incluye [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]. Consulte la sección [Cloud subscriptions that support Azure RMS](../get-started/requirements-subscriptions.md) (Suscripciones de nube que admiten Azure RMS) y compruebe que la suscripción incluye la funcionalidad que desea usar en su organización; para ello, consulte la tabla que aparece en [Comparison of Rights Management Services (RMS) Offerings](https://technet.microsoft.com/dn858608) (Comparación de ofertas de Rights Management Services (RMS)). Debe asignar una licencia de esta suscripción a cada usuario de su organización que vaya a proteger archivos y correos electrónicos con Azure RMS.

## Paso 2: Preparar tu cuenta de inquilino para usar Rights Management
Antes de empezar a usar [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], ten en cuenta los siguientes pasos previos:

1.  Asegúrese de que el inquilino de Azure o de Office 365 contenga las cuentas de usuario y los grupos que se usarán en Azure RMS para autenticar a los usuarios de su organización. Si es necesario, cree estas cuentas y grupos, o sincronícelos desde el directorio local. Para más información, consulte [Preparing for Azure Rights Management](prepare.md) (Preparación para Azure Rights Management).

2.  Decide si quieres que Microsoft administre tu clave de inquilino (la predeterminada) o generarla y administrarla tú mismo (conocido como Aportar tu propia clave, o BYOK). Tenga en cuenta que actualmente, no se puede usar BYOK si se usa Exchange Online. Para más información, consulte [Planeamiento e implementación de la clave de inquilino de Azure Rights Management](plan-implement-tenant-key.md).

3.  Instalación del módulo de Windows PowerShell para [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] en al menos un equipo que tenga acceso a Internet. Este paso puedes hacerlo ahora o más tarde. Para más información, consulte [Instalación de Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md).

4.  Si actualmente está utilizando servicios locales de Rights Management, realice una migración para mover las claves, las plantillas y las direcciones URL a la nube. Para más información, consulte [Migrating from AD RMS to Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) (Migración de AD RMS a Azure Rights Management).

5.  Activa Rights Management para que puedas empezar a usar el servicio. Si se requiere una implementación en fases, configure los controles de incorporación de usuarios para restringir el uso a usuarios específicos. Para más información, consulte [Activación de Azure Rights Management](../deploy-use/activate-service.md).

De forma opcional, considera configurar lo siguiente:

-   Plantillas personalizadas si las plantillas de directiva de derechos predeterminadas no son suficientes para tu organización. Este paso puedes hacerlo ahora o más tarde. Para más información, consulte [Configuración de plantillas personalizadas para Azure Rights Management](../deploy-use/configure-custom-templates.md).

-   Registro de uso para que puedas controlar cómo se usa Rights Management en tu organización. Este paso puedes hacerlo ahora o más tarde. Para más información, consulte [Registro y análisis del uso de Azure Rights Management](../deploy-use/log-analyze-usage.md).

## Paso 3: Configure las aplicaciones y servicios para Rights Management.
La configuración de sus aplicaciones y servicios puede incluir la instalación de la aplicación Rights Management sharing y la habilitación de la compatibilidad con las características de Information Rights Management (IRM) en SharePoint Online o Exchange Online. Para más información, consulte [Configuración de plantillas personalizadas para Azure Rights Management](../deploy-use/configure-applications.md).

Si tiene servicios de TI existentes que necesita para inspeccionar los archivos que se van a proteger con Azure RMS, como soluciones de prevención de pérdida de datos (DPL), puertas de enlace de cifrado de contenido (CEG) y productos antimalware, configure las cuentas de servicio como superusuarios para Azure RMS. Para obtener más información, consulte [Configuring super users for Azure Rights Management and discovery services or data recovery](../deploy-use/configure-super-users.md) (Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos).

Para proteger o desproteger en masa todos los tipos de archivo, instale la herramienta de protección de RMS, que usa el módulo de PowerShell de protección de RMS. Para más información, consulte [Cmdlets de protección de RMS](https://msdn.microsoft.com/library/mt433195.aspx).

Si tienes servicios locales que quieres usar con Azure Rights Management, instala y configura el conector de Rights Management. Para más información, consulte [Implementación del conector de Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## Paso 4: Publicación y consumo de contenido protegido por derechos
Ahora está listo para publicar y consumir contenido protegido, y registrar cómo su empresa usa Rights Management. Para más información, consulte [Ayuda a los usuarios para proteger archivos mediante Azure Rights Management](../deploy-use/help-users.md) y [Registro y análisis del uso de Azure Rights Management](../deploy-use/log-analyze-usage.md).

Si le interesa proteger automáticamente los archivos mediante la infraestructura de clasificación de archivos en un servidor de archivos basado en Windows, consulte [Protección de RMS con la infraestructura de clasificación de archivos (FCI) de Windows Server](../rms-client/configure-fci.md).

## Paso 5: Administrar Rights Management para tu cuenta de inquilino según sea necesario
En cuanto empieces a usar [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], puedes encontrar útil el módulo de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para Windows PowerShell a fin de ayudar a crear scripts para cambios administrativos o a automatizarlos. Para más información, consulte [Administración de Azure Rights Management mediante Windows PowerShell](../deploy-use/administer-powershell.md).





<!--HONumber=Aug16_HO4-->


