---
title: 'Migración de AD RMS-Azure Information Protection: fase 1'
description: Fase 1 de la migración desde AD RMS a Azure Information Protection, donde se describen los pasos del 1 al 3 de la migración de AD RMS a Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/11/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d954d3ee-3c48-4241-aecf-01f4c75fa62c
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 683609cd2da2d13e11f92599813753a2a4747bd2
ms.sourcegitcommit: 0fda9ea4a7b91d4bb3a9e4f9d5cc4106ce1e2d43
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2018
ms.locfileid: "38973378"
---
# <a name="migration-phase-1---preparation"></a>Fase 1 de la migración: preparación

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Use la información siguiente para la fase 1 de la migración desde AD RMS a Azure Information Protection. En estos procedimientos se describen los pasos del 1 al 3 de la [Migración desde AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md) y se prepara el entorno para la migración sin afectar a los usuarios.


## <a name="step-1-install-the-aadrm-powershell-module-and-identify-your-tenant-url"></a>Paso 1: Instalar el módulo de PowerShell para AADRM e identificar la dirección URL del inquilino

Instale el módulo de AADRM para que pueda configurar y administrar el servicio que proporciona la protección de datos para Azure Information Protection.

Para obtener instrucciones, vea [Instalación del módulo de PowerShell para AADRM](../deploy-use/install-powershell.md).

> [!NOTE]
> Si anteriormente ya ha descargado este módulo de Windows PowerShell, ejecute el comando siguiente para comprobar que su número de versión sea como mínimo **2.9.0.0**: `(Get-Module aadrm -ListAvailable).Version`

Para completar algunas de las instrucciones de migración, deberá conocer la dirección URL de servicio de Azure Rights Management de su inquilino, de modo que la pueda sustituir cuando vea referencias a la *\<dirección URL del inquilino\>*. La dirección URL de servicio de Azure Rights Management tiene el formato siguiente: **{GUID}.rms.[Región].aadrm.com**.

Por ejemplo: **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**.

### <a name="to-identify-your-azure-rights-management-service-url"></a>Para identificar la dirección URL de servicio de Azure Rights Management

1. Conéctese con el servicio de Azure Rights Management y, cuando se le pida, escriba las credenciales de administrador global de su inquilino:
    
        Connect-AadrmService
    
2. Obtenga la configuración de su inquilino:
    
        Get-AadrmConfiguration
    
3. Copie el valor mostrado para **LicensingIntranetDistributionPointUrl** y, de esta cadena, quite `/_wmcs\licensing`. 
    
    Lo que queda es la dirección URL del servicio Azure Rights Management para su inquilino de Azure Information Protection. Este valor se suele abreviar como *URL de inquilino* en las siguientes instrucciones de migración.
    
    Para comprobar que tiene el valor correcto, ejecute el siguiente comando de PowerShell:
    
            (Get-AadrmConfiguration).LicensingIntranetDistributionPointUrl -match "https:\/\/[0-9A-Za-z\.-]*" | Out-Null; $matches[0]

## <a name="step-2-prepare-for-client-migration"></a>Paso 2. Preparación para la migración de clientes

En el caso de la mayoría de las migraciones, no resulta práctico migrar todos los clientes a la vez, por lo que es probable que migre los clientes en lotes. Esto significa que, durante un período de tiempo, algunos clientes usarán Azure Information Protection y otros aún usarán AD RMS. Para admitir a los usuarios migrados y aún no migrados, use los controles de incorporación e implemente un script previo a la migración. Este paso es necesario durante el proceso de migración para que los usuarios que aún no se hayan migrado puedan consumir contenido protegido por los usuarios migrados que ahora usen Azure Rights Management.

1. Cree un grupo, por ejemplo, denominado **AIPMigrated**. Este grupo se puede crear en Active Directory y sincronizar en la nube, o se puede crear en Office 365 o Azure Active Directory. No asigne ningún usuario a este grupo en este momento. Los agregará al grupo en un paso posterior, cuando los usuarios se migren.

    Tome nota del identificador de objeto de este grupo. Para ello, puede usar Azure AD PowerShell. Por ejemplo, para la versión 1.0 del módulo, use el comando [Get-MsolGroup](/powershell/msonline/v1/Get-MsolGroup). También puede copiar el identificador de objeto del grupo de Azure Portal.

2. Configure este grupo para controles de incorporación para permitir que solo los usuarios de este grupo usen Azure Rights Management para proteger el contenido. Para ello, en una sesión de PowerShell, conéctese al servicio de Azure Rights Management y, cuando se le pida, especifique las credenciales de administrador global:

        Connect-Aadrmservice

    Después, configure este grupo para controles de incorporación. Para ello, sustituya el identificador de objeto de grupo por el que se muestra en este ejemplo y escriba **Y** para confirmar cuando se le pida:

        Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $False -SecurityGroupObjectId "fba99fed-32a0-44e0-b032-37b419009501" -Scope WindowsApp

