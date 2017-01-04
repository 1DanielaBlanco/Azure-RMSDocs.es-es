---
title: Activar Azure Rights Management | Azure Information Protection
description: "El servicio Azure Rights Management debe activarse antes de que la organización pueda empezar a proteger documentos y correos electrónicos con aplicaciones y servicios que admiten esta solución de protección de información."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/09/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ced42d0856b992d3539575d64f5a49706f1768b3
ms.openlocfilehash: 80fd7a7ce1ac6b7a8b2867729dd3e09e9b106d9b


---

# <a name="activating-azure-rights-management"></a>Activar Rights Management de Azure

>*Se aplica a: Azure Information Protection, Office 365*

Cuando el servicio Azure Rights Management para Azure Information Protection se activa, la organización puede empezar a proteger datos importantes con aplicaciones y servicios que admiten esta solución de protección de información. Los administradores también pueden administrar y supervisar los correos electrónicos y archivos protegidos que posee su organización. Este servicio debe habilitarse antes de poder empezar a usar las características de Information Rights Management (IRM) en Office, SharePoint y Exchange, y de proteger los archivos confidenciales o con información importante.

Si quiere obtener más información sobre el servicio Azure Rights Management antes de activarlo (por ejemplo, qué problemas empresariales soluciona, algunos casos de uso habitual y su funcionamiento), vea [¿Qué es Azure Rights Management?](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> Antes de activar [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], asegúrese de que la organización tenga un plan de servicios que incluya la protección de datos de Azure Rights Management. De lo contrario, no podrá activar Azure Rights Management.
>
> Debe disponer de un [plan Premium de Azure Information Protection](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing) o de un [plan de Office 365 que incluya Rights Management](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

Una vez activado el servicio Azure Rights Management, todos los usuarios de la organización podrán aplicar la protección de la información a los archivos, y todos los usuarios podrán abrir (consumir) los archivos que se hayan protegido con el servicio Azure Rights Management. Sin embargo, si lo prefiere, puede usar controles de incorporación para restringir quién puede aplicar la protección de la información, a fin de realizar una implementación por fases. Para más información, consulte la sección [Configuración de controles de incorporación para una implementación por fases](#configuring-onboarding-controls-for-a-phased-deployment) de este artículo.

Para obtener instrucciones sobre cómo activar el servicio de Rights Management desde su portal de administración, seleccione si va a usar el Centro de administración de Office 365 (versión preliminar o estándar) o el Portal de administración de Azure clásico:


- [Centro de administración de Office 365: versión preliminar](activate-office365-preview.md)
- [Centro de administración de Office 365: clásico](activate-office365-classic.md)
- [Portal de Azure clásico](activate-azure-classic.md)

O bien, puede usar PowerShell para activar [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]:

1. Instale la herramienta de administración de Azure Rights Management, que instala el módulo de administración de Azure Rights Management. Para obtener instrucciones, vea [Instalación de Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md).

2. Desde una sesión de PowerShell, ejecute [Connect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629415.aspx) y, cuando se le pida, proporcione los detalles de la cuenta de administrador global para el inquilino de Azure Information Protection.

3. Ejecute [Enable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629412.aspx), con el que se activará el servicio Azure Rights Management.

## <a name="configuring-onboarding-controls-for-a-phased-deployment"></a>Configuración de controles de incorporación para una implementación por fases
Si no quiere que todos los usuarios puedan proteger los archivos de forma inmediata con Azure Rights Management, puede configurar controles de incorporación de usuarios mediante el comando [Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx) de PowerShell. Puede ejecutar este comando antes o después de activar el servicio Azure Rights Management.

> [!IMPORTANT]
> Para usar este comando, debe tener al menos la versión **2.1.0.0** del [módulo Azure Rights Management PowerShell](http://go.microsoft.com/fwlink/?LinkId=257721).
>
> Para comprobar la versión que tiene instalada, ejecute: **(Get-Module aadrm –ListAvailable).Version**

Por ejemplo, si en principio desea que solo los administradores del grupo "Departamento de TI" (con un identificador de objeto de fbb99ded-32a0-45f1-b038-38b519009503) puedan proteger el contenido con fines de prueba, use el comando siguiente:

```
Set-AadrmOnboardingControlPolicy – SecurityGroupObjectId fbb99ded-32a0-45f1-b038-38b519009503
```
Tenga en cuenta que para esta opción de configuración, debe especificar un grupo; no puede especificar usuarios individuales. Para obtener el identificador de objeto del grupo, use Azure AD PowerShell (por ejemplo, para la [versión 1.0](https://msdn.microsoft.com/library/azure/jj151815\(v=azure.98\).aspx) del módulo, use el comando [Get-MsolGroup](https://msdn.microsoft.com/library/azure/dn194130\(v=azure.98\).aspx)).

O bien, si quiere asegurarse de que solo los usuarios con licencias adecuadas para usar Azure Information Protection puedan proteger el contenido:

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $true
```

Para obtener más información sobre este cmdlet y ejemplos adicionales, consulte la ayuda de [Set-AadrmOnboardingControlPolicy](https://msdn.microsoft.com/library/dn857521.aspx).

Al usar estos controles de incorporación, todos los usuarios de la organización podrán consumir siempre el contenido protegido por el subconjunto de usuarios, pero no podrán aplicar la protección de la información ellos mismos desde aplicaciones cliente. Por ejemplo, no verán en sus clientes de Office las plantillas predeterminadas publicadas automáticamente al activar el servicio Azure Rights Management ni las plantillas personalizadas que se puedan configurar.  Las aplicaciones de lado del servidor, como Exchange, pueden implementar sus propios controles por usuario para que la integración de Rights Management logre el mismo resultado.


## <a name="next-steps"></a>Pasos siguientes
Ahora que ha activado [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] para su organización, siga el [Mapa de ruta de implementación de Azure Information Protection](../plan-design/deployment-roadmap.md) y compruebe si hay otros pasos de configuración que puedan ser necesarios antes de desplegar Azure Information Protection en usuarios y administradores. 

Por ejemplo, es posible que quiera usar [plantillas personalizadas](configure-custom-templates.md) para facilitar a los usuarios la aplicación de la protección de la información a los archivos, la conexión a los servidores locales para usar [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] a través de la instalación del [conector Rights Management](deploy-rms-connector.md) y la implementación de la [aplicación Rights Management sharing](../rms-client/sharing-app-windows.md) que es compatible con la protección de todos los tipos de archivo en todos los dispositivos. 

Servicios de Office, como Exchange Online y SharePoint Online requieren configuración adicional para poder usar sus características de Information Rights Management (IRM). Para obtener información sobre cómo sus aplicaciones funcionan con el servicio de Rights Management, vea [Compatibilidad de aplicaciones con el servicio Azure Rights Management](../understand-explore/applications-support.md).

## <a name="comments"></a>Comentarios

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Dec16_HO2-->


