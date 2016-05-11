---
# required metadata

title: Tutorial de inicio rápido de Azure RMS - Paso 4 | Azure RMS
description: El cuarto paso de un tutorial para probar rápidamente Microsoft Azure Rights Management para su organización en solo 5 pasos que deberían tomarle menos de 15 minutos.
keywords:
author: Cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.assetid: f8340056-87a1-4daa-8b63-3d95fc381b9c

# optional metadata

ROBOTS: 
audience:
ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
ms.tgt_pltfrm:
ms.technology:
ms.custom:

---


# Inicio rápido de Azure RMS; paso 4: pedir a los destinatarios que abran el documento por correo electrónico

Saltar a: 
> [!div class="op_single_selector"]
- [Introducción](quick-start-tutorial.md)
- [Paso 1: Activación de Azure RMS](tutorial-step1.md)
- [Paso 2: Instalación de la aplicación RMS sharing](tutorial-step2.md)
- [Paso 3: Envío del documento confidencial por correo electrónico](tutorial-step3.md)
- [Paso 4: El destinatario lee el documento](tutorial-step4.md)
- [Paso 5: Seguimiento del documento](tutorial-step5.md)


![](../media/AzRMS_QuickStartSteps4.PNG)

Los destinatarios pueden usar muchos dispositivos para leer el documento protegido que envía como datos adjuntos por correo electrónico. Entre los dispositivos, se encuentran el iPad, el iPhone, tabletas y teléfonos Android, y equipos Mac, así como los equipos Windows.

Pídales que lean el mensaje de correo electrónico que ha enviado. Verán el mensaje de correo electrónico con el siguiente texto delante:

**El remitente ha protegido los datos adjuntos con Microsoft RMS. Debe** [iniciar sesión](http://aka.ms/rms)
      **para abrirlos.**

Cuando hacen clic en el vínculo, este los lleva a las instrucciones para instalar la aplicación de uso compartido RMS y, si es necesario, suscribirse a una cuenta gratuita. La cuenta gratuita les concede una suscripción de RMS para individuos, que garantiza que los usuarios autorizados siempre puedan leer un documento protegido, incluso si su organización no dispone de Azure RMS. A continuación, están preparados para leer los datos adjuntos protegidos siguiendo las instrucciones a continuación.

![](../media/AzRMS_Tutorial_4_Screenshots.png)

### Para ver los datos adjuntos del documento protegido

1.  Debido a que Azure Rights Management protegió un documento de Word, hay dos elementos adjuntos en el mensaje de correo electrónico. Estos son en realidad dos versiones del mismo archivo, pero con extensiones de nombre de archivo diferentes. Abra la versión que tiene la extensión de nombre de archivo **.ppdf** (**Confidential.ppdf**).

    Si tiene una versión de [Office en el dispositivo que admite Rights Management](https://technet.microsoft.com/library/dn655136.aspx), puede abrir la otra versión del archivo (**Confidential.docx**) para que se ejecute en Word.

2.  Si se le pide su nombre de usuario y contraseña, escriba su nombre de usuario en el mismo formato que la dirección de correo electrónico que se usó para enviarle el correo electrónico y los datos adjuntos. Por ejemplo, **janetm@contoso.com** o **p.dover@fabrikam.com**. Para la contraseña, escriba la contraseña que proporcionó al suscribirse a RMS para usuarios. O bien, si su organización tiene Azure RMS, debe escribir la contraseña de trabajo habitual.

En este momento, se abre el documento y puede leer el contenido. Por ejemplo, puede decir **Si puede leer esto en los datos adjuntos del correo electrónico, el remitente ha compartido correctamente un archivo protegido con Azure RMS.** Debido a que es de solo lectura, no puede cambiar el contenido.

Como paso opcional, puede pedir el destinatario que reenvíe el correo electrónico a otras personas que no incluyó en el correo electrónico original. Incluso si las otras personas trabajan para una organización como Azure Rights Management o solicitan su propia suscripción de RMS para usuarios, no podrán abrir el archivo adjunto. Cuando se les pide el nombre de usuario, se deniega el acceso al documento.

Ahora que el destinatario ha abierto el archivo adjunto y lo ha enviado de forma opcional a alguien más, espere la notificación por correo electrónico que informa de esta actividad. Sin embargo, los mensajes de correo electrónico son fáciles de perder con el tiempo, así que una mejor manera de realizar un seguimiento de quién tuvo acceso al documento es usar el sitio de seguimiento de documentos, que se explica en el paso final.

|Si desea obtener más información|Información adicional|
|--------------------------------|--------------------------|
|Instrucciones completas para ver archivos protegidos con Azure Rights Management|[Ver y usar archivos que han sido protegidos con Rights Management](../rms-client/sharing-app-view-use-files.md)|
|Acerca de la suscripción gratuita, RMS para usuarios|[RMS para usuarios y Azure Rights Management](../understand-explore/rms-for-individuals.md)|
|Acerca de las dos versiones del archivo que ve adjunto al mensaje de correo electrónico|[¿Qué es el archivo .ppdf que se crea automáticamente?](../rms-client/sharing-app-dialog-box.md#what-s-the-ppdf-file-that-s-automatically-created-)|


>[!div class="step-by-step"]
[« Paso 3](tutorial-step3.md)
[Paso 5 »](tutorial-step5.md)

<!--HONumber=Apr16_HO3-->


