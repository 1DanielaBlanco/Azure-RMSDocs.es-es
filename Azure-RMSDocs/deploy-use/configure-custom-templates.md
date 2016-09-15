---
title: "Configuración de plantillas personalizadas para Azure Rights Management | Azure RMS"
description: "Información e instrucciones para que los administradores configuren y administren plantillas de derechos de uso. Las plantillas facilitan a los usuarios y otros administradores aplicar directivas a archivos confidenciales que restringen el acceso a usuarios autorizados."
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1775d8d0-9a59-42c8-914f-ce285b71ac1c
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ad32910b482ca9d92b4ac8f3f123eda195db29cd
ms.openlocfilehash: 4f04a8b892cfb1f1ab62d1810fae172ad8bc9747


---

# Configuración de plantillas personalizadas para Azure Rights Management

>*Se aplica a: Azure Rights Management, Office 365*

Tras [activar Azure Rights Management](activate-service.md) (Azure RMS), los usuarios pueden automáticamente usar dos plantillas predeterminadas, lo que les facilita la aplicación de directivas para archivos confidenciales para los que desean restringir el acceso solamente a usuarios autorizados de su organización. Estas dos plantillas presentan las restricciones de directivas de derechos siguientes:

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

-   [How to refresh templates for users (Actualización de plantillas para usuarios)](refresh-templates.md)

-   [Use PowerShell to manage templates (Usar PowerShell para administrar plantillas)](configure-templates-with-powershell.md)





<!--HONumber=Aug16_HO4-->


