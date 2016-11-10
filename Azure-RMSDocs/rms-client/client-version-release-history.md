---
title: "Instalación del cliente de Azure Information Protection&colon; Historial de publicación de versiones | Azure Information Protection"
description: "Consulte las novedades o los cambios en una publicación del cliente de Azure Information Protection para Windows."
author: cabailey
manager: mbaldwin
ms.date: 10/27/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b3beeaffd5cf5f0e0a629dd6130d780cec3e05d6
ms.openlocfilehash: ff6573042941640d1cca82d68e85f09c82e3c77b


---

# <a name="azure-information-protection-client-version-release-history"></a>Cliente de Azure Information Protection: historial de publicación de versiones

>*Se aplica a: Azure Information Protection*

El equipo de Azure Information Protection actualiza de forma periódica el cliente de Azure Information Protection para implementar correcciones y agregar nuevas funciones. El cliente se incluye en el catálogo de Microsoft Update (categoría: **Azure Information Protection**), y siempre puede descargar la versión más reciente desde el [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Use la información siguiente para ver las novedades o los cambios de una versión. La versión más reciente aparece en primer lugar. No se muestran las versiones anteriores de la Disponibilidad general. 

> [!NOTE]
> Las revisiones secundarias no se enumeran. Por tanto, si tiene algún problema con el cliente de Azure Information Protection, compruebe primero que no se trate de un problema con la versión más reciente.
>  
> Si el problema persiste, abra una aplicación de Office y, en la pestaña **Inicio**, en el grupo **Protección**, haga clic en **Proteger** y, luego, en **Ayuda y comentarios**. Haga clic en el vínculo **Enviar comentarios**, que puede usar para adjuntar automáticamente los registros de cliente a un mensaje de correo electrónico que se puede enviar al equipo de Information Protection para que lo investiguen. Para opciones de soporte técnico, consulte la información sobre [Opciones de soporte y recursos de la comunidad](../get-started/information-support.md#support-options-and-community-resources).

## <a name="version-1240"></a>Versión 1.2.4.0

**Lanzamiento**: 27/10/2016

**Correcciones**:

- Puede aplicar correctamente una etiqueta que proteja el contenido cuando utiliza Office 2010 y no se ha inicializado el entorno para el servicio de Azure Rights Management (también conocido como "arranque").

- La instalación del cliente se completa cuando el servicio Windows Update está deshabilitado.

- En Office 2016, cuando guarda un documento y una etiqueta aplicada se configura para un encabezado o pie de página, el cursor no salta al encabezado o pie de página.

- La clasificación automática funciona en Word para texto en cuadros de texto integrados.

**Nueva característica**:

- pruebas de diagnóstico y una opción de restablecimiento que un usuario puede ejecutar desde la aplicación de Office cuando se instala el cliente de Azure Information Protection: en la pestaña **Inicio**, en el grupo **Protección**, haga clic primero en **Proteger**, después en **Ayuda y comentarios** y, por último, en **Ejecutar diagnósticos**. 

    Para obtener más información acerca de esta opción, consulte la sección [Para comprobar la instalación, el estado de conexión o notificar un problema](info-protect-client.md#to-verify-installation-connection-status-or-report-a-problem) de la documentación de instalación de cliente.

## <a name="version-11230"></a>Versión 1.1.23.0

**Lanzamiento**: 1/10/2016

Disponibilidad general.

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre cómo instalar el cliente, vea [Instalación del cliente de Azure Information Protection](info-protect-client.md).



<!--HONumber=Oct16_HO4-->


