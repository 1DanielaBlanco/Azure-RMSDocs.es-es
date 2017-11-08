---
title: "Tareas que solía hacer con la aplicación RMS sharing - AIP"
description: "Instrucciones para los usuarios que han actualizado de la aplicación RMS sharing al cliente de Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d7bc2478-c22f-4e19-9992-012658362b25
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: dc0345ed289ecc95643c08ad86c1757848026826
ms.sourcegitcommit: 832d3ef5f9c41d6adb18a8cf5304f6048cc7252e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/24/2017
---
# <a name="user-guide-tasks-that-you-used-to-do-with-the-rms-sharing-application"></a>Guía del usuario: Tareas que solía hacer con la aplicación RMS sharing

¿Recientemente ha hecho la actualización de la aplicación Rights Management sharing (conocida también como "aplicación RMS sharing") al cliente de Azure Information Protection? 

Use la siguiente información para ayudarlo a trabajar con rapidez.

|La aplicación RMS sharing|Cómo hacerlo con el cliente de Azure Information Protection
|-----------|--------------------|
|Protección de un archivo en un dispositivo <br /><br />También se conoce como "protección local".|Para aplicaciones de Office: seleccione una etiqueta que aplique la protección requerida o establezca permisos personalizados.<br /><br />Para otros archivos: utilice la opción de menú del Explorador de archivos, **Clasificar y proteger**, para abrir el cuadro de diálogo **Clasificar y proteger: Azure Information Protection**. A continuación, seleccione una etiqueta que aplique la protección requerida o especifique permisos personalizados propios. <br /><br />Para más información, vea [Clasificación y protección de un archivo o una dirección de correo electrónico](client-classify-protect.md).
|Proteger un archivo que comparte por correo electrónico <br /><br />También se conoce como "uso compartido seguro".|En Outlook, aplique una etiqueta con la protección necesaria al mensaje de correo electrónico o seleccione la opción **No reenviar** de Outlook. Se protegerán automáticamente los datos adjuntos que tengan un [tipo de archivo compatible](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM).<br /><br />Nota: Para realizar el seguimiento de un documento protegido que envía por correo electrónico, protéjalo primero y, después, adjúntelo al mensaje de correo.<br /><br />Para más información, vea [Clasificación y protección de un archivo o una dirección de correo electrónico](client-classify-protect.md).
|Cambiar los permisos en archivos protegidos <br /><br />También se conoce como "Reproteger".|Para aplicaciones de Office que muestran la barra de Azure Information Protection: seleccione una etiqueta que aplica la protección necesaria.<br /><br />Para otros archivos, y si el cliente de Azure Information Protection se encuentra en [modo de solo protección](client-protection-only-mode.md): use la opción de menú del Explorador de archivos, **Clasificar y proteger**, para abrir el cuadro de diálogo **Clasificar y proteger: Azure Information Protection**. A continuación, seleccione una etiqueta que aplique la protección requerida o especifique permisos personalizados propios.<br /><br />Para más información, vea [Clasificación y protección de un archivo o una dirección de correo electrónico](client-classify-protect.md).
|Seguimiento y revocación de documentos|Para aplicaciones de Office: abra el documento y, después, en la pestaña **Inicio** > **Grupo de protección** > **Proteger** > **Realizar un seguimiento y revocar**.<br /><br />En el Explorador de archivos: haga clic con el botón derecho en un archivo o carpeta > **Clasificar y proteger**. Después, en el cuadro de diálogo **Clasificar y proteger: Azure Information Protection**, seleccione **Realizar un seguimiento y revocar**. <br /><br />Para obtener más información, vea [Realizar un seguimiento de los documentos y revocarlos](client-track-revoke.md).
|Ver y usar archivos protegidos|En el caso de los documentos de Office protegidos, debe tener instalado Office. El visor de Azure Information Protection puede abrir muchos otros archivos protegidos, para que pueda leerlos, imprimirlos y guardarlos si tiene permisos para realizar estas acciones. Este visor se instala automáticamente con el cliente, o puede instalarlo por separado.<br /><br />Para más información, vea [Apertura de archivos que se han protegido](client-view-use-files.md).
|Quitar la protección de archivos|Utilice la opción de menú del Explorador de archivos, **Clasificar y proteger**, para abrir el cuadro de diálogo **Clasificar y proteger: Azure Information Protection**. <br /><br />A continuación, para un único archivo, desactive la opción **Protect with custom permissions** (Proteger con permisos personalizados). Para varios archivos o una carpeta, haga clic en **Remove custom permissions** (Quitar permisos personalizados).<br /><br />Para más información, vea [Quitar etiquetas y protección de archivos y correos electrónicos](client-remove-label-protection.md).|

## <a name="cant-find-the-option-youre-looking-for"></a>¿No encuentra la opción que busca?

Si busca una opción específica que suele seleccionar con la aplicación RMS sharing, consulte la tabla siguiente.

|Opción en la aplicación RMS sharing|Información de
|-----------|--------------------|
|**Uso compartido protegido**|Esta opción no está disponible en la cinta de Office. En lugar de compartir directamente desde la aplicación de Office, use la opción contextual del Explorador de archivos, **Clasificar y proteger**, para proteger una copia del documento con permisos personalizados y, luego, comparta el archivo con el cliente de correo electrónico de su elección o con el uso compartido de la ubicación. <br /><br /> También puede adjuntar un documento desprotegido a un correo electrónico que vaya a proteger y el documento se protegerá automáticamente con las mismas restricciones. Sin embargo, no se puede realizar un seguimiento de este documento y revocarlo.
|**Enviarme un correo electrónico cuando alguien trate de abrir estos documentos**|Use el sitio de Seguimiento de documentos para configurar los valores preferidos de notificaciones por correo electrónico: localice el documento protegido que ha compartido > **Configuración** > **Notificaciones por correo electrónico**.
|**Permitirme revocar el acceso a estos documentos de forma instantánea**|Esta opción ya no está disponible. Configure plantillas que no permiten el acceso sin conexión. Además, considere si se debe reducir el período de validez de la licencia de uso para el inquilino; para ello, ejecute [Set-AadrmMaxUseLicenseValidityTime](/powershell/aadrm/vlatest/set-aadrmmaxuselicensevaliditytime).







[!INCLUDE[Commenting house rules](../includes/houserules.md)]  
