---
title: Configuración de la aplicación para autenticación ADAL - AIP
description: Pasos para configurar la aplicación Azure Information Protection para usar la autenticación basada en Azure ADAL
keywords: autenticación, RMS, ADAL, Information Protection,
author: bryanla
ms.author: bryanla
manager: mbaldwin
ms.date: 03/13/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: f89f59b7-33d1-4ab3-bb64-1e9bda269935
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: dd988c808de661b025d23e5fe73fb9f453fced10
ms.sourcegitcommit: bd2b31dd97c8ae08c28b0f5688517110a726e3a1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2019
ms.locfileid: "54070645"
---
# <a name="configure-your-app-for-adal-authentication"></a>Configuración de la aplicación para autenticación ADAL

En este tema se describen los pasos para configurar la aplicación para autenticación basada en la Biblioteca de autenticación de Azure Active Directory (ADAL).

## <a name="azure-authentication-setup"></a>Configuración de la autenticación de Azure

Necesitará lo siguiente:

- Una [suscripción de Microsoft Azure](https://azure.microsoft.com/) (con una evaluación gratuita es suficiente). Para más información, vea [How users sign up for RMS for individuals](../rms-for-individuals-user-sign-up.md) (Cómo se registran los usuarios en RMS para particulares)
- Una suscripción de Microsoft Azure Rights Management (una cuenta gratuita de [RMS para usuarios](https://technet.microsoft.com/library/dn592127.aspx) es suficiente).

> [!NOTE]
> Pregúntele al administrador de TI si dispone de una suscripción a Microsoft Azure Rights Management y solicítele que realice los pasos siguientes. Si la organización no tiene una suscripción, pídale al administrador de TI que cree una. Además, el administrador de TI debe suscribirse con una *cuenta profesional o educativa*, en lugar de con una *cuenta de Microsoft* (es decir, Hotmail).

Después de suscribirse a Microsoft Azure:

- Inicie sesión en el [Portal de administración de Azure](https://manage.windowsazure.com) para la organización mediante una cuenta con privilegios administrativos.

![Inicio de sesión de Azure](../media/AzurePortalLogin.png)

- Desplácese hacia abajo hasta la aplicación de **Active Directory** en el lado izquierdo del portal.

![Seleccione Active Directory](../media/AzureADPick.png)

- Si todavía no ha creado un directorio, elija el botón **Nuevo** en la esquina inferior izquierda del portal.

![Seleccione NUEVO](../media/AzureNewBtn.png)

- Seleccione la pestaña **Rights Management** y asegúrese de que el **Estado de Rights Management** sea **Activo**, **Desconocido** o **No autorizado**. Si el estado es **Inactivo**, elija el botón **Activar** situado en la parte inferior central del portal y confirme la selección.

![Elija ACTIVAR](../media/RMTab.png)

- Ahora cree una *Aplicación nativa* en su directorio. Para ello, seleccione su directorio y elija Aplicaciones.

![Seleccione APLICACIONES](../media/CreateNativeApp.png)

- Después, elija el botón **Agregar** situado en la parte inferior central del portal.

![Seleccione AGREGAR](../media/AddAppBtn.png)

- En el símbolo del sistema, elija **Agregar una aplicación que mi organización está desarrollando**.

![Seleccione Agregar una aplicación que mi organización está desarrollando](../media/AddAnAppPick.png)

- Asígnele un nombre a la aplicación. Para ello, seleccione **APLICACIÓN DE CLIENTE NATIVO** y elija el botón **Siguiente**.

![Asígnele un nombre a la aplicación](../media/TellUsInput.png)

- Agregue un identificador URI de redireccionamiento y elija Siguiente.
  El identificador URI de redireccionamiento debe ser un identificador URI válido y único para su directorio. Por ejemplo, podría usar algo parecido a `https://contoso.azurewebsites.net/.auth/login/done`.

![Agregue un identificador URI de redireccionamiento](../media/RedirectURI.png)

- Seleccione la aplicación en el directorio y elija **CONFIGURAR**.

![Elija CONFIGURAR](../media/ConfigYourApp.png)

>[!NOTE]
> Copie el **ID. DE CLIENTE** y el **IDENTIFICADOR URI DE REDIRECCIONAMIENTO** y consérvelos para usarlos cuando configure el cliente de RMS.

- Vaya a la parte inferior de los ajustes de configuración de la aplicación y elija el botón **Agregar aplicación**, situado bajo **permisos para otras aplicaciones**.

>[!NOTE]
> Los **permisos delegados** que se muestran para Windows Azure Active Directory son correctos de forma predeterminada. Solo debe seleccionarse una opción, y dicha opción es **Iniciar sesión y leer el perfil del usuario**.

![Seleccione Agregar aplicación](../media/PermissionsToOtherBtn.png)

- Elija el botón de signo más situado junto a **Microsoft Rights Management**.

![Seleccione el botón +](../media/ChoosePlusBtn.png)

- Ahora, seleccione la marca de verificación que se encuentra en la esquina inferior izquierda del cuadro de diálogo.

![Seleccione la marca de verificación](../media/choosecheck01.png)

- Ahora ya puede agregar una dependencia a la aplicación para Azure RMS. Para agregar la dependencia, seleccione la nueva entrada **Microsoft Rights Management Services** situada bajo **permisos para otras aplicaciones** y elija la casilla **Create and access protected content for users** (Creación y acceso a contenido protegido para los usuarios) en el cuadro desplegable **Permisos delegados:**.

![Configuración de permisos](../media/AddDependency.png)

- Guarde la aplicación para conservar los cambios. Para ello, elija el icono **Guardar** ubicado en la parte inferior central del portal.

![Seleccione GUARDAR](../media/SaveApplication.png)

