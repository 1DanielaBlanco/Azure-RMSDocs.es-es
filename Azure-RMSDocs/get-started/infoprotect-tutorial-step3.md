---
title: "Paso 3 del tutorial de inicio rápido | Azure Information Protection"
description: "Paso 3 del tutorial introductorio para probar rápidamente Microsoft Azure Information Protection para su organización, que debería tardar unos 30 minutos."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 209815b9-81c9-430c-a82f-32cac991449b
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: ee60db5b9ede65042e9121567cce48e204f25d27


---

# <a name="step-3-install-the-client-and-application"></a>Paso 3: instalar el cliente y la aplicación 

>*Se aplica a: Azure Information Protection*

En este paso, instalará primero el cliente de Azure Information Protection de forma que la directiva que acaba de configurar se descargará en un equipo PC de Windows y mostrará las etiquetas de las aplicaciones de Office.

En segundo lugar, instalará la aplicación Rights Management sharing de forma que pueda compartir de manera segura un documento por correo electrónico y, después, realizar un seguimiento de cómo se usa. 

Ambas instalaciones se integran con aplicaciones de Office y, actualmente, debe instalarlas por separado.


## <a name="install-the-azure-information-protection-client"></a>Instalar el cliente de Azure Information Protection

1. En un equipo PC que tenga Office instalado (pero Word no esté abierto en estos momentos), [descargue el cliente de Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018) del Centro de descarga de Microsoft. 

2. Ejecute **AZInfoProtection.exe** y siga las indicaciones para instalar el cliente.

    Para este tutorial, no importa si selecciona la opción para instalar una directiva de demostración, porque nuestra directiva que acabamos de configurar se descargará de Azure y reemplazará la directiva de demostración si está instalada. Pero puede usar la opción de la directiva de demostración si solo quiere probar las etiquetas predeterminadas sin conectarse a Azure Information Protection. 

## <a name="install-the-rights-management-sharing-application"></a>Instalación de la aplicación de uso compartido Rights Management 

1. Vaya a la página de [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) en el sitio web de Microsoft.

2. En la sección **Equipos** , haga clic en el icono de la **Aplicación RMS para Windows** y guarde el archivo **Setup.exe** para instalar la aplicación de uso compartido Microsoft Rights Management.

3. En la página **Instalar Microsoft RMS** , haga clic en **Siguiente**y espere a que finalice la instalación. Después, haga clic en **Reiniciar** si se le pide que reinicie el equipo, o en **Cerrar** para completar la instalación.


## <a name="verify-the-installations"></a>Comprobar las instalaciones

Compruebe que estas instalaciones se han realizado correctamente al abrir Word y un nuevo documento en blanco (no lo guarde en este momento). Si se le solicita que escriba su nombre de usuario y contraseña, escriba los detalles de la cuenta de administrador global. 

Cuando se cargue el documento, debería ver tres cosas nuevas:

- En la pestaña **Inicio**, un nuevo grupo **Protección** con un botón denominado **Proteger**.

    Haga clic en **Proteger** > **Ayuda y comentarios** y, en el cuadro de diálogo **Microsoft Azure Information Protection**, confirme el estado del cliente. Debería mostrar **Information Protection policy is installed (la directiva de Information Protection se ha instalado)** y un tiempo de conexión reciente. Compruebe que el nombre de usuario que se muestra es correcto para su inquilino.

- En la pestaña **Inicio**, un nuevo grupo **RMS** con un botón denominado **uso compartido protegido**.

- Un nueva barra se muestra debajo de la cinta de opciones; la barra de Information Protection. Muestra el título de **Confidencialidad** y la etiqueta predeterminada que hemos configurado de **Interno**. 
    
    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection: se ha instalado el cliente](../media/word2013-callouts2.png)

Ahora está listo para ver Azure Information Protection en acción.

|Si desea obtener más información|Información adicional|
|--------------------------------|--------------------------|
|Sobre la instalación del cliente de Azure Information Protection|[Instalación del cliente de Azure Information Protection](../rms-client/info-protect-client.md)|
|Sobre la instalación de la aplicación Rights Management sharing y las instrucciones de usuario|[Guía de usuario de la aplicación Rights Management sharing](../rms-client/sharing-app-user-guide.md)|
|Acerca de la instalación con scripts de la aplicación de uso compartido Rights Management para Windows y más información técnica|[Guía del administrador de la aplicación Rights Management sharing](../rms-client/sharing-app-admin-guide.md)|


>[!div class="step-by-step"]
[&#171; Paso 2](infoprotect-tutorial-step2.md)
[Paso 4 &#187;](infoprotect-tutorial-step4.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


