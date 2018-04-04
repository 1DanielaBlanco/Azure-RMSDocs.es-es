---
title: Instalación y configuración del conector de Rights Management - AIP
description: Información para facilitar la instalación y configuración del conector Azure Rights Management (RMS). Estos procedimientos incluyen los pasos 1 a 4 del tema Implementación del conector de Azure Rights Management.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/03/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4fed9d4f-e420-4a7f-9667-569690e0d733
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: a1526c3efea1a03a82baed526d65b748d2aa7bae
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="installing-and-configuring-the-azure-rights-management-connector"></a>Instalación y configuración del conector de Azure Rights Management

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Use la siguiente información como ayuda para instalar y configurar el conector de Azure Rights Management (RMS). Estos procedimientos incluyen los pasos 1 a 4 del tema [Implementación del conector de Azure Rights Management](deploy-rms-connector.md).

Antes de empezar, asegúrese de que ha revisado y comprobado los [requisitos previos](deploy-rms-connector.md#prerequisites-for-the-rms-connector) para esta implementación.


## <a name="installing-the-rms-connector"></a>Instalación del conector RMS

1.  Identifique los equipos (dos como mínimo) que ejecutarán el conector RMS. Deben cumplir con las especificaciones mínimas enumeradas en los requisitos previos.

    > [!NOTE]
    > Instale un solo conector RMS (que consta de múltiples servidores para alta disponibilidad) por inquilino (inquilino de Office 365 o Azure AD). Al contrario de lo que sucede con Active Directory RMS, no tendrá que instalar un conector RMS en cada bosque.

2.  Descargue los archivos de origen para el conector RMS desde el [Centro de descarga de Microsoft](http://go.microsoft.com/fwlink/?LinkId=314106).

    Para instalar el conector RMS, descargue RMSConnectorSetup.exe.

    Además:

    -   Si posteriormente quiere configurar el conector desde un equipo de 32 bits, descargue también RMSConnectorAdminToolSetup_x86.exe.

    -   Si quiere usar la herramienta de configuración del servidor para el conector RMS, para automatizar la configuración de los parámetros de registro en sus servidores locales, descargue también GenConnectorConfig.ps1.

3.  En el equipo en que desea instalar el conector RMS, ejecute **RMSConnectorSetup.exe** con privilegios de administrador.

4.  En la página de bienvenida de la configuración del conector Microsoft Rights Management, seleccione **Instalar el conector Microsoft Rights Management en el ordenador** y, después, haga clic en **Siguiente**.

5.  Lea y acepte los términos de licencia del conector RMS y, a continuación, haga clic en **Siguiente**.

Para continuar, escriba una cuenta y una contraseña para configurar el conector RMS.

## <a name="entering-credentials"></a>Introducción de credenciales
Para poder configurar el conector RMS, debe introducir las credenciales para una cuenta en que tenga suficientes privilegios para configurar el conector RMS. Por ejemplo, puede escribir **admin@contoso.com** y luego especificar la contraseña para esta cuenta.

Esta cuenta no requiere la autenticación multifactor (MFA) porque la herramienta de administración de Microsoft Rights Management no admite MFA para esta cuenta. 

El conector también tiene algunas restricciones de caracteres para esta contraseña. La contraseña no puede tener los siguientes caracteres: símbolo de Y comercial (**&**); corchete angular de apertura (**[**); corchete angular de cierre (**]**); comillas rectas (**"**); y apóstrofo (**'**). Si su contraseña tiene alguno de estos caracteres, se producirá un error en la autenticación para el conector RMS y verá el mensaje de error **Esa combinación de nombre de usuario y contraseña no es correcta**. Esto no afecta a otros escenarios, en los que podrá iniciar sesión correctamente con esta cuenta y contraseña. Si este escenario se aplica a su contraseña, use otra cuenta con una contraseña que no tenga ninguno de estos caracteres especiales o restablézcala y asegúrese de que no los incluya.

Además, si implementó [controles de incorporación](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment), asegúrese de que la cuenta especificada es capaz de proteger el contenido. Por ejemplo, si restringió la capacidad de proteger el contenido al grupo “Departamento de TI”, la cuenta que especifique aquí debe pertenecer a ese grupo. Si no, verá el mensaje de error siguiente: **Error al intentar detectar la ubicación de la organización y el servicio de administración. Asegúrese de que el servicio Microsoft Rights Management está habilitado para su organización.**

Puede usar una cuenta que tenga solo uno de los privilegios siguientes:

-   **Administrador global del inquilino**: una cuenta que es un administrador global del inquilino de Office 365 o inquilino de Azure AD.

-   **Administrador global de Azure Rights Management**: una cuenta de Azure Active Directory a la que se le ha asignado el rol de administrador global de Azure RMS.

-   **Administrador de conector de Azure Rights Management**: una cuenta de Azure Active Directory que tenga otorgados los derechos para instalar y administrar el conector RMS en la organización.

    > [!NOTE]
    > El rol de administrador global de Azure Rights Management y el rol de administrador del conector de Azure Rights Management se asignan a las cuentas mediante el cmdlet de Azure RMS [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator).
    > 
    > Para ejecutar el conector RMS con los privilegios mínimos, cree una cuenta dedicada para este propósito y después asigne el rol de administrador del conector de Azure RMS de la siguiente forma:
    >
    > 1.  Si no lo ha hecho ya, descargue e instale Windows PowerShell para Rights Management. Para más información, vea [Instalación del módulo de PowerShell para AADRM](install-powershell.md).
    >
    >     Inicie Windows PowerShell con el comando **Ejecutar como administrador** y establezca conexión con el servicio Azure RMS mediante el comando [Connect-AadrmService](/powershell/module/aadrm/connect-aadrmservice):
    >
    >     ```
    >     Connect-AadrmService                   //provide Office 365 tenant administrator or Azure RMS global administrator credentials
    >     ```
    > 2.  Luego ejecute el comando [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator) mediante solo uno de los parámetros siguientes:
    >
    >     ```
    >     Add-AadrmRoleBasedAdministrator -EmailAddress <email address> -Role "ConnectorAdministrator"
    >     ```
    >
    >     ```
    >     Add-AadrmRoleBasedAdministrator -ObjectId <object id> -Role "ConnectorAdministrator"
    >     ```
    >
    >     ```
    >     Add-AadrmRoleBasedAdministrator -SecurityGroupDisplayName <group Name> -Role "ConnectorAdministrator"
    >     ```
    >     Por ejemplo, escriba: **Add-AadrmRoleBasedAdministrator -EmailAddress melisa@contoso.com -Role "ConnectorAdministrator"**
    >
    >     Aunque estos comandos asignan el rol de administrador de conector, aquí también puede usar el rol GlobalAdministrator.

Durante el proceso de instalación del conector RMS, se valida e instala todo el software que sea un requisito previo, se instala Internet Information Services (IIS) si ya no lo está, y se instalará y configurará el software del conector. Además, se prepara RMS para su configuración mediante la creación de los siguientes elementos:

-   Una tabla vacía de servidores autorizados para usar el conector para comunicarse con Azure RMS. Agregará servidores a esta tabla posteriormente.

-   Un conjunto de tokens de seguridad para el conector que autorizan operaciones con Azure RMS. Estos tokens se descargan de Azure RMS y se instalan en el equipo local en el Registro. Están protegidos mediante la interfaz de programación de aplicaciones de protección de datos (DPAPI) y las credenciales de la cuenta del sistema local.

En la página final del asistente, haga lo que se indica y, a continuación, haga clic en **Finalizar**:

-   Si este es el primer conector que ha instalado, no seleccione **Iniciar la consola de administración del conector para autorizar servidores** . Seleccionará esta opción después de que haya instalado su segundo (o último) conector RMS. En su lugar, ejecute el asistente de nuevo como mínimo en otro equipo. Debe instalar un mínimo de dos conectores.

-   Si ha instalado su segundo (o último) conector, seleccione **Iniciar la consola de administración del conector para autorizar servidores**.

> [!TIP]
> Llegado a este punto, encontramos una prueba de comprobación que puede llevar a cabo para evaluar si los servicios web para el conector RMS son operativos:
>
> -   En un explorador web, conéctese a **http://&lt;connectoraddress&gt;/_wmcs/certification/servercertification.asmx** y reemplace *&lt;connectoraddress&gt;* por la dirección o el nombre del servidor que tenga instalado el conector RMS. Si la conexión es correcta aparecerá una página **ServerCertificationWebService** .

Si necesita desinstalar el conector RMS, ejecute el asistente de nuevo y seleccione la opción desinstalar.

Si experimenta problemas durante la instalación, compruebe el registro de instalación: **%LocalAppData%\Temp\Microsoft Rights Management connector_\<fecha y hora>.log** 

Por ejemplo, el registro de instalación puede ser similar a C:\Users\Administrator\AppData\Local\Temp\Microsoft Rights Management connector_20170803110352.log

## <a name="authorizing-servers-to-use-the-rms-connector"></a>Autorización para que los servidores usen el conector RMS
Cuando haya instalado el conector RMS en dos equipo al menos, estará preparado para autorizar a los servidores y servicios en que quiera usar el conector RMS. Por ejemplo, sus servidores que ejecutan Exchange Server 2013 o SharePoint Server 2013.

Para definir estos servidores, ejecute la herramienta de administración del conector RMS y agregue entradas a la lista de servidores permitidos. Puede ejecutar esta herramienta cuando seleccione **Iniciar la consola de administración del conector para autorizar servidores** al final del asistente de configuración del conector Rights Management de Microsoft, o puede ejecutarla de forma independiente desde el asistente.

Cuando autorice estos servidores, tenga en cuenta las consideraciones siguientes:

- Los servidores que agregue tendrán garantizados privilegios especiales. Se concederá el [rol de superusuario](configure-super-users.md) en Azure RMS a todas las cuentas que especifique para el rol de Exchange Server en la configuración del conector, lo que les permitirá acceder a todo el contenido de este inquilino de RMS. La característica de superusuario se habilita automáticamente en este momento, si es necesario. Para evitar el riesgo de seguridad de elevación de privilegios, tenga la precaución de especificar únicamente las cuentas que van a ser usadas por los servidores de Exchange de la organización. Todos los servidores configurados como servidores de SharePoint o servidores de archivos que usen FCI tienen garantizados los privilegios de usuario regular.

- Puede agregar servidores múltiples como una entrada única especificando un grupo de seguridad o distribución de Active Directory, o una cuenta de servicio usada por más de un servidor. Cuando use esta configuración, el grupo de servidores compartirá los mismos certificados RMS y todos se considerarán propietarios del contenido que cualquiera de ellos haya protegido. Para minimizar la sobrecarga administrativa, es recomendable que use esta configuración de un solo grupo, en lugar de servidores individuales para autorizar sus servidores de Exchange de la organización o una granja de servidores de SharePoint.

En la página **Servidores a los que se permite utilizar el conector** , haga clic en **Agregar**.

> [!NOTE]
> En Azure RMS, la autorización de servidores es la configuración que en AD RMS equivaldría a la aplicación manual de derechos NTFS a ServerCertification.asmx para las cuentas de servicio o de equipo de servidor, y a la concesión manual de derechos de superusuario a las cuentas de Exchange. En el conector no es necesario aplicar derechos NTFS a ServerCertification.asmx.


### <a name="add-a-server-to-the-list-of-allowed-servers"></a>Agregar un servidor a la lista de servidores autorizados
En la página **Permitir a un servidor que utilice el conector** , escriba el nombre del objeto, o explore para identificar el objeto que se autorizará.

Es importante que autorice el objeto apropiado. Para que un servidor use el conector, se debe seleccionar la cuenta que ejecuta el servicio local (por ejemplo, Exchange o SharePoint) para recibir la autorización. Por ejemplo, si el servicio se ejecuta como una cuenta de servicio configurada, agregue el nombre de esa cuenta de servicio a la lista. Si el servicio se ejecuta como sistema local, agregue el nombre del objeto de equipo (por ejemplo, SERVERNAME$). Como consejo, cree un grupo que contenga estas cuentas y especifique el grupo en lugar de nombres de servidor individuales.

Más información acerca de los diferentes roles del servidor:

-   Para servidores que ejecutan Exchange: Debe especificar un grupo de seguridad y puede usar el grupo predeterminado (**Servidores de Exchange**) que Exchange crea y mantiene automáticamente de todos los servidores Exchange del bosque.

-   Para servidores que ejecutan SharePoint:

    -   Si un servidor de SharePoint 2010 se configura para ejecutarse como sistema local (no usa una cuenta de servicio), cree manualmente un grupo de seguridad en Servicios de dominio de Active Directory y agregue el objeto de nombre del equipo para el servidor de esta configuración a este grupo.

    -   Si un servidor de SharePoint se configura para usar una cuenta de servicio (la práctica recomendada para SharePoint 2010 y la única opción para SharePoint 2016 y SharePoint 2013), haga lo siguiente:

        1.  Agregue la cuenta de servicio que ejecuta el servicio de administración central SharePoint para habilitar SharePoint a fin de que se configure desde la consola del administrador.

        2.  Agregue la cuenta que se ha configurado para el grupo de aplicaciones SharePoint.

        > [!TIP]
        > Si estas dos cuentas son diferentes, tenga en cuenta la creación de un solo grupo que contenga ambas cuentas para minimizar las sobrecargas administrativas.

-   Para servidores de archivos que usan Infraestructura de clasificación de archivos, los servicios asociados se ejecutan como la cuenta del sistema local, de modo que debe autorizar la cuenta del equipo para los servidores de archivo (por ejemplo, SERVERNAME$) o un grupo que contenga esas cuentas de equipo.

Cuando haya acabado de agregar servidores a la lista, haga clic en **Cerrar**.

Si todavía no lo ha hecho, debe configurar ahora el equilibrio de carga para los servidores que tengan instalado el conector RMS, y considerar si usar HTTPS para las conexiones entre estos servidores y los servidores que acaba de autorizar.

## <a name="configuring-load-balancing-and-high-availability"></a>Configuración del equilibrio de carga y alta disponibilidad
Tras haber instalado la segunda o última instancia del conector RMS, defina un nombre de servidor URL conector y configure un sistema de equilibrio de carga.

El nombre de servidor URL conector puede ser cualquier nombre en un espacio de nombres que controle. Por ejemplo, podría crear una entrada en tu sistema DNS para **rmsconnector.contoso.com** y configurar dicha entrada para usar una dirección IP en su sistema de equilibrio de carga. No existen requisitos especiales para este nombre y no es necesario configurarlo en los servidores del conector propiamente dichos. A menos que los servidores Exchange y SharePoint vayan a comunicarse con el conector a través de Internet, este nombre no tiene que resolverse en Internet.

> [!IMPORTANT]
> Recomendamos que no cambie este nombre tras haber configurado servidores Exchange o SharePoint para usar el conector, ya que tendrá que limpiar posteriormente estos servidores de todas las configuraciones de IRM y, después, reconfigurarlos.

Tras crear el nombre en DNS y configurarlo para una dirección IP, configure el equilibrio de carga para esa dirección, que dirige el tráfico a los servidores del conector. Puede usar cualquier equilibrador de carga basado en IP con este motivo, que incluye la característica Equilibrio de carga de red (NLB) en Windows Server. Para más información, vea [Load Balancing Deployment Guide](http://technet.microsoft.com/library/cc754833%28v=WS.10%29.aspx) (Guía para la implementación del equilibrio de carga).

Use la configuración siguiente para configurar el clúster NLB:

-   Puertos: 80 (para HTTP) o 443 (para HTTPS)

    Para obtener más información acerca de si usar HTTP o HTTPS, vea la sección siguiente.

-   Afinidad: Ninguno

-   Método de distribución: Igual

Este nombre que defina para el sistema de carga equilibrada (para los servidores que ejecutan el servicio de conector de RMS) es el nombre del conector RMS de su organización que utilizará más adelante, cuando configure los servidores locales para usar Azure RMS.

## <a name="configuring-the-rms-connector-to-use-https"></a>Configuración del conector RMS para usar HTTPS
> [!NOTE]
> Este paso de configuración es opcional, pero es recomendable para conseguir más seguridad.

Aunque el uso de TLS o SSL es opcional para el conector RMS, lo recomendamos para cualquier servicio de seguridad basado en HTTP. Esta configuración autentica los servidores que ejecutan el conector en sus servidores Exchange y SharePoint que usen el conector. Además, todos los datos que se envían desde estos servidores al conector son cifrados.

Para habilitar el conector RMS para que use TLS, en cada servidor en el que se ejecute el conector RMS, instale un certificado de autenticación del servidor que contenga el nombre que usará para el conector. Por ejemplo, si el nombre del conector RMS que ha definido en DNS es **rmsconnector.contoso.com**, implemente un certificado de autenticación del servidor que contenga **rmsconnector.contoso.com** en el asunto del certificado como el nombre común. También puede especificar **rmsconnector.contoso.com** en el nombre de certificado alternativo como el valor DNS. El certificado no tiene que incluir el nombre del servidor. A continuación, en IIS, enlace este certificado al sitio web predeterminado.

Si usa la opción HTTPS, asegúrese de que todos los servidores que ejecutan el conector tienen un certificado de autenticación de servidor válido que se encadena a una CA raíz en que confían sus servidores Exchange y SharePoint. Además, si la autoridad de certificación (CA) que han emitido los certificados para los servidores del conector publica una lista de revocaciones de certificados (CRL), los servidores Exchange y SharePoint deben ser aptos para descargar esta CRL.

> [!TIP]
> Puede usar la información y los recursos siguientes para tratar de solicitar e instalar un certificado de autenticación de servidor, y para enlazar este certificado al sitio web predeterminado en IIS:
>
> -   Si usa Active Directory Certificate Services (AD CS) y una autoridad de certificación (CA) empresarial para implementar estos certificados de autenticación de servidor, puede duplicar y, a continuación, usar la plantilla de certificados del servidor web. Esta plantilla de certificados usa **Suministrado en la solicitud** para el nombre del asunto del certificado, lo que significa que puede proporcionar el FQDN del nombre del conector RMS para el nombre del asunto del certificado o el nombre alternativo del asunto cuando solicite el certificado.
> -   Si usa un CA independiente o compra este certificado desde otra compañía, vea [Configuración de certificados de servidores de Internet (IIS 7)](http://technet.microsoft.com/library/cc731977%28v=ws.10%29.aspx) de la biblioteca de documentación del [Servidor web (IIS)](http://technet.microsoft.com/library/cc753433%28v=ws.10%29.aspx) en TechNet.
> -   Para configurar IIS de forma que use el certificado, vea [Agregar un enlace a un sitio (IIS 7)](http://technet.microsoft.com/library/cc731692.aspx) de la biblioteca de documentación del [Servidor web (IIS)](http://technet.microsoft.com/library/cc753433%28v=ws.10%29.aspx) en TechNet.

## <a name="configuring-the-rms-connector-for-a-web-proxy-server"></a>Configuración del conector RMS para un servidor proxy web
Si los servidores del conector están instalados en una red que no tiene conexión directa con Internet y precisa configuración manual de un servidor proxy web para acceso de salida a Internet, debe configurar el registro en estos servidores para el conector RMS.

#### <a name="to-configure-the-rms-connector-to-use-a-web-proxy-server"></a>Para configurar el conector RMS para que use el servidor proxy web

1.  En cada servidor que ejecute el conector RMS, abra un editor de registro, como Regedit.

2.  Navegue hasta **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AADRM\Connector**.

3.  Agregue el valor de cadena de **ProxyAddress** y luego establezca que los datos para este valor sean **http://&lt;MyProxyDomainOrIPaddress&gt;:&lt;MyProxyPort&gt;**.

    Por ejemplo: **http://proxyserver.contoso.com:8080**

4.  Cierre el editor del registro y, a continuación, reinicie el servidor o realice un comando IISReset para reiniciar IIS.

## <a name="installing-the-rms-connector-administration-tool-on-administrative-computers"></a>Instalación de la herramienta de administración del conector RMS en equipos administrativos
Puede ejecutar la herramienta de administración del conector RMS desde un equipo que no tenga instalado el conector RMS si cumple los requisitos siguientes:

-   Un equipo físico o virtual que ejecute Windows Server 2012 o Windows Server 2012 R2 (todas las ediciones), Windows Server 2008 R2 o Windows Server 2008 R2 Service Pack 1 (todas las ediciones), Windows 8.1, Windows 8 o Windows 7.

-   Como mínimo 1 GB de RAM.

-   Un mínimo de 64 GB de espacio en disco.

-   Como mínimo una interfaz de red.

-   Acceso a Internet a través de un firewall (o proxy web).

Para instalar la herramienta de administración del conector RMS, ejecute los archivos siguientes:

-   Para un equipo de 32 bits: RMSConnectorAdminToolSetup_x86.exe

-   Para un equipo de 64 bits: RMSConnectorSetup.exe

Si ya ha descargado estos archivos, puede hacerlo desde el [Centro de descarga de Microsoft](http://go.microsoft.com/fwlink/?LinkId=314106).


## <a name="next-steps"></a>Pasos siguientes
Ahora que el conector RMS está instalado y configurado, ya puede configurar los servidores locales para que usen el conector. Vaya a [Configuring servers for the Azure Rights Management connector](configure-servers-rms-connector.md) (Configuración de servidores para el conector de Azure Rights Management).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
