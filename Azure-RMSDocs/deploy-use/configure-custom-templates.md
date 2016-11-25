---
title: "Configuración de plantillas personalizadas para el servicio Azure Rights Management | Azure Information Protection"
description: "Información e instrucciones para que los administradores configuren y administren plantillas de derechos de uso. Las plantillas facilitan a los usuarios y otros administradores aplicar directivas a archivos confidenciales que restringen el acceso a usuarios autorizados."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1775d8d0-9a59-42c8-914f-ce285b71ac1c
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: ea64bd17994a9ce38ed0d758ec63156a7f64c732


---

# <a name="configuring-custom-templates-for-the-azure-rights-management-service"></a>Configuración de plantillas personalizadas para el servicio Azure Rights Management

>*Se aplica a: Azure Information Protection, Office 365*

Cuando el servicio Azure Rights Management se haya [activado](activate-service.md), los usuarios podrán automáticamente usar dos plantillas predeterminadas con las que podrán aplicar directivas de administración de derechos a archivos confidenciales y, de este modo, restringir el acceso solamente a los usuarios autorizados de su organización. Estas dos plantillas presentan las restricciones de directivas de derechos siguientes:

-   Visualización de solo lectura para el contenido protegido

    -   Nombre para mostrar: **&lt;nombre de la organización&gt; - Solo vista confidencial**

    -   Permiso específico: Ver contenido

-   Lectura o modificación de permisos de contenido protegido

    -   Nombre para mostrar: **&lt;nombre de la organización&gt; - Confidencial**

    -   Permisos específicos: Ver contenido, Guardar archivo, Editar contenido, Ver derechos asignados, Permitir macros, Reenviar, Responder y Responder a todos

Además, la [aplicación RMS sharing](../rms-client/sharing-app-windows.md) permite a los usuarios definir su propio conjunto de permisos. Y, para el cliente de Outlook y Outlook Web Access, los usuarios pueden seleccionar la opción [No reenviar](../deploy-use/configure-usage-rights.md#do-not-forward-option-for-emails).

Para muchas organizaciones, las plantillas predeterminadas pueden ser suficientes. Pero si quieres crear tus propias plantillas de directivas de derechos personalizadas, puedes hacerlo. Entre los motivos para crear una plantilla personalizada encontramos los siguientes:

-   Quieres una plantilla que garantice los derechos a una red secundaria de usuarios de la organización, más que a todos los usuarios.

-   Desea que solo un subconjunto de usuarios puedan ver y seleccionar una plantilla (plantilla de departamento) de las aplicaciones, en lugar de que todos los usuarios de la organización vean y puedan seleccionar la plantilla.

-   Quieres definir un derecho personalizado para una plantilla, como Ver y Editar, pero no Copiar e Imprimir.

-   Quieres configurar opciones adicionales en una plantilla, entre las cuales se incluye una fecha de caducidad y si se puede acceder al contenido sin conexión a Internet.

Para que los usuarios puedan seleccionar una plantilla personalizada que contenga una configuración como estas, en primer lugar, debes crear una plantilla personalizada, configurarla y, a continuación, publicarla. Aunque probablemente requerirá solo unas pocas plantillas, puede tener un máximo de 500 plantillas personalizadas guardadas en Azure. 

Use la información siguiente para tratar de configurar y usar plantillas personalizadas:

-   [Cómo crear, configurar y publicar una plantilla personalizada](create-template.md)

-   [Cómo copiar una plantilla](copy-template.md)

-   [Cómo quitar (archivar) plantillas](remove-template.md)

-   [Actualización de plantillas para usuarios](refresh-templates.md)

-   [Referencia de PowerShell para plantillas personalizadas](configure-templates-with-powershell.md)





<!--HONumber=Nov16_HO2-->


