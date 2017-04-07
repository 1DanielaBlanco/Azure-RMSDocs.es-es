---
title: "Instalación de PowerShell para Azure Rights Management - AIP"
description: "Instrucciones para instalar Windows PowerShell para el servicio Azure Rights Management de Azure Information Protection. El nombre de este módulo es AADRM."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/27/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 5dae84eea9e67be75530d69b6124b97c7c29f8a3
ms.sourcegitcommit: 8ae83a9fc03bf2ee39ea758835ef52156f19784d
translationtype: HT
---
# <a name="installing-windows-powershell-for-azure-rights-management"></a>Instalación de Windows PowerShell para Azure Rights Management

>*Se aplica a: Azure Information Protection, Office 365*

Use la información siguiente para que el resulte más fácil instalar el módulo de Windows PowerShell para el servicio Azure Rights Management de Azure Information Protection.

Puede usar este módulo de PowerShell para administrar el servicio Azure Rights Management desde la línea de comandos con cualquier equipo que tenga una conexión a Internet y que cumpla los requisitos previos indicados en la sección siguiente. Windows PowerShell para [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] admite el uso de scripting para la automatización o puede que sea necesario para escenarios de configuración avanzada. Para más información acerca de las tareas de administración y las configuraciones que admite el módulo, consulte [Administración de Azure Rights Management mediante el uso de Windows PowerShell](administer-powershell.md).

## <a name="prerequisites"></a>Requisitos previos
Esta tabla enumera los requisitos previos para instalar Windows PowerShell para [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

|Requisito|Más información|
|---------------|--------------------|
|Una versión de Windows que admita el módulo de administración [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]|Revise la lista de sistemas operativos compatibles en la sección **Requisitos del sistema** de la [página de descargas de la herramienta de administración de Azure Rights Management](http://go.microsoft.com/fwlink/?LinkId=257721).|
|Versión mínima de Windows PowerShell: 2.0<br /><br /> |De forma predeterminada, la mayoría de sistemas operativos de Windows se instalan con una versión 2.0 de Windows PowerShell, como mínimo. Si necesita instalar esta versión mínima admitida, consulte [Instalación de Windows PowerShell 2.0](https://msdn.microsoft.com/library/ff637750.aspx).<br /><br />Sugerencia: Para confirmar la versión de Windows PowerShell que ejecuta, escriba `$PSVersionTable` en una sesión de PowerShell. <br /><br /> Si tiene esta versión mínima, necesitará cargar manualmente el módulo en la sesión de PowerShell ejecutando `Import-Module AADRM` antes de poder usar cualquier cmdlet del módulo de administración de Rights Management. Si tiene Windows PowerShell v3 y versiones posteriores, el módulo se carga automáticamente y no es necesario este comando adicional.|
|Versión mínima de Microsoft .NET Framework: 4.5<br /><br />Nota: Esta versión de Microsoft .NET Framework está incluida con los últimos sistemas operativos, por lo que solo tendrá que instalarla manualmente en el caso de que el sistema operativo del cliente sea anterior a Windows 8.0 o de que el sistema operativo del servidor sea anterior a Windows Server 2012.|Si la versión mínima de Microsoft .NET Framework todavía no está instalada, puede descargar [Microsoft .NET Framework 4.5](http://www.microsoft.com/download/details.aspx?id=30653).<br /><br />Esta versión mínima de Microsoft .NET Framework es necesaria para algunas de las clases que usa el módulo de administración de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].|

> [!NOTE]
> A partir de la versión 2.5.0.0 del módulo de administración de Rights Management, ya no es necesario usar Microsoft Online Services - Ayudante para el inicio de sesión.
> 
> Si tenía instalada una versión anterior del módulo de administración de Rights Management, use **Programas y características** para desinstalar **Administración de Windows Azure AD Rights Management** antes de instalar la versión más reciente.


## <a name="how-to-install-the-rights-management-administration-module"></a>Cómo instalar el módulo de administración Rights Management

1.  Vaya al Centro de descarga de Microsoft y [descargue la herramienta de administración de Azure Rights Management](https://go.microsoft.com/fwlink/?LinkId=257721), que contiene el módulo de administración de [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] para Windows PowerShell.

2.  En la carpeta local en la que has descargado y guardado el archivo de instalación de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], haz doble clic en el archivo ejecutable que has descargado para tu plataforma (WindowsAzureADRightsManagementAdministration_x64 o WindowsAzureADRightsManagementAdministration_x86.exe) para iniciar el asistente para la configuración de administración Azure AD Rights Management.

3.  Complete el asistente.

Ahora ya se ha instalado Windows PowerShell para [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] .

## <a name="next-steps"></a>Pasos siguientes
Inicie una sesión de Windows PowerShell y confirme la versión del módulo instalado. Esta comprobación es especialmente importante si actualizó desde una versión anterior:

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

Para poder ejecutar cualquier comando que configure el servicio de [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] necesita conectarse al servicio con el cmdlet [Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice). 

Cuando termine de ejecutar los comandos de configuración, como procedimiento recomendado, desconéctese del servicio con el cmdlet [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice) . Si no se desconecta, la conexión se desconecta automáticamente tras un período de inactividad. Debido al comportamiento de desconexión automática, es posible que deba conectarse de nuevo ocasionalmente en una sesión de PowerShell. 

> [!NOTE]
> Si el servicio Azure Rights Management aún no está activado, puede activarlo después de haberse conectado al servicio con el cmdlet [Enable-Aadrm](/powershell/aadrm/vlatest/enable-aadrm).


[!INCLUDE[Commenting house rules](../includes/houserules.md)]