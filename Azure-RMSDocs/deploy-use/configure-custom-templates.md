---
title: "Configuración de plantillas personalizadas para Azure RMS - AIP"
description: "Información e instrucciones para que los administradores configuren y administren plantillas de derechos de uso. Las plantillas facilitan a los usuarios y otros administradores aplicar directivas a archivos confidenciales que restringen el acceso a usuarios autorizados."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1775d8d0-9a59-42c8-914f-ce285b71ac1c
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 6c3f066a373d253d8488c805828a65513370e3a4
ms.sourcegitcommit: 7bec3dfe3ce61793a33d53691046c5b2bdba3fb9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/27/2017
---
# <a name="configuring-custom-templates-for-the-azure-rights-management-service"></a>Configuración de plantillas personalizadas para el servicio Azure Rights Management

>*Se aplica a: Azure Information Protection, Office 365*

Cuando el servicio de Azure Rights Management esté [activado](activate-service.md), los usuarios podrán usar automáticamente dos plantillas predeterminadas. Estas plantillas facilitan la aplicación de directivas de administración a archivos confidenciales que restringen el acceso a usuarios autorizados de su organización. Las dos plantillas presentan las restricciones de directivas de derechos siguientes:

-   Visualización de solo lectura para el contenido protegido

    -   Nombre para mostrar: **&lt;nombre de la organización&gt; - Solo vista confidencial** o **Extremadamente confidencial\Todos los empleados**

    -   Permiso específico: Ver contenido

-   Lectura o modificación de permisos de contenido protegido

    -   Nombre para mostrar: **&lt;nombre de la organización&gt; - Confidencial** o **Confidencial\Todos los empleados**

    -   Permisos específicos: Ver contenido, Guardar archivo, Editar contenido, Ver derechos asignados, Permitir macros, Reenviar, Responder y Responder a todos

Además, el [cliente de Azure Information Protection](../rms-client/aip-client.md) permite a los usuarios definir su propio conjunto de permisos. Y, para el cliente de Outlook y Outlook Web Access, los usuarios pueden seleccionar la opción [No reenviar](../deploy-use/configure-usage-rights.md#do-not-forward-option-for-emails).

Para muchas organizaciones, las plantillas predeterminadas pueden ser suficientes. Pero si quieres crear tus propias plantillas de directivas de derechos personalizadas, puedes hacerlo. Entre los motivos para crear una plantilla personalizada encontramos los siguientes:

-   Quieres una plantilla que garantice los derechos a una red secundaria de usuarios de la organización, más que a todos los usuarios.

-   Desea que solo un subconjunto de usuarios puedan ver y seleccionar una plantilla (plantilla de departamento) de las aplicaciones, en lugar de que todos los usuarios de la organización vean y puedan seleccionar la plantilla.

-   Quieres definir un derecho personalizado para una plantilla, como Ver y Editar, pero no Copiar e Imprimir.

-   Quieres configurar opciones adicionales en una plantilla, entre las cuales se incluye una fecha de caducidad y si se puede acceder al contenido sin conexión a Internet.

Para que los usuarios puedan seleccionar una plantilla personalizada que contenga una configuración como estas, en primer lugar, debes crear una plantilla personalizada, configurarla y, a continuación, publicarla. Aunque probablemente necesite solo unas pocas plantillas, puede tener un máximo de 500 plantillas personalizadas guardadas en Azure. 

Use la información siguiente para tratar de configurar y usar plantillas personalizadas:

-   [Cómo crear, configurar y publicar una plantilla personalizada](create-template.md)

-   [Cómo copiar una plantilla](copy-template.md)

-   [Cómo quitar (archivar) plantillas](remove-template.md)

-   [Actualización de plantillas para usuarios](refresh-templates.md)

-   [Referencia de PowerShell para plantillas personalizadas](configure-templates-with-powershell.md)

> [!TIP]
> Las plantillas y nuevas opciones para configurar la protección de Azure Rights Management se están migrando a Azure Portal. Esta funcionalidad está actualmente en versión preliminar. Para obtener más información, consulte el anuncio de la entrada de blog [Azure Information Protection unified administration now in Preview](https://blogs.technet.microsoft.com/enterprisemobility/2017/04/26/azure-information-protection-unified-administration-now-in-preview/) (Administración unificada de Azure Information Protection ahora en versión preliminar). 


[!INCLUDE[Commenting house rules](../includes/houserules.md)]

