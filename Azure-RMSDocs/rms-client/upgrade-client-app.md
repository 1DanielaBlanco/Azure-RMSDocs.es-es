---
title: "Tareas que solía hacer con la aplicación RMS sharing - AIP"
description: "Instrucciones para los usuarios que han actualizado de la aplicación RMS sharing al cliente de Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/15/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d7bc2478-c22f-4e19-9992-012658362b25
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: f3384e7cd049120b76a408cb761a0bb5ad34bf8b
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2017
---
# <a name="tasks-that-you-used-to-do-with-the-rms-sharing-application"></a>Tareas que solía hacer con la aplicación RMS sharing

¿Recientemente ha hecho la actualización de la aplicación Rights Management sharing (conocida también como "aplicación RMS sharing") al cliente de Azure Information Protection? 

Use la siguiente información para ayudarlo a trabajar con rapidez.

|La aplicación RMS sharing|Cómo hacerlo con el cliente de Azure Information Protection
|-----------|--------------------|
|Protección de un archivo en un dispositivo <br /><br />También se conoce como "protección local".|Para aplicaciones de Office: seleccione una etiqueta que aplique la protección requerida o establezca permisos personalizados.<br /><br />Para otros archivos: utilice la opción de menú del Explorador de archivos, **Clasificar y proteger**, para abrir el cuadro de diálogo **Clasificar y proteger: Azure Information Protection**. A continuación, seleccione una etiqueta que aplique la protección requerida o especifique permisos personalizados propios. <br /><br />Para más información, vea [Clasificación y protección de un archivo o una dirección de correo electrónico](client-classify-protect.md).
|Proteger un archivo que comparte por correo electrónico <br /><br />También se conoce como "uso compartido seguro".|Si se comparte internamente: aplique una etiqueta con la protección requerida al documento o al mensaje de correo electrónico, o bien seleccione la opción de Outlook **No reenviar**. <br /><br /> Si se comparte externamente: con una copia del archivo, use permisos personalizados para proteger el archivo desde dentro de la aplicaicón de Office o mediante el Explorador de archivos. Después, comparta el archivo con el mecanismo estándar de uso compartido, como un archivo adjunto a un correo electrónico o una invitación a un documento de SharePoint Online. Considere incluir el vínculo https://aka.ms/rms-signup como instrucciones para el primer uso. <br /><br />Para más información sobre el uso compartido externo, vea la sección [Uso compartido de un archivo de manera segura con personas ajenas a la organización](client-classify-protect.md#safely-share-a-file-with-people-outside-your-organization) de la guía del usuario.
|Cambiar los permisos en archivos protegidos <br /><br />También se conoce como "Reproteger".|Para aplicaciones de Office que muestran la barra de Azure Information Protection: seleccione una etiqueta que aplica la protección necesaria.<br /><br />Para otros archivos, y si el cliente de Azure Information Protection se encuentra en [modo de solo protección](client-protection-only-mode.md): use la opción de menú del Explorador de archivos, **Clasificar y proteger**, para abrir el cuadro de diálogo **Clasificar y proteger: Azure Information Protection**. A continuación, seleccione una etiqueta que aplique la protección requerida o especifique permisos personalizados propios.<br /><br />Para más información, vea [Clasificación y protección de un archivo o una dirección de correo electrónico](client-classify-protect.md).
|Seguimiento y revocación de documentos|Para aplicaciones de Office: abra el documento y, después, en la pestaña **Inicio** > **Grupo de protección** > **Proteger** > **Realizar un seguimiento y revocar**.<br /><br />En el Explorador de archivos: haga clic con el botón derecho en un archivo o carpeta > **Clasificar y proteger**. Después, en el cuadro de diálogo **Clasificar y proteger: Azure Information Protection**, seleccione **Realizar un seguimiento y revocar**. <br /><br />Para obtener más información, vea [Realizar un seguimiento de los documentos y revocarlos](client-track-revoke.md).
|Ver y usar archivos protegidos|El visor de Azure Information Protection puede abrir archivos protegidos, para que pueda leerlos, así como imprimir y guardar estos archivos si tiene permisos para realizar estas acciones. Este visor se instala automáticamente con el cliente, o puede instalarlo por separado.<br /><br />Para más información, vea [Apertura de archivos que se han protegido](client-view-use-files.md).
|Quitar la protección de archivos|Utilice la opción de menú del Explorador de archivos, **Clasificar y proteger**, para abrir el cuadro de diálogo **Clasificar y proteger: Azure Information Protection**. <br /><br />A continuación, para un único archivo, desactive la opción **Protect with custom permissions** (Proteger con permisos personalizados). Para varios archivos o una carpeta, haga clic en **Remove custom permissions** (Quitar permisos personalizados).<br /><br />Para más información, vea [Quitar etiquetas y protección de archivos y correos electrónicos](client-remove-label-protection.md).|

## <a name="cant-find-the-option-youre-looking-for"></a>¿No encuentra la opción que busca?

Si busca una opción específica que suele seleccionar con la aplicación RMS sharing, consulte la tabla siguiente.

|Opción en la aplicación RMS sharing|Información de
|-----------|--------------------|
|**Uso compartido protegido**|Esta opción no está disponible en la cinta de Office. En lugar de compartir directamente desde la aplicación de Office, use la opción contextual del Explorador de archivos, **Clasificar y proteger**, para proteger una copia del documento con permisos personalizados y, luego, comparta el archivo con el cliente de correo electrónico de su elección o con el uso compartido de la ubicación. Considere incluir el vínculo https://aka.ms/rms-signup como instrucciones para el primer uso. <br /><br />Para más información sobre el uso compartido externo, vea la sección [Uso compartido de un archivo de manera segura con personas ajenas a la organización](#safely-share-a-file-with-people-outside-your-organization) de la guía del usuario.
|**Enviarme un correo electrónico cuando alguien trate de abrir estos documentos**|Use el sitio de Seguimiento de documentos para configurar los valores preferidos de notificaciones por correo electrónico: localice el documento protegido que ha compartido > **Configuración** > **Notificaciones por correo electrónico**.
|**Permitirme revocar el acceso a estos documentos de forma instantánea**|Este opción ya no está disponible. Configure plantillas que no permiten el acceso sin conexión. Además, considere si se debe reducir el período de validez de la licencia de uso para el inquilino; para ello, ejecute [Set-AadrmMaxUseLicenseValidityTime](/powershell/aadrm/vlatest/set-aadrmmaxuselicensevaliditytime).







[!INCLUDE[Commenting house rules](../includes/houserules.md)]  
