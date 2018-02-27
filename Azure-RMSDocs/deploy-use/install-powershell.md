---
title: Instalar PowerShell para AADRM - AIP
description: "Instrucciones para instalar Windows PowerShell para el servicio Azure Rights Management de Azure Information Protection. El nombre de este módulo es AADRM."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/20/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 757901d4c16b36dfe14e31f5ab9910c47b0b1917
ms.sourcegitcommit: 31c79d948ec3089a4dc65639f1842c07c7aecba6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/20/2018
---
# <a name="installing-the-aadrm-powershell-module"></a>Instalación del módulo de PowerShell para AADRM

>*Se aplica a: Azure Information Protection, Office 365*

Use la información siguiente para que el resulte más fácil instalar el módulo de Windows PowerShell para el servicio Azure Rights Management de Azure Information Protection. El nombre de este módulo es AADRM.

Puede usar este módulo de PowerShell para administrar el servicio Azure Rights Management desde la línea de comandos con cualquier equipo que tenga una conexión a Internet y que cumpla los requisitos previos indicados en la sección siguiente. Windows PowerShell para [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] admite el uso de scripting para la automatización o puede que sea necesario para escenarios de configuración avanzada. Para más información acerca de las tareas de administración y las configuraciones que admite el módulo, consulte [Administración de Azure Rights Management mediante el uso de Windows PowerShell](administer-powershell.md).

## <a name="prerequisites"></a>Requisitos previos
En esta tabla se muestran los requisitos previos para instalar y usar el módulo de PowerShell para AADRM para el servicio de Azure Rights Management de Azure Information Protection.

|Requisito|Más información|
|---------------|--------------------|
|Versión mínima de Windows PowerShell: 3.0|Para confirmar la versión de Windows PowerShell que ejecuta, escriba `$PSVersionTable` en una sesión de PowerShell. <br /><br /> Si necesita instalar una versión posterior de Windows PowerShell, vea [Actualización de Windows PowerShell existente](/powershell/scripting/setup/installing-windows-powershell#upgrading-existing-windows-powershell).|
|Versión mínima de Microsoft .NET Framework: 4.5<br /><br />Nota: Esta versión de Microsoft .NET Framework está incluida con los últimos sistemas operativos, por lo que solo tendrá que instalarla manualmente en el caso de que el sistema operativo del cliente sea anterior a Windows 8.0 o de que el sistema operativo del servidor sea anterior a Windows Server 2012.|Si la versión mínima de Microsoft .NET Framework todavía no está instalada, puede descargar [Microsoft .NET Framework 4.5](http://www.microsoft.com/download/details.aspx?id=30653).<br /><br />Esta versión mínima de Microsoft .NET Framework es necesaria para algunas de las clases que usa el módulo de AADRM.|

> [!NOTE]
> A partir de la versión 2.5.0.0 del módulo de AADRM, ya no es necesario usar Microsoft Online Services - Ayudante para el inicio de sesión.
> 
> Si tenía instalada una versión anterior del módulo de AADRM, use **Programas y características** para desinstalar **Administración de Windows Azure AD Rights Management** antes de instalar la versión más reciente.


## <a name="how-to-install-the-aadrm-module"></a>Cómo instalar el módulo de AADRM

El módulo AADRM se trasladará a la [Galería de PowerShell](/powershell/gallery/readme), pero también está disponible en el Centro de descarga de Microsoft durante un período limitado. 

### <a name="to-install-the-aadrm-module-from-the-powershell-gallery"></a>Para instalar el módulo de AADRM desde la Galería de PowerShell

Si no está familiarizado con la Galería de PowerShell, vea [Introducción a la Galería de PowerShell](/powershell/gallery/psgallery/psgallery_gettingstarted). Siga las instrucciones relacionadas con los requisitos de la galería, que incluyen la instalación del módulo PowerShellGet y el proveedor de NuGet.

Para ver detalles sobre el módulo de AADRM en la Galería de PowerShell, visite la [página de AADRM](https://www.powershellgallery.com/packages/AADRM).

Para instalar el módulo de AADRM, inicie una sesión de PowerShell y escriba:

    Install-Module -Name AADRM


### <a name="to-install-the-aadrm-module-from-the-microsoft-download-center"></a>Para instalar el módulo de AADRM desde el Centro de descarga de Microsoft

1. Vaya al Centro de descarga de Microsoft y busque la [herramienta de administración de Azure Rights Management](https://go.microsoft.com/fwlink/?LinkId=257721), que contiene el módulo de administración de [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] para Windows PowerShell.

2. Descargue y guarde el archivo instalador [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], **WindowsAzureADRightsManagementAdministration_x64**. A continuación, haga doble clic en este archivo para iniciar el Asistente para instalación del módulo de administración de Azure AD Rights Management.

3.  Siga los pasos del asistente, con el que se instala el módulo de PowerShell para AADRM.

## <a name="next-steps"></a>Pasos siguientes
En una sesión de Windows PowerShell, confirme la versión del módulo instalado. Esta comprobación es especialmente importante si actualizó desde una versión anterior:

```
(Get-Module AADRM –ListAvailable).Version
```

Nota: Si se produce un error en este comando, primero ejecute **Import-Module AADRM**.

Para ver qué cmdlets están disponibles, escriba lo siguiente:

```
Get-Command -Module AADRM
```

Utilice el comando `Get-Help <cmdlet_name>` para ver la Ayuda de un cmdlet específico y use el parámetro **-online** para ver la ayuda más reciente en el sitio de documentación de Microsoft. Por ejemplo:

```
Get-Help Connect-AadrmService -online
```

Para obtener más información:

-   Lista completa de cmdlets disponibles: [AADRM Module](/powershell/aadrm/vlatest/rightsmanagement)

-   Lista de los principales escenarios de configuración que admiten PowerShell: [administración de Azure Rights Management mediante Windows PowerShell](administer-powershell.md)

Para poder ejecutar cualquier comando que configure el servicio de [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] necesita conectarse al servicio con el cmdlet [Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice). Cuando termine de ejecutar los comandos de configuración, como procedimiento recomendado, desconéctese del servicio con el cmdlet [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice) . Si no se desconecta, la conexión se desconecta automáticamente tras un período de inactividad. Debido al comportamiento de desconexión automática, es posible que deba conectarse de nuevo ocasionalmente en una sesión de PowerShell. 

> [!NOTE]
> Si el servicio Azure Rights Management aún no está activado, puede activarlo después de haberse conectado al servicio con el cmdlet [Enable-Aadrm](/powershell/aadrm/vlatest/enable-aadrm).


[!INCLUDE[Commenting house rules](../includes/houserules.md)]