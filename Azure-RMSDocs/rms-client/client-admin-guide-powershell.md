---
title: Uso de PowerShell con el cliente de Azure Information Protection
description: "Instrucciones e información para que los administradores administren el cliente de Azure Information Protection con PowerShell."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/06/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4f9d2db7-ef27-47e6-b2a8-d6c039662d3c
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 27799ff64e8c224c64b0ffc858b79818650d74af
ms.sourcegitcommit: d32d1f5afa5ee9501615a6ecc4af8a4cd4901eae
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-client"></a>Guía del administrador: Uso de PowerShell con el cliente de Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Cuando se instala el cliente de Azure Information Protection, los comandos de PowerShell se instalan automáticamente. Esto le permite administrar el cliente mediante la ejecución de comandos que puede colocar en scripts para la automatización.

Los cmdlets se instalan con el módulo de PowerShell **AzureInformationProtection**. El módulo reemplaza al módulo de RMSProtection que se instala con la herramienta de protección de RMS. Si tiene instalada la herramienta RMSProtection al instalar el cliente de Azure Information Protection, el módulo RMSProtection se desinstala automáticamente.

El módulo AzureInformationProtection incluye todos los cmdlets de Rights Management de la herramienta de protección de RMS. También hay nuevos cmdlets que usan el servicio Azure Information Protection (AIP) para etiquetar. Por ejemplo:

|Cmdlet de etiquetado|Ejemplo de uso|
|----------------|---------------|
|[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)|Para una carpeta compartida, identifique todos los archivos con una etiqueta específica.|
|[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)|Para una carpeta compartida, revise el contenido del archivo y, luego, etiquete automáticamente los archivos no etiquetados, según las condiciones que especificó.|
|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)|Para una carpeta compartida, aplique una etiqueta específica a todos los archivos que no tienen ninguna etiqueta.|
|[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)|Etiqueta archivos de forma no interactiva, por ejemplo mediante un script que se ejecuta según una programación.|


Además, el [analizador de Azure Information Protection](../deploy-use/deploy-aip-scanner.md) (actualmente en versión preliminar), usa cmdlets para instalar y configurar un servicio en Windows Server. A continuación, este analizador le permite detectar, clasificar y proteger archivos en almacenes de datos.

Para obtener una lista de todos los cmdlets y su ayuda correspondiente, consulte [Módulo AzureInformationProtection](/powershell/module/azureinformationprotection). En una sesión de PowerShell, escriba `Get-Help <cmdlet name> -online` para acceder a la ayuda más reciente.  

Este módulo se instala en **\Archivos de programa (x86)\Microsoft Azure Information Protection** y agrega esta carpeta a la variable del sistema **PSModulePath**. El archivo .dll de este módulo se denomina **AIP.dll**.

Como con el módulo RMSProtection, la versión actual del módulo AzureInformationProtection tiene las siguientes limitaciones:

- Puede desproteger carpetas personales de Outlook (archivos .pst), pero actualmente no puede proteger de forma nativa estos archivos u otros archivos de contenedor con el uso de este módulo de PowerShell.

- Puede desproteger los mensajes de correo electrónico de Outlook protegidos (archivos .rpmsg) cuando están en una carpeta personal (.pst) de Outlook, pero no puede desproteger archivos .rpmsg fuera de una carpeta personal.

Antes de empezar a usar estos cmdlets, vea los requisitos previos adicionales y las instrucciones aplicables a su implementación:

