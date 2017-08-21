---
title: "Configuración de marcas visuales para una etiqueta de Azure Information Protection"
description: "Cuando se asigna una etiqueta a un documento o a un mensaje de correo electrónico, puede seleccionar varias opciones para hacer visible la clasificación elegida. Estos marcadores visuales son un encabezado, un pie de página y una marca de agua."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/16/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
ms.openlocfilehash: a65299651abd97adb0fc7641be2f2f3c6f1d8d2f
ms.sourcegitcommit: adb38b008656ac706920a8488fd2beafedadbc97
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2017
---
# <a name="how-to-configure-a-label-for-visual-markings-for-azure-information-protection"></a>Configuración de una etiqueta para marcas visuales de Azure Information Protection

>*Se aplica a: Azure Information Protection*

Cuando se asigna una etiqueta a un documento o a un mensaje de correo electrónico, puede seleccionar varias opciones para hacer visible la clasificación elegida. Estos marcadores visuales son un encabezado, un pie de página y una marca de agua.

Más información sobre estos marcadores visuales:

- Los encabezados y pies de página se aplican a Word, Excel, PowerPoint y Outlook.

- Las marcas de agua se aplican a Word, Excel y PowerPoint:

    - Excel: las marcas de agua son solo visibles en los modos Diseño de página y Vista previa de impresión y cuando se imprimen.
    
    - PowerPoint: las marcas de agua se aplican a la diapositiva patrón, como una imagen de fondo.
    
    - Se admiten varias líneas de texto cuando se usa la versión de vista previa actual del cliente de Azure Information Protection.

- Puede especificar solo una cadena de texto o usar [variables](#using-variables-in-the-text-string) para crear dinámicamente la cadena de texto cuando se aplica el encabezado, el pie de página o la marca de agua.

## <a name="when-visual-markings-are-applied"></a>Cuando se aplican distintivos visuales

En los mensajes de correo electrónico, los distintivos visuales se aplican cuando el mensaje de correo electrónico se envía desde Outlook.

Para los documentos, los distintivos visuales se aplican de la siguiente manera:

- **Para la versión de disponibilidad general** del cliente de Azure Information Protection: 
    
    - En una aplicación de Office, los distintivos visuales de una etiqueta se aplican cuando la etiqueta se aplica y siempre que se guarda el documento. 
    
    - Cuando un documento se etiqueta mediante el Explorador de archivos o PowerShell, los distintivos visuales no se aplican inmediatamente, sino cuando ese documento se abre en una aplicación de Office y cada vez que se guarda el documento.

- **Para la versión de vista previa actual** del cliente de Azure Information Protection: 
    
    - En una aplicación de Office, los distintivos visuales de una etiqueta se aplican cuando la etiqueta se aplica. Los distintivos visuales también se aplican cuando se abre un documento etiquetado y el documento se guardó por primera vez.  
    
    - Cuando un documento se etiqueta mediante el Explorador de archivos o PowerShell, los distintivos visuales no se aplican inmediatamente, sino cuando ese documento se abre en una aplicación de Office y el documento se guardó por primera vez.

## <a name="to-configure-visual-markings-for-a-label"></a>Para configurar distintivos visuales para una etiqueta

Utilice las siguientes instrucciones para configurar las marcas visuales para una etiqueta.

1. Si aún no lo ha hecho, abra una nueva ventana del explorador, inicie sesión en [Azure Portal](https://portal.azure.com) como administrador de seguridad o administrador global y, después, navegue hasta la hoja **Azure Information Protection**.

    Por ejemplo, en el menú del centro, haga clic en **Más servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. Si la etiqueta que quiere configurar para distintivos visuales se va a aplicar a todos los usuarios, seleccione la etiqueta que se va a modificar en la hoja **Policy: Global** (Directiva: Global).

     Si la etiqueta que quiere configurar está en una [directiva de ámbito](configure-policy-scope.md) de modo que se aplica solo a los usuarios seleccionados, seleccione primero esa directiva de ámbito en la hoja inicial de **Azure Information Protection**.

3. En la hoja **Etiqueta**, en la sección **Set visual marking (such as header or footer)** (Establecer marcas visuales [como encabezado y pie de página]), configure los marcadores visuales que quiera y luego haga clic en **Guardar**:

    - Para configurar un encabezado: en **Documents with this label have a header** (Los documentos con esta etiqueta tienen un encabezado), seleccione **On** (Activado) si quiere un encabezado y **Off** (Desactivado) si no. Si selecciona **On** (Desactivado), especifique el texto, el tamaño, el color y la alineación del encabezado.

    - Para configurar un pie de página: en **Documents with this label have a footer** (Los documentos con esta etiqueta tienen un pie de página), seleccione **On** (Activado) si quiere un pie de página y **Off** (Desactivado) si no. Si selecciona **On** (Activado), especifique el texto, el tamaño, el color y la alineación del pie de página del encabezado.

    - Para configurar una marca de agua: en **Documents with this label have a watermark** (Los documentos con esta etiqueta tienen una marca de agua), seleccione **On** (Activado) si quiere una marca de agua y **Off** (Desactivado) si no. Si selecciona **On** (Activado), especifique el texto, el tamaño, el color y el diseño de la marca de agua del encabezado.

4. Para que los cambios estén disponibles para los usuarios, en la hoja **Azure Information Protection**, haga clic en **Publicar**.

## <a name="using-variables-in-the-text-string"></a>Uso de variables en la cadena de texto

Puede usar las siguientes variables en la cadena de texto del encabezado, del pie de página o de la marca de agua:

- `${Item.Label}` para la etiqueta seleccionada. Por ejemplo: interno

- `${Item.Name}` para el nombre de archivo o el asunto de correo electrónico. Por ejemplo: VentasJulio.docx

- `${Item.Location}` para la ruta de acceso y el nombre de archivo de documentos, así como el asunto de los correos electrónicos. Por ejemplo: \\\Ventas\2016\T3\InformeJulio.docx

- `${User.Name}` para el propietario del documento o correo electrónico, por el nombre de usuario que haya iniciado sesión en Windows. Por ejemplo: rsimone

- `${User.PrincipalName}` para el propietario del documento o correo electrónico, por la dirección de correo electrónico (UPN) que haya iniciado sesión en el cliente de Azure Information Protection. Por ejemplo: rsimone@vanarsdelltd.com

- `${Event.DateTime}` para la fecha y hora en que se haya configurado la etiqueta seleccionada. Por ejemplo: 16/08/2016 13:30

Ejemplo: Si especifica la cadena `Document: ${item.name}  Classification: ${item.label}` en el pie de página de la etiqueta **General**, el texto de pie de página aplicado a un documento denominado proyecto.docx será **Documento: proyecto.docx Clasificación: general**.

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
