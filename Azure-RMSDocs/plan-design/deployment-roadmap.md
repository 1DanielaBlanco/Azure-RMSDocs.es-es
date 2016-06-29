---
# required metadata

title: Mapa de ruta de implementación de Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Mapa de ruta de implementación de Azure Rights Management

*Se aplica a: Azure Rights Management, Office 365*

Use los siguientes pasos para prepararse para la implementación y administre Azure Rights Management (Azure RMS) en su organización.

Sin embargo, si solo quiere probar rápidamente Azure RMS por su cuenta, en lugar de implementarlo en un entorno de producción, consulte [Quick start tutorial for Azure Rights Management](../get-started/quick-start-tutorial.md) (Tutorial de inicio rápido de Azure Rights Management)..

Para obtener una lista de escenarios específicos y los pasos de configuración asociada, así como documentación para el usuario final, consulte la [Rapid deployment guide for Azure Rights Management](../get-started/rapid-deployment-guide.md) (Guía de implementación rápida de Azure Rights Management)..

> [!IMPORTANT]
> Antes de realizar los siguientes pasos, asegúrese de que ha examinado los [Requirements for Azure Rights Management](../get-started/requirements-azure-rms.md) (Requisitos de Azure Rights Management)..

## Paso 1: Confirme que tiene una suscripción que incluye Azure Rights Management.
Hay más de un tipo de suscripción que incluye [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]. Consulte la sección [Cloud subscriptions that support Azure RMS](../get-started/requirements-subscriptions.md) (Suscripciones de nube que admiten Azure RMS) y compruebe que la suscripción incluye la funcionalidad que desea usar en su organización; para ello, consulte la tabla que aparece en [Comparison of Rights Management Services (RMS) Offerings](https://technet.microsoft.com/dn858608) (Comparación de ofertas de Rights Management Services (RMS)). Debe asignar una licencia de esta suscripción a cada usuario de su organización que vaya a proteger archivos y correos electrónicos con Azure RMS.

## Paso 2: Preparar tu cuenta de inquilino para usar Rights Management
Antes de empezar a usar [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], ten en cuenta los siguientes pasos previos:

1.  Asegúrese de que el inquilino de Azure o de Office 365 contenga las cuentas de usuario y los grupos que se usarán en Azure RMS para autenticar a los usuarios de su organización. Si es necesario, cree estas cuentas y grupos, o sincronícelos desde el directorio local. Para obtener más información, consulte [Preparing for Azure Rights Management](prepare.md) (Preparación para Azure Rights Management)..

2.  Decide si quieres que Microsoft administre tu clave de inquilino (la predeterminada) o generarla y administrarla tú mismo (conocido como Aportar tu propia clave, o BYOK). Tenga en cuenta que actualmente, no se puede usar BYOK si se usa Exchange Online. Para obtener más información, consulte [Planning and implementing your Azure Rights Management tenant key](plan-implement-tenant-key.md) (Planeación e implementación de la clave de inquilino de Azure Rights Management)..

3.  Instalación del módulo de Windows PowerShell para [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] en al menos un equipo que tenga acceso a Internet. Este paso puedes hacerlo ahora o más tarde. Para obtener más información, vea [Installing Windows PowerShell for Azure Rights Management](../deploy-use/install-powershell.md) (Instalación de Windows PowerShell para Azure Rights Management)..

4.  Si actualmente está utilizando servicios locales de Rights Management, realice una migración para mover las claves, las plantillas y las direcciones URL a la nube. Para obtener más información, consulte [Migrating from AD RMS to Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) (Migración de AD RMS a Azure Rights Management)..

5.  Activa Rights Management para que puedas empezar a usar el servicio. Si se requiere una implementación en fases, configure los controles de incorporación de usuarios para restringir el uso a usuarios específicos. Para obtener más información, consulte [Activating Azure Rights Management](../deploy-use/activate-service.md) (Activar Azure Rights Management)..

De forma opcional, considera configurar lo siguiente:

-   Plantillas personalizadas si las plantillas de directiva de derechos predeterminadas no son suficientes para tu organización. Este paso puedes hacerlo ahora o más tarde. Para obtener más información, consulte [Configuring custom templates for Azure Rights Management](../deploy-use/configure-custom-templates.md) (Configurar plantillas personalizadas para Azure Rights Management)..

-   Registro de uso para que puedas controlar cómo se usa Rights Management en tu organización. Este paso puedes hacerlo ahora o más tarde. Para obtener más información, consulte [Logging and analyzing Azure Rights Management usage](../deploy-use/log-analyze-usage.md) (Registro y análisis del uso de Azure Rights Management)..

## Paso 3: Configure las aplicaciones y servicios para Rights Management.
La configuración de sus aplicaciones y servicios puede incluir la instalación de la aplicación Rights Management sharing y la habilitación de la compatibilidad con las características de Information Rights Management (IRM) en SharePoint Online o Exchange Online. Para obtener más información, consulte [Configuring applications for Azure Rights Management](../deploy-use/configure-applications.md) (Configuración de aplicaciones para Azure Rights Management)..

Si tiene servicios de TI existentes que necesita para inspeccionar los archivos que se van a proteger con Azure RMS, como soluciones de prevención de pérdida de datos (DPL), puertas de enlace de cifrado de contenido (CEG) y productos antimalware, configure las cuentas de servicio como superusuarios para Azure RMS. Para obtener más información, consulte [Configuring super users for Azure Rights Management and discovery services or data recovery](../deploy-use/configure-super-users.md) (Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos)..

Para proteger o desproteger en masa todos los tipos de archivo, instale la herramienta de protección de RMS, que usa el módulo de PowerShell de protección de RMS. Para obtener más información, consulte [RMS Protection Cmdlets](https://msdn.microsoft.com/library/mt433195.aspx) (Cmdlets de protección de RMS)..

Si tienes servicios locales que quieres usar con Azure Rights Management, instala y configura el conector de Rights Management. Para obtener más información, consulte [Deploying the Azure Rights Management connector](../deploy-use/deploy-rms-connector.md) (Implementación del conector de Azure Rights Management)..

## Paso 4: Publicación y consumo de contenido protegido por derechos
Ahora está listo para publicar y consumir contenido protegido, y registrar cómo su empresa usa Rights Management. Para obtener más información, consulte [Helping users to protect files by using Azure Rights Management](../deploy-use/help-users.md) (Ayudar a los usuarios para proteger archivos mediante Azure Rights Management) y [Logging and analyzing Azure Rights Management usage](../deploy-use/log-analyze-usage.md) (Registro y análisis del uso de Azure Rights Management)..

Si le interesa proteger automáticamente los archivos mediante la infraestructura de clasificación de archivos en un servidor de archivos basado en Windows, consulte [RMS protection with Windows Server File Classification Infrastructure (FCI)](../rms-client/configure-fci.md) (Protección de RMS con la infraestructura de clasificación de archivos [FCI] de Windows Server)..

## Paso 5: Administrar Rights Management para tu cuenta de inquilino según sea necesario
En cuanto empieces a usar [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], puedes encontrar útil el módulo de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para Windows PowerShell a fin de ayudar a crear scripts para cambios administrativos o a automatizarlos. Para obtener más información, consulte [Administering Azure Rights Management by using Windows PowerShell](../deploy-use/administer-powershell.md) (Administración de Azure Rights Management mediante Windows PowerShell)..




<!--HONumber=May16_HO2-->


