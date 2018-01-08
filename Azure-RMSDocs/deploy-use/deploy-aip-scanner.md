---
title: "Implementación del analizador de Azure Information Protection"
description: Instrucciones para instalar, configurar y ejecutar el analizador de Azure Information Protection para detectar, clasificar y proteger los archivos en almacenes de datos.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/08/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 20d29079-2fc2-4376-b5dc-380597f65e8a
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 7dfd670df89b652f8ff55452198d8483b55c59cd
ms.sourcegitcommit: 2a7f20684a041385e2d2425ab886e46917d2da9a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/03/2018
---
# <a name="deploying-the-azure-information-protection-scanner-to-automatically-classify-and-protect-files"></a>Implementación del analizador de Azure Information Protection para clasificar y proteger automáticamente los archivos

>*Se aplica a: Azure Information Protection, Windows Server 2016, Windows Server 2012 R2*

> [!NOTE]
> Esta característica se encuentra actualmente en versión preliminar y está sujeta a cambios.

Use esta información para obtener información sobre el analizador de Azure Information Protection y, a continuación, cómo instalarlo, configurarlo y ejecutarlo correctamente. 

Este analizador se ejecuta como un servicio en Windows Server y permite detectar, clasificar y proteger archivos en los almacenes de datos siguientes:

- Carpetas locales en el equipo de Windows Server en el que se ejecuta el analizador.

- Rutas de acceso UNC para recursos compartidos de red que utilizan el protocolo del sistema de archivos de Internet comunes (CIFS).

- Sitios y bibliotecas de SharePoint Server 2016 y SharePoint Server 2013.

## <a name="overview-of-the-azure-information-protection-scanner"></a>Información general del analizador de Azure Information Protection

Cuando haya configurado la [directiva de Azure Information Protection](configure-policy.md) para etiquetas que aplican la clasificación automática, a continuación, se pueden etiquetar los archivos que este analizador detecta. Las etiquetas aplican la clasificación y, opcionalmente, aplican la protección o la quitan:

![Información general del analizador de Azure Information Protection](../media/infoprotect-scanner.png)

El analizador puede inspeccionar cualquier archivo que Windows pueda indexar mediante los iFilters que están instalados en el equipo. Después, para determinar si los archivos necesitan etiquetas, el analizador usa los tipos de información confidencial de la prevención de pérdida de datos (DLP) y la detección de patrones integrados en Office 365, o bien los patrones de expresión regular de Office 365. Dado que el analizador utiliza el cliente de Azure Information Protection, puede clasificar y proteger los mismos [tipos de archivo](../rms-client/client-admin-guide-file-types.md).

Puede ejecutar el analizador solo en modo de detección en los casos en los que los informes se usen para comprobar qué sucedería si los archivos se etiquetaran. También puede ejecutar el analizador para aplicar automáticamente las etiquetas.

Tenga en cuenta que el analizador no detecta ni etiqueta contenido en tiempo real. En su lugar, lo rastrea sistemáticamente en los archivos de los almacenes de datos que especifique, y se puede configurar este ciclo para que se ejecute una sola vez o de manera repetida.

## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Requisitos previos del analizador de Azure Information Protection
Antes de instalar el analizador de Azure Information Protection, asegúrese de que se cumplen los requisitos siguientes.

