---
title: Implementación de una aplicación - AIP
description: En este artículo se describe el proceso de implementación de una aplicación de servicio en un inquilino diferente en la que originalmente se desarrolló.
keywords: ''
author: kkanakas
ms.author: kartikk
manager: mbaldwin
ms.date: 02/27/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 34dc6d6f-cfe4-4848-9b11-8d90c4b38ef7
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.openlocfilehash: 878f19d56b4a2714c0495925ddfb88918a2a92a6
ms.sourcegitcommit: 26a2c1becdf3e3145dc1168f5ea8492f2e1ff2f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2018
ms.locfileid: "44145840"
---
# <a name="deploying-a-service-application-into-a-different-tenant"></a>Implementación de una aplicación de servicio en un inquilino diferente

En este artículo se describe el proceso de implementación de una aplicación de servicio. En este escenario estamos cambiando la aplicación de ser registrada con su inquilino de AD de desarrollo inicial a ser registrada con un inquilino de AD de producción de otra compañía.

> [!Note]
> Este escenario solo es pertinente si la aplicación de servicio utiliza la autenticación de clave simétrica.

## <a name="scenario"></a>Escenario
La compañía *CoolApp* ha desarrollado una aplicación de servicio con Azure Information Protection (AIP) que cifra, etiqueta y protege los documentos cuando los usuarios los exportan de una aplicación empresarial, por ejemplo, Dynamics, SAP o Salesforce. En este escenario, una empresa más grande, *ABC*, adquiere la nueva aplicación de *CoolApp* por tanto el equipo de *CoolApp* necesita implementar su solución en el entorno de *ABC*. 

![Flujo de ejemplo para la creación de una clave simétrica en un inquilino diferente](../media/develop/service-app-provision.jpg)

## <a name="flow-1-coolapp-provides-a-ui-dialog-to-abc-to-implement-the-deployment"></a>Flujo 1: *CoolApp* proporciona un cuadro de diálogo de la interfaz de usuario para que *ABC* realice la implementación

Cuando *ABC* compra la solución de *CoolApp*, el administrador de TI de *ABC* debe crear la entidad de servicio de *CoolApp* y registrar la aplicación en el inquilino de Azure AD de *ABC*. 

Los pasos se describen en la sección **Creación de una entidad de servicio** en [Desarrollo de la aplicación](developing-your-application.md).

![Ejemplo de la interfaz de usuario para que el administrador de TI acceda en la aplicación](../media/develop/how-to-deploy-app-UI.png)

> [!Note]
> Para crear la entidad de servicio en un inquilino, necesita derechos de administrador de inquilinos

El administrador de TI de *ABC*, después inicia la aplicación de *CoolApp* como un servicio en su entorno e inserta los detalles de la aplicación *CoolApp* para que funcione como tal; identificador de aplicación, identificador de inquilino y clave simétrica.

Si la experiencia deseada no es ofrecer el administrador de TI de *ABC* con un cuadro de diálogo de interfaz de usuario para la información de la entidad de servicio, **Flujo 2** es el método que se debe seguir.

## <a name="flow-2-abc-it-administrator-provides-the-key-to-the-coolapp-team"></a>Flujo de 2: el administrador de TI de *ABC* proporciona la clave para el equipo de *CoolApp*

Una vez que el administrador de TI de *ABC* crea la entidad de servicio, como se muestra en la **figura 1**, *ABC* proporciona la información al equipo de *CoolApp*. El equipo de *CoolApp* continúa insertando la información en la aplicación de *CoolApp* para su uso en el inquilino de *ABC*.
