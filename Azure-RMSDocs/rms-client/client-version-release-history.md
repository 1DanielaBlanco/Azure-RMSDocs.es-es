---
title: "Cliente de Azure Information Protection&colon; historial de publicación de versiones y directiva de soporte técnico"
description: "Consulte las novedades o los cambios en una versión del cliente de Azure Information Protection para Windows y conozca la directiva de ciclo de vida de soporte técnico."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/16/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: e107d796ebda1b1942e19ede8c794f79defbf64e
ms.sourcegitcommit: fd3932ab19a00229b56efc3e301abaf9cff3f70b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Cliente de Azure Information Protection: historial de publicación de versiones y directiva de soporte técnico

>*Se aplica a: Azure Information Protection*

El equipo de Azure Information Protection actualiza de forma periódica el cliente de Azure Information Protection para implementar correcciones y agregar nuevas funciones. 

Puede descargar la versión de lanzamiento de disponibilidad general más reciente y la versión preliminar actual desde el [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). Estas versiones también se incluyen en el Catálogo de Microsoft Update (categoría: **Azure Information Protection**), de modo que puede implementar el cliente mediante WSUS, Configuration Manager u otros mecanismos de implementación de software que usan Microsoft Update.

### <a name="servicing-information-and-timelines"></a>Información y escalas de tiempo de mantenimiento

Las versiones de disponibilidad general (GA) del cliente de Azure Information Protection se admiten durante un período de seis meses a partir de su fecha de publicación. Las correcciones y las nuevas funcionalidades siempre se aplican a la versión más reciente de GA y no se aplicarán a las versiones anteriores de GA.

Las versiones preliminares no se deben implementar para los usuarios finales en las redes de producción. En su lugar, use la versión preliminar más reciente para ver y probar nuevas funcionalidades o correcciones que se incluyen en la próxima versión de GA. No se admiten las versiones preliminares que no están actualizadas.

### <a name="release-history"></a>Historial de versiones

Use la información siguiente para consultar las novedades o los cambios en una versión compatible del cliente de Azure Information Protection para Windows. La versión más reciente aparece en primer lugar. 


> [!NOTE]
> Las revisiones secundarias no se enumeran. Por tanto, si tiene algún problema con el cliente de Azure Information Protection, se recomienda que compruebe si se ha corregido en la versión de GA más reciente. Si el problema continúa, compruebe la versión preliminar actual.
>  
> Para obtener soporte técnico, consulte la información sobre [Opciones de soporte y recursos de la comunidad](../get-started/information-support.md#support-options-and-community-resources). También lo invitamos a participar en el equipo de Azure Information Protection, en su [sitio de Yammer](https://www.yammer.com/askipteam/).

## <a name="versions-later-than-110560"></a>Versiones posteriores a la 1.10.56.0

Si tiene una versión del cliente posterior a la 1.10.56.0, se trata de una compilación preliminar para fines de prueba y evaluación. 

Para conocer las novedades o los cambios en la versión preliminar actual con respecto a la última versión de disponibilidad general del cliente, consulte la sección **Detalles** en la [página de descarga](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 

## <a name="version-110560"></a>Versión 1.10.56.0

**Lanzamiento**: 18/09/2017

Esta versión incluye la versión MSIPC 1.0.3219.0619 del cliente RMS.

**Nuevas características**:

- Compatibilidad con las nuevas condiciones de DLP de Office 365 que puede configurar para una etiqueta. Para más información, vea [Configuración de condiciones para una etiqueta de Azure Information Protection](../deploy-use/configure-policy-classification.md).

- Compatibilidad con las etiquetas configuradas para acciones definidas por el usuario. En Outlook, esta etiqueta se aplica automáticamente a la opción No reenviar. En Word, Excel, PowerPoint y el Explorador de archivos, esta etiqueta pide al usuario que especifique permisos personalizados. Para más información, vea [Configuración de una etiqueta de Azure Information Protection para protección](../deploy-use/configure-policy-protection.md).

- Las etiquetas se muestran desde el botón **Proteger** de la cinta de Office, además de mostrarse en la barra de Information Protection. 

- Protección nativa para los siguientes tipos de archivo de Visio: .vsdm, .vsdx, .vssm, .vssx, .vstm y .vstx

- Compatibilidad con configuraciones de cliente avanzadas que se configuran en Azure Portal. Entre ellas, figuran las siguientes:
    
    - [Ocultación del botón No reenviar en Outlook](../rms-client/client-admin-guide-customizations.md#hide-the-do-not-forward-button-in-outlook)
    
    - [Configuración de opciones de permisos personalizados para que no estén disponibles para los usuarios](../rms-client/client-admin-guide-customizations.md#make-the-custom-permissions-options-unavailable-to-users)
    
    - [Ocultación de manera permanente de la barra de Azure Information Protection](../rms-client/client-admin-guide-customizations.md#make-the-custom-permissions-options-unavailable-to-users)
    
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

## <a name="version-172100"></a>Versión 1.7.210.0

**Lanzamiento**: 06/06/2017

Esta versión incluye la versión MSIPC 1.0.2217.1 del cliente RMS.

**Nuevas características**:

- Nuevo cmdlet de PowerShell, [Set-AIPFileClassification](/powershell/module/azureinformationprotection/Set-AIPFileClassification). Cuando ejecuta este cmdlet, revisa el contenido del archivo y aplica automáticamente etiquetas a los archivos no etiquetados, según las condiciones que especifica en la directiva de Azure Information Protection.

**Correcciones**:

- Todos los cmdlets de etiquetado y clasificación ahora se admiten en equipos no conectados a Internet pero que tienen una directiva de Azure Information Protection válida.

- Para mantener la coherencia, un parámetro de salida del cmdlet [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) se cambia de inglés británico (**IsLabelled**) a inglés de Estados Unidos (**IsLabeled**). Si tiene scripts o procesos automatizados que buscan este parámetro, actualice la ortografía de este parámetro.

- Correcciones generales para mantener la estabilidad que incluyen:

    - En Outlook: correcciones de bloqueos, alto consumo de memoria y problemas de visualización de los menús.
    
    - En Word, Excel y PowerPoint: correcciones para un alto uso de CPU, problemas de visualización cuando se guardan archivos Excel de gran tamaño o la aplicación deja de responder. 
    
    Además en estas aplicaciones, para mejorar el rendimiento de Office 2016 con SharePoint Online y OneDrive para la empresa, el etiquetado automático y recomendado se aplica cuando se cierra el archivo en lugar de hacerlo cuando se guarda (ya sea que se guarde automáticamente o el usuario elija guardarlo). Del mismo modo, si la opción **All documents and email must have a label** (Todos los documentos y correos electrónicos deben tener una etiqueta) está habilitada, no se pide a los usuarios que seleccionen una etiqueta hasta que se cierra el archivo. La excepción es para Word 2016 y Excel 2016 y el usuario selecciona la opción **Guardar como**. Luego, esta acción desencadena estos comportamientos de etiquetado si están configurados. 

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre la instalación y el uso del cliente: 

- Para usuarios: [Descarga e instalación del cliente](install-client-app.md)

- Para administradores: [Guía para administradores del cliente de Azure Information Protection](client-admin-guide.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
