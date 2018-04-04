---
title: Cliente de Azure Information Protection&colon; historial de publicación de versiones y directiva de soporte técnico
description: Consulte las novedades o los cambios en una versión del cliente de Azure Information Protection para Windows y conozca la directiva de ciclo de vida de soporte técnico.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/19/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 1da6a647715389f912af5192b5b70a80f0bd35e9
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Cliente de Azure Information Protection: historial de publicación de versiones y directiva de soporte técnico

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2*

El equipo de Azure Information Protection actualiza de forma periódica el cliente de Azure Information Protection para implementar correcciones y agregar nuevas funciones. 

Puede descargar la versión de lanzamiento de disponibilidad general más reciente y la versión preliminar actual desde el [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). Estas versiones también se incluyen en el Catálogo de Microsoft Update (categoría: **Azure Information Protection**), de modo que puede implementar el cliente mediante WSUS, Configuration Manager u otros mecanismos de implementación de software que usan Microsoft Update.

### <a name="servicing-information-and-timelines"></a>Información y escalas de tiempo de mantenimiento

Cada versión de disponibilidad general del cliente de Azure Information Protection es compatible hasta seis meses después del lanzamiento de la versión de disponibilidad general posterior. En esta página no se incluyen las versiones no admitidas del cliente. Las correcciones y las nuevas funcionalidades siempre se aplican a la versión más reciente de GA y no se aplicarán a las versiones anteriores de GA.

Las versiones preliminares no se deben implementar para los usuarios finales en las redes de producción. En su lugar, use la versión preliminar más reciente para ver y probar nuevas funcionalidades o correcciones que se incluyen en la próxima versión de GA. No se admiten las versiones preliminares que no están actualizadas.

### <a name="release-history"></a>Historial de versiones

Use la información siguiente para consultar las novedades o los cambios en una versión compatible del cliente de Azure Information Protection para Windows. La versión más reciente aparece en primer lugar. 

