---
title: Tareas que solía hacer con la aplicación RMS sharing - AIP
description: Instrucciones para los usuarios que han actualizado de la aplicación RMS sharing al cliente de Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/01/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: d7bc2478-c22f-4e19-9992-012658362b25
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 5d7ea7b1997615e3737bba7e906d7efad8bd3e06
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56257882"
---
# <a name="user-guide-tasks-that-you-used-to-do-with-the-rms-sharing-application"></a>Manual del usuario: Tareas que solía hacer con la aplicación RMS sharing

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2*

¿Recientemente ha hecho la actualización de la aplicación Rights Management sharing (conocida también como "aplicación RMS sharing") al cliente de Azure Information Protection? 

Use la siguiente información para ayudarlo a trabajar con rapidez.

|La aplicación RMS sharing|Cómo hacerlo con el cliente de Azure Information Protection
|-----------|--------------------|
|Protección de un archivo en un dispositivo <br /><br />También se conoce como "protección local".|Para aplicaciones de Office: seleccione una etiqueta que aplique la protección necesaria o establezca permisos personalizados.<br /><br />Para otros archivos: Utilice la opción de menú del Explorador de archivos, **Clasificar y proteger**, para abrir el cuadro de diálogo **Clasificar y proteger: Azure Information Protection**. A continuación, seleccione una etiqueta que aplique la protección requerida o especifique permisos personalizados propios. <br /><br />Para más información, vea [Clasificación y protección de un archivo o una dirección de correo electrónico](client-classify-protect.md).
|Proteger un archivo que se comparte por correo electrónico <br /><br />También se conoce como "uso compartido seguro".|En Outlook, aplique una etiqueta con la protección necesaria al mensaje de correo electrónico o seleccione la opción **No reenviar** de Outlook. Se protegerán automáticamente los datos adjuntos que tengan un [tipo de archivo compatible](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM).<br /><br />Nota: Para realizar el seguimiento de un documento protegido que envía por correo electrónico, protéjalo primero y después adjúntelo al mensaje de correo.<br /><br />Para más información, vea [Clasificación y protección de un archivo o una dirección de correo electrónico](client-classify-protect.md).
|Cambiar los permisos en archivos protegidos <br /><br />También se conoce como "Reproteger".|Para aplicaciones de Office que muestran la barra de Azure Information Protection: seleccione una etiqueta que aplica la protección necesaria.<br /><br />Para otros archivos, y si el cliente de Azure Information Protection está en [modo de solo protección](client-protection-only-mode.md): Utilice la opción de menú del Explorador de archivos, **Clasificar y proteger**, para abrir el cuadro de diálogo **Clasificar y proteger: Azure Information Protection**. A continuación, seleccione una etiqueta que aplique la protección requerida o especifique permisos personalizados propios.<br /><br />Para más información, vea [Clasificación y protección de un archivo o una dirección de correo electrónico](client-classify-protect.md).
|Seguimiento y revocación de documentos|Desde Word, Excel y PowerPoint: abra el documento y después en la pestaña **Inicio** > **Grupo de protección** > **Proteger** > **Realizar un seguimiento y revocar**<br /><br />Desde el Explorador de archivos: Haga clic con el botón derecho en un archivo o carpeta > **Clasificar o proteger**. Después, en el cuadro de diálogo **Clasificar y proteger: Azure Information Protection**, seleccione **Realizar un seguimiento y revocar**. <br /><br />Al usar PowerShell desde la versión preliminar actual del cliente de Azure Information Protection: use el parámetro *EnableTracking* con el cmdlet [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel) a fin de registrar el documento etiquetado para su seguimiento.<br /><br />Para obtener más información, vea [Realizar un seguimiento de los documentos y revocarlos](client-track-revoke.md).
|Ver y usar archivos protegidos|En el caso de los documentos de Office protegidos, debe tener instalado Office. El visor de Azure Information Protection puede abrir muchos otros archivos protegidos, para que pueda leerlos, imprimirlos y guardarlos si tiene permisos para realizar estas acciones. Este visor se instala automáticamente con el cliente, o puede instalarlo por separado.<br /><br />Para más información, vea [Apertura de archivos que se han protegido](client-view-use-files.md).
|Quitar la protección de archivos|Utilice la opción de menú del Explorador de archivos, **Clasificar y proteger**, para abrir el cuadro de diálogo **Clasificar y proteger: Azure Information Protection**. <br /><br />A continuación, para un único archivo, desactive la opción **Protect with custom permissions** (Proteger con permisos personalizados). Para varios archivos o una carpeta, haga clic en **Remove custom permissions** (Quitar permisos personalizados).<br /><br />Para más información, vea [Quitar etiquetas y protección de archivos y correos electrónicos](client-remove-label-protection.md).|

## <a name="cant-find-the-option-youre-looking-for"></a>¿No encuentra la opción que busca?

Si busca una opción específica que suele seleccionar con la aplicación RMS sharing, consulte la tabla siguiente.

|Opción en la aplicación RMS sharing|Información de
|-----------|--------------------|
|**Uso compartido protegido**|Esta opción no está disponible en la cinta de Office. En lugar de compartir directamente desde la aplicación de Office, use la opción contextual del Explorador de archivos, **Clasificar y proteger**, para proteger una copia del documento con permisos personalizados y, luego, comparta el archivo con el cliente de correo electrónico de su elección o con el uso compartido de la ubicación. <br /><br /> También puede adjuntar un documento de Office desprotegido a un correo electrónico que vaya a proteger y el documento se protegerá automáticamente con las mismas restricciones. Sin embargo, no se puede realizar un seguimiento de este documento y revocarlo.
|**Enviarme un correo electrónico cuando alguien trate de abrir estos documentos**|Use el sitio de seguimiento de documentos para establecer la configuración de notificaciones de correo electrónico preferida: Busque el documento protegido que se ha compartido > **Configuración** > **Notificaciones por correo electrónico**
|**Permitirme revocar el acceso a estos documentos de forma instantánea**|Este opción ya no está disponible. Use la configuración de protección definida por el administrador que no permite el acceso sin conexión. Además, un administrador puede reducir el período de validez de la licencia de uso para el inquilino ejecutando [Set-AadrmMaxUseLicenseValidityTime](/powershell/aadrm/vlatest/set-aadrmmaxuselicensevaliditytime).
|**Seguimiento de uso** en Outlook|La funcionalidad de tener acceso al sitio de seguimiento de documentos de Outlook ya no está disponible. En su lugar, use la opción **Seguimiento y revocación** desde el Explorador de archivos, Excel, PowerPoint o Word. O bien, mediante un explorador, puede ir directamente al [sitio de seguimiento de documentos](https://go.microsoft.com/fwlink/?LinkId=529562).

## <a name="next-steps"></a>Pasos siguientes
Puede encontrar más instrucciones sobre procedimientos en la guía del usuario de Azure Information Protection:

- [¿Qué desea hacer?](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Información adicional para los administradores    
Vea la [Guía de administrador de cliente de Azure Information Protection](client-admin-guide.md).

  
