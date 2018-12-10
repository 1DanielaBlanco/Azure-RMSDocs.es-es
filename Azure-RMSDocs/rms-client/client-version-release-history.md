---
title: 'Cliente de Azure Information Protection: historial de publicación de versiones y directiva de soporte técnico'
description: Consulte las novedades o los cambios en una versión del cliente de Azure Information Protection para Windows y conozca la directiva de ciclo de vida de soporte técnico.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/05/2018
ms.topic: conceptual
ms.service: information-protection
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: bfca9c6aab0625a9d35d7648a53f7cce6b74bce6
ms.sourcegitcommit: 8e7b135bf48ced7e53d91f45d62b7bbd0f37634e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/04/2018
ms.locfileid: "52861224"
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Cliente de Azure Information Protection: historial de publicación de versiones y directiva de soporte técnico

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2*

El equipo de Azure Information Protection actualiza de forma periódica el cliente de Azure Information Protection para implementar correcciones y agregar nuevas funciones. 

Puede descargar la versión de lanzamiento de disponibilidad general más reciente y la versión preliminar actual (si está disponible) desde el [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). Tras una breve demora de normalmente un par de semanas, se incluye también la versión de disponibilidad general en el catálogo de Microsoft Update (categoría: **Azure Information Protection**). Esta inclusión en el catálogo significa que puede actualizar el cliente mediante WSUS, Configuration Manager u otros mecanismos de implementación de software que usan Microsoft Update.

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

## <a name="version-141510"></a>Versión 1.41.51.0

> [!TIP]
> ¿Está interesado en evaluar el cliente de etiquetado unificado de Azure Information Protection porque sus etiquetas se publican en el Centro de seguridad y cumplimiento de Office 365? Consulte [Cliente de etiquetado unificado de Azure Information Protection: Información de publicación de versión](unifiedlabelingclient-version-release-history.md).

**Lanzamiento**: 27/11/2018

Esta versión incluye la versión MSIPC 1.0.3592.627 del cliente RMS.

**Nuevas características**

- De forma predeterminada, el cliente de Azure Information Protection ahora protege los archivos PDF mediante el estándar ISO para el cifrado de archivos PDF. Anteriormente, había que habilitar esta compatibilidad con una configuración de cliente avanzada.
    
    Si desea revertir el cliente para proteger los archivos PDF mediante una extensión de nombre de archivo .ppdf, use la misma [configuración de cliente avanzada](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption), pero especifique **False**.

- Compatibilidad con [informes centrales](../reports-aip.md) para la característica de análisis de Azure Information Protection anunciada en Microsoft Ignite.

- Excel también admite ahora [distintivos visuales](../configure-policy-markings.md) en distintos colores.

- Para implementaciones de S/MIME existentes, un nuevo ajuste de cliente avanzado (en versión preliminar) para configurar una etiqueta para aplicar automáticamente la protección S/MIME en Outlook. [Más información](client-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)

