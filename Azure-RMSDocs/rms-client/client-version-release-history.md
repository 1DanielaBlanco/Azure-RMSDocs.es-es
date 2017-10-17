---
title: "Cliente de Azure Information Protection&colon; historial de publicación de versiones"
description: "Consulte las novedades o los cambios en una publicación del cliente de Azure Information Protection para Windows."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/09/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ccd6d0cec6a71527fad0303369baad90dd733958
ms.sourcegitcommit: bcc2f69475f811245d2beaf79c67a3d8569c4821
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/11/2017
---
# <a name="azure-information-protection-client-version-release-history"></a>Cliente de Azure Information Protection: historial de publicación de versiones

>*Se aplica a: Azure Information Protection*

El equipo de Azure Information Protection actualiza de forma periódica el cliente de Azure Information Protection para implementar correcciones y agregar nuevas funciones. El cliente se incluye en el Catálogo de Microsoft Update (categoría: **Azure Information Protection**) y siempre se puede descargar la versión más reciente de disponibilidad general (GA) y la próxima versión (la versión preliminar) desde el [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Las versiones preliminares no se deben implementar para los usuarios finales en las redes de producción. En su lugar, use las versiones preliminares para ver y probar nuevas funcionalidades o correcciones que se incluyen en la próxima versión de GA. 

Use la información siguiente para ver las novedades o los cambios de una versión de GA. La versión más reciente aparece en primer lugar. Para ver los cambios de la versión preliminar actual, vea la información de la página de descarga.

> [!NOTE]
> Las revisiones secundarias no se enumeran. Por tanto, si tiene algún problema con el cliente de Azure Information Protection, compruebe primero que no se trate de un problema con la versión de GA más reciente. Si es así, compruebe la versión preliminar actual.
>  
> Si el problema persiste, vea la información de [Opciones de soporte técnico y recursos de la comunidad](../get-started/information-support.md#support-options-and-community-resources). También lo invitamos a participar en el equipo de Azure Information Protection, en su [sitio de Yammer](https://www.yammer.com/askipteam/).

## <a name="version-110560"></a>Versión 1.10.56.0

**Lanzamiento**: 18/09/2017

Esta versión incluye la versión MSIPC 1.0.3219.0619 del cliente RMS.

**Nuevas características**:

- Compatibilidad con las etiquetas configuradas para acciones definidas por el usuario. En Outlook, esta etiqueta se aplica automáticamente a la opción No reenviar. En Word, Excel, PowerPoint y el Explorador de archivos, esta etiqueta pide al usuario que especifique permisos personalizados. Para más información, vea [Configuración de una etiqueta de Azure Information Protection para protección](../deploy-use/configure-policy-protection.md).

- Compatibilidad con las nuevas condiciones de DLP de Office 365 que puede configurar para una etiqueta. Para más información, vea [Configuración de condiciones para una etiqueta de Azure Information Protection](../deploy-use/configure-policy-classification.md).

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

## <a name="version-14210"></a>Versión 1.4.21.0

**Lanzamiento**: 15/03/2017

**Nuevos requisitos:**

La versión anterior introdujo el nuevo requisito previo de Microsoft .NET Framework 4.6.2 para todo el cliente. Aunque no se recomienda, puede omitir este requisito previo con un parámetro de instalación personalizada: **DowngradeDotNetRequirement**. Para más información, consulte el [sección de instalación del cliente](client-admin-guide.md#how-to-install-the-azure-information-protection-client-for-users) de la guía del administrador.

**Nuevas características**:

- Capacidad de establecer permisos personalizados desde su aplicación de Office, lo que le permite establecer protección únicamente para usted, para grupos externos o parta todos los usuarios de otra organización. Para obtener más información, consulte [Establecimiento de permisos personalizados para un documento](client-classify-protect.md#set-custom-permissions-for-a-document) en la guía del usuario.
    
- Los archivos PDF ahora admiten etiquetas que solo se aplican para clasificación.

- Para archivos PDF, el visor ahora admite opciones, como búsqueda, zoom y giro. Para usar estas opciones, haga clic con el botón derecho en el archivo cuando se muestra en el visor.

**Correcciones**:

- Compatibilidad para unidades asignadas para clasificar y proteger archivos.

- Compatibilidad con archivos de gran tamaño (más de 250 MB) en el visor del cliente de Azure Information Protection. 

- Cuando se configura HYOK, Outlook puede aplicar etiquetas que están configuradas para utilizar plantillas de Azure Rights Management o AD RMS.

## <a name="version-131552"></a>Versión 1.3.155.2

**Lanzamiento**: 02/08/2017

**Nuevos requisitos**:

Microsoft .NET Framework

- Esta versión del cliente de Azure Information Protection requiere una versión mínima de Microsoft .NET Framework 4.6.2 y, en su defecto, el instalador intenta descargarla e instalarla. Una vez completada la instalación del cliente de Azure Information Protection, puede ser necesario reiniciar el equipo.

- Si el visor de Azure Information Protection se instala por separado, se requiere una versión mínima de Microsoft .NET Framework 4.5.2 y, en su defecto, el instalador no lo descarga ni lo instala.

**Nuevas características**:

- Un cliente nuevo y unificado que combina las características de la aplicación Rights Management sharing para Windows con el cliente de Azure Information Protection. Incluye:
    
    - Integración con el Explorador de archivos de Windows (menú contextual) para aplicar etiquetas y protección. Admite formatos de archivo adicionales y la selección de varios archivos.
    - Un visor de documentos protegidos (incluye PDF protegido para SharePoint).
    - Cmdlets de PowerShell para obtener y establecer etiquetas para los archivos que están almacenados localmente o en recursos compartidos de red. Estos cmdlets se instalan como los cmdlets incluidos anteriormente con la herramienta de protección de RMS (módulo RMSProtection).
    - Registros de uso del cliente donde se registra información como qué etiquetas se han aplicado, cómo y por quién.

Esta versión del cliente es la [versión de disponibilidad general](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/08/azure-information-protection-december-update-moves-to-general-availability/) del cliente de versión preliminar que se presentó por primera vez en diciembre de 2016. Para obtener más información sobre esta versión del cliente, vea las siguientes guías:

- [Guía de administrador de cliente de Azure Information Protection](client-admin-guide.md)

- [Guía del usuario de Azure Information Protection](client-user-guide.md)


## <a name="version-1240"></a>Versión 1.2.4.0

**Lanzamiento**: 27/10/2016

**Nueva característica**:

- pruebas de diagnóstico y una opción de restablecimiento que un usuario puede ejecutar desde la aplicación de Office cuando se instala el cliente de Azure Information Protection: en la pestaña **Inicio**, en el grupo **Protección**, haga clic primero en **Proteger**, después en **Ayuda y comentarios** y, por último, en **Ejecutar diagnósticos**. 

    Para más información sobre esta opción, consulte la sección [Additional checks and troubleshooting](client-admin-guide.md#additional-checks-and-troubleshooting) (Comprobaciones adicionales y solución de problemas) en la guía del administrador.

**Correcciones**:

- La instalación del cliente se completa cuando el servicio Windows Update está deshabilitado.

- En Office 2016, cuando guarda un documento y una etiqueta aplicada se configura para un encabezado o pie de página, el cursor no salta al encabezado o pie de página.

- La clasificación automática funciona en Word para texto en cuadros de texto integrados.


## <a name="version-11230"></a>Versión 1.1.23.0

**Lanzamiento**: 1/10/2016

Disponibilidad general.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre la instalación y el uso del cliente:

- Para usuarios: [Descarga e instalación del cliente](install-client-app.md)

- Para administradores: [Guía para administradores del cliente de Azure Information Protection](client-admin-guide.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]