---
title: "Clasificación y protección de archivos o correos electrónicos mediante Azure Information Protection | Azure Information Protection"
description: "Instrucciones de cómo clasificar y proteger sus documentos y correos electrónicos."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/05/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 75268245-6f14-4218-b904-202f63fb3ce6
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 171a47f9c22dec24f72f8f21392d6577efd807a5
ms.openlocfilehash: d050629999c3a886eb8d422f4f38c22d586e0824


---

# <a name="classify-and-protect-a-file-or-email-by-using-azure-information-protection"></a>Clasificación y protección de archivos o correos electrónicos mediante Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8 y Windows 7 con SP1*

**[Esta versión del cliente está en versión preliminar y sujeta a cambios.]**

La manera más fácil de clasificar y proteger sus documentos y correos electrónicos es crearlos y editarlos con las aplicaciones de escritorio de Office: **Word**, **Excel**, **PowerPoint**, **Outlook**. 

Sin embargo, también puede clasificar y proteger archivos mediante el **Explorador de archivos**, que admite tipos de archivo adicionales y es una forma cómoda de clasificar y proteger varios archivos a la vez.

## <a name="using-office-apps-to-classify-and-protect-your-documents-and-emails"></a>Uso de aplicaciones de Office para clasificar y proteger los documentos y correos electrónicos

Use la barra de Azure Information Protection y seleccione una de las etiquetas configuradas para usted. Por ejemplo:

![Ejemplo de barra de Azure Information Protection](../media/info-protect-bar-not-set-callout.png)


## <a name="using-file-explorer-to-classify-and-protect-files"></a>Uso del Explorador de archivos para clasificar y proteger archivos

Con el Explorador de archivos, puede clasificar y proteger rápidamente un solo archivo, varios archivos o una carpeta. 

Cuando seleccione una carpeta, todos los archivos que contiene y sus subcarpetas se seleccionan automáticamente para las opciones de clasificación y protección establecidas. Sin embargo, los nuevos archivos que se crean en esa carpeta o en las subcarpetas no se configuran automáticamente con esas opciones.

Cuando utiliza el Explorador de archivos para clasificar y proteger los archivos, podría observar que las etiquetas no siempre están disponibles. Esto sucede cuando los archivos que selecciona no admiten la clasificación. Para estos archivos, solo puede seleccionar una etiqueta si el administrador la ha configurado para aplicar protección. O bien, puede especificar su propia configuración de protección. 

Para ver una lista de tipos de archivo admitidos por el Explorador de archivos, consulte la sección [Tipos de archivos admitidos para clasificación y protección](#file-types-supported-for-classification-and-protection) en esta página.


### <a name="to-classify-and-protect-a-file-by-using-file-explorer"></a>Para clasificar y proteger un archivo mediante el Explorador de archivos

1.  En el Explorador de archivos, seleccione un archivo, varios archivos o una carpeta. Haga clic con el botón derecho y seleccione **Classify and protect (preview)** (Clasificar y proteger [versión preliminar]). 

2. En el cuadro de diálogo **Classify and protect - Azure Information Protection** (Clasificar y proteger: Azure Information Protection), use las etiquetas del mismo modo que en una aplicación de Office, que establece la clasificación y protección definidas por el administrador. Si no se puede seleccionar una etiqueta (no se encuentra disponible), el archivo seleccionado no admite la clasificación, pero puede protegerlo.

3. Si desea especificar su propia configuración de protección en lugar de usar la configuración de protección que el administrador podría haber incluido con la etiqueta seleccionada, seleccione **Protect with custom permissions** (Proteger con permisos personalizados).
    
    Cualquier permiso personalizado que especifique reemplaza, en lugar de complementar, la configuración de protección que el administrador podría haber definido para la etiqueta elegida.  

4. Si ha seleccionado la opción de permisos personalizados, especifique ahora lo siguiente:

    - **Seleccionar permisos**: seleccione el nivel de acceso que quiere que tengan las personas al proteger los archivos seleccionados.
    
    - **Seleccionar usuarios**: especifique las personas que deben tener los permisos seleccionados para los archivos. En el caso de personas y grupos de su organización, puede usar la libreta de direcciones para buscarlos y seleccionarlos. Cuando las personas proceden de otra organización, debe especificar su dirección de correo electrónico completa. Asegúrese de usar una dirección de correo de empresa ya que las direcciones de correo electrónico personales no se admiten actualmente.
        
    - **Expire access on** (Fecha de expiración de acceso): seleccione esta opción solo para archivos dependientes del tiempo, de modo que las personas que ha especificado no puedan abrir los archivos seleccionados después de una fecha especificada. Aún podrá abrir el archivo original, pero después de medianoche (su zona horaria actual), el día seleccionado, las personas que haya especificado no podrán abrir el archivo.

5. Haga clic en **Aplicar** y luego en **Cerrar**.

Los archivos seleccionados están ahora clasificados y protegidos, de acuerdo con sus selecciones. En algunos casos (al agregar protección cambia la extensión de nombre de archivo), el archivo original del Explorador de archivos se reemplaza por un nuevo archivo que tiene el icono de bloqueo de Azure Information Protection. Por ejemplo:

![Archivo protegido con icono de bloqueo para Azure Information Protection](../media/Pfile.png)

Si cambia de opinión sobre la clasificación y la protección o más tarde necesita modificar la configuración, solo tiene que repetir este proceso con su nueva configuración.

La clasificación y la protección que especificó permanece con el archivo, incluso si lo envía por correo electrónico o lo guarda en otra ubicación. Si ha protegido el archivo, puede realizar un seguimiento de cómo las personas lo usan y, si es necesario, revocar el acceso a él. Para más información, consulte [Seguimiento y revocación de los documentos protegidos al usar Azure Information Protection](client-track-revoke.md). 

#### <a name="file-types-supported-for-classification-and-protection"></a>Tipos de archivo admitidos en la clasificación y la protección

Solo se admite la clasificación para los siguientes tipos de archivo. Otros tipos de archivo admiten la clasificación cuando también están protegidos.

- **Microsoft Visio**: .vsdx, .vsdm, .vssx, .vssm, .vsd, .vdw, .vst

- **Microsoft Project**: .mpp, .mpt

- **Microsoft Publisher**: .pub

- **Microsoft Office 97, Office 2010, Office 2003**: .xls, .xlt, .doc, .dot, .ppt, .pps, .pot

- **Microsoft XPS**: .xps .oxps

- **Imágenes**: .jpg, .jpe, .jpeg, .jif, .jfif,. jfi.png, .tif, .tiff

- **SolidWorks**: .sldprt, .slddrw, .sldasm

- **Autodesk Design Review 2013**: .dwfx

- **Adobe Photoshop**: .psd

- **Digital Negative**: .dng


La protección mediante el servicio Rights Management se admite para los tipos de archivo documentados en la [configuración de la API de archivo](../develop/file-api-configuration.md). Esta protección se puede aplicar automáticamente cuando se selecciona una etiqueta que el administrador ha configurado, o puede especificar su propia configuración de protección mediante [niveles de permiso](../deploy-use/configure-usage-rights.md#rights-included-in-permissions-levels). 


## <a name="other-instructions"></a>Otras instrucciones
Para obtener instrucciones sobre procedimientos, consulte las siguientes secciones de la guía de usuario de Azure Information Protection:

-   [¿Qué desea hacer?](client-user-guide.md#what-do-you-want-to-do)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



<!--HONumber=Jan17_HO4-->


