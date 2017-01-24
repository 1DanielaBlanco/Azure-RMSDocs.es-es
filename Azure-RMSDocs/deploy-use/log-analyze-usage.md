---
title: "Registro y análisis del servicio Azure Rights Management | Azure Information Protection"
description: "Información e instrucciones sobre cómo usar el registro de uso con Azure Rights Management (Azure RMS)."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a735f3f7-6eb2-4901-9084-8c3cd3a9087e
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: ca8694a26f0f9b537a3e3a6b1f468d89cefe6206


---

# <a name="logging-and-analyzing-usage-of-the-azure-rights-management-service"></a>Registro y análisis del uso del servicio Azure Rights Management

>*Se aplica a: Azure Information Protection, Office 365*

Use esta información como ayuda para comprender cómo puede usar el registro de uso del servicio Azure Rights Management de Azure Information Protection. Este servicio proporciona protección para los datos de los documentos y mensajes de correo electrónico de su organización y puede registrar todas las solicitudes para obtener acceso a ellos. Entre ellas, se incluyen las solicitudes de los usuarios, las acciones que realicen los administradores de este servicio y las que realicen los operadores de Microsoft para admitir su implementación Azure Information Protection.

A continuación, puede usar estos registros del servicio Azure Rights Management para admitir los siguientes escenarios empresariales:

-   **Analizar enfoques empresariales**

    Los registros que genera el servicio Azure Rights Management se pueden importar al repositorio que elija (como una base de datos, un sistema de procesamiento analítico en línea —OLAP— o un sistema de asignar y reducir) para analizar la información y producir informes. Por ejemplo, podría identificar quién está obteniendo acceso a sus datos protegidos. Puede determinar a qué datos protegidos están obteniendo acceso los usuarios, así como desde dónde y desde qué dispositivos. Puede averiguar si estas personas logran leer contenido protegido. También puede identificar qué personas han leído un documento importante que estaba protegido.

-   **Supervisar para controlar el abuso**

    La información de registro de Azure Rights Management está a su disposición casi en tiempo real, por lo que puede supervisar de manera continua el uso que se haga en su empresa del servicio Azure Rights Management. El 99,9 % de los registros están disponibles a los 15 minutos de que se realice la acción en el servicio.

    Por ejemplo, puede que quiera que se le envíe una alerta si se produce un aumento repentino de los usuarios que leen los datos protegidos fuera del horario laboral estándar, lo que podría indicar que un usuario malintencionado está recopilando información para venderla a competidores. O bien, si el mismo usuario aparentemente accede a los datos desde dos direcciones IP diferentes dentro de un breve intervalo de tiempo, lo que podría indicar que se ha puesto en peligro una cuenta de usuario.

-   **Realizar análisis forenses**

    Si tiene una pérdida de información, es probable que se le pregunte quién accedió recientemente a documentos específicos y a qué información accedió la persona sospechosa. Puede responder a este tipo de preguntas cuando use este registro, ya que los usuarios que usan contenido protegido siempre deben obtener una licencia de Rights Management para abrir documentos e imágenes que estén protegidos mediante el servicio Azure Rights Management, incluso en el caso de que esos archivos se muevan por correo electrónico o se copien en unidades USB u otras unidades de almacenamiento. Esto significa que podrá usar los registros como origen fundamental de la información para realizar el análisis forense cuando proteja sus datos con el servicio Azure Rights Management.

> [!NOTE]
> Si solo está interesado en el registro de las tareas administrativas del servicio Azure Rights Management y no quiere realizar un seguimiento del modo en que los usuarios usan el servicio Rights Management, puede usar el cmdlet [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) de Windows PowerShell de Azure Rights Management.
> 
> También puede usar el Portal de Azure clásico para ver informes de uso de alto nivel que incluyen **Resumen de RMS**, **Usuarios activos de RMS**, **Plataformas de dispositivos RMS** y **Uso de aplicaciones de RMS**. Para tener acceso a estos informes desde el Portal de Azure clásico, haga clic en **Active Directory**, seleccione un directorio y ábralo y, luego, haga clic en **INFORMES**.