|Requisito|Más información|
|---------------|--------------------|
|Equipo con Windows Server en el que se ejecutará el servicio del analizador:<br /><br />- 4 procesadores<br /><br />- 4 GB de RAM|Windows Server 2016 o Windows Server 2012 R2. <br /><br />Nota: Para llevar a cabo pruebas o evaluaciones en un entorno que no sea de producción, puede usar un sistema operativo cliente de Windows que sea [compatible con el cliente de Azure Information Protection](../get-started/requirements.md#client-devices).<br /><br />Este equipo puede ser un equipo físico o virtual que tenga una conexión de red rápida y confiable a los almacenes de datos que deban analizarse. <br /><br />Asegúrese de que este equipo tenga la [conectividad a Internet](../get-started/requirements.md#firewalls-and-network-infrastructure) necesaria para Azure Information Protection. De lo contrario, debe configurarlo como un [equipo desconectado](../rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers). |
|SQL Server para almacenar la configuración del analizador:<br /><br />- Instancia local o remota|SQL Server 2012 es la versión mínima para las siguientes ediciones:<br /><br />- SQL Server Enterprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express|
|Cuenta de servicio en la que se ejecutará el servicio del analizador|Esta cuenta debe ser de Active Directory y estar sincronizada con Azure AD, con los siguientes requisitos adicionales:<br /><br />- **Derecho de iniciar sesión localmente**. Este derecho es necesario para la instalación y configuración del analizador, pero no para la operación. Debe conceder este derecho a la cuenta de servicio, pero puede quitarlo después de haber confirmado que el analizador puede detectar, clasificar y proteger los archivos.<br /><br />- **Derecho de iniciar sesión como servicio**. Este derecho se concede automáticamente a la cuenta de servicio durante la instalación del analizador y es necesario para la instalación, la configuración y el funcionamiento del analizador. <br /><br />- Permisos a los repositorios de datos: debe conceder permisos de **lectura** y **escritura** para analizar los archivos y, a continuación, aplicar la clasificación y la protección a los archivos que cumplan las condiciones establecidas en la directiva de Azure Information Protection. Para ejecutar el analizador solo en modo de detección, el permiso de **lectura** es suficiente.<br /><br />- Para las etiquetas que ofrecen una segunda protección o quitan la protección: para asegurarse de que el analizador siempre tenga acceso a los archivos protegidos, convierta esta cuenta en un [superusuario](configure-super-users.md) para el servicio de Azure Rights Management y asegúrese de que la característica de superusuario esté habilitada. Para obtener más información sobre los requisitos de la cuenta para aplicar la protección, consulte [Preparación de usuarios y grupos para Azure Information Protection](../plan-design/prepare.md).|
|Cliente de Azure Information Protection instalado en el equipo con Windows Server|Actualmente, el analizador de Azure Information Protection requiere la versión preliminar del cliente de Azure Information Protection.<br /><br />Debe instalar el cliente completo para el analizador. No instale el cliente solo con el módulo de PowerShell.<br /><br />Para obtener instrucciones de instalación del cliente, consulte la [guía del administrador](../rms-client/client-admin-guide.md).|
|Etiquetas configuradas que aplican la clasificación automática y, opcionalmente, la protección|Para obtener más información sobre cómo configurar las condiciones, consulte [Configuración de las condiciones para la clasificación automática y recomendada en Azure Information Protection](configure-policy-classification.md).<br /><br />Para obtener más información sobre cómo configurar las etiquetas para aplicar la protección a los archivos, consulte [Configuración de una etiqueta para la protección de Rights Management](configure-policy-protection.md).<br /><br />Estas etiquetas pueden estar en la directiva global, o en una o varias [directivas con ámbito](configure-policy-scope.md).|


## <a name="install-the-azure-information-protection-scanner"></a>Instalación del analizador de Azure Information Protection

1. Mediante la cuenta de servicio que ha creado para ejecutar el analizador, inicie sesión en el equipo con Windows Server que ejecutará el analizador.

2. Inicie una sesión de Windows PowerShell con la opción **Ejecutar como administrador**.

3. Ejecute el cmdlet [AIPScanner Install](/powershell/module/azureinformationprotection/Install-AIPScanner) y especifique la instancia de SQL Server en la que se va a crear una base de datos para el analizador de Azure Information Protection: 
    
    ```
    Install-AIPScanner -SqlServerInstance <database name>
    ```
    
    Ejemplos:
    
    Para una instancia predeterminada: `Install-AIPScanner -SqlServerInstance SQLSERVER1`
    
    Para una instancia con nombre: `Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER`
    
    Para SQL Server Express: `Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS`
    
    Si necesita más [ejemplos detallados](/powershell/module/azureinformationprotection/install-aipscanner#examples), use la ayuda en línea sobre este cmdlet.
    
    Cuando se le pida, proporcione las credenciales de la cuenta de servicio del analizador (\<dominio\nombre de usuario>) y la contraseña.

4. Compruebe que el servicio esté ahora instalado mediante **Herramientas administrativas** > **Servicios**. 
    
    El servicio instalado se denomina **Analizador de Azure Information Protection** y está configurado para ejecutarse con la cuenta de servicio del analizador que ha creado.

Ahora que ha instalado el analizador, debe obtener un token de Azure AD para que la cuenta de servicio del analizador se autentique y se pueda ejecutar en modo desatendido. 

## <a name="get-an-azure-ad-token-for-the-scanner-service-account-to-authenticate-to-the-azure-information-protection-service"></a>Obtención de un token de Azure AD para la autenticación de la cuenta de servicio del analizador en el servicio de Azure Information Protection

1. Desde el mismo equipo con Windows Server, o desde el escritorio, inicie sesión en Azure Portal para crear dos aplicaciones de Azure AD que son necesarias para especificar un token de acceso para la autenticación. Después de un inicio de sesión interactivo inicial, este token permite que el analizador se ejecute de forma no interactiva.
    
    Para crear estas aplicaciones, siga las instrucciones de [Cómo etiquetar archivos de manera no interactiva para Azure Information Protection](../rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) de la guía del administrador.

2. Desde el equipo con Windows Server, todavía con la sesión iniciada con la cuenta de servicio del analizador, ejecute [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) y especifique los valores que ha copiado en el paso anterior:
    
    ```
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application>  -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application >
    ```

3. Cuando se le solicite, especifique la contraseña de las credenciales de la cuenta de servicio para Azure AD y, a continuación, haga clic en **Aceptar**.

El analizador tiene ahora un token para autenticarse en Azure AD, que es válido durante un año, dos años, o nunca expira, según la configuración de la **aplicación web/API** en Azure AD. Cuando expire el token, deberá repetir los pasos del 1 al 3.

Ahora está listo para especificar los almacenes de datos que se deben analizar. 

## <a name="specify-data-stores-for-the-azure-information-protection-scanner"></a>Especificación de almacenes de datos para el analizador de Azure Information Protection

Use el cmdlet [Add-AIPScannerRepository](/powershell/module/azureinformationprotection/Add-AIPScannerRepository) para especificar los almacenes de datos que el analizador de Azure Information Protection debe analizar. Puede especificar carpetas locales, rutas UNC y direcciones URL de SharePoint Server para los sitios y las bibliotecas de SharePoint. 

Versiones compatibles para SharePoint: SharePoint Server 2016 y SharePoint Server 2013.

1. Desde el mismo equipo con Windows Server, en la sesión de PowerShell, ejecute el comando siguiente para agregar el primer almacén de datos:
    
        Add-AIPScannerRepository -Path <path>
    
    Por ejemplo: `Add-AIPScannerRepository -Path \\NAS\Documents`
    
    Para obtener otros ejemplos, consulte la [ayuda en línea](/powershell/module/azureinformationprotection/Add-AIPScannerRepository#examples) sobre este cmdlet.

2. Repita este comando para todos los almacenes de datos que quiera analizar. Si necesita eliminar un almacén de datos que ha agregado, use el cmdlet [Remove-AIPScannerRepository](/powershell/module/azureinformationprotection/Remove-AIPScannerRepository).

3. Ejecute el cmdlet [Get-AIPScannerRepository](/powershell/module/azureinformationprotection/Get-AIPScannerRepository) para confirmar que ha especificado correctamente todos los almacenes de datos:
    
        Get-AIPScannerRepository

Con la configuración predeterminada del analizador, ahora está listo para ejecutar el primer examen en modo de detección.

## <a name="run-a-discovery-cycle-and-view-reports-for-the-azure-information-protection-scanner"></a>Ejecución de un ciclo de detección y consulta de los informes del analizador de Azure Information Protection

1. Mediante **Herramientas administrativas** > **Servicios**, inicie el servicio **Analizador de Azure Information Protection**.

2. Espere a que el analizador complete su ciclo. Cuando el analizador haya rastreado todos los archivos de los almacenes de datos que ha especificado, el servicio se detendrá. Puede utilizar el registro de eventos local de **aplicaciones y servicios** de Windows, **Azure Information Protection**, para confirmar cuándo se detiene el servicio. Busque el id. de evento informativo **911**.

3. Revise los informes almacenados en %*localappdata*%\Microsoft\MSIP\Scanner\Reports que tengan un formato de archivo .csv. Con la configuración predeterminada del analizador, solo los archivos que cumplen las condiciones para la clasificación automática se incluyen en estos informes.
    
    Si los resultados no son los esperados, tendrá que ajustar las condiciones que ha especificado en la directiva de Azure Information Protection. Si es así, repita los pasos del 1 al 3 hasta que esté listo para cambiar la configuración para aplicar la clasificación y, opcionalmente, la protección. Cada vez que repita estos pasos, primero ejecute el siguiente comando de PowerShell en el equipo con Windows Server:
    
        Set-AIPScannerConfiguration -Schedule OneTime

Cuando esté listo para etiquetar automáticamente los archivos que el analizador detecta, continúe con el procedimiento siguiente. 

## <a name="configure-the-azure-information-protection-scanner-to-apply-classification-and-protection-to-discovered-files"></a>Configuración del analizador de Azure Information Protection para aplicar la clasificación y la protección a los archivos detectados

En su configuración predeterminada, el analizador se ejecuta una vez y en el modo solo informe. Para cambiar esta configuración, ejecute el cmdlet [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).

1. En el equipo con Windows Server, en la sesión de PowerShell, ejecute el siguiente comando:
    
        Set-AIPScannerConfiguration -ScanMode Enforce -Schedule Continuous
    
    Hay otras opciones de configuración que tal vez quiera cambiar. Por ejemplo, si se cambian los atributos de archivo y lo que se registra en los informes. Además, si la directiva de Azure Information Protection incluye la configuración que requiere un mensaje de justificación para bajar el nivel de clasificación o quitar la protección, especifique ese mensaje mediante el uso de este cmdlet. Use la [ayuda en línea](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration#parameters) para obtener más información sobre cada opción de configuración. 

2. Mediante **Herramientas administrativas** > **Servicios**, reinicie el servicio **Analizador de Azure Information Protection**.

3. Al igual que antes, supervise el registro de eventos y los informes para ver qué archivos se han etiquetado, qué clasificación se ha aplicado y si se ha aplicado la protección.

Dado que hemos configurado la programación para que se ejecute continuamente, cuando el analizador haya completado el examen de todos los archivos, iniciará un nuevo ciclo para detectar archivos nuevos y modificados.

## <a name="when-files-are-rescanned-by-the-azure-information-protection-scanner"></a>Cuando el analizador de Azure Information Protection vuelve a examinar los archivos

En el primer ciclo de examen, el analizador inspecciona todos los archivos de los almacenes de datos configurados y, después, en los exámenes posteriores, solo inspecciona los archivos nuevos o modificados. 

Puede forzar a que el analizador inspeccione todos los archivos de nuevo mediante la ejecución de [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) con el parámetro `-Type` establecido en **Completo**. Esta configuración es útil si quiere que los informes incluyan todos los archivos y suele usarse cuando el analizador se ejecuta en modo de detección. Cuando finaliza el examen completo, el tipo de examen cambia automáticamente a incremental para que en los análisis posteriores solo se examinen los archivos nuevos o modificados.

Además, se inspeccionan todos los archivos cuando el analizador descarga una directiva de Azure Information Protection con condiciones nuevas o modificadas. El escáner actualiza la directiva cada hora y cuando se inicia el servicio.

## <a name="optimizing-the-performance-of-the-azure-information-protection-scanner"></a>Optimización del rendimiento del analizador de Azure Information Protection

Para maximizar el rendimiento del analizador:

- **Use una conexión de red de alta velocidad y estable entre el equipo que actúa como analizador y el almacén para los datos examinados**.
    
    Por ejemplo, conecte el equipo que actúa como analizador a la misma red LAN o al mismo segmento de red que el almacén de datos examinados (se prefiere la segunda opción).
    
    La calidad de la conexión de red afecta al rendimiento del analizador, ya que, al inspeccionar archivos, el analizador transfiere el contenido de los archivos al equipo que ejecuta el servicio de examen. Al reducir (o eliminar) el número de saltos de red que los datos deben realizar, también se reduce la carga de la red. 

- **Asegúrese de que el equipo que actúa como analizador tenga recursos del procesador disponibles**.
    
    Inspeccione el contenido de los archivos para obtener una coincidencia según las condiciones que haya configurado. Las acciones de cifrado y descifrado de archivos suponen una carga elevada para el procesador. Supervise los ciclos de examen típicos de los almacenes de datos que haya especificado para identificar si la falta de recursos del procesador afecta negativamente al rendimiento del analizador.
    
- **No examine carpetas locales del equipo que ejecute el servicio de analizador**.
    
    Si tiene carpetas para examinar en un servidor Windows, instale el analizador en otro equipo y configure las carpetas como recursos compartidos de red para realizar el examen. Al separar ambas funciones de los archivos de hospedaje y de examen, los recursos de cálculo de esos servicios no interferirán entre sí.

Otros factores que influyen en el rendimiento del analizador:

- La carga actual y los tiempos de respuesta de los almacenes de datos que contienen los archivos para examinar.

- Ejecución del analizador en modo de detección o aplicación
    
    El modo de detección suele tener un ritmo de examen superior en comparación con el modo de aplicación, ya que la detección requiere una única acción de lectura de archivo, mientras que el modo de aplicación requiere acciones de lectura y escritura.

- Cambio de las condiciones de Azure Information Protection
    
    Obviamente, el primer ciclo de examen, que se produce cuando el analizador inspecciona todos los archivos, requerirá más tiempo que los siguientes ciclos de examen, ya que, de forma predeterminada, solo se examinan los archivos nuevos o modificados. Sin embargo, si cambia las condiciones de la directiva de Azure Information Protection, todos los archivos se examinarán una vez más, tal como se describe en la [sección anterior](#when-files-are-rescanned-by-the-azure-information-protection-scanner).

- Elección del nivel de registro
    
    Puede elegir entre **Depurar**, **Información**, **Error** y **Desactivado** para los informes del analizador. **Desactivado** da como resultado un rendimiento óptimo; **Depurar** ralentiza considerablemente el analizador y debe usarse solo para solucionar problemas. Para obtener más información, consulte el parámetro *ReportLevel* del cmdlet [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).

- En cuanto a los archivos:
    
    - Los archivos de Office se examinan más rápido que los archivos PDF.
    
    - Los desprotegidos se examinan más rápido que los protegidos.
    
    - Obviamente, los archivos de gran tamaño se examinan más lentamente que aquellos más pequeños.

## <a name="list-of-cmdlets-for-the-azure-information-protection-scanner"></a>Lista de cmdlets del analizador de Azure Information Protection 

Otros cmdlets del analizador le permiten cambiar la cuenta de servicio y la base de datos del analizador, obtener la configuración actual del analizador y desinstalar el servicio del analizador. El analizador utiliza los siguientes cmdlets:

- [Add-AIPScannerRepository](/powershell/module/azureinformationprotection/Add-AIPScannerRepository)

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerRepository](/powershell/module/azureinformationprotection/Get-AIPScannerRepository)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Remove-AIPScannerRepository](/powershell/module/azureinformationprotection/Remove-AIPScannerRepository)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)


## <a name="event-log-ids-and-descriptions"></a>Id. de registro de eventos y descripciones

Use las siguientes secciones para identificar los id. de eventos y las descripciones posibles para el analizador. Estos eventos se registran en el servidor que ejecuta el servicio analizador, en el registro de eventos de **aplicaciones y servicios** de Windows, **Azure Information Protection**.

-----

Información **910**

**Se ha iniciado el ciclo del analizador.**

Este evento se registra cuando el servicio del analizador se inicia y comienza a examinar los archivos en los repositorios de datos que ha especificado.

----

Información **911**

**Ha finalizado el ciclo del analizador.**

Este evento se registra cuando el analizador ha terminado su examen único, ya que el servidor se ha iniciado o el analizador ha terminado un ciclo para una programación continua.

----

Información **913**

**El analizador se ha detenido porque está establecido en Nunca.**

Este evento se registra cuando el analizador está configurado para ejecutarse una vez y no de forma continua, y el servicio analizador de Azure Information Protection se ha reiniciado manualmente desde que se inició el equipo.  

Para volver a analizar los archivos, debe establecer la programación en **OneTime** o **Continuous** y, después, reiniciar el servicio manualmente. Para cambiar la programación, use el cmdlet [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) y el parámetro **Schedule**.

----

Error **912**

**Se ha producido un error desconocido.**

Encontrará más información en el informe detallado almacenado en % localappdata%\Microsoft\MSIP\Scanner\Reports\DetailedReport_YYYY_MM_DD_HH_MM.csv.

Póngase en contacto con el [soporte técnico de Microsoft](../get-started/information-support.md#to-contact-microsoft-support) si este evento continúa registrándose. 

----

Error **914**

**El servicio se ha detenido automáticamente debido a una configuración incorrecta: el archivo de la directiva no se encuentra o está dañado.**

Este evento se registra cuando el cliente de Azure Information Protection no tiene un archivo de directiva válido para que el analizador se ejecute.

La directiva de Azure Information Protection se almacena en %localappdata%\Microsoft\MSIP y debe configurarse con etiquetas que tengan las condiciones para aplicar la clasificación automática. O bien, la directiva debe configurarse para una etiqueta predeterminada.

Asegúrese de que los firewalls no estén bloqueando la conectividad a Internet requerida. Para obtener más información, consulte los requisitos de [Firewalls e infraestructura de red](../get-started/requirements.md#firewalls-and-network-infrastructure) de Azure Information Protection. Si no es posible conectarse a Internet, siga las instrucciones para admitir [equipos desconectados](../rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers).


## <a name="next-steps"></a>Pasos siguientes

Es posible que se pregunte: [¿Cuál es la diferencia entre FCI de Windows Server y el analizador de Azure Information Protection?](../get-started/faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

También puede usar PowerShell para clasificar y proteger los archivos de forma interactiva desde el equipo de escritorio. Para obtener más información sobre este y otros escenarios en que se utiliza PowerShell, consulte [Uso de PowerShell con el cliente de Azure Information Protection](../rms-client/client-admin-guide-powershell.md).


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
