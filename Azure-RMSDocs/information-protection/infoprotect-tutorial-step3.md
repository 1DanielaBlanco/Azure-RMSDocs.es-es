---
title: "Paso 3 del tutorial de inicio rápido de Azure Information Protection | Azure Rights Management"
description: "Paso 3 del tutorial introductorio para probar rápidamente Microsoft Azure Information Protection para su organización, que contiene solo 4 pasos que deberían tardar menos de 15 minutos."
author: cabailey
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 209815b9-81c9-430c-a82f-32cac991449b
translationtype: Human Translation
ms.sourcegitcommit: c9f9211e7c1dcf293caf81475515114b5433d6a7
ms.openlocfilehash: 320cd688ba5aabcb966009907d568033149953e3


---

# Paso 3: instalar el cliente de Azure Information Protection 

>*Se aplica a: Azure Information Protection (versión preliminar)*

**[Esta información es preliminar y está sujeta a cambios. ]**

En este paso, instalará el cliente de Azure Information Protection de forma que la directiva que acaba de configurar se descargará en un equipo PC de Windows y mostrará las etiquetas de las aplicaciones de Office. 

1. En un equipo PC que tenga Office instalado (pero Word no esté abierto en estos momentos), [descargue el cliente de Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018) del Centro de descarga de Microsoft. 

2. Ejecute **AZInfoProtection.exe** y siga las indicaciones para instalar el cliente.

    Para este tutorial, no importa si selecciona la opción para instalar una directiva de demostración, porque nuestra directiva que acabamos de configurar se descargará de Azure y reemplazará la directiva de demostración si está instalada. Pero puede usar la opción de la directiva de demostración si solo quiere probar las etiquetas predeterminadas sin conectarse a Azure Information Protection. 

3. Compruebe que el cliente se ha instalado al abrir Word y un nuevo documento en blanco (no lo guarde en este momento). Si se le solicita que escriba su nombre de usuario y contraseña, escriba los detalles de la cuenta de administrador global. Cuando se cargue el documento, debería ver dos cosas:

    - En la pestaña **Inicio**, un nuevo grupo **Protección** con un botón denominado **Proteger**.

        Haga clic en **Proteger** > **Ayuda y comentarios** y, en el cuadro de diálogo **Microsoft Azure Information Protection**, confirme el estado del cliente. Debería mostrar **Information Protection policy is installed (la directiva de Information Protection se ha instalado)** y un tiempo de conexión reciente. Compruebe que el nombre de usuario que se muestra es correcto para su inquilino.

    - Un nueva barra se muestra debajo de la cinta de opciones; la barra de Information Protection. Muestra el título de **Confidencialidad** y la etiqueta predeterminada que hemos configurado de **Interno**. 
    
        ![Paso 3 del tutorial de inicio rápido de Azure Information Protection: se ha instalado el cliente](../media/word2013-callouts2.png)

Está listo para el paso final para ver la clasificación, el etiquetado y la protección en funcionamiento.

|Si desea obtener más información|Información adicional|
|--------------------------------|--------------------------|
|Acerca de cómo instalar el cliente|[Instalación del cliente de Azure Information Protection](info-protect-client.md)|


>[!div class="step-by-step"]
[&#171; Paso 2](infoprotect-tutorial-step2.md)
[Paso 4 &#187;](infoprotect-tutorial-step4.md)


<!--HONumber=Aug16_HO4-->


