---
title: 'Migración de AD RMS-Azure Information Protection: fase 3'
description: Fase 3 de la migración desde AD RMS a Azure Information Protection, donde se describe el paso 7 de la migración de AD RMS a Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/11/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 13729d124ce0e49eddeda6c4c19aeae2c62eb8c6
ms.sourcegitcommit: 5b4eb0e17fb831d338d8c25844e9e6f4ca72246d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/10/2018
ms.locfileid: "53174257"
---
# <a name="migration-phase-3---client-side-configuration"></a>Fase 3 de la migración: configuración del lado cliente

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Use la información siguiente para la fase 3 de la migración desde AD RMS a Azure Information Protection. En estos procedimientos se describe el paso 7 de la [Migración desde AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

## <a name="step-7-reconfigure-windows-computers-to-use-azure-information-protection"></a>Paso 7. Reconfiguración de los equipos Windows para usar Azure Information Protection

Para equipos Windows que usan aplicaciones de escritorio de Office 2016 del tipo Hacer clic y ejecutar:

- Puede volver a configurar estos clientes para que usen Azure Information Protection mediante la redirección de DNS. Este es el método preferido para la migración de clientes porque es el más sencillo. Sin embargo, está restringido a aplicaciones de escritorio de Office 2016 (o versiones posteriores) del tipo Hacer clic y ejecutar en equipos Windows.
    
    El método requiere crear un registro SRV y establecer un permiso de denegación NTFS para los usuarios del punto de conexión de publicación de AD RMS.

- Para equipos Windows que no usan la versión Hacer clic y ejecutar de Office 2016:
    
    No podrá usar la redirección de DNS; deberá usar la edición del registro. Si usa Office 2016 junto a otras versiones de Office, puede usar este único método en todos los equipos Windows, o bien combinar el redireccionamiento DNS con la edición del registro. 
    
    La edición del registro es más sencilla al editar e implementar scripts que puede descargar. 

Vea las secciones siguientes para obtener más información sobre cómo volver a configurar los clientes Windows.

## <a name="client-reconfiguration-by-using-dns-redirection"></a>Reconfiguración de clientes mediante el redireccionamiento DNS

Este método es adecuado solo para los clientes Windows que ejecuten aplicaciones de escritorio de Office 2016 (o versiones posteriores) del tipo Hacer clic y ejecutar. 

1. Cree un registro SRV de DNS usando el siguiente formato:
    
    `_rmsredir._http._tcp.<AD RMS cluster>. <TTL> IN SRV <priority> <weight> <port> <your tenant URL>.`
    
    Para *\<clústeres de AD RMS>*, especifique el FQDN del clúster de AD RMS. Por ejemplo, **rmscluster.contoso.com**.
    
    Si solo tiene un clúster de AD RMS en el dominio, puede especificar solo el nombre del dominio que contenga el clúster. En nuestro ejemplo, sería **contoso.com**. Al especificar el nombre del dominio en este registro, el redireccionamiento se aplicará a todos los clústeres de AD RMS del dominio.
    
    Se ignorará el número de *\<puerto>*.
    
    Para la *\<URL de su inquilino\>*, especifique la [URL de servicio de Azure Rights Management para su inquilino](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url).
    
    Si usa el rol de servidor DNS en Windows Server, puede tomar la tabla siguiente como ejemplo de cómo especificar las propiedades del registro SRV en la consola del administrador de DNS.
    
    |Campo|Valor|  
    |-----------|-----------|  
    |**Dominio**|_tcp.rmscluster.contoso.com|  
    |**Servicio**|_rmsredir|  
    |**Protocolo**|_http|  
    |**Prioridad**|0|  
    |**Ponderación**|0|  
    |**Número de puerto**|80|  
    |**Host que ofrece este servicio**|5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com|  

2. Establecer un permiso de denegación para los usuarios de Office 2016 en el punto de conexión de publicación de AD RMS:

    a. En uno de los servidores de AD RMS del clúster, inicie la consola de Internet Information Services (IIS) Manager.

    b. Vaya a **Sitio web predeterminado** > **_wmcs** > **licensing** > **licensing.asmx**.

    c. Haga clic con el botón derecho en **licensing.asmx** > **Propiedades** > **Editar**.

    d. En el cuadro de diálogo **Permisos para licensing.asmx**, seleccione **Usuarios** si quiere establecer el redireccionamiento para todos los usuarios, o haga clic en **Agregar** para especificar un grupo que contenga los usuarios a los que quiera aplicar dicho redireccionamiento.
    
    Aunque todos los usuarios estén usando Office 2016, es preferible especificar inicialmente un subconjunto de usuarios para una migración por fases.
    
    e. En el grupo seleccionado, seleccione **Denegar** para los permisos **Leer y ejecutar** y **Leer**. Después, haga clic en **Aceptar** dos veces.

    f. Para confirmar que esta configuración funciona según lo esperado, intente conectarse al archivo licensing.asmx directamente desde un explorador. Debería ver el siguiente mensaje de error, que provoca que el cliente que ejecuta Office 2016 busque el registro SRV:
    
    **Mensaje de error 401.3: no tiene permisos para ver este directorio o esta página con las credenciales que ha suministrado (acceso denegado debido a las listas de control de acceso).**


## <a name="client-reconfiguration-by-using-registry-edits"></a>Reconfiguración del cliente mediante el uso de modificaciones del Registro

Este método es adecuado para todos los clientes Windows y debe usarse si se ejecuta una versión de Office anterior a 2016. En este método, se usan scripts de migración para volver a configurar los clientes de AD RMS:

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

### <a name="modifying-the-scripts-for-registry-edits"></a>Modificación de los scripts para editar el registro

1. Vuelva a los scripts de migración, **Migrate-Client.cmd** y **Migrate-User.cmd**, que extrajo previamente, cuando los descargó durante la [fase de preparación](migrate-from-ad-rms-phase1.md#step-2-prepare-for-client-migration).

2.  Siga las instrucciones de **Migrate-Client.cmd** para modificar el script de modo que contenga la dirección URL del servicio Azure Rights Management del inquilino y también los nombres de servidor de las direcciones URL de licencias de intranet y extranet del clúster de AD RMS. Luego, incremente la versión del script como se ha explicado anteriormente. Una buena práctica para realizar el seguimiento de las versiones de script es usar la fecha actual en el siguiente formato: AAAAMMDD
    
    > [!IMPORTANT]
    > Como antes, tenga cuidado y no incluya espacios adicionales antes ni después de las direcciones.
    > 
    > Además, si los servidores de AD RMS usan certificados de servidor SSL/TLS, compruebe si los valores de la dirección URL de administración de licencias incluyen el número de puerto **443** en la cadena. Por ejemplo: https://rms.treyresearch.net:443/_wmcs/licensing. Para encontrar esta información en la consola de Active Directory Rights Management Services, haga clic en el nombre del clúster y vea la información de **Detalles del clúster**. Si ve el número de puerto 443 incluido en la dirección URL, incluya este valor cuando modifique el script. Por ejemplo: https://rms.treyresearch.net:**443**. 
    
    Si necesita recuperar la dirección URL de servicio de Azure Rights Management para *&lt;YourTenantURL&gt;*, consulte [Para identificar la dirección URL de servicio de Azure Rights Management](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url).

3. Siguiendo las instrucciones del principio de este paso, configure los métodos de implementación de script para ejecutar **Migrate-Client.cmd** y **Migrate-User.cmd** en los equipos cliente Windows que usan los miembros del grupo AIPMigrated. 

## <a name="next-steps"></a>Pasos siguientes
Para continuar con la migración, vaya a [Fase 4 de la migración: configuración de servicios auxiliares](migrate-from-ad-rms-phase4.md).
