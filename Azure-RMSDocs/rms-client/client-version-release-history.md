---
title: 'Cliente de Azure Information Protection: historial de publicación de versiones y directiva de soporte técnico'
description: Consulte las novedades o los cambios en una versión del cliente de Azure Information Protection para Windows y conozca la directiva de ciclo de vida de soporte técnico.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/31/2018
ms.topic: article
ms.service: information-protection
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 3e067f42b216efda48d46cd95be66c4939bf6240
ms.sourcegitcommit: ba7ef4fe439bbf00cdad888017cbb8f44c801f77
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/31/2018
ms.locfileid: "43348698"
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Cliente de Azure Information Protection: historial de publicación de versiones y directiva de soporte técnico

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2*

El equipo de Azure Information Protection actualiza de forma periódica el cliente de Azure Information Protection para implementar correcciones y agregar nuevas funciones. 

Puede descargar la versión de lanzamiento de disponibilidad general más reciente y la versión preliminar actual (si está disponible) desde el [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). La versión de disponibilidad general se incluye también en el Catálogo de Microsoft Update (categoría: **Azure Information Protection**), de modo que puede actualizar el cliente mediante WSUS, Configuration Manager u otros mecanismos de implementación de software que usan Microsoft Update.

Para obtener más información, consulte [Actualización y mantenimiento del cliente de Azure Information Protection](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client).

### <a name="servicing-information-and-timelines"></a>Información y escalas de tiempo de mantenimiento

Cada versión de disponibilidad general del cliente de Azure Information Protection es compatible hasta seis meses después del lanzamiento de la versión de disponibilidad general posterior. En esta página no se incluyen las versiones no admitidas del cliente. Las correcciones y las nuevas funcionalidades siempre se aplican a la versión más reciente de GA y no se aplicarán a las versiones anteriores de GA.

Las versiones preliminares no se deben implementar para los usuarios finales en las redes de producción. En su lugar, use la versión preliminar más reciente para ver y probar nuevas funcionalidades o correcciones que se incluyen en la próxima versión de GA. No se admiten las versiones preliminares que no están actualizadas.

### <a name="release-history"></a>Historial de versiones

Use la información siguiente para consultar las novedades o los cambios en una versión compatible del cliente de Azure Information Protection para Windows. La versión más reciente aparece en primer lugar. 