- Un nuevo ajuste de cliente avanzado, como alternativa a la modificación del Registro para evitar solicitudes de inicio de sesión para el servicio Azure Information Protection para [equipos desconectados](client-admin-guide-customizations.md#support-for-disconnected-computers).

**Correcciones**:

- El cliente de Azure Information Protection ya no excluye la extensiones de nombre de archivo .zip, .rar y .msg para el Explorador de archivos (clic derecho) y los comandos de PowerShell. Sin embargo, estas extensiones de nombre de archivo excluidas permanecen excluidas de manera predeterminada para el analizador. 

- El cliente de Azure Information Protection puede desproteger varios archivos (selección múltiple y una carpeta que contiene los archivos protegidos) cuando se usa el Explorador de archivos (haciendo clic derecho).

- Para Excel:
    
    - Ahora se aplican marcas visuales si guarda la hoja de cálculo mientras edita una celda.
    
    - Excel 2010: cuando una hoja de cálculo está protegida con el [nivel de permiso](../configure-usage-rights.md#rights-included-in-permissions-levels) de coautor, el botón **Eliminar etiqueta** ahora está disponible cuando hace clic con el botón derecho en el archivo y selecciona **Clasificar y proteger**.

- La configuración de cliente avanzada que puede [quitar encabezados y pies de página de otras soluciones de etiquetado](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions) ahora es compatible con los diseños personalizados.

**Cambios adicionales**:

- Cuando se establece la programación del analizador en **Siempre**, ahora hay un retraso de 30 segundos entre uno y otro análisis.

- El analizador ya no cambia el propietario de Rights Management para los archivos que etiqueta cuando el archivo ya está protegido.

## <a name="version-137190"></a>Versión 1.37.19.0

**Lanzamiento**: 17/09/2018

Esta versión incluye la versión MSIPC 1.0.3592.627 del cliente RMS.

**Nuevas características**: 

- Compatibilidad con el estándar ISO de cifrado de archivos PDF cuando se define una nueva [configuración avanzada del cliente](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption). Cuando esta opción se configura en **True**, los documentos PDF que se protegen conservan su extensión de nombre de archivo .pdf (en lugar de cambiar a .ppdf) y se pueden abrir con lectores de PDF que admitan este estándar ISO. Actualmente, debe indicar a los usuarios que abran manualmente estos documentos PDF protegidos el visor de Azure Information Protection. Para ayudar a que los usuarios puedan hacerlo, cuando abran uno de estos archivos PDF protegidos, verán una página con iconos que pueden seleccionar para su sistema operativo.

- Compatibilidad con nuevos tipos de información confidencial que le ayudarán a clasificar los documentos que contienen información personal. [Más información](../configure-policy-classification.md#sensitive-information-types-that-require-a-minimum-version-of-the-client) 

- Las etiquetas que se aplican a la protección se mostrarán ahora en las aplicaciones de Office 2016 (versión mínima 1805, compilación 9330.2078) cuando se asigne al usuario una licencia de Azure Rights Management (también conocido como Azure Information Protection para Office 365).

- Compatibilidad de etiquetado con el formato **Documento Open XML estricto** en archivos de Word, Excel y PowerPoint. Para más información sobre los formatos Open XML, vea la entrada del blog de Office sobre [nuevas opciones de formato de archivo en el nuevo Office](https://www.microsoft.com/en-us/microsoft-365/blog/2012/08/13/new-file-format-options-in-the-new-office/). 

- Compatibilidad con los archivos que se han protegido con Secure Islands cuando esos archivos no sean documentos PDF y de Office. Por ejemplo, proteger archivos de texto e imagen. O archivos que tienen una extensión de nombre de archivo .pfile. Esta compatibilidad habilita nuevos escenarios, como el analizador de Azure Information Protection, que pueden inspeccionar estos archivos para la búsqueda de información confidencial y vuelven a etiquetarlos automáticamente para Azure Information Protection. [Más información](client-admin-guide-customizations.md#support-for-files-protected-by-secure-islands)

- Nueva configuración de cliente avanzada para quitar los encabezados y los pies de página que se han aplicado a los documentos mediante otras soluciones de etiquetado. [Más información](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)

- Para el analizador de Azure Information Protection:

    - Nuevo cmdlet, [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner): se debe ejecutar después de actualizar desde la versión de disponibilidad general actual (1.29.5.0) o una versión anterior.
    
    - Nuevo cmdlet, [Get AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus): obtiene el estado actual del servicio para el analizador.  
    
    - Nuevo cmdlet, [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan): indica al analizador que inicie un ciclo de exploración única cuando la programación se establece en manual.
    
    - SharePoint Server 2010 es compatible con los clientes que tengan [soporte extendido para esta versión de SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).
    
- Compatibilidad con la nueva hoja **Azure Information Protection - Nodos (versión preliminar)** en Azure Portal, que le permite administrar los escáneres desde una ubicación central. La información de los escáneres implementados que tienen conectividad con Azure se actualiza cada cinco minutos. En esta hoja, puede iniciar el escáner para un examen único, volver a examinar todos los archivos, comprobar el estado de un escáner y ver la velocidad del examen.

**Correcciones**

- Para el analizador de Azure Information Protection:
    
    - Para documentos que están protegidos en las bibliotecas de SharePoint, si el parámetro *DefaultOwner* no se usa en el repositorio de datos, el valor de Editor de SharePoint se usa ahora como valor predeterminado en lugar del valor de autor.
    
    - Entre los informes del analizador se incluyen "Última modificación por" para documentos de Office.
    
    - Ahora puede proteger todos los tipos de archivo mediante el carácter comodín `*` al editar el Registro, tal como se describe en la sección [Edición del registro para el escáner](../deploy-aip-scanner.md#editing-the-registry-for-the-scanner).

- La visualización de mensajes de correo electrónico mediante los iconos de flecha Siguiente elemento y Elemento anterior de la barra de herramientas de acceso rápido muestra la etiqueta correcta para cada correo electrónico.

- Al clasificar y proteger mediante el Explorador de archivos, PowerShell o el analizador, los metadatos de documentos de Office no se quitan ni se cifran.

- Los permisos personalizados admiten las direcciones de correo electrónico del destinatario que contienen un apóstrofo.

- El entorno de equipo se inicializará correctamente (arranque) cuando esta acción se inicie abriendo un documento protegido que se almacena en SharePoint Online.

- Cuando usa el cliente para hacer clic con el botón derecho en Explorador de archivos, PowerShell o el analizador, se bloquea el etiquetado para los archivos que están en ubicaciones de WebDav porque se trata de un escenario no compatible.

- El icono Eliminar etiqueta no se muestra en las aplicaciones cliente (Word, Excel, PowerPoint ni Outlook) cuando se establece la [configuración de directiva](../configure-policy-settings.md) de **All documents and emails must have a label** (Todos los documentos y correos electrónicos deben tener una etiqueta).

**Cambios adicionales**:

- Para [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration):
    
    - Los valores del parámetro *Schedule* ya no son **OneTime**, **Continuous** y **Never**, ahora son **Manual** y **Always**.
        
    - El parámetro *Type* se quita, por lo que también se quita de la salida al ejecutar [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration). De forma predeterminada, solo se inspeccionan los archivos nuevos o modificados tras el primer ciclo de examen. Si ha establecido previamente el parámetro *Type* en **Full** para volver a examinar todos los archivos, ejecute ahora [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan) con el parámetro *Reset*. El analizador también debe configurarse para una programación manual, lo que requiere que el parámetro *Schedule* se establezca en **Manual** con [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).
    
- La lista de exclusión predeterminada del cliente y el analizador ahora incluye archivos .zip, .rar y .msg. El analizador también excluye los archivos .rtf. [Más información](client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)

- La versión de directiva ha cambiado a 1.4. La identificación del número de versión es necesaria para [configurar los equipos desconectados](client-admin-guide-customizations.md#support-for-disconnected-computers).

- El vínculo **Send Us Feedback** (Envíenos sus comentarios) del cuadro de diálogo **Help and Feedback** (Ayuda y comentarios) se ha eliminado. Se ha reemplazado temporalmente por **Report an Issue** (Informar de un problema), pero este vínculo ahora solo se muestra en versiones preliminares. De forma predeterminada, esta opción envía un correo electrónico a Microsoft, pero puede cambiar esta dirección de correo electrónico por una cadena HTTP que especifique. Por ejemplo, una página web personalizada que tiene para que los usuarios notifiquen problemas o una dirección de correo electrónico que vaya a su departamento de soporte técnico. Para modificar esta dirección, use una [configuración de cliente avanzada](client-admin-guide-customizations.md#modify-the-email-address-for-the-report-an-issue-link).

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

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre la instalación y el uso del cliente: 

- Para usuarios: [Descarga e instalación del cliente](install-client-app.md)

- Para administradores: [Guía para administradores del cliente de Azure Information Protection](client-admin-guide.md)

