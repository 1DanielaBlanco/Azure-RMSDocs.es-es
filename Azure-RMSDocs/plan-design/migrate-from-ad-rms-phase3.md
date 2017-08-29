---
title: "Migración de AD RMS-Azure Information Protection: fase 3"
description: "Fase 3 de la migración desde AD RMS a Azure Information Protection, donde se describe el paso 7 de la migración de AD RMS a Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/22/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 35bd2d176cb71c54a489d4f4b8faca4d668a7867
ms.sourcegitcommit: c960f1d2140dea11e54cbeb37d53d1512621d90c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2017
---
# <a name="migration-phase-3---client-side-configuration"></a>Fase 3 de la migración: configuración del lado cliente

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Office 365*

Use la información siguiente para la fase 3 de la migración desde AD RMS a Azure Information Protection. En estos procedimientos se describe el paso 7 de la [Migración desde AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

## <a name="step-7-reconfigure-clients-to-use-azure-information-protection"></a>Paso 7. Volver a configurar los clientes para usar Azure Information Protection

Para clientes de dispositivos móviles y equipos Mac:

- Quite los registros de DNS SRV que creó cuando implementó la [extensión de AD RMS para dispositivos móviles](http://technet.microsoft.com/library/dn673574.aspx).

Para los clientes de Windows:

- Use los scripts de migración siguientes para volver a configurar los clientes de AD RMS. Estos scripts restablecen la configuración en los equipos Windows para que usen el servicio de Azure Rights Management en lugar de AD RMS: 
    
    **CleanUpRMS.cmd**
    
    - Elimina el contenido de todas las carpetas y claves del Registro usadas por el cliente de AD RMS para almacenar su configuración. En esta información se incluye la ubicación del clúster de AD RMS del cliente.
    
    **MigrateClient.cmd**
    
    - Configura el cliente para inicializar el entorno de usuario (arranque) para el servicio de Azure Rights Management.
    
    - Configura el cliente para conectarse a su servicio de Azure Rights Management y obtener licencias de uso para contenido protegido por el clúster de AD RMS. 

Si no puede realizar la migración de todos los clientes de Windows a la vez, ejecute los procedimientos siguientes en lotes de clientes. Agregue a cada usuario que quiera migrar en el lote y que tenga un equipo Windows al grupo **AIPMigrated** que ha creado anteriormente.

### <a name="windows-client-reconfiguration-by-using-registry-edits"></a>Reconfigurar un cliente de Windows modificando el Registro

1. Vuelva a los scripts de migración, **CleanUpRMS.cmd** y **MigrateClient.cmd**, que ha extraído previamente.

2.  Siga las instrucciones de **MigrateClient.cmd** para modificar el script de modo que contenga la dirección URL de servicio de Azure Rights Management de su inquilino y también los nombres de servidor de las direcciones URL de licencias de intranet y extranet del clúster de AD RMS.

    > [!IMPORTANT]
    > Como antes, tenga cuidado y no incluya espacios adicionales antes ni después de las direcciones.
    > 
    > Además, si los servidores de AD RMS usan certificados de servidor SSL/TLS, compruebe si los valores de la dirección URL de administración de licencias incluyen el número de puerto **443** en la cadena. Por ejemplo: https:// rms.treyresearch.net:443/_wmcs/licensing. Para encontrar esta información en la consola de Active Directory Rights Management Services, haga clic en el nombre del clúster y vea la información de **Detalles del clúster**. Si ve el número de puerto 443 incluido en la dirección URL, incluya este valor cuando modifique el script. Por ejemplo, https://rms.treyresearch.net:**443**. 

    Si necesita recuperar la dirección URL de servicio de Azure Rights Management para *&lt;YourTenantURL&gt;*, consulte [Para identificar la dirección URL de servicio de Azure Rights Management](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url).

3.  Ejecute **CleanUpRMS.cmd** y, después, **MigrateClient.cmd** en los equipos cliente de Windows que usen los miembros del grupo **AIPMigrated**. Por ejemplo, cree un objeto de directiva de grupo que ejecute estos scripts y asígnelo a este grupo de usuarios.

## <a name="next-steps"></a>Pasos siguientes
Para continuar con la migración, vaya a [Fase 4 de la migración: configuración de servicios auxiliares](migrate-from-ad-rms-phase3.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]