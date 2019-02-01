---
title: 'Guía de inicio rápido: Configuración de una etiqueta para usuarios para proteger fácilmente los correos electrónicos que contienen información confidencial (AIP)'
description: Configure una etiqueta que protege un correo electrónico para un usuario aplicando automáticamente la protección No reenviar.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2019
ms.topic: quickstart
ms.service: information-protection
ms.openlocfilehash: 6b892b1c845ea7d2e8670f054e0166eb160f3294
ms.sourcegitcommit: 9a9c55c96a7e99bcca742e759a3f08507e3b9801
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/29/2019
ms.locfileid: "55231011"
---
# <a name="quickstart-configure-a-label-for-users-to-easily-protect-emails-that-contain-sensitive-information"></a>Inicio rápido: Configuración de una etiqueta para usuarios para proteger fácilmente los correos electrónicos que contienen información confidencial

En este inicio rápido, configurará una etiqueta existente para aplicar automáticamente la configuración de protección No reenviar.

La directiva de Azure Information Protection actual ya contiene dos etiquetas que tienen esta configuración:

- **Confidencial \ Solo destinatarios**

- **Extremadamente confidencial \ Solo destinatarios**

Sin embargo, si su directiva es anterior o si la protección no estaba activada en el momento en que se creó la directiva de su organización, no tendrá estas etiquetas. 

Puede finalizar esta configuración en 5 minutos.

## <a name="prerequisites"></a>Requisitos previos

Para completar este tutorial rápido, necesitará:

1. Una suscripción que incluya el plan 1 o el plan 2 de Azure Information Protection.
    
    Si no tiene una de estas suscripciones, puede crear una cuenta [gratuita](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) para su organización.

2. Ha agregado la hoja Azure Information Protection a Azure Portal y ha confirmado que el servicio de protección está activado.

    Si necesita ayuda con estas acciones, consulte [Quickstart: Introducción a Azure Portal](quickstart-viewpolicy.md).

3. Una etiqueta existente de Azure Information Protection para configurar. 
    
    Puede usar una de las etiquetas predeterminadas o bien una etiqueta que haya creado. Si necesita ayuda para crear una nueva etiqueta, consulte [Inicio rápido: Creación de una nueva etiqueta de Azure Information Protection para usuarios específicos](quickstart-label-specificusers.md).

4. Para probar la nueva etiqueta: el cliente de Azure Information Protection debe estar instalado en equipos para los usuarios. 
    
    Para probar la etiqueta por usted mismo, instale el cliente visitando el [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) y descargando **AzInfoProtection.exe** desde la página de Azure Information Protection.

5. Para probar la nueva etiqueta: Un equipo con Windows (como mínimo Windows 7 con Service Pack 1) y, en este equipo, haber iniciado sesión en aplicaciones de Office desde una de las siguientes categorías:
    
    - Aplicaciones de Office, versión mínima 1805, compilación 9330.2078 de Office 365 Empresa o Microsoft 365 Empresa cuando se le asigna una licencia de Azure Rights Management (también conocido como Azure Information Protection para Office 365).
    
    - Office 365 ProPlus.
    
    - Office Professional Plus 2019.
    
    - Office Professional Plus 2016.
    
    - Office Professional Plus 2013 con Service Pack 1.
    
    - Office Professional Plus 2010 con Service Pack 2.

Para ver una lista completa de los requisitos previos para utilizar Azure Information Protection, consulte [Requisitos de Azure Information Protection](requirements.md).

## <a name="configure-an-existing-label-to-apply-the-do-not-forward-protection"></a>Configuración de una etiqueta existente para aplicar la protección No reenviar

1. Abra una nueva ventana del explorador e inicie sesión en [Azure Portal](https://portal.azure.com) como administrador global. Después, vaya a **Azure Information Protection**. 
    
    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.
    
    Si no es el administrador global, utilice el siguiente vínculo para roles alternativos: [Inicio de sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal)

2. Desde la opción de menú **Clasificaciones** > **Etiquetas**: en la hoja **Azure Information Protection: etiquetas**, seleccione la etiqueta que desea configurar para aplicar la protección. 

3. En la hoja **Etiqueta**, busque **Set permissions for documents and emails containing this label** (Establecer permisos para documentos y correos electrónicos que contengan esta etiqueta). Seleccione **Proteger** y, a continuación, **Protección**:
    
    ![Configurar la protección para una etiqueta de Azure Information Protection](./media/info-protect-protection-bar-configured.png).

4. En la hoja **Protección**, asegúrese de que **Azure (clave en la nube)** esté seleccionado.
    
5. Seleccione **Establecer permisos definidos por el usuario (versión preliminar)**.

6. Asegúrese de que la opción siguiente está seleccionada: **En Outlook, seleccione No reenviar**.

7. Si se selecciona, desactive la opción: **En Word, Excel, PowerPoint y el Explorador de archivos, solicite al usuario permisos personalizados**.

8. Haga clic en **Aceptar** en la hoja **Protección** y, a continuación, haga clic en **Guardar** en la hoja **Etiqueta**.

La etiqueta está configurada ahora para mostrarse solo en Outlook y aplicar la protección No reenviar a los correos electrónicos.

## <a name="test-your-new-label"></a>Prueba de la nueva etiqueta

La etiqueta configurada solo se muestra en Outlook y es adecuada para los correos electrónicos enviados a cualquier destinatario fuera de su organización cuando Exchange Online está configurado para las [nuevas capacidades de cifrado de mensajes de Office 365](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e).

1. En el equipo, abra Outlook y cree un nuevo mensaje de correo electrónico. Si Outlook ya está abierto, reinícielo para forzar una actualización de directiva.

2. Especifique los destinatarios y algún texto para el mensaje de correo electrónico y, a continuación, aplique la etiqueta que acaba de crear. 
    
    El mensaje de correo electrónico se clasifica de acuerdo con el nombre de la etiqueta y se protege con la restricción No reenviar.

3. Envíe el correo electrónico. 

En este caso, los destinatarios no podrán reenviar el correo electrónico, imprimirlo ni guardarlo con otro nombre, así como tampoco copiar contenido de este ni guardar los datos adjuntos. El mensaje de correo electrónico protegido se puede leer por cualquier usuario en cualquier dispositivo.

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no desea mantener esta configuración y prefiere devolver la etiqueta al estado previo en que no aplica la protección, haga lo siguiente:

1. Desde la opción de menú **Clasificaciones** > **Etiquetas**: en la hoja **Azure Information Protection: Etiquetas**, seleccione la etiqueta que configuró. 

3. En la hoja **Etiqueta**, busque **Establecer permisos para documentos y correos electrónicos que contengan esta etiqueta**, seleccione **No configurado** y, luego, **Guardar**.

## <a name="next-steps"></a>Pasos siguientes

Este inicio rápido incluye las opciones mínimas para configurar rápidamente una etiqueta que facilite a los usuarios la protección de sus correos electrónicos. Sin embargo, si la configuración es demasiado restrictiva o no es lo suficientemente restrictiva, debe ver otras configuraciones de ejemplo:

- [Etiqueta para correo electrónico protegido que admite permisos menos restrictivos que No reenviar](configure-policy-protection.md#example-4-label-for-protected-email-that-supports-less-restrictive-permissions-than-do-not-forward)

- [Etiqueta que cifra el contenido pero no limita el acceso a este](configure-policy-protection.md#example-5-label-that-encrypts-content-but-doesnt-restrict-who-can-access-it)

Para obtener todas las instrucciones acerca de cómo configurar una etiqueta que aplica la protección, consulte [Configuración de una etiqueta para la protección de Rights Management](configure-policy-protection.md). 
