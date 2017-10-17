---
title: "Migración de AD RMS-Azure Information Protection: fase 3"
description: "Fase 3 de la migración desde AD RMS a Azure Information Protection, donde se describe el paso 7 de la migración de AD RMS a Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/11/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 5de30d095e1c279babb8f8be74a5a9b9d54db204
ms.sourcegitcommit: 45c23b3b353ad0e438292cb1cd8d1b13061620e1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="migration-phase-3---client-side-configuration"></a>Fase 3 de la migración: configuración del lado cliente

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Office 365*

Use la información siguiente para la fase 3 de la migración desde AD RMS a Azure Information Protection. En estos procedimientos se describe el paso 7 de la [Migración desde AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

## <a name="step-7-reconfigure-windows-computers-to-use-azure-information-protection"></a>Paso 7. Reconfiguración de los equipos Windows para usar Azure Information Protection

En los equipos Windows, use dos scripts de migración para volver a configurar los clientes de AD RMS:

- Migrate-Client.cmd

- Migrate-User.cmd

El script de configuración de cliente (Migrate-Client.cmd) configura las opciones de equipo en el Registro, lo que significa que debe ejecutarse en un contexto de seguridad que pueda realizar esos cambios. Esto normalmente implica uno de los métodos siguientes:

- Usar la directiva de grupo para ejecutar el script como un script de inicio de equipo.

- Usar la instalación de software de directiva de grupo para asignar el script al equipo.

- Usar una solución de implementación de software para implementar el script en los equipos. Por ejemplo, use [paquetes y programas](/sccm/apps/deploy-use/packages-and-programs) de System Center Configuration Manager. En las propiedades del paquete y el programa, en **Modo de ejecución**, especifique que el script se ejecuta con permisos administrativos en el dispositivo. 

- Si el usuario tiene privilegios de administrador locales, use un script de inicio de sesión.

El script de configuración de usuario (Migrate-User.cmd) configura las opciones de usuario y limpia el almacén de licencias de cliente. Esto significa que este script debe ejecutarse en el contexto del usuario real. Por ejemplo:

- Usar un script de inicio de sesión.

- Usar la instalación de software de directiva de grupo para publicar el script para que lo ejecute el usuario.

- Usar una solución de implementación de software para implementar el script para los usuarios. Por ejemplo, use [paquetes y programas](/sccm/apps/deploy-use/packages-and-programs) de System Center Configuration Manager. En las propiedades del paquete y el programa, en **Modo de ejecución**, especifique que el script se ejecuta con los permisos del usuario. 

- Pida al usuario que ejecute el script al iniciar sesión en el equipo.

Los dos scripts incluyen un número de versión y no se vuelven a ejecutar hasta que se modifica este número de versión. Esto significa que puede dejar los scripts aquí hasta que finalice la migración. Sin embargo, si realiza cambios en los scripts que quiere que los equipos y los usuarios vuelvan a ejecutar en los equipos Windows, actualice la siguiente línea de ambos scripts a un valor superior:

    SET Version=20170427

El script de configuración de usuario está diseñado para ejecutarse después del script de configuración de cliente y usa el número de versión de esta comprobación. Si no se ha ejecutado el script de configuración de cliente con la misma versión, se detendrá. Esta comprobación garantiza que los dos scripts se ejecuten en la secuencia correcta. 

Si no puede realizar la migración de todos los clientes de Windows a la vez, ejecute los procedimientos siguientes en lotes de clientes. Agregue a cada usuario que quiera migrar en el lote y que tenga un equipo Windows al grupo **AIPMigrated** que ha creado anteriormente.

### <a name="windows-client-reconfiguration-by-using-registry-edits"></a>Reconfigurar un cliente de Windows modificando el Registro

1. Vuelva a los scripts de migración, **Migrate-Client.cmd** y **Migrate-User.cmd**, que extrajo previamente, cuando los descargó durante la [fase de preparación](migrate-from-ad-rms-phase1.md#step-2-prepare-for-client-migration).

2.  Siga las instrucciones de **Migrate-Client.cmd** para modificar el script de modo que contenga la dirección URL del servicio Azure Rights Management del inquilino y también los nombres de servidor de las direcciones URL de licencias de intranet y extranet del clúster de AD RMS. Luego, incremente la versión del script como se ha explicado anteriormente. Una buena práctica para realizar el seguimiento de las versiones de script es usar la fecha actual en el formato AAAAMMDD.

    > [!IMPORTANT]
    > Como antes, tenga cuidado y no incluya espacios adicionales antes ni después de las direcciones.
    > 
    > Además, si los servidores de AD RMS usan certificados de servidor SSL/TLS, compruebe si los valores de la dirección URL de administración de licencias incluyen el número de puerto **443** en la cadena. Por ejemplo: https:// rms.treyresearch.net:443/_wmcs/licensing. Para encontrar esta información en la consola de Active Directory Rights Management Services, haga clic en el nombre del clúster y vea la información de **Detalles del clúster**. Si ve el número de puerto 443 incluido en la dirección URL, incluya este valor cuando modifique el script. Por ejemplo, https://rms.treyresearch.net:**443**. 

    Si necesita recuperar la dirección URL de servicio de Azure Rights Management para *&lt;YourTenantURL&gt;*, consulte [Para identificar la dirección URL de servicio de Azure Rights Management](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url).

3. Siguiendo las instrucciones del principio de este paso, configure los métodos de implementación de script para ejecutar **Migrate-Client.cmd** y **Migrate-User.cmd** en los equipos cliente Windows que usan los miembros del grupo AIPMigrated. 

## <a name="next-steps"></a>Pasos siguientes
Para continuar con la migración, vaya a [Fase 4 de la migración: configuración de servicios auxiliares](migrate-from-ad-rms-phase3.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]