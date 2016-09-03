---
title: "Configuración de servidores para el conector de Azure Rights Management | Azure RMS"
description: "Utilice la siguiente información para configurar los servidores locales que utilizarán el conector de Azure Rights Management (RMS). Estos procedimientos incluyen el paso 5 de la implementación del conector de Azure Rights Management."
author: cabailey
manager: mbaldwin
ms.date: 06/08/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 75846ee1-2370-4360-81ad-e2b6afe3ebc9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 26b043f1f9e7a1e0cd00c2f31c28f7d6685f0232
ms.openlocfilehash: d2b15dac1f2b2163ff72d80c97ca0d5da44fd13c


---

# Configuración de servidores para el conector de Azure Rights Management

>*Se aplica a: Azure Rights Management, Windows Server 2012, Windows Server 2012 R2*


Utilice la siguiente información para configurar los servidores locales que utilizarán el conector de Azure Rights Management (RMS). Estos procedimientos incluyen el paso 5 de la [implementación del conector de Azure Rights Management](deploy-rms-connector.md).

Antes de comenzar, asegúrese de que ha instalado y configurado el conector de RMS y que ha comprobado que se cumplen los [requisitos previos](deploy-rms-connector.md#prerequisites-for-the-rms-connector) que son aplicables a los servidores que utilizarán el conector.


## Configuración de servidores para que usen el conector RMS
Después de haber instalado y configurado el conector RMS, está listo para configurar los servidores locales que utilizarán Rights Management y se conectarán a Azure RMS mediante el conector. Esto supone configurar los siguientes servidores:

-   **Para Exchange 2016 y Exchange 2013**: servidores de acceso de cliente y servidores de buzones

-   **Para Exchange 2010**: servidores de acceso de cliente y servidores de transporte de concentradores

-   **Para SharePoint**: servidores web front-end de SharePoint, incluidos los que hospedan el servidor de la administración central

-   **Para la infraestructura de clasificación de archivos**: equipos con Windows Server que tengan instalado el Administrador de recursos de archivos

Esta configuración precisa parámetros de registro. Para ello, tiene dos opciones: automáticamente mediante la herramienta de configuración del servidor para el conector de Microsoft RMS o manualmente mediante la edición del Registro.

---

**De manera automática, con la herramienta de configuración del servidor para el conector de Microsoft RMS:**

- Ventajas:

    - Sin edición directa del registro. Este proceso se automatiza para usted mediante un script.

    - Sin necesidad de ejecutar un cmdlet de Windows PowerShell para obtener su URL de Microsoft RMS.

    - Si la ejecuta de forma local, se comprueban automáticamente los requisitos previos (pero no se solucionan de forma automática).

Desventajas:

- Cuando ejecuta la herramienta, debe realizar una conexión a un servidor que ya ejecuta el conector RMS.

---

**De forma manual, mediante la edición del Registro:**

- Ventajas:

    - No se requiere conexión a un servidor que ejecute el conector RMS.

- Desventajas:

    - Más sobrecargas administrativas que son propensas a errores.

    - Debe obtener tu URL de Microsoft RMS, lo que precisa que ejecute un comando Windows PowerShell.

    - Siempre debe hacer la comprobación de todos los requisitos previos.


---

> [!IMPORTANT]
> En ambos casos, debe instalar los requisitos previos manualmente y configurar Exchange, SharePoint y la infraestructura de clasificación de archivos para utilizar Rights Management.

Para la mayoría de organizaciones, la configuración automática mediante la herramienta de configuración del servidor para el conector RMS de Microsoft será la mejor opción, ya que proporciona mayor eficacia y fiabilidad que la configuración manual.

Después de realizar los cambios de configuración en estos servidores, debe reiniciarlos si se está ejecutando Exchange o SharePoint y los ha configurado previamente para usar AD RMS. No es necesario reiniciar estos servidores si es la primera vez que los va a configurar para Rights Management. Siempre debe reiniciar el servidor de archivos configurado para utilizar la infraestructura de clasificación de archivos después de realizar estos cambios de configuración.

### Cómo usar la herramienta de configuración del servidor para el conector de Microsoft RMS

1.  Si no ha descargado ya el script para la herramienta de configuración del servidor para el conector de Microsoft RMS (GenConnectorConfig.ps1), descárguela desde el [Centro de descarga de Microsoft](http://go.microsoft.com/fwlink/?LinkId=314106).

2.  Guarde el archivo GenConnectorConfig.ps1 en el equipo en que ejecutará la herramienta. Si va a ejecutar la herramienta localmente, debe ser el servidor que desea configurar para comunicarse con el conector RMS. De otro modo, puede guardarla en cualquier equipo.

3.  Decida cómo ejecutar la herramienta:

    -   **Localmente**: Puede ejecutar la herramienta de forma interactiva, desde el servidor que se va a configurar para comunicarse con el conector RMS. Esta ejecución es útil para una configuración de uso único, como un entorno de evaluación.

    -   **Implementación de software**Puede ejecutar la herramienta para producir archivos de registro que, a continuación, implementará en un servidor pertinente (o más) mediante una aplicación de administración de sistemas que admite la implementación de software, como un administrador de la configuración del centro de sistemas.

    -   **Directiva de grupo**: Puede ejecutar la herramienta para producir un script que le proporcione a un administrador que pueda crear objetos de directivas de grupo para los servidores que se van a configurar. Este script crea un objeto de directiva de grupo para cada tipo de servidor que se va a configurar, que el administrador pueda asignar a servidores pertinentes posteriormente.

    > [!NOTE]
    > Esta herramienta configura los servidores que se comunicarán con el conector RMS y que se enumeran al principio de esta sección. No ejecute esta herramienta en los servidores que ejecutan el conector RMS.

4.  Inicie Windows PowerShell con la opción **Ejecutar como administrador** y use el comando Get-help para leer instrucciones sobre cómo usar la herramienta para el método de configuración elegido:

    ```
    Get-help .\GenConnectorConfig.ps1 -detailed
    ```

Para ejecutar el script, debe escribir la dirección URL del conector RMS para la organización. Escriba el prefijo del protocolo (HTTP:// o HTTPS://) y el nombre del conector que ha definido en DNS para la dirección equilibrada de carga de su conector. Por ejemplo, https://connector.contoso.com. Entonces la herramienta usa esa URL para poner en contacto los servidores que ejecutan el conector RMS y obtener otros parámetros que se usan para crear las configuraciones requeridas.

> [!IMPORTANT]
> Al ejecutar esta herramienta, asegúrese de especificar el nombre del conector RMS de carga equilibrada para su organización y no el nombre de un único servidor que ejecuta el servicio del conector RMS.

Use las secciones siguientes para obtener información específica para cada tipo de servicio:

-   [Configuración de un servidor Exchange para usar el conector](#configuring-an-exchange-server-to-use-the-connector)

-   [Configuración de un servidor SharePoint para usar el conector](#configuring-a-sharepoint-server-to-use-the-connector)

-   [Configuración de un servidor de archivos para que la Infraestructura de clasificación de archivos use el conector](#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)

> [!NOTE]
> Después de configurar estos servidores para usar el conector, es posible que las aplicaciones cliente que se han instalado localmente en esos servidores no funcionen con RMS. Cuando esto ocurre, se debe a que las aplicaciones tratan de usar el conector en lugar de usar RMS directamente, que no es compatible.
>
> Además, si Office 2010 se instala localmente en un servidor Exchange, es posible que las características IRM de la aplicación cliente funcionen desde ese equipo después de configurar el servidor para usar el conector, pero esto no es compatible.
>
> En ambos escenarios, debe instalar las aplicaciones cliente en equipos independientes que no estén configurados para usar el conector. Entonces usarán correctamente RMS de forma directa.

## Configuración de un servidor Exchange para usar el conector
Los siguientes roles de Exchange se comunican con el conector RMS:

-   Para Exchange 2016 y Exchange 2013: servidor de acceso de cliente y servidor de buzones

-   Para Exchange 2010: Servidor de acceso de cliente y servidor de transporte de concentradores

Para usar el conector RMS, estos servidores con Exchange deben ejecutar una de las versiones de software siguientes:

-   Exchange Server 2016

-   Exchange Server 2013 con la actualización acumulativa 3 de Exchange 2013

-   Exchange Server 2010 con la actualización acumulativa 6 de Exchange 2010 Service Pack 3

También necesitará instalar en estos servidores una versión del cliente de RMS que incluye compatibilidad con el Modo criptográfico 2 de RMS. La versión mínima compatible en Windows Server 2008 está incluida en la revisión que puede descargarse desde [Se aumentó la longitud de la clave RSA hasta 2048 bits para AD RMS en Windows Server 2008 R2 y Windows Server 2008](http://support.microsoft.com/kb/2627272). La versión mínima para Windows Server 2008 R2 se puede descargar desde [Se ha aumentado la longitud de la clave RSA hasta 2048 bits para AD RMS en Windows 7 o Windows Server 2008 R2](http://support.microsoft.com/kb/2627273). Windows Server 2012 y Windows Server 2012 R2 son compatibles de forma nativa con el Modo 2 criptográfico.

> [!IMPORTANT]
> Si estas versiones (o posteriores) de Exchange y del cliente RMS no están instaladas, no podrá configurar Exchange para usar el conector. Compruebe que estas versiones están instaladas antes de continuar.

### Para configurar los servidores Exchange para que usen el conector

1. Asegúrese de que los servidores de Exchange estén autorizados para usar el conector de RMS; para ello, utilice la herramienta de administración del conector de RMS y la información de la sección [Autorización para que los servidores usen el conector RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). Esta configuración es necesaria para que Exchange pueda usar el conector de RMS.

2.  En los roles de servidor de Exchange que se comunican con el conector RMS, realice una de las acciones siguientes:

    -   Ejecute la herramienta de configuración del servidor para el conector de Microsoft RMS. Para más información, consulte [Cómo usar la herramienta de configuración del servidor para el conector de Microsoft RMS](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector) en este tema.

        Por ejemplo, para ejecutar la herramienta de forma local y configurar un servidor que ejecute Exchange 2016 o Exchange 2013:

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetExchange2013
        ```

    -   Edite el Registro manualmente mediante la información de [Registry settings for the RMS connector](rms-connector-registry-settings.md) (Configuración del Registro para el conector de RMS) para agregar manualmente la configuración del Registro en los servidores. 

3.  Habilita la funcionalidad IRM en Exchange. Para más información, consulte [Procedimientos de Information Rights Management](https://technet.microsoft.com/library/dd351212%28v=exchg.150%29.aspx) en la biblioteca de Exchange.

    > [!NOTE]
    > De forma predeterminada, después de ejecutar **Set-IRMConfiguration -InternalLicensingEnabled $true**, IRM se habilita automáticamente para Outlook Web App y dispositivos móviles, además de habilitarse para buzones de correo. Sin embargo, los administradores pueden deshabilitar IRM en diferentes niveles, por ejemplo, para un servidor de acceso de cliente, para el directorio virtual de Outlook Web App o la directiva de buzón de Outlook Web App y para una directiva de buzón de dispositivos móviles. Si los usuarios no pueden ver las plantillas de Azure RMS en Outlook Web App (después de esperar un día) o en dispositivos móviles, pero sí pueden verlas en el cliente de Outlook, compruebe los ajustes de configuración pertinentes para asegurarse de que IRM no está deshabilitado. Para obtener más información, consulte [Habilitar o deshabilitar el servicio Information Rights Management en los servidores de acceso de cliente](https://technet.microsoft.com/library/dd876938(v=exchg.150).aspx) en la documentación de Exchange. 


## Configuración de un servidor SharePoint para usar el conector
Los siguientes roles de SharePoint se comunican con el conector RMS:

-   Servidores web front-end de SharePoint, incluidos los que hospedan el servidor de la administración central

Para usar el conector RMS, estos servidores con SharePoint deben ejecutar una de las versiones de software siguientes:

-   SharePoint Server 2016

-   SharePoint Server 2013

-   SharePoint Server 2010

Un servidor que ejecute SharePoint 2016 o SharePoint 2013 también debe ejecutar una versión del cliente MSIPC 2.1 que sea compatible con el conector RMS. Para asegurarse de que tiene una versión compatible, descargue el cliente más reciente desde el [Centro de descarga de Microsoft](http://www.microsoft.com/download/details.aspx?id=38396).

> [!WARNING]
> Hay varias versiones del cliente MSIPC 2.1, de modo que asegúrese de que tiene la versión 1.0.2004.0 o posterior.
>
> Para ello, compruebe el número de versión de MSIPC.dll, que se encuentra en **\Archivos de programa\Active Directory Rights Management Services Client 2.1**. El cuadro de diálogo Propiedades muestra el número de la versión del cliente MSIPC 2.1.

Los servidores que ejecutan SharePoint 2010 deben tener instalada una versión del cliente MSDRM que sea compatible con el Modo criptográfico 2 de RMS. La versión mínima compatible para Windows Server 2008 está incluida en la revisión que puedes descargar desde [Se aumentó la longitud de la clave RSA hasta 2048 bits para AD RMS en Windows Server 2008 R2 y en Windows Server 2008](http://support.microsoft.com/kb/2627272), y la versión mínima para Windows Server 2008 R2 se puede descargar desde [Se aumentó la longitud de la clave RSA hasta 2048 bits para AD RMS en Windows 7 o en Windows Server 2008 R2](http://support.microsoft.com/kb/2627273). Windows Server 2012 y Windows Server 2012 R2 son compatibles de forma nativa con el Modo 2 criptográfico.

### Para configurar servidores SharePoint para que usen el conector

1. Asegúrese de que los servidores de SharePoint estén autorizados para usar el conector de RMS; para ello, utilice la herramienta de administración del conector de RMS y la información de la sección [Autorización para que los servidores usen el conector RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). Esta configuración es necesaria para que Exchange pueda usar el conector de RMS.

2.  En los servidores de SharePoint que se comunican con el conector RMS, realice una de las acciones siguientes:

    -   Ejecute la herramienta de configuración del servidor para el conector de Microsoft RMS. Para más información, consulte [Cómo usar la herramienta de configuración del servidor para el conector de Microsoft RMS](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector) en este tema.

        Por ejemplo, para ejecutar la herramienta de forma local y configurar un servidor que ejecute SharePoint 2016 o SharePoint 2013:

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetSharePoint2013
        ```

    -   Si usa SharePoint 2016 o SharePoint 2013, edite el Registro manualmente mediante la información de [Registry settings for the RMS connector](rms-connector-registry-settings.md) (Configuración del Registro para el conector RMS) para agregar manualmente la configuración del Registro en los servidores. 

3.  Habilite IRM en SharePoint. Para más información, consulte [Configuración de Information Rights Management (SharePoint Server 2010)](https://technet.microsoft.com/library/hh545607%28v=office.14%29.aspx) en la biblioteca de SharePoint.

    Cuando siga estas instrucciones, debe configurar SharePoint para usar el conector especificando **Use este servidor RMS** y luego escriba la dirección URL del conector de equilibrio de carga que ha configurado. Escriba el prefijo del protocolo (HTTP:// o HTTPS://) y el nombre del conector que ha definido en DNS para la dirección equilibrada de carga de su conector. Por ejemplo, si el nombre del conector es https://connector.contoso.com, la configuración se parecerá a la imagen siguiente:

    ![Configuración de SharePoint Server para el conector RMS](../media/AzRMS_SharePointConnector.png)

    Después de habilitar IRM en una granja de SharePoint, puede habilitar IRM en bibliotecas individuales mediante la opción **Information Rights Management** en la página **Configuración de la biblioteca** para cada una de ellas.


## Configuración de un servidor de archivos para que la Infraestructura de clasificación de archivos use el conector
Para usar el conector RMS y la Infraestructura de la clasificación de archivos para proteger documentos de Office, el servidor de archivos debe ejecutar uno de los sistemas operativos siguientes:

-   Windows Server 2012 R2

-   Windows Server 2012

### Para configurar servidores de archivo para que usen el conector

1.  Asegúrese de que los servidores de archivos estén autorizados para usar el conector de RMS; para ello, utilice la herramienta de administración del conector de RMS y la información de la sección [Autorización para que los servidores usen el conector RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). Esta configuración es necesaria para que Exchange pueda usar el conector de RMS.

2.  En los servidores de archivos configurados para la infraestructura de clasificación de archivos y que se comunicarán con el conector RMS, realice una de las acciones siguientes:

    -   Ejecute la herramienta de configuración del servidor para el conector de Microsoft RMS. Para más información, consulte [Cómo usar la herramienta de configuración del servidor para el conector de Microsoft RMS](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector) en este tema.

        Por ejemplo, para ejecutar la herramienta de forma local y configurar un servidor de archivos que ejecute FCI:

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetFCI2012
        ```

    - Edite el Registro manualmente mediante la información de [Registry settings for the RMS connector](rms-connector-registry-settings.md) (Configuración del Registro para el conector de RMS) para agregar manualmente la configuración del Registro en los servidores. 

3.  Cree reglas de clasificación y tareas de administración de archivos para proteger los documentos con el cifrado de RMS y, a continuación, especifique una plantilla de RMS para aplicar automáticamente las directivas de RMS. Para obtener más información, consulte [Información general sobre el Administrador de recursos del servidor de archivos](http://technet.microsoft.com/library/hh831701.aspx) en la biblioteca de documentación de Windows Server.

## Pasos siguientes
Ahora que ya está instalado y configurado el conector RMS, y sus servidores están configurados para usarlo, los administradores informáticos y los usuarios pueden proteger y consumir mensajes de correo electrónico y documentos mediante Azure RMS. Para facilitar este proceso a los usuarios, implemente la aplicación de uso compartido RMS, que instala un complemento para Office y agrega nuevas opciones de menú contextual al Explorador de archivos. Para más información, vea [Rights Management sharing application administrator guide](../rms-client/sharing-app-admin-guide.md) (Guía de administrador de la aplicación Rights Management sharing).

Puede utilizar el [mapa de ruta de implementación de Azure Rights Management](../plan-design/deployment-roadmap.md) para comprobar si existen otros pasos de configuración que podría querer hacer antes de implementar [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] para usuarios y administradores.

Para supervisar el conector de RMS, vea [Monitor the Azure Rights Management connector (Supervisión del conector de Azure Rights Management)](monitor-rms-connector.md). 



<!--HONumber=Aug16_HO4-->


