---
title: Implementación del analizador de Azure Information Protection
description: Instrucciones para instalar, configurar y ejecutar el analizador de Azure Information Protection para detectar, clasificar y proteger los archivos en almacenes de datos.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/15/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 20d29079-2fc2-4376-b5dc-380597f65e8a
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: d81e8f851f2b624ca81912bc3af8487522bf2873
ms.sourcegitcommit: 4ed27f50545aae1a58cc922202959d427bcba7ac
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/16/2019
ms.locfileid: "56323689"
---
# <a name="deploying-the-azure-information-protection-scanner-to-automatically-classify-and-protect-files"></a>Implementación del analizador de Azure Information Protection para clasificar y proteger automáticamente los archivos

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2016 y Windows Server 2012 R2*

> [!NOTE]
> Este artículo es aplicable a la versión de disponibilidad general actual del analizador de Azure Information Protection.
> 
> Si desea obtener instrucciones de implementación de la versión preliminar actual del analizador, que incluye la configuración desde Azure Portal, vea [Implementación de la versión preliminar del analizador de Azure Information Protection para clasificar y proteger archivos automáticamente](deploy-aip-scanner-preview.md).

Use esta información para obtener información sobre el analizador de Azure Information Protection y, a continuación, cómo instalarlo, configurarlo y ejecutarlo correctamente.

Este analizador se ejecuta como un servicio en Windows Server y permite detectar, clasificar y proteger archivos en los almacenes de datos siguientes:

- Carpetas locales en el equipo de Windows Server en el que se ejecuta el analizador.

- Rutas de acceso UNC para recursos compartidos de red que usan el protocolo de Bloque de mensajes del servidor (SMB).

- Sitios y bibliotecas de SharePoint Server 2016 y SharePoint Server 2013. SharePoint Server 2010 también se admite en clientes que tengan [compatibilidad ampliada para esta versión de SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).

