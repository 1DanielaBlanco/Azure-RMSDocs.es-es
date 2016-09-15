---
title: "Aplicación Rights Management sharing&colon; Instalación y configuración para clientes | Azure RMS"
description: "Información para administradores sobre cómo implementar la aplicación Rights Management (RMS) sharing en dispositivos móviles y equipos con Windows."
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: b9af5dc3-73d4-4147-b7ef-f6803b0d5216
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ad32910b482ca9d92b4ac8f3f123eda195db29cd
ms.openlocfilehash: c73529b39f31fc6d819a3123bbdc2416f2d996f4


---

# Aplicación de uso compartido Rights Management Instalación y configuración para clientes

>*Se aplica a: Azure Rights Management, Office 365*

Es precisa la aplicación de uso compartido Rights Management (RMS) para equipos cliente que usen Azure RMS con Office 2010, y se es recomienda para todos los equipos y dispositivos móviles compatibles con Azure RMS. La aplicación de uso compartido RMS se integra con aplicaciones Office mediante la instalación de un complemento Office para que los usuarios puedan proteger fácilmente los archivos y correos electrónicos directamente desde la cinta. También ofrece protección genérica para tipos de archivo que no son compatibles de forma nativa con Azure RMS, y un sitio de seguimiento de documentos para que los usuarios controlen y revoquen los archivos que hayan protegido.

## La aplicación de uso compartido de RMS para Windows: Instalación y configuración
Para instalar y configurar la aplicación RMS sharing para Windows para una implementación empresarial, consulte la [guía del administrador de la aplicación Rights Management sharing](../rms-client/sharing-app-admin-guide.md).

> [!TIP]
> Si desea instalar y probar rápidamente la aplicación RMS sharing para un solo equipo, consulte [Download and install the Rights Management sharing application](../rms-client/install-sharing-app.md) (Descarga e instalación de la aplicación Rights Management sharing) en la [guía de usuario de la aplicación Rights Management sharing](../rms-client/sharing-app-user-guide.md).

## La aplicación RMS sharing para plataformas móviles: instalación y administración
Para instalar la aplicación de uso compartido de RMS en plataformas móviles, descargue la aplicación pertinente mediante los vínculos de la [página de Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970). No es necesaria ninguna configuración para usar Azure RMS con esta aplicación.

**Si tiene Microsoft Intune**: dado que la aplicación RMS sharing incluye el Kit de desarrollo de software para aplicaciones de Microsoft Intune, tiene las siguientes opciones:

-   Para los dispositivos que están inscritos por Intune, puede implementar y administrar la aplicación RMS sharing para dispositivos que ejecutan iOS y Android. Para más información, consulte [Configure and deploy mobile application management policies in the Microsoft Intune console](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console) (Configuración e implementación de directivas de administración de aplicaciones móviles en la consola de Microsoft Intune). Para el paso 2, siga las instrucciones para publicar una aplicación administrada por directivas.

-   En el caso de dispositivos que no están inscritos por Intune, puede administrar la aplicación RMS sharing para dispositivos que ejecuten Android. Para más información, consulte [Create and deploy mobile app management policies with Microsoft Intune](/intune/deploy-use/create-and-deploy-mobile-app-management-policies-with-microsoft-intune) (Creación e implementación de directivas de administración de aplicaciones móviles con Microsoft Intune).




<!--HONumber=Aug16_HO4-->


