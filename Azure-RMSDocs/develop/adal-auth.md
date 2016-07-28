---
title: "Configuración de Azure RMS para la autenticación ADAL | Azure RMS"
description: "Describe los pasos para configurar la autenticación basada en Azure ADAL"
keywords: "autenticación, RMS, ADAL"
author: bruceperlerms
manager: mbaldwin
ms.date: 06/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f89f59b7-33d1-4ab3-bb64-1e9bda269935
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 56d0538243af49580f24c701ad5097b30f3059b0
ms.openlocfilehash: 9b912a2a66838dc6e6a3b227bcfe4ac589fe06c1


---

# Configuración de Azure RMS para la autenticación ADAL

En este tema se describe cómo configurar la autenticación basada en Azure ADAL.

## Configuración de la autenticación de Azure

Necesitará lo siguiente:

- Una [suscripción de Microsoft Azure](https://azure.microsoft.com/en-us/) (con una evaluación gratuita es suficiente). Para obtener más información, vea [How users sign up for RMS for individuals](../understand-explore/rms-for-individuals-user-sign-up.md) (Cómo registrarse para RMS para usuarios)
- Una suscripción de Microsoft Azure Rights Management (una cuenta gratuita de [RMS para usuarios](https://technet.microsoft.com/en-us/library/dn592127.aspx) es suficiente).

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
  El identificador URI de redireccionamiento debe ser un identificador URI válido y único para su directorio. Por ejemplo, podría usar algo parecido a `com.mycompany.myapplication://authorize`.

![Agregue un identificador URI de redireccionamiento](../media/RedirectURI.png)

- Seleccione la aplicación en el directorio y elija **CONFIGURAR**.

![Elija CONFIGURAR](../media/ConfigYourApp.png)

>[!NOTE] 
> Copie el **ID. DE CLIENTE** y el **IDENTIFICADOR URI DE REDIRECCIONAMIENTO** y consérvelos para usarlos cuando configure el cliente de RMS.

- Vaya a la parte inferior de los ajustes de configuración de la aplicación y elija el botón **Agregar aplicación**, situado bajo **permisos para otras aplicaciones**.

>[!NOTE] 
> Los **permisos delegados** que se muestran para Windows Azure Active Directory son correctos de forma predeterminada. Solo debe seleccionarse una opción, y dicha opción es **Iniciar sesión y leer el perfil del usuario**.

![Seleccione Agregar aplicación](../media/PermissionsToOtherBtn.png)

- Ahora, agregue el GUID `00000012-0000-0000-c000-000000000000` al cuadro de edición **EMPEZANDO POR** y elija el botón de comprobación.

![Agregue el GUID](../media/AddGUID.png)

- Elija el botón de signo más situado junto a **Microsoft Rights Management**.

![Seleccione el botón +](../media/ChoosePlusBtn.png)

- Ahora, seleccione la marca de verificación que se encuentra en la esquina inferior izquierda del cuadro de diálogo.

![Seleccione la marca de verificación](../media/ChooseCheck.png)

- Ahora ya puede agregar una dependencia a la aplicación para Azure RMS. Para agregar la dependencia, seleccione la nueva entrada **Microsoft Rights Management Services** situada bajo **permisos para otras aplicaciones** y elija la casilla **Create and access protected content for users** (Creación y acceso a contenido protegido para los usuarios) en el cuadro desplegable **Permisos delegados:**.

![Configuración de permisos](../media/AddDependency.png)

- Guarde la aplicación para conservar los cambios. Para ello, elija el icono **Guardar** ubicado en la parte inferior central del portal.

![Seleccione GUARDAR](../media/SaveApplication.png)



<!--HONumber=Jul16_HO3-->


