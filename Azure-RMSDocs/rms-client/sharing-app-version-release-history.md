---
# required metadata

title: Aplicación Rights Management sharing&colon; Historial de publicación de versiones | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 6751bd90-959f-4eba-91ed-6588ac983762

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Aplicación de uso compartido Rights Management Historial de publicación de versiones

*Se aplica a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*

El equipo de Rights Management actualiza periódicamente la aplicación para uso compartido de Rights Management con correcciones y nuevas funcionalidades. Use la información siguiente para ver las novedades o los cambios de una versión. La versión más reciente aparece en primer lugar.

No se enumeran las versiones anteriores al 1 de enero de 2015.

> [!NOTE]
> Si tiene comentarios o alguna pregunta sobre la aplicación RMS sharing, envíe un mensaje de correo electrónico a [AskIPTeam](mailto:AskIPTeam@microsoft.com?subject=RMS%20sharing%20app:%20Feedback%20or%20question)..

## Versión 1.0.2004.0
**Lanzamiento**: 11/12/2015

**Correcciones**:

-   Solo el propietario del archivo y las personas con niveles de permisos de **Copropietario** pueden desproteger archivos. Anteriormente, el propietario y las personas con niveles de permisos de **Coautor** y **Copropietario** podían desproteger archivos.

-   Protección nativa para archivos **.tif** (además de archivos .tiff), para generar un archivo **.ptif** de solo lectura protegido por RMS.

-   Mejoras para los mensajes de error (precisión y claridad).

-   Mejoras de rendimiento para cifrar y descifrar el contenido.

**Nuevas características**:

-   Soporte para instalación por parte de usuarios que no sean administradores para que los usuarios estándar puedan instalar la aplicación de uso compartido RMS.

    Hay algunas restricciones para los usuarios estándar que ejecuten Office 2010. Para más información, consulte la sección [Si no es administrador local y usa Office 2010](install-sharing-app.md#if-you-are-not-a-local-administrator-and-use-office-2010) en las instrucciones para el usuario de [Descarga e instalación de la aplicación Rights Management sharing](install-sharing-app.md).

## Versión 1.0.1908.0
**Lanzamiento**: 16/09/2015

**Correcciones**:

-   Compatibilidad con Multi-Factor Authentication (MFA) para Azure RMS, que también elimina la dependencia del Ayudante para el inicio de sesión de Microsoft en aplicaciones que usan la autenticación moderna.

    Para obtener más información, consulte la sección [Multi-factor authentication (MFA) and Azure RMS](../get-started/requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-rms) (Multi-Factor Authentication [MFA] y Azure RMS) en [Requirements for Azure Rights Management](../get-started/requirements-azure-rms.md) (Requisitos de Azure Rights Management)..

## Versión 1.0.1784.0
**Lanzamiento**: 30/07/2015

**Correcciones**:

-   El intervalo de actualización predeterminado para las plantillas de directiva de derechos se reduce de 7 días a 1 día.

-   Número reducido de regresiones y errores menores.

## Versión 1.0.1770.0
**Lanzamiento**: 25/04/2015

**Correcciones**:

-   Ahora, solo los propietarios y los copropietarios pueden quitar la protección. Los coautores no pueden quitar la protección.

-   Ahora se pueden proteger los archivos que están en un recurso compartido de red.

**Nuevas características**:

-   Compatibilidad con la revocación y el seguimiento de documentos. Para obtener más información, consulte [Track and revoke your documents when you use the RMS sharing application](sharing-app-track-revoke.md) (Seguimiento y revocación de documentos cuando se usa la aplicación RMS sharing)..

-   Compatibilidad con plantillas al elegir **Uso compartido seguro**:

    -   ahora puede seleccionar plantillas.

    -   En lugar del control deslizante, verá un cuadro de lista que incluye las plantillas y los permisos personalizados.

    -   Ya no verá las opciones **Permitir consumo en todos los dispositivos** y **Aplicar restricciones de uso**. En su lugar, se activa automáticamente **Protección genérica** , en función del tipo de archivo.

    Para obtener más información, consulte [Dialog box options for the Rights Management sharing application](sharing-app-dialog-box.md) (Opciones de cuadro de diálogo para la aplicación Rights Management sharing)..

## Versión 1.0.1667.0
**Lanzamiento**: 19/01/2015

**Correcciones**:

-   Compatibilidad con fuentes del idioma chino en el visor de PPDF de la aplicación de uso compartido de RMS.

-   Control de errores y mensajería mejorados.

-   Corrección de un problema con la notificación de actualización automática cuando hay una versión más reciente de la aplicación disponible para descargar.

**Nuevas características**:

-   **Compatibilidad con varios dominios de correo electrónico dentro de su organización**: Si usa AD RMS y los usuarios de su organización tienen varios dominios de correo electrónico, esta actualización permite que los usuarios consuman contenido que protegieron los usuarios de la organización en otros dominios. Para obtener más información, consulte la sección [AD RMS only: Support for multiple email domains within your organization](sharing-app-admin-guide.md#ad-rms-only-support-for-multiple-email-domains-within-your-organization) (Solo AD RMS: Compatibilidad con varios dominios de correo electrónico dentro de su organización) de la [Rights Management sharing application administrator guide](sharing-app-admin-guide.md) (Guía de administrador de la aplicación Rights Management sharing)..



<!--HONumber=Apr16_HO4-->


