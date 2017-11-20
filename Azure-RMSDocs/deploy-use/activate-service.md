---
title: "Activación de Azure Rights Management - AIP"
description: "El servicio Azure Rights Management debe activarse antes de que la organización pueda empezar a proteger documentos y correos electrónicos con aplicaciones y servicios que admiten esta solución de protección de información."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/15/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 75c0bf83c84cb8b5d2116b05dbf2def790562b4e
ms.sourcegitcommit: fd3932ab19a00229b56efc3e301abaf9cff3f70b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="activating-azure-rights-management"></a>Activar Rights Management de Azure

>*Se aplica a: Azure Information Protection, Office 365*

> [!NOTE]
> Esta información de configuración es para los administradores responsables de un servicio que se aplica a todos los usuarios de una organización. Si busca ayuda e información para usar la funcionalidad de Rights Management con una aplicación específica o cómo abrir un archivo o un correo electrónico protegido por derechos, use la ayuda y las instrucciones que se incluyen con la aplicación.
>
> Por ejemplo, para las aplicaciones de Office, haga clic en el icono de Ayuda y escriba términos de búsqueda como **Rights Management** o **IRM**. Para el cliente de Azure Information Protection para Windows, vea la [Guía del usuario de Azure Information Protection](../rms-client/client-user-guide.md).
>
> Para obtener soporte técnico y consultar otras cuestiones sobre el servicio, vea la información sobre [Opciones de soporte y recursos de la comunidad](../get-started/information-support.md#support-options-and-community-resources).

Cuando el servicio Azure Rights Management para Azure Information Protection se activa para el inquilino, la organización puede empezar a proteger datos importantes con aplicaciones y servicios que admiten esta solución de protección de información. Los administradores también pueden administrar y supervisar los correos electrónicos y archivos protegidos que posee su organización. Este servicio debe habilitarse antes de poder empezar a usar las características de Information Rights Management (IRM) en Office, SharePoint y Exchange, y de proteger los archivos confidenciales o con información importante.

Si quiere obtener más información sobre el servicio Azure Rights Management antes de activarlo (por ejemplo, qué problemas empresariales soluciona, algunos casos de uso habitual y su funcionamiento), vea [¿Qué es Azure Rights Management?](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> No active el servicio Azure Rights Management si tiene Active Directory Rights Management Services (AD RMS) implementado en la organización. [Más información](prepare-environment-adrms.md).

Antes de activar [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], asegúrese de que la organización tenga un plan de servicios que incluya la protección de datos de Azure Rights Management. De lo contrario, no podrá activar Azure Rights Management. Debe tener uno de los siguientes elementos:

- Un [plan de Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing). 

- Un [plan de Office 365 que incluya Rights Management](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

Una vez activado el servicio Azure Rights Management, todos los usuarios de la organización podrán aplicar la protección de la información a los archivos, y todos los usuarios podrán abrir (consumir) los archivos que se hayan protegido con el servicio Azure Rights Management. Sin embargo, si lo prefiere, puede usar controles de incorporación para restringir quién puede aplicar la protección de la información, a fin de realizar una implementación por fases. Para más información, consulte la sección [Configuración de controles de incorporación para una implementación por fases](#configuring-onboarding-controls-for-a-phased-deployment) de este artículo.

Para obtener instrucciones sobre cómo activar el servicio de Rights Management desde su portal de administración, seleccione si va a usar el Centro de administración de Office 365 o Azure Portal:

- [**Centro de administración de Office 365**](activate-office365.md): requiere una cuenta de administrador global.

- [**Azure Portal**](activate-azure.md): requiere una cuenta de administrador global o una [cuenta de administrador de seguridad](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles).

O bien, puede usar PowerShell para activar [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]:

1. Instale la herramienta de administración de Azure Rights Management, que instala el módulo de administración de Azure Rights Management. Para obtener instrucciones, vea [Instalación de Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md).

2. Desde una sesión de PowerShell, ejecute [Connect-AadrmService](/powershell/module/aadrm/connect-aadrmservice) y, cuando se le pida, proporcione los detalles de la cuenta de administrador global para el inquilino de Azure Information Protection.

3. Ejecute [Enable-Aadrm](/powershell/module/aadrm/enable-aadrm), con el que se activará el servicio Azure Rights Management.

## <a name="configuring-onboarding-controls-for-a-phased-deployment"></a>Configuración de controles de incorporación para una implementación por fases
Si no quiere que todos los usuarios puedan proteger los archivos de forma inmediata con Azure Rights Management, puede configurar controles de incorporación de usuarios mediante el comando [Set-AadrmOnboardingControlPolicy](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy) de PowerShell. Puede ejecutar este comando antes o después de activar el servicio Azure Rights Management.

> [!IMPORTANT]
> Para usar este comando, debe tener al menos la versión **2.1.0.0** del [módulo Azure Rights Management PowerShell](https://go.microsoft.com/fwlink/?LinkId=257721).
>
> Para comprobar la versión que tiene instalada, ejecute: **(Get-Module aadrm –ListAvailable).Version**

Por ejemplo, si en principio desea que solo los administradores del grupo "Departamento de TI" (con un identificador de objeto de fbb99ded-32a0-45f1-b038-38b519009503) puedan proteger el contenido con fines de prueba, use el comando siguiente:

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $False -SecurityGroupObjectId "fbb99ded-32a0-45f1-b038-38b519009503"
```

Tenga en cuenta que para esta opción de configuración, debe especificar un grupo; no puede especificar usuarios individuales. Para obtener el id. de objeto del grupo, puede usar Azure AD PowerShell. Por ejemplo, para la versión 1.0 del módulo, use el comando [Get-MsolGroup](/powershell/msonline/v1/get-msolgroup). También puede copiar el valor **Id. de objeto** del grupo de Azure Portal.

O bien, si quiere asegurarse de que solo los usuarios con licencias adecuadas para usar Azure Information Protection puedan proteger el contenido:

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $True
```

Cuando ya no necesite usar los controles de incorporación, tanto si ha usado la opción de licencias o de grupo, ejecute:

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $False
```


Para obtener más información sobre este cmdlet y ejemplos adicionales, consulte la ayuda de [Set-AadrmOnboardingControlPolicy](/powershell/aadrm/vlatest/set-aadrmonboardingcontrolpolicy).

Al usar estos controles de incorporación, todos los usuarios de la organización podrán consumir siempre el contenido protegido por el subconjunto de usuarios, pero no podrán aplicar la protección de la información ellos mismos desde aplicaciones cliente. Por ejemplo, no verán en sus clientes de Office las plantillas predeterminadas publicadas automáticamente al activar el servicio Azure Rights Management ni las plantillas personalizadas que se puedan configurar.  Las aplicaciones de lado del servidor, como Exchange, pueden implementar sus propios controles por usuario para que la integración de Rights Management logre el mismo resultado.


## <a name="next-steps"></a>Pasos siguientes
Ahora que ha activado [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] para su organización, siga el [Mapa de ruta de implementación de Azure Information Protection](../plan-design/deployment-roadmap.md) y compruebe si hay otros pasos de configuración que puedan ser necesarios antes de desplegar Azure Information Protection en usuarios y administradores. 

Por ejemplo, es posible que quiera usar [plantillas](configure-policy-templates.md) para facilitar a los usuarios la aplicación de la protección de la información a los archivos, la conexión a los servidores locales para usar [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] instalando el [conector Rights Management](deploy-rms-connector.md) y la implementación del [cliente de Azure Information Protection](../rms-client/aip-client.md), que es compatible con la protección de todos los tipos de archivo en todos los dispositivos. 

Servicios de Office, como Exchange Online y SharePoint Online requieren configuración adicional para poder usar sus características de Information Rights Management (IRM). Para obtener información sobre cómo sus aplicaciones funcionan con el servicio de Rights Management, vea [Compatibilidad de aplicaciones con el servicio Azure Rights Management](../understand-explore/applications-support.md).


[!INCLUDE[Commenting house rules](../includes/houserules.md)]