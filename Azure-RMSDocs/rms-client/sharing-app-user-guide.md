---
# required metadata

title: Manual del usuario de la aplicación Rights Management sharing | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: eaf6d02c-aa36-4915-856e-49bb71ab1484

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Guía de usuario de la aplicación de uso compartido Rights Management

*Se aplica a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*

La aplicación Microsoft Rights Management (RMS) sharing de Windows le ayuda a mantener protegidos los documentos y las imágenes importantes de aquellas personas que no deben verlos, aunque los envíe por correo electrónico o los guarde en otro dispositivo. También puede usar esta aplicación para abrir y usar los archivos que otros usuarios han protegido con la misma tecnología de Rights Management.

Lo único que necesita es un equipo que ejecute al menos Windows 7 con Service Pack 1. A continuación, [descargue e instale](http://go.microsoft.com/fwlink/?LinkId=303970) esta aplicación gratuita de Microsoft.

Si tiene preguntas a las que no encuentra respuesta en esta guía, consulte [Preguntas más frecuentes sobre la aplicación Microsoft Rights Management sharing](http://go.microsoft.com/fwlink/?LinkId=303971). Si experimenta problemas, esta página también tiene cierta información sobre solución de problemas.

## Ejemplos de uso de la aplicación RMS sharing
Estos son solo algunos ejemplos de cómo puede usar la aplicación RMS sharing para ayudar a proteger sus archivos.

|Quiero ….|Cómo lo hago|
|----------------|------------------|
|**… compartir información financiera de forma segura con alguien en quien confío que trabaja para otra organización**<br /><br />Trabaja con una empresa asociada y desea enviarles por correo electrónico una hoja de cálculo de Excel que contiene las cifras de ventas proyectadas. Quiere que puedan ver las cifras pero no cambiarlas.|Use el botón **Uso compartido seguro** de la cinta de opciones de Excel, escriba las direcciones de correo electrónico de las dos personas de la compañía asociada con las que trabaja, seleccione **Visor - Solo ver**y haga clic en **Enviar**..<br /><br />Cuando llega el correo electrónico a la compañía asociada, solo los destinatarios del correo electrónico pueden ver la hoja de cálculo, pero no pueden guardarla, editarla, imprimirla ni reenviarla.<br /><br />Paso a paso: [Protección de un archivo que comparte por correo electrónico con la aplicación Rights Management sharing](sharing-app-protect-by-email.md)..|
|**… enviar un documento por correo electrónico de forma segura a alguien que usa un dispositivo iOS**<br /><br />Desea enviar por correo electrónico un documento de Word altamente confidencial a un compañero, que sabe que regularmente comprueba el correo electrónico en su dispositivo iOS.|En el Explorador de archivos, haga clic con el botón derecho en el archivo y seleccione **Uso compartido seguro** para enviar el archivo como adjunto a su compañero de trabajo.<br /><br />El destinatario recibe el correo electrónico en su dispositivo iOS. Como no tiene Office para iPad e iPhone, el destinatario recibe el correo electrónico en su dispositivo iOS, hace clic en el vínculo del correo que le indica cómo descargar la aplicación de uso compartido, instala la versión para dispositivos iOS y, luego, ve el documento¹.<br /><br />Paso a paso: [Protección de un archivo que comparte por correo electrónico con la aplicación Rights Management sharing](sharing-app-protect-by-email.md)..|
|**… comprobar quién ha abierto mis documentos protegidos y cuándo, y revocar el acceso si fuera necesario**<br /><br />Comparte de forma segura un documento de diseño confidencial con posibles proveedores y ahora desea ver quién accedió a él, cuándo y desde dónde. Luego, cuando a uno de los proveedores se le adjudica el negocio, quiere revocar el acceso al documento original para que las personas con las que lo compartió ya no puedan leerlo.|Después de compartir un documento por correo electrónico, vaya al [sitio de seguimiento de documentos](http://go.microsoft.com/fwlink/?LinkId=529562) para comprobar quién tiene acceso a ese documento y cuándo. Si necesita dejar de compartirlo, seleccione la opción para revocar el acceso.<br /><br />Paso a paso: [Seguimiento y revocación de documentos cuando se usa la aplicación RMS sharing](sharing-app-track-revoke.md)..|
|**… leer datos adjuntos que he recibido en un mensaje de correo electrónico con datos adjuntos de archivo compartidos de forma segura, pero no puedo leerlos porque mi compañía no usa Rights Management**<br /><br />El remitente del correo electrónico es alguien en quien confía porque ya ha hecho negocios con él en el pasado y sospecha que podría estar enviándole información sobre una posible nueva oportunidad de negocio.|Siga las instrucciones que se indican en el correo electrónico y haga clic en el vínculo para suscribirse a Microsoft Rights Management. Microsoft confirma que su organización no tiene una suscripción que incluye Azure Rights Management, le envía un correo electrónico para finalizar el proceso de suscripción gratuita y usted inicia sesión con la nueva cuenta. Haga clic en el segundo vínculo en el correo electrónico para instalar la aplicación Rights Management sharing y, luego, ya puede abrir los datos adjuntos de correo electrónico para obtener información sobre la nueva oportunidad de negocio.<br /><br />Paso a paso: [Visualización y uso de archivos protegidos por Rights Management](sharing-app-view-use-files.md)..|
|**… proteger archivos confidenciales de la compañía en mi equipo portátil para que no puedan acceder a ellos personas de fuera**<br /><br />Viaja mucho y usa su equipo portátil para obtener acceso a los archivos, que también actualiza, de una carpeta que debe protegerse contra el acceso no autorizado.|Tiene instalada la aplicación RMS sharing en su equipo portátil. Use el Explorador de archivos para proteger los archivos mediante una plantilla, que protege los archivos rápidamente. Si le roban su equipo portátil, tiene la tranquilidad de que nadie de fuera de su compañía puede tener acceso a estos documentos.<br /><br />Paso a paso: [Protección de un archivo en un dispositivo (proteger en contexto) mediante la aplicación Rights Management sharing](sharing-app-protect-in-place.md)..|
¹ Representación de PDF con tecnología Foxit. Copyright © 2003–2014 by Foxit Corporation.

## ¿Qué desea hacer?
> [!NOTE]
> Para obtener más información técnica, como los tipos de archivos compatibles y cómo instalar esta aplicación en una red de empresa, consulte la [Rights Management sharing application administrator guide](sharing-app-admin-guide.md) (Guía de administrador de la aplicación Rights Management sharing)..

-   [Descargar e instalar la aplicación RMS sharing](install-sharing-app.md)

-   [Proteger un archivo en un dispositivo (protección en contexto)](sharing-app-protect-in-place.md)

-   [Proteger un archivo que comparte por correo electrónico](sharing-app-protect-by-email.md)

-   [Realizar un seguimiento de los documentos y revocarlos](sharing-app-track-revoke.md)

-   [Ver y usar archivos protegidos](sharing-app-view-use-files.md)

-   [Quitar la protección de un archivo](sharing-app-remove-protection.md)

-   [Usar de métodos abreviados de teclado](sharing-app-keyboard-shortcuts.md)

-   [Especificar la configuración en el cuadro de diálogo](sharing-app-dialog-box.md)





<!--HONumber=Apr16_HO4-->


