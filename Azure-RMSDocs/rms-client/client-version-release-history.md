---
title: "Cliente de Azure Information Protection&colon; historial de publicación de versiones"
description: "Consulte las novedades o los cambios en una publicación del cliente de Azure Information Protection para Windows."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/15/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 70c358954a39b02610a77ec81074379dc574158b
ms.sourcegitcommit: d5ce1bce5e63b3e510033ff9d4d246dd3511ed7c
ms.translationtype: HT
ms.contentlocale: es-ES
---
# <a name="azure-information-protection-client-version-release-history"></a>Cliente de Azure Information Protection: historial de publicación de versiones

>*Se aplica a: Azure Information Protection*

El equipo de Azure Information Protection actualiza de forma periódica el cliente de Azure Information Protection para implementar correcciones y agregar nuevas funciones. El cliente se incluye en el Catálogo de Microsoft Update (categoría: **Azure Information Protection**) y siempre puede descargar la versión más reciente de disponibilidad general (GA) y la próxima versión (la versión preliminar) desde el [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Las versiones preliminares no se deben implementar para los usuarios finales en las redes de producción. En su lugar, use las versiones preliminares para ver y probar nuevas funcionalidades o correcciones que se incluyen en la próxima versión de GA. 

Use la información siguiente para ver las novedades o los cambios de una versión de GA. La versión más reciente aparece en primer lugar. Para información sobre la versión preliminar actual, consulte la información que aparece en la página de descarga.

> [!NOTE]
> Las revisiones secundarias no se enumeran. Por tanto, si tiene algún problema con el cliente de Azure Information Protection, compruebe primero que no se trate de un problema con la versión de GA más reciente. Si es así, compruebe la versión preliminar actual.
>  
> Si el problema persiste, vea la información de [Opciones de soporte técnico y recursos de la comunidad](../get-started/information-support.md#support-options-and-community-resources). También lo invitamos a participar en el equipo de Azure Information Protection, en su [sitio de Yammer](https://www.yammer.com/askipteam/).

## <a name="version-14210"></a>Versión 1.4.21.0

**Lanzamiento**: 15/03/2017

**Nuevos requisitos:**

La versión anterior introdujo el nuevo requisito previo de Microsoft .NET Framework 4.6.2 para todo el cliente. Aunque no se recomienda, puede omitir este requisito previo con un parámetro de instalación personalizada: **DowngradeDotNetRequirement**. Para más información, consulte el [sección de instalación del cliente](client-admin-guide.md#how-to-install-the-azure-information-protection-client-for-users) de la guía del administrador.


**Correcciones**:

- Compatibilidad para unidades asignadas para clasificar y proteger archivos.

- Compatibilidad para archivos de gran tamaño (>&250; MB) en el visor. 

- Cuando se configura HYOK, Outlook puede aplicar etiquetas que están configuradas para utilizar plantillas de Azure Rights Management o AD RMS.


**Nuevas características**:

- Capacidad de establecer permisos personalizados desde su aplicación de Office, lo que le permite establecer protección únicamente para usted, para grupos externos o parta todos los usuarios de otra organización. Para obtener más información, consulte [Establecimiento de permisos personalizados para un documento](client-classify-protect.md#set-custom-permissions-for-a-document) en la guía del usuario.
    
- Los archivos PDF ahora admiten etiquetas que solo se aplican para clasificación.

- Para archivos PDF, el visor ahora admite opciones, como búsqueda, zoom y giro. Para usar estas opciones, haga clic con el botón derecho en el archivo cuando se muestra en el visor.


## <a name="version-131552"></a>Versión 1.3.155.2

**Lanzamiento**: 02/08/2017

**Nuevos requisitos**:

Microsoft .NET Framework

- Esta versión del cliente de Azure Information Protection requiere una versión mínima de Microsoft .NET Framework 4.6.2 y, en su defecto, el instalador intenta descargarla e instalarla. Una vez completada la instalación del cliente de Azure Information Protection, puede ser necesario reiniciar el equipo.

- Si el visor de Azure Information Protection se instala por separado, se requiere una versión mínima de Microsoft .NET Framework 4.5.2 y, en su defecto, el instalador no lo descarga ni lo instala.

**Nuevas características**:

- Un cliente nuevo y unificado que combina las características de la aplicación Rights Management sharing para Windows con el cliente de Azure Information Protection. Incluye:
    
    - Integración con el Explorador de archivos de Windows (menú contextual) para aplicar etiquetas y protección. Admite la selección de varios archivos y formatos de archivo adicionales.
    - Un visor de documentos protegidos (incluye PDF protegido para SharePoint).
    - Cmdlets de PowerShell para obtener y establecer etiquetas para los archivos que están almacenados localmente o en recursos compartidos de red. Estos cmdlets se instalan como los cmdlets incluidos anteriormente con la herramienta de protección de RMS (módulo RMSProtection).
    - Registros de uso del cliente donde se registra información como qué etiquetas se han aplicado, cómo y por quién.

Esta versión del cliente es la [versión de disponibilidad general](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/08/azure-information-protection-december-update-moves-to-general-availability/) del cliente de versión preliminar que se presentó por primera vez en diciembre de 2016. Para obtener más información sobre esta versión del cliente, vea las siguientes guías:

- [Guía de administrador de cliente de Azure Information Protection](client-admin-guide.md)

- [Guía del usuario de Azure Information Protection](client-user-guide.md)


## <a name="version-1240"></a>Versión 1.2.4.0

**Lanzamiento**: 27/10/2016

**Correcciones**:

- La instalación del cliente se completa cuando el servicio Windows Update está deshabilitado.

- En Office 2016, cuando guarda un documento y una etiqueta aplicada se configura para un encabezado o pie de página, el cursor no salta al encabezado o pie de página.

- La clasificación automática funciona en Word para texto en cuadros de texto integrados.

**Nueva característica**:

- pruebas de diagnóstico y una opción de restablecimiento que un usuario puede ejecutar desde la aplicación de Office cuando se instala el cliente de Azure Information Protection: en la pestaña **Inicio**, en el grupo **Protección**, haga clic primero en **Proteger**, después en **Ayuda y comentarios** y, por último, en **Ejecutar diagnósticos**. 

    Para más información sobre esta opción, consulte la sección [Additional checks and troubleshooting](client-admin-guide.md#additional-checks-and-troubleshooting) (Comprobaciones adicionales y solución de problemas) en la guía del administrador.

## <a name="version-11230"></a>Versión 1.1.23.0

**Lanzamiento**: 1/10/2016

Disponibilidad general.

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre la instalación del cliente:

- Para usuarios: [Descarga e instalación del cliente](install-client-app.md)

- Para administradores: [Guía para administradores del cliente de Azure Information Protection](client-admin-guide.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]