Para analizar y etiquetar los archivos en los repositorios en la nube, use [Cloud App Security](https://docs.microsoft.com/cloud-app-security/) en lugar del escáner.

## <a name="overview-of-the-azure-information-protection-scanner"></a>Información general del analizador de Azure Information Protection

Cuando haya configurado la [directiva de Azure Information Protection](configure-policy.md) para etiquetas que aplican la clasificación automática, a continuación, se pueden etiquetar los archivos que este analizador detecta. Las etiquetas aplican la clasificación y, opcionalmente, aplican la protección o la quitan:

![Información general de la arquitectura del analizador de Azure Information Protection](./media/infoprotect-scanner.png)

El analizador puede inspeccionar cualquier archivo que Windows pueda indexar mediante los iFilters que están instalados en el equipo. Después, para determinar si los archivos necesitan etiquetas, el analizador usa los tipos de información confidencial de la prevención de pérdida de datos (DLP) y la detección de patrones integrados en Office 365, o bien los patrones de expresión regular de Office 365. Dado que el analizador utiliza el cliente de Azure Information Protection, puede clasificar y proteger los mismos [tipos de archivo](./rms-client/client-admin-guide-file-types.md).

Puede ejecutar el analizador solo en modo de detección en los casos en los que los informes se usen para comprobar qué sucedería si los archivos se etiquetaran. También puede ejecutar el analizador para aplicar automáticamente las etiquetas. También puede ejecutar el analizador para detectar los archivos que contienen tipos de información confidencial, sin configurar las etiquetas para las condiciones que aplican la clasificación automática.

Tenga en cuenta que el analizador no detecta ni etiqueta contenido en tiempo real. En su lugar, lo rastrea sistemáticamente en los archivos de los almacenes de datos que especifique, y se puede configurar este ciclo para que se ejecute una sola vez o de manera repetida.

Puede especificar los tipos de archivo desea examinar, o incluso excluirlos del examen. Para restringir los archivos que inspecciona el analizador, defina una lista de tipos de archivo mediante el uso de [Set-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Set-AIPScannerScannedFileTypes).


## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Requisitos previos del analizador de Azure Information Protection
Antes de instalar el analizador de Azure Information Protection, asegúrese de que se cumplen los requisitos siguientes.

|Requisito|Más información|
|---------------|--------------------|
|Equipo con Windows Server en el que se ejecutará el servicio del analizador:<br /><br />-4 procesadores de núcleo<br /><br />- 8 GB de RAM<br /><br />-10 GB de espacio libre (promedio) para los archivos temporales|Windows Server 2016 o Windows Server 2012 R2. <br /><br />Nota: Para llevar a cabo pruebas o evaluaciones en un entorno que no sea de producción, puede usar un sistema operativo cliente de Windows que sea [compatible con el cliente de Azure Information Protection](requirements.md#client-devices).<br /><br />Este equipo puede ser un equipo físico o virtual que tenga una conexión de red rápida y confiable a los almacenes de datos que deban analizarse.<br /><br /> El analizador requiere suficiente espacio en disco para crear archivos temporales para cada archivo que analiza, cuatro archivos por núcleo. El espacio en disco recomendado de 10 GB permite que 4 procesadores de núcleo examinen 16 archivos, cada uno con un tamaño de 625 MB. <br /><br />Si no es posible la conectividad a Internet debido a las directivas de la organización, consulte la sección [Implementación del analizador con configuraciones alternativas](#deploying-the-scanner-with-alternative-configurations). En caso contrario, asegúrese de que este equipo tiene conectividad a Internet que permite las siguientes direcciones URL:<br /> \*.aadrm.com <br /> \*.azurerms.com<br /> \*.informationprotection.azure.com <br /> informationprotection.hosting.portal.azure.net <br /> \*.aria.microsoft.com|
|Cuenta de servicio en la que se ejecutará el servicio del analizador |Además de ejecutar el servicio de examen en el equipo con Windows Server, esta cuenta de Windows se autentica en Azure AD y descarga la directiva de Azure Information Protection. Esta cuenta debe ser una cuenta de Active Directory y sincronizarse con Azure AD. Si no puede sincronizar esta cuenta debido a las directivas de la organización, consulte la sección [Implementación del analizador con configuraciones alternativas](#deploying-the-scanner-with-alternative-configurations).<br /><br />Esta cuenta de servicio tiene los siguientes requisitos:<br /><br />- Asignación de derechos de usuario de **inicio de sesión localmente**. Este derecho es necesario para la instalación y configuración del analizador, pero no para la operación. Debe conceder este derecho a la cuenta de servicio, pero puede quitarlo después de haber confirmado que el analizador puede detectar, clasificar y proteger los archivos. Si no es posible conceder este derecho ni siquiera durante un breve período de tiempo debido a las directivas de la organización, consulte la sección [Implementación del analizador con configuraciones alternativas](#deploying-the-scanner-with-alternative-configurations).<br /><br />- Asignación de derechos de usuario de **inicio de sesión como servicio**. Este derecho se concede automáticamente a la cuenta de servicio durante la instalación del analizador y es necesario para la instalación, la configuración y el funcionamiento del analizador. <br /><br />- Permisos a los repositorios de datos: debe conceder permisos de **lectura** y **escritura** para analizar los archivos y después aplicar la clasificación y la protección a los archivos que cumplan las condiciones establecidas en la directiva de Azure Information Protection. Para ejecutar el analizador solo en modo de detección, el permiso de **lectura** es suficiente.<br /><br />- Para las etiquetas que ofrecen una segunda protección o quitan la protección: para asegurarse de que el analizador siempre tenga acceso a los archivos protegidos, convierta esta cuenta en un [superusuario](configure-super-users.md) para el servicio de Azure Rights Management y asegúrese de que la característica de superusuario esté habilitada. Para obtener más información sobre los requisitos de la cuenta para aplicar la protección, consulte [Preparación de usuarios y grupos para Azure Information Protection](prepare.md). Además, si ha implementado [controles de incorporación](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) para una implementación por fases, asegúrese de que esta cuenta se incluye en los controles de incorporación que ha configurado.|
|SQL Server para almacenar la configuración del analizador:<br /><br />- Instancia local o remota<br /><br />- Rol Sysadmin para instalar el escáner|SQL Server 2012 es la versión mínima para las siguientes ediciones:<br /><br />- SQL Server Enterprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express<br /><br />Si instala más de una instancia del analizador, cada una requerirá su propia base de datos de SQL Server.<br /><br />Cuando instale el analizador y su cuenta tenga el rol de administrador del sistema, el proceso de instalación creará automáticamente la base de datos AzInfoProtectionScanner y concederá el rol db_owner necesario a la cuenta de servicio que ejecuta el analizador. Si no puede conceder el rol de administrador del sistema o las directivas de la organización requieren la creación y la configuración manual de bases de datos, consulte la sección [Implementación del analizador con configuraciones alternativas](#deploying-the-scanner-with-alternative-configurations).<br /><br />El tamaño de la base de datos de configuración varía con cada implementación, pero se recomienda asignar 500 MB por cada 1 000 000 archivos que quiera examinar. |
|Cliente de Azure Information Protection instalado en el equipo con Windows Server|Debe instalar el cliente completo para el analizador. No instale el cliente solo con el módulo de PowerShell.<br /><br />Para obtener instrucciones de instalación del cliente, consulte la [guía del administrador](./rms-client/client-admin-guide.md). Si ha instalado previamente el analizador y ahora debe actualizarlo a una versión posterior, consulte [Upgrading the Azure Information Protection scanner](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner) (Actualización del analizador Azure Information Protection).|
|Etiquetas configuradas que aplican la clasificación automática y, opcionalmente, la protección|Para más información sobre cómo configurar una etiqueta de condiciones y cómo aplicar protección:<br /> - [Configuración de las condiciones para la clasificación automática y recomendada](configure-policy-classification.md)<br /> - [Configuración de una etiqueta para la protección de Rights Management](configure-policy-protection.md) <br /><br />Sugerencia: Puede usar las instrucciones del [tutorial](infoprotect-quick-start-tutorial.md) para probar el analizador con una etiqueta que busca números de tarjeta de crédito en un documento de Word preparado. Sin embargo, deberá cambiar la configuración de etiqueta para que **Select how this label is applied** (Seleccionar cómo se aplica esta etiqueta) se establezca en **Automático** en lugar de en **Recomendado**. A continuación, quite la etiqueta del documento (si está aplicada) y copie el archivo en un repositorio de datos para el analizador. Para pruebas rápidas, podría tratarse de una carpeta local en el equipo del analizador.<br /><br /> Si bien puede ejecutar el analizador incluso si no ha configurado las etiquetas que aplican la clasificación automática, este escenario no se incluye en estas instrucciones. [Más información](#using-the-scanner-with-alternative-configurations)|
|Para que se examinen los sitios y las bibliotecas de SharePoint:<br /><br />- SharePoint 2016<br /><br />- SharePoint 2013<br /><br />- SharePoint 2010|El analizador no admite otras versiones de SharePoint.<br /><br />Para grandes granjas de servidores de SharePoint, compruebe si necesita aumentar el umbral de vista de lista (de manera predeterminada, 5000) para que el analizador acceda a todos los archivos. Para obtener más información, vea la siguiente documentación de SharePoint: [Administrar listas y bibliotecas grandes en SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)|
|Para los documentos de Office que se van a examinar:<br /><br />- Formatos de archivo 97-2003 y formatos Open XML de Office para Word, Excel y PowerPoint|Para obtener más información sobre los tipos de archivo que el analizador admite para estos formatos de archivo, vea [Tipos de archivos compatibles con el cliente de Azure Information Protection](./rms-client/client-admin-guide-file-types.md)|
|Para rutas de acceso largas:<br /><br />- Máximo de 260 caracteres, a menos que el analizador esté instalado en Windows 2016 y el equipo esté configurado para admitir rutas de acceso largas|Windows 10 y Windows Server 2016 admiten longitudes de ruta de acceso de más de 260 caracteres con la siguiente [configuración de directiva de grupo](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/): **Directiva de equipo local** > **Configuración del equipo** > **Plantillas administrativas** > **Todas las configuraciones** > **NTFS** > **Habilitar rutas de acceso Win32 largas**<br /><br /> Para obtener más información, vea la sección [Maximum Path Length Limitation](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) (Limitación de longitud máxima de ruta de acceso) de la documentación para desarrolladores de Windows 10.

Si no se cumplen todos los requisitos de la tabla porque están prohibidos por las directivas de la organización, consulte alternativas en la sección siguiente.

Si se cumplen todos los requisitos, vaya directamente a la [sección de instalación](#install-the-scanner).

### <a name="deploying-the-scanner-with-alternative-configurations"></a>Implementación del analizador con configuraciones alternativas

Los requisitos previos descritos en la tabla son los requisitos predeterminados para el analizador y se recomiendan porque son la configuración más sencilla para la implementación del analizador. Deben ser adecuados para las pruebas iniciales de manera que pueda comprobar la funcionalidad del analizador. Sin embargo, en un entorno de producción, las directivas de la organización podrían prohibir estos requisitos predeterminados debido a una o varias de las siguientes restricciones:

- No se permite la conectividad a Internet en los servidores

- No se puede conceder el rol de administrador del sistema o las bases de datos deben crearse y configurarse manualmente

- No se puede conceder a las cuentas de servicio el derecho **Iniciar sesión localmente**

- No se pueden sincronizar las cuentas de servicio con Azure Active Directory, pero los servidores tienen conectividad a Internet

El analizador puede superar a estas restricciones, pero requieren una configuración adicional.


#### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>Restricción: el servidor del analizador no tiene conectividad a Internet

Siga las instrucciones para un [equipo desconectado](./rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers). 

Tenga en cuenta que, en esta configuración, el analizador no puede aplicar protección (o quitar protección) mediante el uso de la clave de su organización basada en la nube. En su lugar, el analizador está limitado al uso de etiquetas que aplican solo clasificación, o protección que usa [HYOK](configure-adrms-restrictions.md). 

#### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>Restricción: No se puede conceder el rol de administrador del sistema o las bases de datos deben crearse y configurarse manualmente

Si no se le puede conceder el rol de administrador del sistema para instalar el analizador, puede quitar este rol una vez completada la instalación del analizador. Cuando se usa esta configuración, la base de datos se crea automáticamente y se le conceden automáticamente los permisos necesarios a la cuenta de servicio para el analizador. Sin embargo, la cuenta de usuario que configura el analizador requiere el rol db_owner para la base de datos AzInfoProtectionScanner, y debe conceder manualmente este rol a la cuenta de usuario.

Si se no se le puede conceder el rol de administrador del sistema ni siquiera temporalmente, debe crear manualmente una base de datos denominada AzInfoProtectionScanner antes de instalar el analizador. Cuando se use esta configuración, asigne los roles siguientes:
    
|Cuenta|Rol de nivel de base de datos|
|--------------------------------|---------------------|
|Cuenta de servicio para el analizador|db_owner|
|Cuenta de usuario para la instalación del analizador|db_owner|
|Cuenta de usuario para la configuración del analizador |db_owner|

Normalmente, usará la misma cuenta de usuario para instalar y configurar el analizador. Pero si usa cuentas diferentes, ambas requieren el rol db_owner para la base de datos AzInfoProtectionScanner.

#### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>Restricción: no se puede conceder a la cuenta de servicio del analizador el derecho **Iniciar sesión localmente**

Si las directivas de la organización prohíben el derecho **Iniciar sesión localmente**, pero permiten el derecho **Iniciar sesión como proceso por lotes**, siga las instrucciones de [Especificación y uso del parámetro Token en Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) en la guía del administrador.

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>Restricción: no se puede sincronizar la cuenta de servicio del analizador con Azure Active Directory, pero el servidor tiene conectividad a Internet

Puede tener una cuenta para ejecutar el servicio del analizador y usar otra cuenta para autenticarse en Azure Active Directory:

- Para la cuenta de servicio del analizador, puede usar una cuenta de Windows local o una cuenta de Active Directory.

- Para la cuenta de Azure Active Directory, siga las instrucciones de [Especificación y uso del parámetro Token en Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) en la guía del administrador.


## <a name="install-the-scanner"></a>Instalación del escáner

1. Inicie sesión en el equipo de Windows Server en el que se ejecutará el analizador. Use una cuenta que tenga derechos de administrador local y que tenga permisos para escribir en la base de datos maestra de SQL Server.

2. Inicie una sesión de Windows PowerShell con la opción **Ejecutar como administrador**.

3. Ejecute el cmdlet [AIPScanner Install](/powershell/module/azureinformationprotection/Install-AIPScanner) y especifique la instancia de SQL Server en la que se va a crear una base de datos para el analizador de Azure Information Protection: 
    
    ```
    Install-AIPScanner -SqlServerInstance <name>
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

## <a name="get-an-azure-ad-token-for-the-scanner"></a>Obtención de un token de Azure AD para el escáner

El token de Azure AD permite la autenticación de la cuenta de servicio del escáner en el servicio Azure Information Protection.

1. Desde el mismo equipo con Windows Server, o desde el escritorio, inicie sesión en Azure Portal para crear dos aplicaciones de Azure AD que son necesarias para especificar un token de acceso para la autenticación. Después de un inicio de sesión interactivo inicial, este token permite que el analizador se ejecute de forma no interactiva.
    
    Para crear estas aplicaciones, siga las instrucciones de [Cómo etiquetar archivos de manera no interactiva para Azure Information Protection](./rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) de la guía del administrador.

2. En el equipo de Windows Server, si se ha concedido el **derecho de iniciar sesión localmente** a la cuenta del servicio de analizador: inicie sesión con esta cuenta e inicie una sesión de PowerShell. Ejecute [AIPAuthentication conjunto](/powershell/module/azureinformationprotection/set-aipauthentication), especificando los valores que ha copiado en el paso anterior:
    
    ```
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application> -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application>
    ```
    
    Cuando se le solicite, especifique la contraseña de las credenciales de la cuenta de servicio para Azure AD y, a continuación, haga clic en **Aceptar**.
    
    Si no se puede conceder el derecho **Iniciar sesión localmente** a su cuenta de servicio del analizador: siga las instrucciones en la sección [Especificación y uso del parámetro Token en Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) en la guía de administración. 

El analizador tiene ahora un token para autenticarse en Azure AD, que es válido durante un año, dos años, o nunca expira, según la configuración de la **aplicación web/API** en Azure AD. Cuando expire el token, deberá repetir los pasos 1 y 2.

Ahora está listo para especificar los almacenes de datos que se deben analizar. 

## <a name="specify-data-stores-for-the-scanner"></a>Especificación de los almacenes de datos para el escáner

Use el cmdlet [Add-AIPScannerRepository](/powershell/module/azureinformationprotection/Add-AIPScannerRepository) para especificar los almacenes de datos que el analizador de Azure Information Protection debe analizar. Puede especificar carpetas locales, rutas UNC y direcciones URL de SharePoint Server para los sitios y las bibliotecas de SharePoint. 

Versiones compatibles de SharePoint: SharePoint Server 2016 y SharePoint Server 2013. SharePoint Server 2010 también se admite en clientes que tengan [compatibilidad ampliada para esta versión de SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).

1. Desde el mismo equipo con Windows Server, en la sesión de PowerShell, ejecute el comando siguiente para agregar el primer almacén de datos:
    
        Add-AIPScannerRepository -Path <path>
    
    Por ejemplo: `Add-AIPScannerRepository -Path \\NAS\Documents`
    
    Para obtener otros ejemplos, consulte la [ayuda en línea](/powershell/module/azureinformationprotection/Add-AIPScannerRepository#examples) sobre este cmdlet.

2. Repita este comando para todos los almacenes de datos que quiera analizar. Si necesita eliminar un almacén de datos que ha agregado, use el cmdlet [Remove-AIPScannerRepository](/powershell/module/azureinformationprotection/Remove-AIPScannerRepository).

3. Ejecute el cmdlet [Get-AIPScannerRepository](/powershell/module/azureinformationprotection/Get-AIPScannerRepository) para confirmar que ha especificado correctamente todos los almacenes de datos:
    
        Get-AIPScannerRepository

Con la configuración predeterminada del analizador, ahora está listo para ejecutar el primer examen en modo de detección.

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>Ejecución de un ciclo de detección y visualización de informes del escáner

1. En la sesión de PowerShell, inicie el analizador ejecutando el comando siguiente:
    
        Start-AIPScan
    
    Como alternativa, puede iniciar el analizador desde Azure Portal. En la hoja **Azure Information Protection: Nodos**, seleccione el nodo del analizador y, a continuación, la opción **Examinar ahora**:
    
    ![Inicio del examen con el analizador de Azure Information Protection](./media/scanner-scan-now.png)

2. Espere a que el escáner complete su ciclo y ejecute el comando siguiente:
    
        Get-AIPScannerStatus
    
    Como alternativa, puede ver el estado en la hoja **Azure Information Protection: Nodos** de Azure Portal, seleccionando la columna **ESTADO**.
    
    Busque el estado para mostrar **Inactivo** en lugar de **Examinando**.
    
    Cuando el analizador haya rastreado todos los archivos de los almacenes de datos que ha especificado, el analizador se detendrá, aunque el servicio del analizador sigue ejecutándose.
    
    Compruebe el registro de eventos local de Windows **Aplicaciones y servicios**, **Azure Information Protection**. Este registro también informa cuando el escáner ha terminado de examinar, con un resumen de los resultados. Busque el id. de evento informativo **911**.

3. Revise los informes almacenados en %*localappdata*%\Microsoft\MSIP\Scanner\Reports. Los archivos .txt de resumen incluyen el tiempo invertido en analizar, el número de archivos examinados y cuántos archivos tenían una coincidencia para los tipos de información. Los archivos .csv contienen más detalles para cada archivo. Esta carpeta contiene hasta 60 informes de cada ciclo de examen y, todos, menos el último, se comprimen para ayudar a minimizar el espacio en disco necesario.
    
    > [!NOTE]
    > Puede cambiar el nivel de registro con el parámetro *ReportLevel* mediante [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/set-aipscannerconfiguration), pero no puede cambiar el nombre ni la ubicación de la carpeta del informe. Considere la posibilidad de utilizar una unión de directorio para la carpeta si desea almacenar los informes en una partición o un volumen diferentes.
    >
    > Por ejemplo, con el comando [Mklink](/windows-server/administration/windows-commands/mklink): `mklink /j D:\Scanner_reports C:\Users\aipscannersvc\AppData\Local\Microsoft\MSIP\Scanner\Reports`
    
    Con la configuración predeterminada, solo los archivos que cumplen las condiciones configuradas para la clasificación automática se incluyen en los informes detallados. Si no ve ninguna etiqueta aplicada en estos informes, compruebe que la configuración de etiquetas incluye la clasificación automática en lugar de la recomendada.
    
    > [!TIP]
    > Los escáneres envían esta información a Azure Information Protection cada cinco minutos para que pueda ver los resultados casi en tiempo real desde Azure Portal. Para más información, consulte [Reporting for Azure Information Protection](reports-aip.md) (Informes para Azure Information Protection). 
        
    Si los resultados no son los esperados, tendrá que ajustar las condiciones que ha especificado en la directiva de Azure Information Protection. Si es así, repita los pasos del 1 al 3 hasta que esté listo para cambiar la configuración para aplicar la clasificación y, opcionalmente, la protección. 

Cuando esté listo para etiquetar automáticamente los archivos que el analizador detecta, continúe con el procedimiento siguiente. 

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>Configuración del escáner para aplicar la clasificación y protección

En su configuración predeterminada, el analizador se ejecuta una vez y en el modo solo informe. Para cambiar esta configuración, ejecute el cmdlet [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).

1. En el equipo con Windows Server, en la sesión de PowerShell, ejecute el siguiente comando:
    
        Set-AIPScannerConfiguration -Enforce On -Schedule Always
    
    Hay otras opciones de configuración que tal vez quiera cambiar. Por ejemplo, si se cambian los atributos de archivo y lo que se registra en los informes. Además, si la directiva de Azure Information Protection incluye la configuración que requiere un mensaje de justificación para bajar el nivel de clasificación o quitar la protección, especifique ese mensaje mediante el uso de este cmdlet. Use la [ayuda en línea](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration#optional-parameters) para obtener más información sobre cada opción de configuración. 

2. Tome nota de la hora actual y vuelva a iniciar el escáner mediante la ejecución del comando siguiente:
    
        Start-AIPScan
    
    Como alternativa, puede iniciar el analizador desde Azure Portal. En la hoja **Azure Information Protection: Nodos**, seleccione el nodo del analizador y, a continuación, la opción **Examinar ahora**:
    
    ![Inicio del examen con el analizador de Azure Information Protection](./media/scanner-scan-now.png)

3. Vuelva a supervisar el registro de eventos para el tipo informativo **911**, con una marca de tiempo posterior a cuando se inició el examen en el paso anterior. 
    
    Después, compruebe los informes para ver qué archivos se han etiquetado, qué clasificación se ha aplicado a cada archivo y si se les ha aplicado la protección. O bien, utilice Azure Portal para ver más fácilmente esta información.

Dado que hemos configurado la programación para que se ejecute continuamente, cuando el escáner haya completado el examen de todos los archivos, iniciará un nuevo ciclo para detectar cualquier archivo nuevo y modificado.


## <a name="how-files-are-scanned"></a>¿Cómo se examinan los archivos?

El analizador pasar por los siguientes procesos cuando examina los archivos.

### <a name="1-determine-whether-files-are-included-or-excluded-for-scanning"></a>1. Determinar si los archivos se incluyen o excluyen para el análisis 
El analizador omite automáticamente los archivos que se [excluyen de la clasificación y la protección](./rms-client/client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection), como los archivos ejecutables y los archivos del sistema.

Puede cambiar este comportamiento mediante la definición de una lista de tipos de archivo para examinar o excluir del análisis. Al especificar esta lista y no especificar un repositorio de datos, la lista se aplica a todos los repositorios de datos que no tienen su propia lista especificada. Para especificar esta lista, use [Set-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Set-AIPScannerScannedFileTypes). 

Después de haber especificado la lista de tipos de archivo, puede agregar un nuevo tipo de archivo a la lista mediante [Add-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Add-AIPScannerScannedFileTypes), y quitar un tipo de archivo de la lista mediante [Remove-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Remove-AIPScannerScannedFileTypes).

### <a name="2-inspect-and-label-files"></a>2. Inspeccionar y etiquetar los archivos

Después el analizador usa filtros para buscar tipos de archivo admitidos. El sistema operativo usa estos mismos filtros para Windows Search y la indización. Sin ninguna configuración adicional, se usa Windows IFilter se usa para analizar los tipos de archivo que usan Word, Excel, PowerPoint y para documentos PDF y archivos de texto.

Para obtener una lista completa de tipos de archivo que se admiten de forma predeterminada e información adicional sobre cómo configurar los filtros existentes que incluyan archivos .tiff y archivos .zip, vea [Tipos de archivo compatibles para inspección](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-inspection).

Después de la inspección, estos tipos de archivo pueden etiquetarse mediante las condiciones que ha especificado para las etiquetas. O bien, si está utilizando el modo de detección, se pueden notificar que estos archivos contienen las condiciones que ha especificado para las etiquetas, o todos los tipos conocidos de información confidencial. 

Con todo, el analizador no puede etiquetar los archivos en las siguientes circunstancias:

- Si la etiqueta aplica clasificación pero no protección, y el tipo de archivo no [admiten la clasificación solo](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only).

- Si la etiqueta aplica clasificación y protección, pero el analizador no protege el tipo de archivo.
    
    De forma predeterminada, el analizador protege solo tipos de archivos de Office y archivos PDF cuando están protegidos mediante el estándar ISO para el cifrado de archivos PDF. Pueden protegerse otros tipos de archivos cuando se [edita el registro](#editing-the-registry-for-the-scanner) tal como se describe en la siguiente sección.

Por ejemplo, después de inspeccionar los archivos que tienen una extensión .txt, el analizador no puede aplicar una etiqueta que está configurada para la clasificación, pero no la protección, porque el tipo de archivo .txt no admite solo clasificación. Si la etiqueta está configurada para protección y clasificación y se modifica el registro para el tipo de archivo .txt, el analizador puede etiquetar el archivo. 

> [!TIP]
> Durante este proceso, si el analizador se detiene y no completa el examen de un gran número de archivos en un repositorio:
> 
> - Es posible que tenga que aumentar el número de puertos dinámicos del sistema operativo que hospeda los archivos. Refuerzo de los servidores de SharePoint puede ser uno de los motivos por los que el analizador supera el número de conexiones de red permitido y, por tanto, se detiene.
>     
>     Para comprobar si esta es la causa por la que se detiene el analizador, busque para ver si el siguiente mensaje de error se registra para el analizador en %*localappdata*%\Microsoft\MSIP\Logs\MSIPScanner.iplog (si hay varios registros se comprimen en zip): **No se puede conectar al servidor remoto---> System.Net.Sockets.SocketException: Solo se permite un uso de cada dirección de socket (protocolo/dirección de red/puerto) de IP:port**
>    
>     Para obtener más información sobre cómo ver el intervalo de puerto actual y aumentar el intervalo, vea [Configuración que puede modificarse para mejorar el rendimiento de red](https://docs.microsoft.com/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance).
> 
> - Para grandes granjas de servidores de SharePoint, es posible que tenga que aumentar el umbral de vista de lista (de manera predeterminada, 5000). Para obtener más información, vea la siguiente documentación de SharePoint: [Administrar listas y bibliotecas grandes en SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server).

### <a name="3-label-files-that-cant-be-inspected"></a>3. Etiquetar los archivos que no se pueden inspeccionar
Para los tipos de archivo que no se pueden inspeccionar, el analizador aplica la etiqueta predeterminada en la directiva de Azure Information Protection, o la etiqueta predeterminada que configure para el analizador.

Como en el paso anterior, el analizador no puede etiquetar los archivos en las siguientes circunstancias:

- Si la etiqueta aplica clasificación pero no protección, y el tipo de archivo no [admiten la clasificación solo](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only).

- Si la etiqueta aplica clasificación y protección, pero el analizador no protege el tipo de archivo.
    
    De forma predeterminada, el analizador protege solo tipos de archivos de Office y archivos PDF cuando están protegidos mediante el estándar ISO para el cifrado de archivos PDF. Pueden protegerse otros tipos de archivos cuando se [edita el registro](#editing-the-registry-for-the-scanner) tal como se describe a continuación.


### <a name="editing-the-registry-for-the-scanner"></a>Edición del registro para el analizador

Para cambiar este comportamiento predeterminado del analizador para proteger otros tipos de archivo que no sean de Office y PDF, debe editar el registro manualmente y especificar los tipos de archivo adicionales que quiere que estén protegidos, y el tipo de protección (nativa o genérica). Para obtener instrucciones, vea [Configuración de la API de archivo](develop/file-api-configuration.md) en la guía del desarrollador. En esta documentación para desarrolladores, se hace referencia a la protección genérica como "PFile". Además, establezca lo siguiente para el analizador:

- El analizador tiene su propio comportamiento predeterminado: Solo los formatos de archivo de Office y documentos PDF están protegidos de forma predeterminada. Si no se modifica el registro, el analizador no protegerá ni etiquetará ningún otro tipo de archivo.

- Si quiere el mismo comportamiento de protección predeterminado del cliente de Azure Information Protection, donde todos los archivos se protegen automáticamente con protección nativa o genérica: especifique el comodín `*` como clave del Registro y `Default` como datos de valor.

Cuando edite el registro, cree manualmente la clave **MSIPC** y la clave **FileProtection** si no existen, así como una clave para cada extensión de nombre de archivo.

Por ejemplo, para que el escáner proteja las imágenes TIFF además de los archivos de Office y PDF, el registro después de que se haya editado tendrá un aspecto similar al de la siguiente ilustración. Como un archivo de imagen, los archivos TIFF admiten la protección nativa y la extensión de nombre de archivo resultante es .ptiff.

![Edición del registro para que el analizador aplique la protección](./media/editregistry-scanner.png)

Para obtener una lista de tipos de archivo de texto e imágenes que admiten la protección nativa de forma similar pero deben especificarse en el registro, vea [Tipos de archivos compatibles para protección y clasificación](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection) en la Guía del administrador.

Para los archivos que no son compatibles con la protección nativa, especifique la extensión de nombre de archivo como una nueva clave y **PFile** para protección genérica. La extensión de nombre de archivo resultante para el archivo protegido es .pfile.


## <a name="when-files-are-rescanned"></a>¿Cuándo se vuelven a examinan los archivos?

En el primer ciclo de examen, el analizador inspecciona todos los archivos de los almacenes de datos configurados y, después, en los exámenes posteriores, solo inspecciona los archivos nuevos o modificados. 

Puede forzar al analizador a que inspeccione de nuevo todos los archivos mediante la ejecución de [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan) con el parámetro `-Reset`. El analizador debe configurarse para una programación manual, lo que requiere que el parámetro `-Schedule` se establezca en **Manual** con [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).

Como alternativa, puede forzar que el analizador vuelva a inspeccionar todos los archivos desde la hoja **Azure Information Protection: Nodos** de Azure Portal. Seleccione el analizador en la lista y, a continuación, seleccione la opción **Rescan all files** (Volver a examinar todos los archivos):

![Volver a examinar con al analizador de Azure Information Protection](./media/scanner-rescan-files.png)

Volver a inspeccionar todos los archivos resulta útil si quiere que los informes incluyan todos los archivos. Esta opción de configuración suele usarse cuando el analizador se ejecuta en modo de detección. Cuando finaliza el examen completo, el tipo de examen cambia automáticamente a incremental para que en los análisis posteriores solo se examinen los archivos nuevos o modificados.

Además, se inspeccionan todos los archivos cuando el analizador descarga una directiva de Azure Information Protection con condiciones nuevas o modificadas. El analizador actualiza la directiva cada hora y cuando se inicia el servicio y la directiva es anterior a una hora.  

> [!TIP]
> Si necesita actualizar la directiva antes de este intervalo de una hora, por ejemplo, durante un período de prueba: Elimine manualmente el archivo de directiva, **Policy.msip** de **%LocalAppData%\Microsoft\MSIP\Policy.msip** y de **%LocalAppData%\Microsoft\MSIP\Scanner**. Después, reinicie el servicio Analizador de Azure Information Protection.
> 
> Si ha cambiado la configuración de protección de la directiva, también deberá esperar 15 minutos desde el guardado de la configuración de protección para reiniciar el servicio.

Si el analizador ha descargado una directiva sin ninguna condición automática configurada, la copia del archivo de la directiva que esté en la carpeta del analizador no se actualizará. En tal caso, deberá eliminar el archivo de directiva, **Policy.msip**, de **%LocalAppData%\Microsoft\MSIP\Policy.msip** y **%LocalAppData%\Microsoft\MSIP\Scanner** para que el analizador pueda usar un archivo de directiva recientemente descargado que contenga etiquetas configuradas correctamente para las condiciones automáticas.

## <a name="using-the-scanner-with-alternative-configurations"></a>Uso del analizador con configuraciones alternativas

Existen dos escenarios alternativos que el escáner de Azure Information Protection admite donde no es necesario que las etiquetas se configuren para ninguna condición: 
- Aplique una etiqueta predeterminada a todos los archivos en un repositorio de datos.
    
    Para esta configuración, utilice el cmdlet [Set-AIPScannerRepository](/powershell/module/azureinformationprotection/Set-AIPScannerRepository) y establezca el parámetro *MatchPolicy* en **Off**. 
    
    El contenido de los archivos no se inspecciona y todos los archivos del repositorio de datos se etiquetan con arreglo a la etiqueta predeterminada que especifique para el repositorio de datos (con el parámetro *SetDefaultLabel*) o, si esto no se especifica, la etiqueta predeterminada que se determine como valor de directiva para la cuenta del analizador.
    

- Identifique todas las condiciones personalizadas y los tipos conocidos de información confidencial.
    
    Para esta configuración, utilice el cmdlet [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) y establezca el parámetro *DiscoverInformationTypes* en **All**.
    
    El analizador utiliza cualquier condición personalizada que haya especificado para las etiquetas en la directiva de Azure Information Protection, y la lista de tipos de información que están disponibles para especificar para las etiquetas en la directiva de Azure Information Protection.
    
    En este Inicio rápido se usa esta configuración: [Inicio rápido: Búsqueda de información confidencial](quickstart-findsensitiveinfo.md).

## <a name="optimizing-the-performance-of-the-scanner"></a>Optimización del rendimiento del escáner

Para maximizar el rendimiento del analizador:

- **Use una conexión de red de alta velocidad y estable entre el equipo que actúa como analizador y el almacén para los datos examinados**.
    
    Por ejemplo, conecte el equipo que actúa como analizador a la misma red LAN o al mismo segmento de red que el almacén de datos examinados (se prefiere la segunda opción).
    
    La calidad de la conexión de red afecta al rendimiento del analizador, ya que, al inspeccionar archivos, el analizador transfiere el contenido de los archivos al equipo que ejecuta el servicio de examen. Al reducir (o eliminar) el número de saltos de red que los datos deben realizar, también se reduce la carga de la red. 

- **Asegúrese de que el equipo que actúa como analizador tenga recursos del procesador disponibles**.
    
    Inspeccione el contenido de los archivos para obtener una coincidencia según las condiciones que haya configurado. Las acciones de cifrado y descifrado de archivos suponen una carga elevada para el procesador. Supervise los ciclos de examen típicos de los almacenes de datos que haya especificado para identificar si la falta de recursos del procesador afecta negativamente al rendimiento del analizador.
    
- **No examine carpetas locales del equipo que ejecute el servicio de analizador**.
    
    Si tiene carpetas para examinar en un servidor Windows, instale el analizador en otro equipo y configure las carpetas como recursos compartidos de red para realizar el examen. Al separar ambas funciones de los archivos de hospedaje y de examen, los recursos de cálculo de esos servicios no interferirán entre sí.

Si es necesario, instale varias instancias del analizador. Cada instancia del analizador requiere su propia base de datos de configuración en otra instancia de SQL Server.

Otros factores que influyen en el rendimiento del analizador:

- La carga actual y los tiempos de respuesta de los almacenes de datos que contienen los archivos para examinar.

- Ejecución del analizador en modo de detección o aplicación
    
    El modo de detección suele tener un ritmo de examen superior en comparación con el modo de aplicación, ya que la detección requiere una única acción de lectura de archivo, mientras que el modo de aplicación requiere acciones de lectura y escritura.

- Cambio de las condiciones de Azure Information Protection
    
    Obviamente, el primer ciclo de examen, que se produce cuando el analizador inspecciona todos los archivos, requerirá más tiempo que los siguientes ciclos de examen, ya que, de forma predeterminada, solo se examinan los archivos nuevos o modificados. Sin embargo, si cambia las condiciones de la directiva de Azure Information Protection, todos los archivos se examinarán una vez más, tal como se describe en la [sección anterior](#when-files-are-rescanned).

- Elección del nivel de registro
    
    Puede elegir entre **Depurar**, **Información**, **Error** y **Desactivado** para los informes del analizador. **Desactivado** da como resultado un rendimiento óptimo; **Depurar** ralentiza considerablemente el analizador y debe usarse solo para solucionar problemas. Para obtener más información, consulte el parámetro *ReportLevel* del cmdlet [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).

- En cuanto a los archivos:
    
    - Los archivos de Office se examinan más rápido que los archivos PDF.
    
    - Los desprotegidos se examinan más rápido que los protegidos.
    
    - Obviamente, los archivos de gran tamaño se examinan más lentamente que aquellos más pequeños.

- Además:
    
    - Confirme que la cuenta de servicio que ejecuta el analizador tiene únicamente los derechos que se documentan en la sección de [requisitos previos del analizador](#prerequisites-for-the-azure-information-protection-scanner) y, a continuación, configure la [propiedad de cliente avanzada](./rms-client/client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner) para deshabilitar el nivel de integridad bajo para el analizador.
    
    - El analizador se ejecuta más rápidamente cuando se usa la [configuración alternativa](#using-the-scanner-with-alternative-configurations) para aplicar una etiqueta predeterminada a todos los archivos porque el analizador no inspecciona el contenido del archivo.
    
    - El analizador se ejecuta más lentamente cuando se usa la [configuración alternativa](#using-the-scanner-with-alternative-configurations) para identificar todas las condiciones personalizadas y los tipos conocidos de información confidencial.
    

## <a name="list-of-cmdlets-for-the-scanner"></a>Lista de cmdlets para el escáner 

Otros cmdlets del analizador le permiten cambiar la cuenta de servicio y la base de datos del analizador, obtener la configuración actual del analizador y desinstalar el servicio del analizador. El analizador utiliza los siguientes cmdlets:

- [Add-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Add-AIPScannerScannedFileTypes)

- [Add-AIPScannerRepository](/powershell/module/azureinformationprotection/Add-AIPScannerRepository)

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerRepository](/powershell/module/azureinformationprotection/Get-AIPScannerRepository)

- [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Remove-AIPScannerRepository](/powershell/module/azureinformationprotection/Remove-AIPScannerRepository)

- [Remove-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Remove-AIPScannerScannedFileTypes)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [Set-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Set-AIPScannerScannedFileTypes)

- [Set-AIPScannerRepository](/powershell/module/azureinformationprotection/Set-AIPScannerRepository)

- [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)

- [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner)


## <a name="event-log-ids-and-descriptions-for-the-scanner"></a>Identificadores de registro de eventos y descripciones para el escáner

Use las siguientes secciones para identificar los id. de eventos y las descripciones posibles para el analizador. Estos eventos se registran en el servidor que ejecuta el servicio analizador, en el registro de eventos de **aplicaciones y servicios** de Windows, **Azure Information Protection**.

-----

Información **910**

**Se ha iniciado el ciclo del analizador.**

Este evento se registra cuando el servicio del analizador se inicia y comienza a examinar los archivos en los repositorios de datos que ha especificado.

----

Información **911**

**Ha finalizado el ciclo del analizador.**

Este evento se registra cuando el analizador ha terminado un examen manual o el analizador ha terminado un ciclo para una programación continua.

Si el analizador se ha configurado para ejecutarse manualmente en lugar de continuamente, use el cmdlet [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan) para ejecutar un nuevo examen. Para cambiar la programación, use el cmdlet [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) y el parámetro **Schedule**.

----

## <a name="next-steps"></a>Pasos siguientes

¿Está interesado en cómo el equipo de ingeniería y operaciones de servicios centrales de Microsoft ha implementado este escáner?  Lea el caso práctico técnico: [Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner) (Automatización de la protección de datos con el escáner de Azure Information Protection).

Tal vez se pregunte: [¿Cuál es la diferencia entre FCI de Windows Server y el analizador de Azure Information Protection?](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

También puede usar PowerShell para clasificar y proteger los archivos de forma interactiva desde el equipo de escritorio. Para obtener más información sobre este y otros escenarios en que se utiliza PowerShell, consulte [Uso de PowerShell con el cliente de Azure Information Protection](./rms-client/client-admin-guide-powershell.md).