- [Azure Information Protection y servicio Azure Rights Management](#azure-information-protection-service-and-azure-rights-management-service)

    - Aplicable si usa solo la clasificación o la clasificación con Rights Management Protection: tiene una suscripción que incluye Azure Information Protection (por ejemplo, Enterprise Mobility + Security).
    - Aplicable si usa solo la protección con el servicio Azure Rights Management: tiene una suscripción que incluye el servicio Azure Rights Management (por ejemplo, Office 365 E3 y Office 365 E5).

- [Active Directory Rights Management Services](#active-directory-rights-management-services)

    - Aplicable si usa solo la protección con la versión local de Azure Rights Management; Active Directory Rights Management Services (AD RMS).


## <a name="azure-information-protection-and-azure-rights-management-service"></a>Azure Information Protection y servicio Azure Rights Management

Lea esta sección antes de empezar a usar los comandos de PowerShell si su organización usa Azure Information Protection para la clasificación y la protección, o solo el servicio Azure Rights Management para la protección de datos.


### <a name="prerequisites"></a>Requisitos previos

Además de los requisitos previos para instalar el módulo AzureInformationProtection, existen requisitos previos adicionales para el etiquetado de Azure Information Protection y el servicio de protección de datos Azure Rights Management:

1. El servicio Azure Rights Management debe estar activado.

2. Para quitar la protección de los archivos para otros usuarios con su propia cuenta: 
    
    - La característica de superusuario debe habilitarse para su organización y su cuenta debe estar configurada para interactuar como superusuario en Azure Rights Management.

3. Para proteger o desproteger archivos directamente sin interacción del usuario: 
    
    - Cree una cuenta de entidad de servicio, ejecute RMSServerAuthentication y considere la posibilidad establecer dicha entidad de servicio como un superusuario para Azure Rights Management.

4. Para las regiones fuera de Estados Unidos: 
    
    - Edite el Registro para la detección de servicios.

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>Requisito previo 1: el servicio Azure Rights Management debe estar activado

Este requisito previo se aplica si utiliza la protección de datos mediante etiquetas o con una conexión directa al servicio Azure Rights Management para aplicar la protección de datos.

Si no está activado el inquilino de Azure Information Protection, vea las instrucciones en [Activar Azure Rights Management](../deploy-use/activate-service.md).

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>Requisito previo 2: quitar la protección de archivos para otros usuarios con su propia cuenta

Los escenarios típicos para quitar la protección de archivos para otros usuarios incluyen la detección de datos o la recuperación de datos. Si usa etiquetas para aplicar la protección, puede quitar la protección estableciendo una nueva etiqueta que no aplica protección o quitando la etiqueta. Pero lo mejor es que se conecte directamente al servicio Azure Rights Management para quitar la protección.

Debe tener permisos de uso de Rights Management para quitar la protección de archivos, o bien ser un superusuario. Para la detección o recuperación de datos, suele usarse la característica de superusuario. Para habilitar esta característica y configurar su cuenta como un superusuario, vea [Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos](../deploy-use/configure-super-users.md).

#### <a name="prerequisite-3-to-protect-or-unprotect-files-without-user-interaction"></a>Requisito previo 3: proteger o desproteger archivos sin interacción del usuario

Puede conectarse directamente al servicio Azure Rights Management de forma no interactiva para proteger o desproteger archivos.

Debe usar una cuenta de entidad de servicio para conectarse al servicio Azure Rights Management de forma no interactiva, lo que se hace mediante el cmdlet `Set-RMSServerAuthentication`. Debe hacerlo para cada sesión de Windows PowerShell que ejecuta cmdlets que se conectan directamente al servicio Azure Rights Management. Antes de ejecutar este cmdlet, debe disponer de estos tres identificadores:

- BposTenantId

- AppPrincipalId

- Clave simétrica

Puede usar los siguientes comandos de PowerShell y las instrucciones comentadas para obtener automáticamente los valores de los identificadores y ejecutar el cmdlet Set-RMSServerAuthentication. También puede obtener y especificar los valores manualmente.

Para obtener los valores automáticamente y ejecutar Set-RMSServerAuthentication:

````
# Make sure that you have the AADRM and MSOnline modules installed

$newServicePrincipalName="<new service principal name>"
Connect-AadrmService
$bposTenantID=(Get-AadrmConfiguration).BPOSId
Disconnect-AadrmService
Connect-MsolService
New-MsolServicePrincipal -DisplayName $servicePrincipalName

# Copy the value of the generated symmetric key

$symmetricKey="<value from the display of the New-MsolServicePrincipal command>"
$appPrincipalID=(Get-MsolServicePrincipal | Where { $_.DisplayName -eq $servicePrincipalName }).AppPrincipalId
Set-RMSServerAuthentication -Key $symmetricKey -AppPrincipalId $appPrincipalID -BposTenantId $bposTenantID

````

En las secciones siguientes se explica cómo obtener manualmente y especificar estos valores, con más información sobre cada paso.

##### <a name="to-get-the-bpostenantid"></a>Para obtener BposTenantId

Ejecute el cmdlet Get-AadrmConfiguration desde el módulo de Windows PowerShell para Azure RMS:

1. Si este módulo aún no está instalado en el equipo, vea [Instalación de Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md).

2. Inicie Windows PowerShell con la opción **Ejecutar como administrador**.

3. Use el cmdlet `Connect-AadrmService` para conectarse al servicio Azure Rights Management:
    
        Connect-AadrmService
    
    Cuando se le solicite, escriba las credenciales de administrador de inquilinos de Azure Information Protection. Normalmente, usará una cuenta de administrador global de Office 365 o Azure Active Directory.
    
4. Ejecute `Get-AadrmConfiguration` y realice una copia del valor BPOSId.
    
    A continuación se muestra un ejemplo de salida de Get-AadrmConfiguration:
    
            BPOSId                                   : 23976bc6-dcd4-4173-9d96-dad1f48efd42
        
            RightsManagement ServiceId               : 1a302373-f233-440600909-4cdf305e2e76
        
            LicensingIntranetDistributionPointUrl    : https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/licensing
        
            LicensingExtranetDistributionPointUrl    : https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/licensing
        
            CertificationIntranetDistributionPointUrl: https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/certification
        
            CertificationExtranetDistributionPointUrl: https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/certification

5. Desconéctese del servicio:
    
        Disconnect-AadrmService

##### <a name="to-get-the-appprincipalid-and-symmetric-key"></a>Para obtener AppPrincipalId y la clave simétrica

Cree una entidad de servicio nueva mediante la ejecución del cmdlet `New-MsolServicePrincipal` desde el módulo MSOnline de PowerShell para Azure Active Directory y utilice las instrucciones siguientes. 

> [!IMPORTANT]
> No utilice el cmdlet de PowerShell de Azure AD más reciente, New-AzureADServicePrincipal, para crear esta entidad de servicio. El servicio Azure Rights Management no admite el comando New-AzureADServicePrincipal. 

1. Si el módulo MSOnline no está ya instalado en el equipo, ejecute `Install-Module MSOnline`.

2. Inicie Windows PowerShell con la opción **Ejecutar como administrador**.

3. Utilice el cmdlet **Connect-MsolService** para conectarse a Azure AD:
    
        Connect-MsolService
    
    Cuando se le pida, escriba las credenciales de administrador de inquilinos de Azure AD (normalmente, usará una cuenta de administrador global de Office 365 o Azure Active Directory).

4. Ejecute el cmdlet New-MsolServicePrincipal para crear una nueva entidad de servicio:
    
        New-MsolServicePrincipal
    
    Cuando se le solicite, escriba el nombre para mostrar que haya elegido para esta entidad de servicio que le ayuda a identificar su propósito más adelante como una cuenta para conectarse al servicio Azure Rights Management, a fin de que pueda proteger y desproteger archivos.
    
    Un ejemplo de la salida de New-MsolServicePrincipal:
    
        Supply values for the following parameters:
        
        DisplayName: AzureRMSProtectionServicePrincipal
        The following symmetric key was created as one was not supplied
        zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=
        
        Display Name: AzureRMSProtectionServicePrincipal
        ServicePrincipalNames: (b5e3f7g1-b5c2-4c96-a594-a0807f65bba4)
        ObjectId: 23720996-593c-4122-bfc7-1abb5a0b5109
        AppPrincialId: b5e3f76a-b5c2-4c96-a594-a0807f65bba4
        TrustedForDelegation: False
        AccountEnabled: True
        Addresses: ()
        KeyType: Symmetric
        KeyId: 8ef61651-ca11-48ea-a350-25834a1ba17c
        StartDate: 3/7/2014 4:43:59 AM
        EndDate: 3/7/2014 4:43:59 AM
        Usage: Verify

5. En esta salida, tome nota de la clave simétrica y de AppPrincipalId.

    Es importante que cree una copia de esta clave simétrica. No podrá recuperar la clave posteriormente, por lo que si no la conoce cuando tenga que autenticarse en el servicio Azure Rights Management, deberá crear una entidad de servicio.

A partir de estas instrucciones y de los ejemplos expuestos, se dispone de tres identificadores necesarios para ejecutar Set-RMSServerAuthentication:

- Id. de inquilino: **23976bc6-dcd4-4173-9d96-dad1f48efd42**

- Clave simétrica: **zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=**

- AppPrincipalId: **b5e3f76a-b5c2-4c96-a594-a0807f65bba4**

El comando de ejemplo presentará el siguiente aspecto:

    Set-RMSServerAuthentication -Key zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=-AppPrincipalId b5e3f76a-b5c2-4c96-a594-a0807f65bba4-BposTenantId 23976bc6-dcd4-4173-9d96-dad1f48efd42

Como se muestra en el comando anterior, puede proporcionar los valores con un solo comando, lo que haría en un script para que se ejecute de manera no interactiva. Pero para realizar una prueba, puede escribir Set-RMSServerAuthentication y proporcionar los valores uno a uno cuando se le pida. Cuando finalice la ejecución del comando, el cliente funcionará en "modo de servidor", lo que es adecuado para el uso no interactivo, como los scripts y la infraestructura de clasificación de archivos de Windows Server.

Considere la posibilidad de convertir esta cuenta de entidad de servicio en un superusuario: para asegurarse de que esta cuenta de entidad de servicio siempre pueda desproteger los archivos de otros usuarios, se puede configurar como superusuario. Del mismo modo que configura una cuenta de usuario estándar como superusuario, use el mismo cmdlet de Azure RMS, [Add-AadrmSuperUser](/powershell/aadrm/vlatest/Add-AadrmSuperUser.md), pero especifique el parámetro **ServicePrincipalId** con el valor de AppPrincipalId.

Para más información, vea [Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos](../deploy-use/configure-super-users.md).

> [!NOTE]
> Para utilizar su propia cuenta para autenticarse en el servicio Azure Rights Management, no hay necesidad de ejecutar Set-RMSServerAuthentication antes de proteger o desproteger archivos u obtener plantillas.

#### <a name="prerequisite-4-for-regions-outside-north-america"></a>Requisito previo 4: Para las regiones fuera de Estados Unidos

Si usa una cuenta de entidad de servicio para proteger archivos y descargar plantillas fuera de la región de Norteamérica de Azure, debe modificar el Registro: 

1. Vuelva a ejecutar el cmdlet Get-AadrmConfiguration y anote los valores de **CertificationExtranetDistributionPointUrl** y **LicensingExtranetDistributionPointUrl**.

2. En cada equipo donde se van a ejecutar los cmdlets AzureInformationProtection, abra el Editor del Registro y vaya a: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC`

3. Si no ve una clave **ServiceLocation**, créela, para que la ruta de acceso al registro aparezca como **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation**

4. Para la clave **ServiceLocation**, cree dos claves si no existen, denominadas **EnterpriseCertification** y **EnterprisePublishing**. 
    
    No cambie el nombre "(Default)" del valor de cadena que se crea automáticamente para estas claves, pero modifique la cadena para especificar los datos de los valores:

    - Para **EnterpriseCertification**, pegue el valor de CertificationExtranetDistributionPointUrl.
    
    - Para **EnterprisePublishing**, pegue el valor de LicensingExtranetDistributionPointUrl.
    
    Por ejemplo, la entrada del Registro de EnterpriseCertification debe ser similar a la siguiente:
    
    ![Editar el Registro del módulo de PowerShell de Azure Information Protection para regiones fuera de Norteamérica](../media/registry-example-rmsprotection.png)

5. Cierre el Editor del Registro. No es necesario reiniciar el equipo. Sin embargo, si usa una cuenta de entidad de servicio en lugar de su propia cuenta de usuario, debe ejecutar el comando Set-RMSServerAuthentication después realizar esta modificación del registro.

### <a name="example-scenarios-for-using-the-cmdlets-for-azure-information-protection-and-the-azure-rights-management-service"></a>Escenarios de ejemplo para usar los cmdlets de Azure Information Protection y del servicio Azure Rights Management

Resulta más eficaz utilizar etiquetas para clasificar y proteger archivos, porque solo necesita dos cmdlets, que se pueden ejecutar de forma autónoma o conjunta: [Get-AIPFileStatus](/powershell/azureinformationprotection/get-aipfilestatus) y [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel). Recurra a la ayuda de ambos cmdlets para obtener más información y ejemplos.

Sin embargo, para proteger o desproteger archivos conectándose directamente al servicio Azure Rights Management, normalmente debe ejecutar una serie de cmdlets como se describe a continuación.

En primer lugar, si necesita autenticarse en el servicio Azure Rights Management con una cuenta de entidad de servicio en lugar de usar su propia cuenta, en una sesión de PowerShell, escriba:

    Set-RMSServerAuthentication

Cuando se le solicite, escriba los tres identificadores como se describe en [Requisito previo 3: proteger o desproteger archivos sin interacción del usuario](client-admin-guide-powershell.md#prerequisite-3-to-protect-or-unprotect-files-without-user-interaction).

Para poder proteger los archivos, debe descargar las plantillas de Rights Management en el equipo e identificar la que se usará y el número de identificador correspondiente. En la salida, puede copiar el identificador de plantilla:

    Get-RMSTemplate
    
La salida puede ser parecida a la siguiente:

    TemplateId        : {82bf3474-6efe-4fa1-8827-d1bd93339119}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content cannot be modified.
    Name              : Contoso, Ltd - Confidential View Only
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    
    TemplateId        : {e6ee2481-26b9-45e5-b34a-f744eacd53b0}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content can be modified but cannot be copied and printed.
    Name              : Contoso, Ltd - Confidential
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    FromTemplate      : True

Tenga en cuenta que si no ejecuta el comando Set-RMSServerAuthentication, se autentica en el servicio Azure Rights Management con su propia cuenta de usuario. Si interactúa con un equipo que no está unido a un dominio, las credenciales actuales siempre se usan automáticamente. En cambio, si trabaja con un equipo de un grupo de trabajo, se le pide que inicie sesión en Azure, y estas credenciales se almacenan en la memoria caché para los comandos ulteriores. En este escenario, si más adelante necesita iniciar sesión como un usuario distinto, use el cmdlet `Clear-RMSAuthentication`.

Ahora que ya sabe el identificador de plantilla, puede utilizarlo con el cmdlet `Protect-RMSFile` para proteger un único archivo o todos los archivos de una carpeta. Por ejemplo, si desea proteger un único archivo y sobrescribir el original con el uso de la plantilla de "Contoso, Ltd - Confidencial":

    Protect-RMSFile -File C:\Test.docx -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

La salida puede ser parecida a la siguiente:

    InputFile             EncryptedFile
    ---------             -------------
    C:\Test.docx          C:\Test.docx

Para proteger todos los archivos de una carpeta, use el parámetro **-Folder** con una letra de unidad y la ruta de acceso, o la ruta de acceso UNC. Por ejemplo:

    Protect-RMSFile -Folder \Server1\Documents -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

La salida puede ser parecida a la siguiente:

    InputFile                          EncryptedFile
    ---------                          -------------
    \Server1\Documents\Test1.docx     \Server1\Documents\Test1.docx
    \Server1\Documents\Test2.docx     \Server1\Documents\Test2.docx
    \Server1\Documents\Test3.docx     \Server1\Documents\Test3.docx
    \Server1\Documents\Test4.docx     \Server1\Documents\Test4.docx

Si la extensión de nombre de archivo no cambia después de aplicar la protección, siempre se puede utilizar el cmdlet `Get-RMSFileStatus` más adelante para comprobar si el archivo está protegido. Por ejemplo:

    Get-RMSFileStatus -File \Server1\Documents\Test1.docx

La salida puede ser parecida a la siguiente:

    FileName                              Status
    --------                              ------
    \Server1\Documents\Test1.docx         Protected

Para desproteger un archivo, debe tener derechos de propietario o de extracción desde el momento en que se protegió el archivo, o bien debe ejecutar los cmdlets como superusuario. A continuación, use el cmdlet Unprotect. Por ejemplo:

    Unprotect-RMSFile C:\test.docx -InPlace

La salida puede ser parecida a la siguiente:

    InputFile                             DecryptedFile
    ---------                             -------------
    C:\Test.docx                          C:\Test.docx

Tenga en cuenta que si las plantillas de Rights Management cambian, debe volver a descargarlas con `Get-RMSTemplate -force`. 

## <a name="active-directory-rights-management-services"></a>Active Directory Rights Management Services

Lea esta sección antes de empezar a utilizar los comandos de PowerShell para proteger o desproteger archivos si su organización usa simplemente Active Directory Rights Management Services.


### <a name="prerequisites"></a>Requisitos previos

Además de los requisitos previos para instalar el módulo AzureInformationProtection, la cuenta usada para proteger o desproteger archivos debe tener permisos de lectura y ejecución para acceder a ServerCertification.asmx:

1. Inicie sesión en un servidor de AD RMS.

2. Haga clic en **Inicio** y luego en **Equipo**.

3. En el Explorador de archivos, vaya a %systemdrive%\Initpub\wwwroot\_wmsc\Certification.

4. Haga clic con el botón derecho en **ServerCertification.asmx** y luego haga clic en **Propiedades**.

5. En el cuadro de diálogo **Propiedades de ServerCertification.asmx**, haga clic en la pestaña **Seguridad**. 

6. Haga clic en los botones **Continuar** o **Editar**. 

7. En el cuadro de diálogo **Permissions for ServerCertification.asmx** (Permisos para ServerCertification.asmx), haga clic en **Agregar**. 

8. Agregue el nombre de cuenta. Si otras cuentas de administradores de AD RMS o de servicio también van a usar estos cmdlets para proteger y desproteger archivos, agregue también esas cuentas. 
    
    Para proteger o desproteger archivos de forma no interactiva, agregue las cuentas de equipo pertinentes. Por ejemplo, agregue la cuenta de equipo del equipo de Windows Server que esté configurado para la infraestructura de clasificación de archivos y vaya a usar un script de PowerShell para proteger archivos. Este escenario necesita la versión preliminar actual del cliente de Azure Information Protection.

9. En la columna **Permitir**, asegúrese de que las casillas **Leer y ejecutar** y **Leer** estén activadas.

10. Haga clic en **Aceptar** dos veces.

### <a name="example-scenarios-for-using-the-cmdlets-for-active-directory-rights-management-services"></a>Escenarios de ejemplo para usar los cmdlets para Active Directory Rights Management Services

Un escenario típico para estos cmdlets es proteger todos los archivos de una carpeta mediante una plantilla de directiva de permisos, o bien desproteger un archivo. 

En primer lugar, si tiene más de una implementación de AD RMS, necesita los nombres de los servidores de AD RMS, que puede obtener con el cmdlet Get-RMSServer para mostrar una lista de los servidores disponibles:

    Get-RMSServer

La salida puede ser parecida a la siguiente:

    Number of RMS Servers that can provide templates: 2 
    ConnectionInfo             DisplayName          AllowFromScratch
    --------------             -------------        ----------------
    Microsoft.InformationAnd…  RmsContoso                       True
    Microsoft.InformationAnd…  RmsFabrikam                      True

Para poder proteger los archivos, debe obtener una lista de las plantillas de RMS para identificar cuál va a usar y el número de identificador correspondiente. Solo necesita especificar también el servidor de RMS cuando tiene más de una implementación de AD RMS. 

En la salida, puede copiar el identificador de plantilla:

    Get-RMSTemplate -RMSServer RmsContoso

La salida puede ser parecida a la siguiente:

    TemplateId        : {82bf3474-6efe-4fa1-8827-d1bd93339119}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content cannot be modified.
    Name              : Contoso, Ltd - Confidential View Only
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    
    
    TemplateId        : {e6ee2481-26b9-45e5-b34a-f744eacd53b0}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content can be modified but cannot be copied and printed.
    Name              : Contoso, Ltd - Confidential
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    FromTemplate      : True

Ahora que ya sabe el identificador de plantilla, puede utilizarlo con el cmdlet Protect-RMSFile para proteger un único archivo o todos los archivos de una carpeta. Por ejemplo, si desea proteger un único archivo y reemplazar el original con el uso de la plantilla de "Contoso, Ltd - Confidencial":

    Protect-RMSFile -File C:\Test.docx -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

La salida puede ser parecida a la siguiente:

    InputFile             EncryptedFile
    ---------             -------------
    C:\Test.docx          C:\Test.docx   

Para proteger todos los archivos de una carpeta, use el parámetro -Folder con una letra de unidad y la ruta de acceso, o la ruta de acceso UNC. Por ejemplo:

    Protect-RMSFile -Folder \\Server1\Documents -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

La salida puede ser parecida a la siguiente:

    InputFile                          EncryptedFile
    ---------                          -------------
    \\Server1\Documents\Test1.docx     \\Server1\Documents\Test1.docx   
    \\Server1\Documents\Test2.docx     \\Server1\Documents\Test2.docx   
    \\Server1\Documents\Test3.docx     \\Server1\Documents\Test3.docx   
    \\Server1\Documents\Test4.docx     \\Server1\Documents\Test4.docx   

Si la extensión de nombre de archivo no cambia después de aplicar la protección, siempre se puede usar el cmdlet Get-RMSFileStatus más adelante para comprobar si el archivo está protegido. Por ejemplo: 

    Get-RMSFileStatus -File \\Server1\Documents\Test1.docx

La salida puede ser parecida a la siguiente:

    FileName                              Status
    --------                              ------
    \\Server1\Documents\Test1.docx        Protected

Para desproteger un archivo, debe tener derechos de uso de propietario o de extracción desde el momento en que se haya protegido el archivo, o bien debe ser superusuario para AD RMS. A continuación, use el cmdlet Unprotect. Por ejemplo:

    Unprotect-RMSFile C:\test.docx -InPlace

La salida puede ser parecida a la siguiente:

    InputFile                             DecryptedFile
    ---------                             -------------
    C:\Test.docx                          C:\Test.docx

## <a name="how-to-label-files-non-interactively-for-azure-information-protection"></a>Cómo etiquetar archivos de manera no interactiva para Azure Information Protection

Puede ejecutar los cmdlets de etiquetado de forma no interactiva mediante el cmdlet **Set-AIPAuthentication**. También se requiere el funcionamiento no interactivo para el analizador de Azure Information Protection, actualmente en versión preliminar.

De forma predeterminada, al ejecutar los cmdlets para etiquetado, los comandos se ejecutan en su propio contexto de usuario en una sesión interactiva de PowerShell. Para ejecutarlos de manera desatendida, cree una nueva cuenta de usuario de Azure AD con este fin. Después, en el contexto de ese usuario, ejecute el cmdlet Set-AIPAuthentication para establecer y almacenar las credenciales mediante el uso de un token de acceso de Azure AD. Esta cuenta de usuario se autentica y se arranca después para el servicio Azure Rights Management. La cuenta descarga la directiva de Azure Information Protection, así como las plantillas de Rights Management que utilizan las etiquetas.

> [!NOTE]
> Si usa [directivas con ámbito](../deploy-use/configure-policy-scope.md), recuerde que es posible que deba agregar esta cuenta a dichas directivas.

La primera vez que ejecute este cmdlet, deberá iniciar sesión en Azure Information Protection. Especifique el nombre de la cuenta de usuario y la contraseña que ha creado para el usuario desatendido. Después de eso, esta cuenta podrá ejecutar los cmdlets de etiquetado de manera no interactiva hasta que expire el token de autenticación. 

Para que la cuenta de usuario pueda iniciar sesión de forma interactiva la primera vez, debe tener el derecho de **inicio de sesión local**. Este derecho es estándar para las cuentas de usuario, pero las directivas de la empresa pueden impedir esta configuración para las cuentas de servicio. En ese caso, puede ejecutar Set-AIPAuthentication con el parámetro *Token*, con el fin de que la autenticación se complete sin el aviso de inicio de sesión. Puede ejecutar este comando como si fuera una tarea programada y otorgar a la cuenta el derecho menor de **inicio de sesión con un trabajo de Batch**. Para más información, consulte las secciones siguientes. 

Cuando el token expire, vuelva a ejecutar el cmdlet para adquirir uno nuevo.

Si ejecuta este cmdlet sin parámetros, la cuenta adquiere un token de acceso que es válido durante 90 días o hasta que expire la contraseña.  

Para controlar cuándo expira el token de acceso, ejecute este cmdlet con parámetros. Esto le permite configurar el token de acceso durante un año, dos años, o para que nunca expire. Esta configuración requiere que tenga dos aplicaciones registradas en Azure Active Directory: una **aplicación web o API** y una **aplicación nativa**. Los parámetros de este cmdlet utilizan valores de estas aplicaciones.

Después de ejecutar este cmdlet, puede ejecutar los cmdlets de etiquetado en el contexto de la cuenta de usuario que ha creado.

### <a name="to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication"></a>Para crear y configurar las aplicaciones de Azure AD para Set-AIPAuthentication

1. En una nueva ventana del explorador, inicie sesión en [Azure Portal](https://portal.azure.com/).

2. Para el inquilino de Azure AD que se utiliza con Azure Information Protection, vaya a **Azure Active Directory** > **Registros de aplicaciones**. 

3. Seleccione **Nuevo registro de aplicaciones** para crear la aplicación web o API. En la etiqueta **Crear**, especifique los valores siguientes y, después, haga clic en **Crear**:
    
    - Nombre: **AIPOnBehalfOf**
    
    Si lo prefiere, especifique un nombre diferente. Debe ser único para cada inquilino.
    
    - Tipo de aplicación: **Aplicación web o API**
    
    - Dirección URL de inicio de sesión: **http://localhost**

4. Seleccione la aplicación que acaba de crear (por ejemplo, **AIPOnBehalfOf**). A continuación, en la hoja **Configuración**, seleccione **Propiedades**. En la hoja **Propiedades**, copie el valor para el **Id. de aplicación** y, después, cierre la hoja. 
    
    Este valor lo utiliza el parámetro `WebAppId` cuando se ejecuta el cmdlet Set-AIPAuthentication. Péguelo y guárdelo para consultarlo más tarde.

5. En la hoja **Configuración**, seleccione **Permisos necesarios**. En la hoja **Permisos necesarios**, seleccione **Conceder permisos**, haga clic en **Sí** para confirmar y cierre la hoja.

6. En la hoja **Configuración**, seleccione **Claves**. Agregue una nueva clave con una descripción y elija la duración (1 año, 2 años o que nunca expire). A continuación, seleccione **Guardar** y copie la cadena del **valor** que se muestra. Es importante guardar esta cadena porque no se muestra de nuevo y no se puede recuperar. Al igual que con cualquier clave que use, almacene el valor guardado de forma segura y restrinja el acceso a este.
    
    Este valor lo utiliza el parámetro `WebAppKey` cuando se ejecuta el cmdlet Set-AIPAuthentication.

7. De vuelta a la hoja **Registros de aplicaciones**, seleccione **Nuevo registro de aplicaciones**, para crear la aplicación nativa. En la etiqueta **Crear**, especifique los valores siguientes y, después, haga clic en **Crear**:
    
    - Nombre: **AIPClient**
    
    Si lo prefiere, especifique un nombre diferente. Debe ser único para cada inquilino.
    
    - Tipo de aplicación: **Nativa**
    
    - Dirección URL de inicio de sesión: **http://localhost**

8. Seleccione la aplicación que acaba de crear (por ejemplo, **AIPClient**). A continuación, en la hoja **Configuración**, seleccione **Propiedades**. En la hoja **Propiedades**, copie el valor para el **Id. de aplicación** y, después, cierre la hoja.
    
    Este valor lo utiliza el parámetro `NativeAppId` cuando se ejecuta el cmdlet Set-AIPAuthentication. Péguelo y guárdelo para consultarlo más tarde.

9. En la hoja **Configuración**, seleccione **Permisos necesarios**. 

10. En la hoja **Permisos necesarios**, haga clic en **Agregar** y, después, haga clic en **Seleccionar una API**. En el cuadro de búsqueda, escriba **AIPOnBehalfOf**. Seleccione este valor en el cuadro de lista y, después, haga clic en **Seleccionar**.

11. En la hoja **Habilitar acceso**, seleccione **AIPOnBehalfOf**, haga clic en **Seleccionar** y, después, haga clic en **Listo**.

12. En la hoja **Permisos necesarios**, seleccione **Conceder permisos**, haga clic en **Sí** para confirmar y cierre la hoja.
    
Ya ha completado la configuración de las dos aplicaciones y tiene los valores que necesita para ejecutar [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) con parámetros *WebAppId*, *WebAppKey* y *NativeAppId*. Por ejemplo:

`Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "sc9qxh4lmv31GbIBCy36TxEEuM1VmKex5sAdBzABH+M=" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f"`

Ejecute este comando en el contexto de la cuenta que etiquetará y protegerá los documentos de una manera no interactiva. Por ejemplo, una cuenta de usuario para los scripts de PowerShell o la cuenta de servicio para ejecutar el analizador de Azure Information Protection.  

La primera vez que se ejecuta este comando se le pide que inicie sesión, que crea y almacena de forma segura el token de acceso de su cuenta en % localappdata%\Microsoft\MSIP. Después de este inicio de sesión inicial, puede etiquetar y proteger los archivos de manera no interactiva en el equipo. Sin embargo, si usa una cuenta de servicio para etiquetar y proteger los archivos, y la cuenta no puede iniciar sesión de forma interactiva, siga las instrucciones de la siguiente sección para que la cuenta se pueda autenticar mediante un token.

### <a name="specify-and-use-the-token-parameter-for-set-aipauthentication"></a>Especificación y uso del parámetro Token en Set-AIPAuthentication

> [!NOTE]
> Esta opción está en fase de versión preliminar y necesita la versión preliminar actual del cliente de Azure Information Protection.

Use los siguientes pasos adicionales e instrucciones para evitar el inicio de sesión interactivo inicio de sesión de una cuenta que etiqueta y protege los archivos. Normalmente, estos pasos adicionales solo son necesarios si a esta cuenta no se le puede otorgar el derecho **inicio de sesión local** derecha, pero se le otorga el derecho **iniciar sesión como trabajo de Batch**. Por ejemplo, esto puede suceder en la cuenta de servicio que ejecuta el detector de Azure Information Protection.

1. Cree un script de PowerShell en el equipo local.

2. Ejecute Set-AIPAuthentication para obtener un token de acceso y cópielo en el Portapapeles.

2. Modifique el script de PowerShell para incluir el token.

3. Cree una tarea que ejecute el script de PowerShell en el contexto de la cuenta de servicio que etiquetará y protegerá los archivos.

4. Confirme que el token se guarda para la cuenta de servicio y elimine el script de PowerShell.


#### <a name="step-1-create-a-powershell-script-on-your-local-computer"></a>Paso 1: Cree un script de PowerShell en el equipo local

1. En el equipo, cree un nuevo script de PowerShell llamado Aipauthentication.ps1.

2. Copie y pegue el siguiente comando en este script:
    
         Set-AIPAuthentication -WebAppId <ID of the "Web app / API" application>  -WebAppKey <key value generated in the "Web app / API" application> -NativeAppId <ID of the "Native" application > -Token <token value>

3. Con las instrucciones de la sección anterior, modifique este comando mediante la especificación de sus propios valores para los parámetros **WebAppId**, **WebAppkey** y **NativeAppId**. En este momento, no tiene el valor del parámetro **Token**, así que lo especificará más adelante. 
    
    Por ejemplo: `Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "sc9qxh4lmv31GbIBCy36TxEEuM1VmKex5sAdBzABH+M=" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f -Token <token value>`
    
#### <a name="step-2-run-set-aipauthentication-to-get-an-access-token-and-copy-it-to-the-clipboard"></a>Paso 2: Ejecute Set-AIPAuthentication para obtener un token de acceso y cópielo en el Portapapeles

1. Abra una sesión de Windows PowerShell.

2. Con los mismos valores que ha especificado en el script, ejecute el siguiente comando:
    
        (Set-AIPAuthentication -WebAppId <ID of the "Web app / API" application>  -WebAppKey <key value generated in the "Web app / API" application> -NativeAppId <ID of the "Native" application >).token | clip
    
    Por ejemplo: `(Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "sc9qxh4lmv31GbIBCy36TxEEuM1VmKex5sAdBzABH+M=" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f").token | clip`

#### <a name="step-3-modify-the-powershell-script-to-supply-the-token"></a>Paso 3: Modifique el script de PowerShell para suministrar el token

1. En el script de PowerShell, especifique el valor del token (para lo que debe pegar la cadena desde el Portapapeles) y guarde el archivo.

2. Firme el script. Si no firma el script (más seguro), debe configurar Windows PowerShell en el equipo que ejecutará los comandos de etiquetado. Por ejemplo, ejecute una sesión de Windows PowerShell con la opción **Ejecutar como administrador** y escriba: `Set-ExecutionPolicy RemoteSigned`. Sin embargo, esta configuración permite la ejecución de todos los scripts sin firmar cuando se almacenan en este equipo (menos seguro).
    
    Para más información acerca de la firma de scripts de Windows PowerShell, consulte [about_Signing](/powershell/module/microsoft.powershell.core/about/about_signing) en la biblioteca de documentación de PowerShell.

3. Copie este script de PowerShell en el equipo que etiquetará y protegerá los archivos, y elimine el de su equipo. Por ejemplo, copie el script de PowerShell en C:\Scripts\Aipauthentication.ps1 en un equipo con Windows Server.

#### <a name="step-4-create-a-task-that-runs-the-powershell-script"></a>Paso 4: Cree una tarea que ejecute el script de PowerShell

1. Asegúrese de que la cuenta de servicio que etiquetará y protegerá los archivos tiene el derecho de **inicio de sesión como trabajo de Batch**.

2. En el equipo que etiquetará y protegerá los archivos, abra el Programador de tareas y cree una nueva tarea. Configure esta tarea para que se ejecute como la cuenta de servicio que etiquetará y protegerá los archivos y, después, configure los siguientes valores para las **acciones**:
    
    - **Acción**: `Start a program`
    - **Programa o script**: `Powershell.exe`
    - **Agregar argumentos (opcional)**: `-NoProfile -WindowStyle Hidden -command "&{C:\Scripts\Aipauthentication.ps1}"` 
    
    Para la línea de argumento, especifique sus propios nombre de archivo y ruta de acceso, en caso de que sean diferentes de los del ejemplo.

3. Ejecute manualmente esta tarea.

#### <a name="step-4-confirm-that-the-token-is-saved-and-delete-the-powershell-script"></a>Paso 4: Confirme que el token se guarda y elimine el script de PowerShell

1. Confirme que el token se ha almacenado en la carpeta %localappdata%\Microsoft\MSIP del perfil de la cuenta de servicio. Este valor lo protege la cuenta de servicio.

2. Elimine el script de PowerShell que contiene el valor del token (por ejemplo, Aipauthentication.ps1).
    
    Opcionalmente, elimine la tarea. Si el token expira, debe repetir este proceso, en cuyo caso puede ser más cómodo dejar la tarea configurada para que esté lista para volver a ejecutarse cuando copie el nuevo script PowerShell con el nuevo valor del token.

## <a name="next-steps"></a>Pasos siguientes
Para obtener ayuda sobre los cmdlets cuando esté en una sesión de PowerShell, escriba `Get-Help <cmdlet name> cmdlet` y utilice el parámetro -online para leer la información más actualizada. Por ejemplo: 

    Get-Help Get-RMSTemplate -online

Vea la información adicional siguiente que puede necesitar para la compatibilidad con el cliente de Azure Information Protection:

- [Customizations](client-admin-guide-customizations.md) (Personalizaciones)

- [Archivos de cliente y registro de uso](client-admin-guide-files-and-logging.md)

- [Seguimiento de documentos](client-admin-guide-document-tracking.md)

- [Tipos de archivos admitidos](client-admin-guide-file-types.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
