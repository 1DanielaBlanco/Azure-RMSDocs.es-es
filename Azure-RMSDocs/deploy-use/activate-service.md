---
title: "Activación de Azure Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/16/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: bf5e3561ef24d8f44e791ff7bdc8450a73f79705
ms.openlocfilehash: d66e4e6bca253bc2bf9d12ba22ed0202cba2edaf


---

# Activar Rights Management de Azure

*Se aplica a: Azure Rights Management, Office 365*

Cuando activa [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS), su organización puede empezar a proteger datos importantes con aplicaciones y servicios que admiten esta solución de protección de información. Los administradores también pueden administrar y supervisar los correos electrónicos y archivos protegidos que posee su organización. Debe habilitar [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para poder empezar a usar las características de Information Rights Management (IRM) en Office, SharePoint y Exchange y proteger los archivos confidenciales o con información importante.

Si desea obtener más información sobre Azure Rights Management antes de activar el servicio (por ejemplo, problemas empresariales que soluciona, algunos casos de uso habitual y su funcionamiento), consulte [¿Qué es Azure Rights Management?](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> Antes de activar [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], asegúrese de que la organización tenga un plan de servicios que incluya los de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]. De lo contrario, no podrá activar Azure RMS.
>
> Para información, consulte la sección [Suscripciones en la nube que son compatibles con Azure RMS](../get-started/requirements-subscriptions.md).

Una vez activado Azure RMS, todos los usuarios de la organización podrán aplicar la protección de la información a los archivos y abrir (consumir) los archivos protegidos con Azure RMS. Sin embargo, si lo prefiere, puede usar controles de incorporación para restringir quién puede aplicar la protección de la información, a fin de realizar una implementación por fases. Para más información, consulte la sección [Configuración de controles de incorporación para una implementación por fases](#configuring-onboarding-controls-for-a-phased-deployment) de este artículo.

Para obtener instrucciones sobre cómo activar Rights Management desde su portal de administración, seleccione si va a usar el Centro de administración de Office 365 (versión preliminar o estándar) o el Portal de administración de Azure clásico:


- [Centro de administración de Office 365: versión preliminar](activate-office365-preview.md)
- [Centro de administración de Office 365: clásico](activate-office365-classic.md)
- [Portal de Azure clásico](activate-azure-classic.md)

O bien, puede usar Windows PowerShell para activar [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]:

1. Instale la herramienta de administración de Azure Rights Management, que instala el módulo de administración de Azure Rights Management. Para obtener instrucciones, vea [Instalación de Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md).

2. Desde una sesión de Windows PowerShell, ejecute [Connect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629415.aspx) y, cuando se le solicite, proporcione los detalles de la cuenta de administrador global para el inquilino de Azure RMS.

3. Ejecute [Enable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629412.aspx), que activa el servicio Azure RMS.

## Configuración de controles de incorporación para una implementación por fases
Si no desea que todos los usuarios puedan proteger los archivos de forma inmediata con Azure RMS, puede configurar controles de incorporación para el usuario mediante el comando [Set AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx) de Windows PowerShell. Puede ejecutar este comando antes o después de activar Azure RMS.

> [!IMPORTANT]
> Para usar este comando, debe tener al menos la versión **2.1.0.0** del [módulo Azure RMS Windows PowerShell](http://go.microsoft.com/fwlink/?LinkId=257721).
>
> Para comprobar la versión que tiene instalada, ejecute: **(Get-Module aadrm –ListAvailable).Version**

Por ejemplo, si en principio desea que solo los administradores del grupo "Departamento de TI" (con un identificador de objeto de fbb99ded-32a0-45f1-b038-38b519009503) puedan proteger el contenido con fines de prueba, use el comando siguiente:

```
Set-AadrmOnboardingControlPolicy – SecurityGroupObjectId fbb99ded-32a0-45f1-b038-38b519009503
```
Tenga en cuenta que para esta opción de configuración, debe especificar un grupo; no puede especificar usuarios individuales.

O bien, si desea asegurarse de que solo los usuarios con licencias adecuadas para usar Azure RMS puedan proteger el contenido:

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $true
```
Al usar estos controles de incorporación, todos los usuarios de la organización podrán consumir siempre el contenido protegido por el subconjunto de usuarios, pero no podrán aplicar la protección de la información ellos mismos desde aplicaciones cliente. Por ejemplo, no verán en sus clientes de Office las plantillas predeterminadas publicadas automáticamente al activar Azure RMS o las plantillas personalizadas que pueda configurar.  Las aplicaciones de servidor, como Exchange, pueden implementar sus propios controles por usuario para la integración de RMS lograr el mismo resultado.


## Pasos siguientes
Ahora que ha activado [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] para su organización, use [Plan para la implementación de Azure Rights Management](../plan-design/deployment-roadmap.md) para comprobar si hay otros pasos de configuración que puedan ser necesarios antes de revertir [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] a usuarios y administradores. 

Por ejemplo, es posible que desee usar [plantillas personalizadas](configure-custom-templates.md) para facilitar a los usuarios la aplicación de la protección de la información a los archivos, la conexión a los servidores locales para utilizar [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] a través de la instalación del [conector RMS](deploy-rms-connector.md) y la implementación de la [aplicación Rights Management sharing](../rms-client/sharing-app-windows.md) que es compatible con la protección de todos los tipos de archivo en todos los dispositivos. 

Servicios de Office, como Exchange Online y SharePoint Online requieren configuración adicional para poder usar sus características de Information Rights Management (IRM). Para obtener información sobre cómo sus aplicaciones funcionan con [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], consulte [Cómo son compatibles las aplicaciones con Azure Rights Management](../understand-explore/applications-support.md).




<!--HONumber=Jun16_HO4-->