3. [Descargue el siguiente archivo](https://go.microsoft.com/fwlink/?LinkId=524619) que contiene scripts de migración de cliente:
    
    **Migration-Scripts.zip**
    
4. Extraiga los archivos y siga las instrucciones de **Prepare-Client.cmd** de modo que contenga el nombre del servidor de la dirección URL de licencias de extranet del clúster de AD RMS. 
    
    Para buscar este nombre, en la consola de Active Directory Rights Management Services, haga clic en el nombre del clúster. En la información **Detalles del clúster**, copie el nombre del servidor del valor **Licencias** de la sección de direcciones URL de clúster de extranet. Por ejemplo: **rmscluster.contoso.com**.

    > [!IMPORTANT]
    > En las instrucciones se incluye cómo reemplazar las direcciones de ejemplo de **adrms.contoso.com** por las direcciones de sus servidores de AD RMS. Al hacerlo, asegúrese de que no haya ningún espacio adicional antes o después de las direcciones, ya que interrumpirá el script de migración y es muy difícil de identificar como la causa principal del problema. Algunas herramientas de edición agregan automáticamente un espacio después de pegar texto.
    >

5. Implemente este script en todos los equipos Windows para asegurarse de que, al empezar a migrar clientes, los clientes que aún queden por migrar sigan pudiendo comunicarse con AD RMS aunque consuman contenido protegido por clientes migrados que ahora usen el servicio de Azure Rights Management.

    Puede usar la directiva de grupo u otro mecanismo de implementación de software para implementar este script.

## <a name="step-3-prepare-your-exchange-deployment-for-migration"></a>Paso 3: Preparación de la implementación de Exchange para la migración

Si usa Exchange local o Exchange Online, es posible que haya integrado previamente Exchange con la implementación de AD RMS. En este paso, los configurará para que usen la configuración existente de AD RMS para admitir contenido protegido con Azure RMS. 

Asegúrese de que tiene la [dirección URL de servicio de Azure Rights Management del inquilino](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url) para que pueda reemplazar este valor por la *&lt;YourTenantURL&gt;* en los comandos siguientes. 

**Si ha integrado Exchange Online con AD RMS**, abra una sesión de PowerShell para Exchange Online y ejecute los siguientes comandos de PowerShell uno a uno, o en un script:

    $irmConfig = Get-IRMConfiguration
    $list = $irmConfig.LicensingLocation
    $list += "<YourTenantURL>/_wmcs/licensing"
    Set-IRMConfiguration -LicensingLocation $list
    Set-IRMConfiguration -internallicensingenabled $false
    Set-IRMConfiguration -internallicensingenabled $true 

**Si ha integrado Exchange local con AD RMS**: para cada organización de Exchange, agregue primero los valores del Registro en cada servidor de Exchange Server y, después, ejecute los comandos de PowerShell: 

Valores del Registro para Exchange 2013 y Exchange 2016:

**Ruta de acceso del Registro:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**Tipo:** Reg_SZ

**Valor:** https://\<Dirección URL del inquilino\>/_wmcs/licensing

**Datos:** https://\<Dirección URL de licencias de extranet de AD RMS\>/_wmcs/licensing

---

Valores del Registro para Exchange 2010:

**Ruta de acceso del Registro:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Tipo:** Reg_SZ

**Valor:** https://\<Dirección URL del inquilino\>/_wmcs/licensing

**Datos:** https://\<Dirección URL de licencias de extranet de AD RMS>/_wmcs/licensing

---

Comandos de PowerShell para ejecutar de uno por uno, o en un script

    $irmConfig = Get-IRMConfiguration
    $list = $irmConfig.LicensingLocation
    $list += "<YourTenantURL>/_wmcs/licensing"
    Set-IRMConfiguration -LicensingLocation $list
    Set-IRMConfiguration -internallicensingenabled $false
    Set-IRMConfiguration -RefreshServerCertificates
    Set-IRMConfiguration -internallicensingenabled $true
    IISReset


Después de ejecutar estos comandos para Exchange Online o Exchange local, si la implementación de Exchange se ha configurado para admitir contenido protegido por AD RMS, también admitirá contenido protegido por Azure RMS después de la migración. La implementación de Exchange seguirá usando AD RMS para admitir contenido protegido hasta un paso posterior de la migración.


## <a name="next-steps"></a>Pasos siguientes
Vaya a [Fase 2: configuración del lado servidor para AD RMS](migrate-from-ad-rms-phase2.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