> [!NOTE]
> Las revisiones secundarias no se enumeran. Por tanto, si tiene algún problema con el cliente de Azure Information Protection, se recomienda que compruebe si se ha corregido en la versión de GA más reciente. Si el problema continúa, compruebe la versión preliminar actual.
>  
> Para obtener soporte técnico, consulte la información sobre [Opciones de soporte y recursos de la comunidad](../information-support.md#support-options-and-community-resources). También lo invitamos a participar en el equipo de Azure Information Protection, en su [sitio de Yammer](https://www.yammer.com/askipteam/).

## <a name="versions-later-than-12950"></a>Versiones posteriores a 1.29.5.0

Si tiene una versión del cliente posterior a la 1.29.5.0, se trata de una compilación preliminar con fines de prueba y evaluación.

Esta versión incluye la versión MSIPC 1.0.3592.627 del cliente RMS.

**Nuevas características**: 

- Compatibilidad con el estándar ISO de cifrado de archivos PDF para que los documentos que se protegen conserven su extensión de nombre de archivo .pdf de manera predeterminada y se puedan abrir con lectores de PDF que admiten esta norma ISO. Actualmente, debe indicar a los usuarios que abran manualmente estos documentos PDF protegidos el visor de Azure Information Protection. Para ayudar a que los usuarios puedan hacerlo, cuando abran uno de estos archivos PDF protegidos, verán una página con iconos que pueden seleccionar para su sistema operativo. Si no quiere este comportamiento y, en su lugar, requiere paridad con la versión de disponibilidad general del cliente de Azure Information Protection, puede establecer una [configuración de cliente avanzada](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption).

- Compatibilidad con nuevos tipos de información confidencial que le ayudarán a clasificar los documentos que contienen información personal. [Más información](../configure-policy-classification.md#sensitive-information-types-that-require-a-minimum-version-of-the-client) 

- Compatibilidad de etiquetado con el formato **Documento Open XML estricto** en archivos de Word, Excel y PowerPoint. Para más información sobre los formatos Open XML, vea la entrada del blog de Office sobre [nuevas opciones de formato de archivo en el nuevo Office](https://www.microsoft.com/en-us/microsoft-365/blog/2012/08/13/new-file-format-options-in-the-new-office/). 

- Compatibilidad con los archivos que se han protegido con Secure Islands cuando esos archivos no sean documentos PDF y de Office. Por ejemplo, proteger archivos de texto e imagen. O archivos que tienen una extensión de nombre de archivo .pfile. Esta compatibilidad habilita nuevos escenarios, como el analizador de Azure Information Protection, que pueden inspeccionar estos archivos para la búsqueda de información confidencial y vuelven a etiquetarlos automáticamente para Azure Information Protection. [Más información](client-admin-guide-customizations.md#support-for-files-protected-by-secure-islands)

- El vínculo **Envíenos sus comentarios** del cuadro de diálogo **Ayuda y comentarios** se reemplaza por **Notificar un problema**, que es una opción que puede personalizar. De manera predeterminada, esta opción envía un correo electrónico a Microsoft. Puede cambiar esta dirección de correo electrónico para que cuando los usuarios seleccionen esta opción, use una cadena HTTP que el usuario especifica. Por ejemplo, una página web personalizada que tiene para que los usuarios notifiquen problemas o una dirección de correo electrónico que vaya a su departamento de soporte técnico. Para modificar esta dirección, use una [configuración de cliente avanzada](client-admin-guide-customizations.md#modify-the-email-address-for-the-report-an-issue-link).

- Nueva configuración de cliente avanzada para quitar los encabezados y los pies de página que se han aplicado a los documentos mediante otras soluciones de etiquetado. [Más información](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)

- Para el analizador de Azure Information Protection:

    - Nuevo cmdlet, [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner): hay que ejecutarlo después de actualizar desde la versión de disponibilidad general actual (1.29.5.0) o una versión anterior.
    
    - Nuevo cmdlet, [Get AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus): obtiene el estado actual del servicio para el analizador.  
    
    - Nuevo cmdlet, [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan): indica al analizador que inicie un ciclo de exploración única cuando la programación se establece en manual.
    
    - SharePoint Server 2010 es compatible con los clientes que tengan [soporte extendido para esta versión de SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).
    
**Correcciones**

- Para el analizador de Azure Information Protection:
    
    - Para documentos que están protegidos en las bibliotecas de SharePoint, si el parámetro *DefaultOwner* no se usa en el repositorio de datos, el valor de Editor de SharePoint se usa ahora como valor predeterminado en lugar del valor de autor.
    
    - Entre los informes del analizador se incluyen "Última modificación por" para documentos de Office.

- Al clasificar y proteger mediante PowerShell o el analizador, los metadatos de documentos de Office no se quitan ni se cifran.

- La visualización de mensajes de correo electrónico mediante los iconos de flecha Siguiente elemento y Elemento anterior de la barra de herramientas de acceso rápido muestra la etiqueta correcta para cada correo electrónico.

- Permisos personalizados es compatible con las direcciones de correo electrónico del destinatario que contienen un apóstrofo.

- El entorno de equipo se inicializará correctamente (arranque) cuando esta acción se inicie abriendo un documento protegido que se almacena en SharePoint Online.

- Cuando usa el cliente para hacer clic con el botón derecho en Explorador de archivos, PowerShell o el analizador, se bloquea el etiquetado para los archivos que están en ubicaciones de WebDav porque se trata de un escenario no compatible.

- El icono Eliminar etiqueta no se muestra en las aplicaciones cliente (Word, Excel, PowerPoint ni Outlook) cuando se establece la [configuración de directiva](../configure-policy-settings.md) de **All documents and emails must have a label** (Todos los documentos y correos electrónicos deben tener una etiqueta).

**Cambios adicionales**:
   
- Para [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration):
    
    - Los valores del parámetro *Schedule* ya no son **OneTime**, **Continuous** y **Never**, ahora son **Manual** y **Always**.
        
    - El parámetro *Type* se quita, por lo que también se quita de la salida al ejecutar [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration). De forma predeterminada, solo se inspeccionan los archivos nuevos o modificados tras el primer ciclo de examen. Si ha establecido previamente el parámetro *Type* en **Full** para volver a examinar todos los archivos, ejecute ahora [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan) con el parámetro *Reset*. El analizador también debe configurarse para una programación manual, lo que requiere que el parámetro *Schedule* se establezca en **Manual** con [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).
    
- En el analizador, la lista de exclusión predeterminada ahora incluye los archivos .msg, .rar, .rtf y .zip. [Más información](client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-scanner)

- La versión de directiva ha cambiado a 1.4. La identificación del número de versión es necesaria para [configurar los equipos desconectados](client-admin-guide-customizations.md#support-for-disconnected-computers).

## <a name="version-12950"></a>Versión 1.29.5.0 

**Lanzamiento**: 26/06/2018

Esta versión incluye la versión MSIPC 1.0.3403.1224 del cliente de RMS.

**Correcciones**:

- En el caso de las versiones de Outlook 16.0.9324.1000 y versiones posteriores (Hacer clic y ejecutar), la barra de Azure Information Protection admite las opciones de presentación de monitor más recientes, que antes podían provocar que la barra se mostrara fuera de las aplicaciones de Outlook.

- Las marcas visuales que configure [por tipo de aplicación de Office](../configure-policy-markings.md#setting-different-visual-markings-for-word-excel-powerpoint-and-outlook) ahora reemplazan un encabezado o pie de página que se aplicó anteriormente por una etiqueta de Azure Information Protection.

- Cuando un archivo de Excel ya tiene la etiqueta y esta aplica marcas visuales, se aplicarán también las marcas visuales de la etiqueta a una nueva hoja.

- Cuando utiliza la configuración avanzada del cliente para [etiquetar un documento de Office utilizando una propiedad personalizada existente](client-admin-guide-customizations.md#label-an-office-document-by-using-an-existing-custom-property), el etiquetado automático no invalida el etiquetado manual.

## <a name="version-127480"></a>Versión 1.27.48.0

**Lanzamiento**: 30/05/2018

Esta versión incluye la versión MSIPC 1.0.3403.1224 del cliente de RMS.

**Nuevas características**: 

- Para el analizador de Azure Information Protection:
    
    - Puede especificar una lista de tipos de archivo para incluir en el examen o excluir de este. Para especificar esta lista, use [Set-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Set-AIPScannerScannedFileTypes). Después de haber especificado la lista de tipos de archivo, puede agregar un nuevo tipo de archivo a la lista mediante [Add-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Add-AIPScannerScannedFileTypes), y quitar un tipo de archivo de la lista mediante [Remove-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Remove-AIPScannerScannedFileTypes).
    
    - Puede etiquetar archivos sin inspeccionar el contenido mediante la aplicación de una etiqueta predeterminada. Utilice el cmdlet [Set-AIPScannerRepository](/powershell/module/azureinformationprotection/Set-AIPScannerRepository) y establezca el parámetro *MatchPolicy* en **Off**. 
    
    - Puede detectar archivos con tipos de información confidencial sin configurar etiquetas de clasificación automática. Utilice el cmdlet [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) y establezca el parámetro *DiscoverInformationTypes* en **All**.
    
    - De forma predeterminada, solo los tipos de documento de Office están protegidos. Otros tipos de archivo se pueden proteger al definirlos en el registro. Para obtener instrucciones, vea [Configuración de la API de archivo](../develop/file-api-configuration.md) en la guía del desarrollador.
    
    - De forma predeterminada, el analizador se ejecuta ahora con un nivel de integridad bajo para una mayor seguridad en caso de que ejecute el analizador con una cuenta que tenga derechos con privilegios. Cuando la cuenta de servicio que ejecuta el analizador tiene únicamente los derechos que se documentan en la sección de [requisitos previos del analizador](../deploy-aip-scanner.md#prerequisites-for-the-azure-information-protection-scanner), el nivel de integridad bajo no es necesario, y no se recomienda porque afecta negativamente al rendimiento. Puede utilizar una configuración de cliente avanzada para deshabilitar el nivel de integridad bajo. [Más información](client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner) 
    
- Para [Get-AIPFileStatus](/powershell/module/azureinformationprotection/Get-AIPFileStatus), el resultado incluye ahora al propietario y al emisor de Rights Management, así como la fecha en que se protegió el contenido.
 
**Cambios adicionales**:

- Para el analizador de Azure Information Protection: 
    
    - Si instaló una versión anterior del analizador, vuelva a ejecutar el comando de instalación del analizador con [Install AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner) después de haber actualizado el cliente de Azure Information Protection. Se conservarán las opciones de configuración para el analizador y los repositorios. La reinstalación del analizador concede al servicio del analizador permisos de eliminación de cuenta para la base de datos del analizador, que se necesitarán para los informes.    
    
    - Se ha cambiado el nombre del parámetro *ScanMode* de [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) a **Enforce**, con valores de Off y On.
    
    - Para usar una etiqueta predeterminada, ya no es necesario configurar una etiqueta predeterminada como una valor de directiva. Simplemente especifique esta etiqueta predeterminada con la configuración del repositorio. 

- Se ha quitado la página principal "Enhorabuena" y "Novedades de Azure Information Protection", que se mostraba en el primer uso en las aplicaciones de Office.

## <a name="version-12660"></a>Versión 1.26.6.0

**Lanzamiento**: 17/04/2018

Esta versión incluye la versión MSIPC 1.0.3403.1224 del cliente de RMS.

**Nuevas características**:

- El analizador de Azure Information Protection: el módulo de PowerShell de la que se incluye con el cliente tiene nuevos cmdlets para instalar y configurar el analizador, con el fin de que pueda detectar, clasificar y proteger los archivos de sus almacenes de datos locales. Para obtener instrucciones, consulte [Implementación del analizador de Azure Information Protection para clasificar y proteger automáticamente los archivos](../deploy-aip-scanner.md). 
- Ahora puede establecer distintivos visuales diferentes para Word, Excel, PowerPoint y Outlook mediante el uso de la instrucción variable "If.App" en la cadena de texto e identificar el tipo de aplicación. [More information]configure-policy-markings.md#setting-different-visual-markings-for-word-excel-powerpoint-and-outlook)

- Compatibilidad con la [configuración de directivas](../configure-policy-settings.md). **Muestre la barra de Information Protection en las aplicaciones de Office**. Si este valor está desactivado, los usuarios seleccionan las etiquetas en el botón **Proteger** de la cinta.

- Una nueva configuración avanzada de cliente (aún en versión preliminar) para activar la clasificación y ejecutarla continuamente en segundo plano. Cuando esta configuración está habilitada, en el caso de las aplicaciones de Office, la clasificación automática y recomendada se ejecuta continuamente en segundo plano, en lugar de ejecutarse cuando se guardan los documentos. Gracias a este cambio de comportamiento ahora se puede aplicar la clasificación automática y recomendada a los documentos almacenados en SharePoint Online. [Más información](client-admin-guide-customizations.md#turn-on-classification-to-run-continuously-in-the-background)

- Una nueva configuración de cliente avanzada para que Outlook no aplique la etiqueta predeterminada configurada en la directiva de Azure Information Protection. Por el contrario, Outlook puede aplicar otra etiqueta predeterminada o ninguna. [Más información](client-admin-guide-customizations.md#set-a-different-default-label-for-outlook) 

- En el caso de las aplicaciones de Office, al especificar permisos personalizados, ahora se puede examinar y seleccionar los usuarios desde un icono de la libreta de direcciones. Esta opción aporta paridad a la experiencia del usuario al especificar permisos personalizados mediante el Explorador de archivos.

- Compatibilidad con un método de autenticación completamente no interactivo en las cuentas de servicio que use PowerShell y a las que no se puede conceder el derecho de **inicio de sesión local**. Este método de autenticación requiere que se utilice el nuevo parámetro *Token* con [Set-AIPAuthentication](/powershell/module/azureinformationprotection/Set-AIPAuthentication) y que se ejecute un script de PowerShell como una tarea. [Más información](client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)

- Nuevo parámetro, *IntegratedAuth* para [Set-RMSServerAuthentication](/powershell/module/azureinformationprotection/set-rmsserverauthentication). Este parámetro admite el modo de servidor de AD RMS, que es necesario para que AD RMS sea compatible con el FCI de Windows Server.


**Correcciones**:

Correcciones de estabilidad y de escenarios concretos:

- En el caso de las versiones de Office 16.0.8628.2010 y versiones posteriores (hacer clic y ejecutar), la barra de Azure Information Protection admite las opciones de presentación de monitor más recientes, que antes podían provocar que la barra se mostrará fuera de las aplicaciones de Office.

- Si dos organizaciones que usan Azure Information Protection comparten documentos y correos electrónicos con etiquetas, las etiquetas de cada una de ellas se conservan, no se reemplazan por las de la otra.

- Para Excel:
        
    - Compatibilidad con el cambio de temas de Office o de Windows, lo que anteriormente provocaba que Excel no mostrara datos tras dicho cambio.
        
    - Compatibilidad con celdas que contienen referencias cruzadas, lo que anteriormente provocaba daños en el texto de la celda.
    
    - Compatibilidad para escribir caracteres japoneses, chinos o coreanos, que previamente cerraban una ventana para que estos caracteres no se pudieran seleccionar.
    
    - Compatibilidad para comentarios, que previamente cerraban el comentario mientras se escribía.

- En PowerPoint: compatibilidad con coautoría, que anteriormente podría provocar la pérdida de datos.

- Ahora, los archivos con la extensión .xml se pueden inspeccionar para realizar la clasificación automática o recomendada.

- Ahora, el visor puede abrir archivos de texto protegidos (.ptxt y .pxml) cuyo tamaño supere los 20 MB. 
- Outlook ya no se bloquea cuando se utilizan los avisos de Outlook.

- Arranque correcto en Office de 64 bits, para que pueda proteger documentos y correos electrónicos.

- Ahora puede configurar una etiqueta para los permisos definidos por el usuario de Word, Excel, PowerPoint y el Explorador de archivos, así como usar la configuración de cliente avanzada para ocultar las opciones de permisos personalizados. [Más información](client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users) 

- Vuelva a usar la fuente Calibri si los marcadores visuales de la directiva de Azure Information Protection están configurados con un nombre de fuente que no esté instalada en el cliente.

- Evite que Office deje de funcionar tras la actualización del cliente de Azure Information Protection.

- Para las aplicaciones de Office, mejora del rendimiento y reducción del consumo de memoria.

- Cuando configure una etiqueta para los permisos definidos por el usuario y la protección de HYOK (AD RMS), la protección ya no utiliza el servicio Azure Rights Management de forma incorrecta.

- Para una experiencia de administración más coherente, las subetiquetas ya no heredan los distintivos visuales ni la configuración de protección de su etiqueta primaria.

**Cambios adicionales**:

- Para [registro de uso del cliente](client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client ): los identificadores de evento 102 y 103 se reemplazan por el identificador de evento 101.

## <a name="version-110560"></a>Versión 1.10.56.0

**Lanzamiento**: 18/09/2017

Esta versión incluye la versión MSIPC 1.0.3219.0619 del cliente RMS.

**Nuevas características**:

- Compatibilidad con las nuevas condiciones de DLP de Office 365 que puede configurar para una etiqueta. Para más información, vea [Configuración de condiciones para una etiqueta de Azure Information Protection](../configure-policy-classification.md).

- Compatibilidad con las etiquetas configuradas para acciones definidas por el usuario. En Outlook, esta etiqueta se aplica automáticamente a la opción No reenviar. En Word, Excel, PowerPoint y el Explorador de archivos, esta etiqueta pide al usuario que especifique permisos personalizados. Para más información, vea [Configuración de una etiqueta de Azure Information Protection para protección](../configure-policy-protection.md).

- Las etiquetas admiten varios idiomas. A partir del 30 de agosto de 2017, en la [directiva predeterminada](../configure-policy-default.md) se incluye compatibilidad con varios idiomas que se muestra a los usuarios en esta versión del cliente. Para que los usuarios vean las etiquetas de una directiva predeterminada en su idioma preferido antes de esta fecha y para las etiquetas que configure, vea [How to configure labels for different languages in Azure Information Protection](Cómo configurar etiquetas y plantillas para distintos idiomas en Azure Information Protection)configure-policy-languages.md).

- Las etiquetas se muestran desde el botón **Proteger** de la cinta de Office, además de mostrarse en la barra de Information Protection. 

- Protección nativa para los siguientes tipos de archivo de Visio: .vsdm, .vsdx, .vssm, .vssx, .vstm y .vstx

- Compatibilidad con configuraciones de cliente avanzadas que se configuran en Azure Portal. Entre ellas, figuran las siguientes:
    
    - [Mostrar u ocultar el botón No reenviar en Outlook](client-admin-guide-customizations.md#hide-or-show-the-do-not-forward-button-in-outlook)
    
    - [Configuración de las opciones de permisos personalizados para que estén disponibles o no disponibles para los usuarios](client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users)
    
    - [Ocultación de manera permanente de la barra de Azure Information Protection](client-admin-guide-customizations.md#permanently-hide-the-azure-information-protection-bar)
    
    - [Habilitación de la clasificación recomendada en Outlook](client-admin-guide-customizations.md#enable-recommended-classification-in-outlook)

- En PowerShell, se admite el etiquetado de archivos de forma no interactiva mediante los nuevos cmdlets de PowerShell, [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) y [Clear-AIPAuthentication](/powershell/module/azureinformationprotection/clear-aipauthentication). Para más información sobre cómo usar estos cmdlets, vea la [sección de PowerShell](client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) de la guía para administradores.

- En el caso de los cmdlets de PowerShell, [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) y [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification), existen nuevos parámetros: **Owner** y **PreserveFileDetails**. Estos parámetros permiten especificar una dirección de correo electrónico para la propiedad personalizada Owner y dejar la fecha sin modificar para los documentos que etiquete.

**Correcciones**:

Correcciones de estabilidad y de escenarios concretos:

- Compatibilidad con la protección genérica de archivos grandes que anteriormente podían provocar daños si eran mayores de 1 GB. Ahora, el tamaño de archivo está limitado solo por el espacio en disco y la memoria disponibles. Para más información sobre las limitaciones de tamaño de archivo, vea [Tamaños de archivo compatibles para protección](client-admin-guide-file-types.md#file-sizes-supported-for-protection) en la guía para administradores.

- El visor del cliente de Azure Information Protection abre los archivos PDF protegidos (.ppdf) como de solo vista.

- Compatibilidad con el etiquetado y la protección de los archivos almacenados en SharePoint Server.

- Las marcas de agua ahora admiten varias líneas. Además, las marcas visuales ahora se aplican a un documento [solo al guardar por primera vez]configure-policy-markings.md#when-visual-markings-are-applied) en lugar de hacerlo cada vez que se guarda un documento.

- La opción **Ejecutar diagnósticos** del cuadro de diálogo **Ayuda y comentarios** se ha sustituido por **Restablecer configuración**. Ha cambiado el comportamiento de esta acción para incluir el cierre de sesión del usuario y eliminar la directiva de Azure Information Protection. Para más información, vea [Más información sobre la opción Restablecer configuración](..\rms-client\client-admin-guide.md#more-information-about-the-reset-settings-option) de la guía para administradores.

- Compatibilidad con la autenticación de proxy.

Correcciones para una mejor experiencia del usuario:

- Validación de correo electrónico cuando los usuarios especifican permisos personalizados. Además, ahora pueden especificarse varias direcciones de correo electrónico al presionar Entrar.

- La etiqueta principal no se muestra cuando todas sus etiquetas secundarias están configuradas para la protección y el cliente no tiene una edición de Office que admita la protección. 

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre la instalación y el uso del cliente: 

- Para usuarios: [Descarga e instalación del cliente](install-client-app.md)

- Para administradores: [Guía para administradores del cliente de Azure Information Protection](client-admin-guide.md)