Use las secciones siguientes para más información sobre el registro de uso de Azure Rights Management.

## <a name="how-to-enable-azure-rights-management-usage-logging"></a>Habilitación del registro de uso de Azure Rights Management
A partir de febrero de 2016, el registro de uso de Azure Rights Management se habilita de forma predeterminada para todos los clientes. Esto se aplica a los clientes que activaron su servicio de Azure Rights Management antes de febrero de 2016 y a los clientes que activaron el servicio después de febrero de 2016. 

> [!NOTE]
> Ni el almacenamiento de registro ni la funcionalidad de la característica de registro generan costos adicionales.
> 
> Si utilizó el registro de uso de Azure Rights Management antes de febrero de 2016, necesitaría una suscripción a Azure y almacenamiento suficiente en Azure, lo que ya no sucede.



## <a name="how-to-access-and-use-your-azure-rights-management-usage-logs"></a>Cómo acceder a los registros de uso de Azure Rights Management y usarlos
El servicio Azure Rights Management escribe los registros en su cuenta de almacenamiento de Azure como serie de blobs. Cada blob contiene uno o más registros, en formato de registro extendido W3C. Los nombres de blob son números, en el orden en que se crearon. La sección [Cómo interpretar los registros de uso de Azure Rights Management](#how-to-interpret-your-azure-rights-management-usage-logs) que aparece más adelante en este documento contiene más información acerca del contenido del registro y su creación.

Puede que los registros tarden en aparecer en su cuenta de almacenamiento después de realizar alguna acción de Azure Rights Management. La mayoría de los registros aparecen en 15 minutos. Recomendamos que descargue los registros en el almacenamiento local, como una carpeta local, una base de datos o un repositorio de asignar-reducir.

Para descargar sus registros de uso, deberá usar el módulo de administración de Azure Rights Management para Windows PowerShell. Para obtener instrucciones de instalación, consulte [Instalación de Windows PowerShell para Azure Rights Management](install-powershell.md). Si anteriormente ya ha descargado este módulo de Windows PowerShell, ejecute el comando siguiente para comprobar que su número de versión sea como mínimo **2.4.0.0**: `(Get-Module aadrm -ListAvailable).Version` 

### <a name="to-download-your-usage-logs-by-using-powershell"></a>Descargar sus registros de uso mediante PowerShell

1.  Inicie Windows PowerShell con la opción **Ejecutar como administrador** y use el cmdlet [Connect-AadrmService](https://msdn.microsoft.com/library/azure/dn629415.aspx) para conectarse al servicio de Azure Rights Management:

    ```
    Connect-AadrmService
    ```
    
2.  Ejecute el siguiente comando para descargar los registros para una fecha específica: 

    ```
    Get-AadrmUserLog -Path <location> -fordate <date>
    ```

    Por ejemplo, después de crear una carpeta denominada Registros en la unidad E:
    
    * Para descargar registros para una fecha específica (por ejemplo, 01/02/2016), ejecute el siguiente comando: `Get-AadrmUserLog -Path E:\Logs -fordate 2/1/2016`
    
    * Para descargar registros para un intervalo de fechas (por ejemplo, de 01/02/2016 a 14/02/2016), ejecute el siguiente comando: `Get-AadrmUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016` 

Al especificar solo el día, como en nuestros ejemplos, se supone que la hora es 00:00:00 en su hora local y que luego se convierte a UTC. Al especificar una hora con sus parámetros -fromdate o -todate (por ejemplo, -fordate "2/1/2016 15:00:00"), esa fecha y hora se convierten a UTC. A partir de ese momento, el comando Get-AadrmUserLog obtiene los registros para ese período UTC.

No puede especificar menos de un día entero para la descarga.

De forma predeterminada, este cmdlet usa tres subprocesos para descargar los registros. Si tiene ancho de banda de red suficiente y desea reducir el tiempo necesario para descargar los registros, use el parámetro -NumberOfThreads, que admite un valor entre 1 y 32. Por ejemplo, si ejecuta el siguiente comando, el cmdlet genera 10 subprocesos para descargar los registros: `Get-AadrmUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016 -numberofthreads 10`


> [!TIP]
> Puede agrupar todos los archivos de registro descargados en un formato CSV mediante el uso del [Analizador del registro de Microsoft](https://www.microsoft.com/download/details.aspx?id=24659), una herramienta para realizar conversiones entre diversos formatos de archivo conocidos. También puede usar esta herramienta para convertir datos al formato SYSLOG o importarlo a un base de datos. Una vez que haya instalado la herramienta, ejecute `LogParser.exe /?` para obtener ayuda e información para usar esta herramienta. 
>
> Por ejemplo, puede ejecutar el siguiente comando para importar todas la información en un formato de archivo .log: `logparser –i:w3c –o:csv "SELECT * INTO AllLogs.csv FROM *.log"`

#### <a name="if-you-manually-enabled-azure-rights-management-usage-logging-before-the-logging-change-february-22-2016"></a>Si habilitó manualmente el registro de uso de Azure Rights Management antes del cambio de registro (22 de febrero de 2016).


Si ha usado el registro de uso antes del cambio de registro, tendrá registros de uso en su cuenta de almacenamiento de Azure configurada. Microsoft no copiará estos registros de su cuenta de almacenamiento a la nueva cuenta de almacenamiento administrada de Azure Rights Management como parte de este cambio de registro. Es responsable de administrar el ciclo de vida de los registros generados anteriormente y puede usar el cmdlet [Get-AadrmUsageLog](https://msdn.microsoft.com/library/dn629401.aspx) para descargar sus registros antiguos. Por ejemplo:

- Para descargar todos los registros disponibles en su carpeta E:\logs: `Get-AadrmUsageLog -Path "E:\Logs"`
    
- Para descargar un intervalo específico de blobs: `Get-AadrmUsageLog –Path "E:\Logs" –FromCounter 1024 –ToCounter 2047`

Tenga en cuenta que no tiene que descargar registros con el cmdlet Get-AadrmUsageLog si se aplica algo de lo siguiente:

-  Activó el servicio Azure Rights Management el 22 de febrero de 2016 o antes, pero no habilitó la característica de registro de uso.

- Activó el servicio Azure Rights Management después del 22 de febrero de 2016.

## <a name="how-to-interpret-your-azure-rights-management-usage-logs"></a>Interpretación de los registros de uso de Azure Rights Management
Use la siguiente información como ayuda para interpretar los registros de uso de Azure Rights Management.

### <a name="the-log-sequence"></a>La secuencia de registro
El servicio Azure Rights Management escribe los registros como serie de blobs. 

Cada entrada en el registro tiene una marca de tiempo UTC. Dado que el servicio Azure Rights Management se ejecuta en varios servidores de varios centros de datos, a veces puede parecer que los registros estén fuera de secuencia, incluso aunque estén ordenados por su marca de tiempo. Sin embargo, la diferencia es mínima y generalmente se encuentra en un margen de un minuto. En la mayoría de los casos, este asunto no sería un problema para análisis de registros.

### <a name="the-blob-format"></a>El formato del blob
Cada blob está en formato de registro extendido W3C. Empieza por las siguientes dos líneas:

**#Software: RMS**

**#Version: 1.1**

La primera línea identifica que se trata de registros de Azure Rights Management. La segunda línea identifica que el resto del blob sigue la especificación de la versión 1.1. Recomendamos que las aplicaciones que analicen estos registros comprueben estas dos líneas antes de continuar analizando el resto del blob.

La tercera enumera una lista de nombres de campos separados por pestañas:

**#Fields: date            time            row-id        request-type           user-id       result          correlation-id          content-id                owner-email           issuer                     template-id             file-name                  date-published      c-info         c-ip            admin-action            acting-as-user**

Cada una de las líneas posteriores es un registro. Los valores de los campos se encuentran en el mismo orden que la línea anterior y están separados por pestañas. Use la siguiente tabla para interpretar los campos.

|Nombre de campo|Tipo de datos W3C|Descripción|Valor de ejemplo|
|--------------|-----------------|---------------|-----------------|
|date|Fecha|Fecha UTC cuando se realizó el servicio de la solicitud.<br /><br />El origen es el reloj local del servidor que realizó el servicio de la solicitud.|2013-06-25|
|time|Hora|Hora UTC en formato de 24 hora cuando se realizó el servicio de la solicitud.<br /><br />El origen es el reloj local del servidor que realizó el servicio de la solicitud.|21:59:28|
|row-id|Texto|GUID único para este registro. Si un valor no está presente, use el valor del identificador de correlación para identificar la entrada.<br /><br />Este valor es útil cuando agrega registros o copia registros en otro formato.|1c3fe7a9-d9e0-4654-97b7-14fafa72ea63|
|request-type|Nombre|Nombre de la API de RMS que se solicitó.|AcquireLicense|
|user-id|Cadena|El usuario que realizó la solicitud.<br /><br />El valor se incluye entre comillas únicas. Las llamadas de una clave de inquilino administrada por usted (BYOK) tienen un valor de **"**, que también se aplica cuando los tipos de solicitud son anónimos.|‘joe@contoso.com’|
|result|String|'Success' si se ha proporcionado la solicitud correctamente.<br /><br />El tipo de error entre comillas si se produjo un error de la solicitud.|'Success'|
|correlation-id|Texto|GUID que es común entre el registro del cliente de RMS y el registro del servidor para una solicitud proporcionada.<br /><br />Este valor puede ser útil para ayudar a solucionar problemas del cliente.|cab52088-8925-4371-be34-4b71a3112356|
|content-id|Texto|GUID, entre llaves, que identifica el contenido protegido (por ejemplo, un documento).<br /><br />Este campo tiene un valor solo si request-type es AcquireLicense y está en blanco para todos los demás tipos de solicitudes.|{bb4af47b-cfed-4719-831d-71b98191a4f2}|
|owner-email|Cadena|Dirección de correo electrónico del propietario del documento.|alice@contoso.com|
|issuer|Cadena|Dirección de correo electrónico del emisor del documento.|alice@contoso.com (o) FederatedEmail.4c1f4d-93bf-00a95fa1e042@contoso.onmicrosoft.com'|
|template-id|String|Identificador de la plantilla que se usa para proteger el documento.|{6d9371a6-4e2d-4e97-9a38-202233fed26e}|
|file-name|String|Nombre de archivo del documento que se ha protegido. <br /><br />Actualmente, algunos archivos (como documentos de Office) se muestran como GUID en lugar del nombre de archivo real.|TopSecretDocument.docx|
|date-published|Fecha|Fecha en la que se ha protegido el documento.|2015-10-15T21:37:00|
|c-info|Cadena|Información acerca de la plataforma del cliente que está realizando la solicitud.<br /><br />La cadena específica varía, en función de la aplicación (por ejemplo, el sistema operativo o el explorador).|'MSIPC;version=1.0.623.47;AppName=WINWORD.EXE;AppVersion=15.0.4753.1000;AppArch=x86;OSName=Windows;OSVersion=6.1.7601;OSArch=amd64'|
|c-ip|Address|Dirección IP del cliente que realiza la solicitud.|64.51.202.144|


#### <a name="exceptions-for-the-user-id-field"></a>Excepciones para el campo user-id
Aunque el campo user-id suele indicar el usuario que hay realizado la solicitud, hay dos excepciones en las que el valor no se asigna a un usuario real:

-   El valor **'microsoftrmsonline@&lt;YourTenantID&gt;.rms.&lt;region&gt;.aadrm.com'**.

    Esto indica que un servicio de Office 365, como Exchange Online o SharePoint Online, está realizando la solicitud. En la cadena, *&lt;YourTenantID&gt;* es el GUID de su inquilino y *&lt;region&gt;* es la región donde se registra el inquilino. Por ejemplo, **na** representa a Norteamérica, **eu** representa a Europa y **ap** representa a Asia.

-   Si está usando el conector RMS.

    Las solicitudes de este conector se registran con el nombre de entidad de servicio de **Aadrm_S-1-7-0**, que se genera automáticamente al instalar el conector RMS.

#### <a name="typical-request-types"></a>Tipos de solicitudes típicas
Hay muchos tipos de solicitudes del servicio Azure Rights Management, pero en la tabla siguiente se identifican algunos de los tipos que normalmente se usan más.

|Tipo de solicitud|Descripción|
|----------------|---------------|
|AcquireLicense|Un cliente solicita desde un equipo basado en Windows una licencia para contenido protegido con RMS.|
|AcquirePreLicense|Un cliente, en nombre del usuario, solicita una licencia para contenido protegido con RMS.|
|AcquireTemplates|Se ha realizado una llamada para adquirir plantillas basadas en identificadores de plantilla.|
|AcquireTemplateInformation|Se ha realizado una llamada para obtener los identificadores de la plantilla del servicio.|
|AddTemplate|Se realiza una llamada desde el Portal de Azure clásico para agregar una plantilla.|
|AllDocsCsv|Se realiza una llamada desde el sitio de seguimiento de documentos para descargar el archivo CSV de la página **Todos los documentos**.|
|BECreateEndUserLicenseV1|Se realiza una llamada desde un dispositivo móvil para crear una licencia de usuario final.|
|BEGetAllTemplatesV1|Se realiza una llamada desde un dispositivo móvil (back-end) para obtener todas las plantillas.|
|Certify|El cliente está certificando el contenido para la protección.|
|DeleteTemplateById|Se realiza una llamada desde el Portal de Azure clásico para eliminar una plantilla por identificador de plantilla.|
|DocumentEventsCsv|Se realiza una llamada desde el sitio de seguimiento de documentos para descargar el archivo CSV de un solo documento.|
|ExportTemplateById|Se realiza una llamada desde el Portal de Azure clásico para exportar una plantilla en función de un identificador de plantilla.|
|FECreateEndUserLicenseV1|Similar a la solicitud AcquireLicense pero desde dispositivos móviles.|
|FECreatePublishingLicenseV1|Lo mismo que Certify y GetClientLicensorCert combinados, desde clientes móviles.|
|FEGetAllTemplates|Se realiza una llamada desde un dispositivo móvil (front-end) para obtener las plantillas.|
|FindServiceLocationsForUser|Se realiza una llamada para consultar las direcciones URL, que se usan para llamar a Certify o AcquireLicense.|
|GetAllDocs|Se realiza una llamada desde el sitio de seguimiento de documentos para cargar la página **Todos los documentos** para un usuario, o buscar todos los documentos del inquilino. Use este valor con los campos admin-action y acting-as-admin:<br /><br />- admin-action está vacío: un usuario ve la página **Todos los documentos** de sus propios documentos.<br /><br />- admin-action es true y acting-as-user está vacío: un administrador ve todos los documentos de su inquilino.<br /><br />- admin-action es true y acting-as-user no está vacío: un administrador ve la página **Todos los documentos** de un usuario.|
|GetAllTemplates|Se realiza una llamada desde el Portal de Azure clásico para obtener todas las plantillas.|
|GetClientLicensorCert|El cliente está solicitando un certificado de publicación (que se utiliza posteriormente para proteger contenido) desde un equipo con Windows.|
|GetConfiguration|Se llama a un cmdlet de Azure PowerShell para obtener la configuración del inquilino de Azure RMS.|
|GetConnectorAuthorizations|Se realiza una llamada desde los conectores de RMS para obtener su configuración de la nube.|
|GetRecipients|Se realiza una llamada desde el sitio de seguimiento de documentos para ir a la vista de lista de un solo documento.|
|GetSingle|Se realiza una llamada desde el sitio de seguimiento de documentos para ir a la página de un **solo documento**.|
|GetTenantFunctionalState|El Portal de Azure clásico está comprobando si el servicio Azure Rights Management está activado.|
|GetTemplateById|Se realiza una llamada desde el Portal de Azure clásico para obtener una plantilla especificando un identificador de plantilla.|
|KeyVaultDecryptRequest|El cliente está intentando descifrar el contenido protegido con RMS. Solo es válido para una clave de inquilino administrada por el cliente (BYOK) en el Almacén de claves de Azure.|
|KeyVaultGetKeyInfoRequest|Se realiza una llamada para comprobar si la clave especificada que se usará en Azure Key Vault para la clave de inquilino de Azure Information Protection es accesible y si se ha usado antes.|
|KeyVaultSignDigest|Se realiza una llamada cuando se usa una clave administrada por el cliente (BYOK) del Almacén de claves de Azure para firmar. Suele llamarse una vez por cada elemento AcquireLicence (o FECreateEndUserLicenseV1), Certify y GetClientLicensorCert (o FECreatePublishingLicenseV1).|
|KMSPDecrypt|El cliente está intentando descifrar el contenido protegido con RMS. Solo es válido para una clave de inquilino administrada por el cliente (BYOK) heredada.|
|KMSPSignDigest|Se realiza una llamada cuando se usa una clave administrada por el cliente (BYOK) heredada para firmar. Suele llamarse una vez por cada elemento AcquireLicence (o FECreateEndUserLicenseV1), Certify y GetClientLicensorCert (o FECreatePublishingLicenseV1).|
|LoadEventsForMap|Se realiza una llamada desde el sitio de seguimiento de documentos para ir a la vista de mapa de un solo documento.|
|LoadEventsForSummary|Se realiza una llamada desde el sitio de seguimiento de documentos para ir a la vista Escala de tiempo de un solo documento.|
|LoadEventsForTimeline|Se realiza una llamada desde el sitio de seguimiento de documentos para ir a la vista de mapa de un solo documento.|
|ImportTemplate|Se realiza una llamada desde el Portal de Azure clásico para importar una plantilla.|
|RevokeAccess|Se realiza una llamada desde el sitio de seguimiento de documentos para revocar un documento.|
|SearchUsers |Se realiza una llamada desde el sitio de seguimiento de documentos para buscar todos los usuarios de un inquilino.|
|ServerCertify|Se realiza una llamada desde un cliente habilitado para RMS (como SharePoint) para certificar el servidor.|
|SetUsageLogFeatureState|Se realiza una llamada para habilitar el registro de uso.|
|SetUsageLogStorageAccount|Se realiza una llamada para especificar la ubicación de los registros del servicio Azure Rights Management.|
|UpdateNotificationSettings|Se realiza una llamada desde el sitio de seguimiento de documentos para cambiar la configuración de notificaciones de un solo documento.|
|UpdateTemplate|Se realiza una llamada desde el Portal de Azure clásico para actualizar una plantilla existente.|


## <a name="windows-powershell-reference"></a>Referencia de Windows PowerShell
Desde febrero de 2016, el único cmdlet de Windows PowerShell que se necesita para el registro de uso de Azure Rights Management es el siguiente: [Get-AadrmUserLog](https://msdn.microsoft.com/library/azure/mt653941.aspx). 

Antes de que se produjera este cambio, se necesitaban los siguientes cmdlets para los registros de uso de Azure Rights Management (ahora están en desuso):  

-   [Disable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629404.aspx)

-   [Enable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx)

-   [Get-AadrmUsageLog](https://msdn.microsoft.com/library/azure/dn629401.aspx)

-   [Get-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629425.aspx)

-   [Get-AadrmUsageLogLastCounterValue](https://msdn.microsoft.com/library/azure/dn629423.aspx)

-   [Get-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629419.aspx)

-   [Set-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx)

Si tiene registros en su propio almacenamiento de Azure desde antes del cambio de registro de Azure Rights Management, puede descargarlos con estos cmdlets más antiguos mediante Get-AadrmUsageLog y Get-AadrmUsageLogLastCounterValue, como antes. Sin embargo, todos los nuevos registros de uso se escribirán en el nuevo almacenamiento de Azure RMS y deben descargarse con Get-AadrmUserLog.

Para obtener más información acerca de cómo usar Windows PowerShell para el servicio Azure Rights Management, consulte [Administración del servicio Azure Rights Management mediante Windows PowerShell](administer-powershell.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]





<!--HONumber=Jan17_HO4-->