> [!NOTE]
> Las revisiones secundarias no se enumeran. Por tanto, si tiene algún problema con el cliente de Azure Information Protection, se recomienda que compruebe si se ha corregido en la versión de GA más reciente. Si el problema continúa, compruebe la versión preliminar actual.
>  
> Para obtener soporte técnico, consulte la información sobre [Opciones de soporte y recursos de la comunidad](../get-started/information-support.md#support-options-and-community-resources). También lo invitamos a participar en el equipo de Azure Information Protection, en su [sitio de Yammer](https://www.yammer.com/askipteam/).

## <a name="versions-later-than-110560"></a>Versiones posteriores a la 1.10.56.0

Si tiene una versión del cliente posterior a la 1.10.56.0, se trata de una compilación preliminar para fines de prueba y evaluación.

La versión preliminar actual es la **1.21.203.0** y tiene los siguientes cambios con respecto a la versión de disponibilidad general actual del cliente.

Esta versión incluye la versión MSIPC 1.0.3403.1224 del cliente de RMS.

**Nuevas características**:

- El analizador de Azure Information Protection: el módulo de PowerShell de la que se incluye con el cliente tiene nuevos cmdlets para instalar y configurar el analizador, con el fin de que pueda detectar, clasificar y proteger los archivos de sus almacenes de datos locales. Para obtener instrucciones, consulte [Implementación del analizador de Azure Information Protection para clasificar y proteger automáticamente los archivos](../deploy-use/deploy-aip-scanner.md). 

- En el caso de las aplicaciones de Office, la clasificación automática y recomendada se ejecuta continuamente en segundo plano, en lugar de ejecutarse cuando se guardan los documentos. Gracias a este cambio de comportamiento ahora se puede aplicar la clasificación automática y recomendada a los documentos almacenados en SharePoint Online. [Más información](../deploy-use/configure-policy-classification.md#how-automatic-or-recommended-labels-are-applied) 

- Ahora puede establecer distintivos visuales diferentes para Word, Excel, PowerPoint y Outlook mediante el uso de la instrucción variable "If.App" en la cadena de texto e identificar el tipo de aplicación. [Más información](../deploy-use/configure-policy-markings.md#setting-different-visual-markings-for-word-excel-powerpoint-and-outlook)

- Compatibilidad con la [configuración de directivas](../deploy-use/configure-policy-settings.md). **Muestre la barra de Information Protection en las aplicaciones de Office**. Si este valor está desactivado, los usuarios seleccionan las etiquetas en el botón **Proteger** de la cinta.

- Una nueva configuración de cliente avanzada para que Outlook no aplique la etiqueta predeterminada configurada en la directiva de Azure Information Protection. Por el contrario, Outlook puede aplicar otra etiqueta predeterminada o ninguna. [Más información](client-admin-guide-customizations.md#set-a-different-default-label-for-outlook) 

- En el caso de las aplicaciones de Office, al especificar permisos personalizados, ahora se puede examinar y seleccionar los usuarios desde un icono de la libreta de direcciones. Esta opción aporta paridad a la experiencia del usuario al especificar permisos personalizados mediante el Explorador de archivos.

- Compatibilidad con un método de autenticación completamente no interactivo en las cuentas de servicio que use PowerShell y a las que no se puede conceder el derecho de **inicio de sesión local**. Este método de autenticación requiere que se utilice el nuevo parámetro *Token* con [Set-AIPAuthentication](/powershell/module/azureinformationprotection/Set-AIPAuthentication) y que se ejecute un script de PowerShell como una tarea. [Más información](../rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)

- Nuevo parámetro, *IntegratedAuth* para [Set-RMSServerAuthentication](/powershell/module/azureinformationprotection/set-rmsserverauthentication). Este parámetro admite el modo de servidor de AD RMS, que es necesario para que AD RMS sea compatible con el FCI de Windows Server.


**Correcciones**:

Correcciones de estabilidad y de escenarios concretos:

- En el caso de las versiones de Office 16.0.8628.2010 y versiones posteriores (hacer clic y ejecutar), la barra de Azure Information Protection admite las opciones de presentación de monitor más recientes, que antes podían provocar que la barra se mostrará fuera de las aplicaciones de Office.

- Si dos organizaciones que usan Azure Information Protection comparten documentos y correos electrónicos con etiquetas, las etiquetas de cada una de ellas se conservan, no se reemplazan por las de la otra.

- Compatibilidad con celdas de Excel que contienen referencias cruzadas, lo que anteriormente provocaba daños en el texto de la celda.

- Compatibilidad con el cambio de temas de Office o de Windows, lo que anteriormente provocaba que Excel no mostrara datos tras dicho cambio.

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


## <a name="version-110560"></a>Versión 1.10.56.0

**Lanzamiento**: 18/09/2017

Esta versión incluye la versión MSIPC 1.0.3219.0619 del cliente RMS.

**Nuevas características**:

- Compatibilidad con las nuevas condiciones de DLP de Office 365 que puede configurar para una etiqueta. Para más información, vea [Configuración de condiciones para una etiqueta de Azure Information Protection](../deploy-use/configure-policy-classification.md).

- Compatibilidad con las etiquetas configuradas para acciones definidas por el usuario. En Outlook, esta etiqueta se aplica automáticamente a la opción No reenviar. En Word, Excel, PowerPoint y el Explorador de archivos, esta etiqueta pide al usuario que especifique permisos personalizados. Para más información, vea [Configuración de una etiqueta de Azure Information Protection para protección](../deploy-use/configure-policy-protection.md).

- Las etiquetas admiten varios idiomas. A partir del 30 de agosto de 2017, en la [directiva predeterminada](../deploy-use/configure-policy-default.md) se incluye compatibilidad con varios idiomas que se muestra a los usuarios en esta versión del cliente. Para que los usuarios vean las etiquetas de una directiva predeterminada en su idioma preferido antes de esta fecha y para las etiquetas que configure, vea [Cómo configurar etiquetas y plantillas para distintos idiomas en Azure Information Protection](../deploy-use/configure-policy-languages.md).

- Las etiquetas se muestran desde el botón **Proteger** de la cinta de Office, además de mostrarse en la barra de Information Protection. 

- Protección nativa para los siguientes tipos de archivo de Visio: .vsdm, .vsdx, .vssm, .vssx, .vstm y .vstx

- Compatibilidad con configuraciones de cliente avanzadas que se configuran en Azure Portal. Entre ellas, figuran las siguientes:
    
    - [Mostrar u ocultar el botón No reenviar en Outlook](../rms-client/client-admin-guide-customizations.md#hide-or-show-the-do-not-forward-button-in-outlook)
    
    - [Configuración de las opciones de permisos personalizados para que estén disponibles o no disponibles para los usuarios](../rms-client/client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users)
    
    - [Ocultación de manera permanente de la barra de Azure Information Protection](../rms-client/client-admin-guide-customizations.md#permanently-hide-the-azure-information-protection-bar)
    
    - [Habilitación de la clasificación recomendada en Outlook](../rms-client/client-admin-guide-customizations.md#enable-recommended-classification-in-outlook)

- En PowerShell, se admite el etiquetado de archivos de forma no interactiva mediante los nuevos cmdlets de PowerShell, [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) y [Clear-AIPAuthentication](/powershell/module/azureinformationprotection/clear-aipauthentication). Para más información sobre cómo usar estos cmdlets, vea la [sección de PowerShell](../rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) de la guía para administradores.

- En el caso de los cmdlets de PowerShell, [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) y [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification), existen nuevos parámetros: **Owner** y **PreserveFileDetails**. Estos parámetros permiten especificar una dirección de correo electrónico para la propiedad personalizada Owner y dejar la fecha sin modificar para los documentos que etiquete.

**Correcciones**:

Correcciones de estabilidad y de escenarios concretos:

- Compatibilidad con la protección genérica de archivos grandes que anteriormente podían provocar daños si eran mayores de 1 GB. Ahora, el tamaño de archivo está limitado solo por el espacio en disco y la memoria disponibles. Para más información sobre las limitaciones de tamaño de archivo, vea [Tamaños de archivo compatibles para protección](client-admin-guide-file-types.md#file-sizes-supported-for-protection) en la guía para administradores.

- El visor del cliente de Azure Information Protection abre los archivos PDF protegidos (.ppdf) como de solo vista.

- Compatibilidad con el etiquetado y la protección de los archivos almacenados en SharePoint Server.

- Las marcas de agua ahora admiten varias líneas. Además, las marcas visuales ahora se aplican a un documento [solo al guardar por primera vez](../deploy-use/configure-policy-markings.md#when-visual-markings-are-applied) en lugar de hacerlo cada vez que se guarda un documento.

- La opción **Ejecutar diagnósticos** del cuadro de diálogo **Ayuda y comentarios** se ha sustituido por **Restablecer configuración**. Ha cambiado el comportamiento de esta acción para incluir el cierre de sesión del usuario y eliminar la directiva de Azure Information Protection. Para más información, vea [Más información sobre la opción Restablecer configuración](..\rms-client\client-admin-guide.md#more-information-about-the-reset-settings-option) de la guía para administradores.

- Compatibilidad con la autenticación de proxy.

Correcciones para una mejor experiencia del usuario:

- Validación de correo electrónico cuando los usuarios especifican permisos personalizados. Además, ahora pueden especificarse varias direcciones de correo electrónico al presionar Entrar.

- La etiqueta principal no se muestra cuando todas sus etiquetas secundarias están configuradas para la protección y el cliente no tiene una edición de Office que admita la protección. 

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre la instalación y el uso del cliente: 

- Para usuarios: [Descarga e instalación del cliente](install-client-app.md)

- Para administradores: [Guía para administradores del cliente de Azure Information Protection](client-admin-guide.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
