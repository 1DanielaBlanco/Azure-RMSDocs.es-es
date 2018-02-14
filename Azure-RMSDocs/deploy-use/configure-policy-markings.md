---
title: "Configuración de marcas visuales para una etiqueta de Azure Information Protection"
description: "Cuando se asigna una etiqueta a un documento o a un mensaje de correo electrónico, puede seleccionar varias opciones para hacer visible la clasificación elegida. Estos marcadores visuales son un encabezado, un pie de página y una marca de agua."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/06/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
ms.openlocfilehash: 01208dda12b5989e546c1042b48c17e166d48687
ms.sourcegitcommit: d32d1f5afa5ee9501615a6ecc4af8a4cd4901eae
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="how-to-configure-a-label-for-visual-markings-for-azure-information-protection"></a>Configuración de una etiqueta para marcas visuales de Azure Information Protection

>*Se aplica a: Azure Information Protection*

Cuando se asigna una etiqueta a un documento o a un mensaje de correo electrónico, puede seleccionar varias opciones para hacer visible la clasificación elegida. Estos marcadores visuales son un encabezado, un pie de página y una marca de agua.

Más información sobre estos marcadores visuales:

- Los encabezados y pies de página se aplican a Word, Excel, PowerPoint y Outlook.

- Las marcas de agua se aplican a Word, Excel y PowerPoint:

    - Excel: las marcas de agua son solo visibles en los modos Diseño de página y Vista previa de impresión y cuando se imprimen.
    
    - PowerPoint: las marcas de agua se aplican a la diapositiva patrón, como una imagen de fondo.
    
    - Se admiten varias líneas de texto.

- Puede especificar solo una cadena de texto o usar [variables](#using-variables-in-the-text-string) para crear dinámicamente la cadena de texto cuando se aplica el encabezado, el pie de página o la marca de agua.

- Los marcadores visuales admiten un solo idioma.

## <a name="when-visual-markings-are-applied"></a>Cuando se aplican distintivos visuales

En los mensajes de correo electrónico, los distintivos visuales se aplican cuando el mensaje de correo electrónico se envía desde Outlook.

Para los documentos, los distintivos visuales se aplican de la siguiente manera:

- En una aplicación de Office, los distintivos visuales de una etiqueta se aplican cuando la etiqueta se aplica. Los distintivos visuales también se aplican cuando se abre un documento etiquetado y el documento se guardó por primera vez.  

- Cuando un documento se etiqueta mediante el Explorador de archivos o PowerShell, los distintivos visuales no se aplican inmediatamente, sino cuando ese documento se abre en una aplicación de Office y el documento se guardó por primera vez.

## <a name="to-configure-visual-markings-for-a-label"></a>Para configurar distintivos visuales para una etiqueta

Utilice las siguientes instrucciones para configurar las marcas visuales para una etiqueta.

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e inicie sesión en [Azure Portal](https://portal.azure.com) como administrador de seguridad o administrador global. Después, vaya a la hoja **Azure Information Protection**. 
    
    Por ejemplo, en el menú del centro, haga clic en **Más servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. Si la etiqueta que quiere configurar se va a aplicar a todos los usuarios, quédese en la hoja **Azure Information Protection - Global policy** (Azure Information Protection: directiva global).
    
    Si la etiqueta que quiere configurar se encuentra en una [directiva con ámbito](configure-policy-scope.md) para que se aplique únicamente a los usuarios seleccionados, en la selección del menú **DIRECTIVAS**, seleccione **Directivas con ámbito**. Después, seleccione la directiva con ámbito en la hoja **Azure Information Protection - Scoped policies** (Azure Information Protection: directivas con ámbito).

3. En la hoja **Etiqueta**, en la sección **Set visual marking (such as header or footer)** (Establecer marcas visuales [como encabezado y pie de página]), configure los marcadores visuales que quiera y luego haga clic en **Guardar**:
    
    - Para configurar un encabezado: en **Documents with this label have a header** (Los documentos con esta etiqueta tienen un encabezado), seleccione **On** (Activado) si quiere un encabezado y **Off** (Desactivado) si no. Si selecciona **Activado**, especifique el texto, el tamaño, la [fuente](#setting-the-font-name), el [color](#setting-the-font-color) y la alineación del encabezado.
    
    - Para configurar un pie de página: en **Documents with this label have a footer** (Los documentos con esta etiqueta tienen un pie de página), seleccione **On** (Activado) si quiere un pie de página y **Off** (Desactivado) si no. Si selecciona **Activado**, especifique el texto, el tamaño, la [fuente](#setting-the-font-name), el [color](#setting-the-font-color) y la alineación del pie de página.
    
    - Para configurar una marca de agua: en **Documents with this label have a watermark** (Los documentos con esta etiqueta tienen una marca de agua), seleccione **On** (Activado) si quiere una marca de agua y **Off** (Desactivado) si no. Si selecciona **Activado**, especifique el texto, el tamaño, la [fuente](#setting-the-font-name), el [color](#setting-the-font-color) y la alineación de la marca de agua.

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

## <a name="setting-different-visual-markings-for-word-excel-powerpoint-and-outlook"></a>Establecimiento de distintivos visuales diferentes para Word, Excel, PowerPoint y Outlook

Esta opción está actualmente en fase de versión preliminar y requiere la versión preliminar del cliente de Azure Information Protection.

De forma predeterminada, las marcas visuales que se especifican se aplican en Word, Excel, PowerPoint y Outlook. Sin embargo, es posible especificar marcas visuales por tipo de aplicación de Office si se usa una instrucción variable "If.App" en la cadena de texto y se identifica el tipo de aplicación mediante el uso de los valores **Word**, **Excel**, **PowerPoint** o **Outlook**. Estos valores también se pueden abreviar, algo que es necesario si se desea especificar más de uno en la misma instrucción If.App.

Use la siguiente sintaxis:

    ${If.App.<application type>}<your visual markings text> ${If.End}

En esta instrucción, esta sintaxis distingue mayúsculas de minúsculas.

Ejemplos:

- **Establecer el texto del encabezado solo para documentos de Word:**
    
    `${If.App.Word}This Word document is sensitive ${If.End}`
    
    Solo en los encabezados de los documentos de Word, la etiqueta aplica el texto del encabezado "This Word document is sensitive". En las restantes aplicaciones de Office no se aplica texto de encabezado.

- **Establecer el texto del pie de página para Word, Excel y Outlook y un texto de pie de página diferente para PowerPoint:**
    
    `${If.App.WXO}This content is confidential. ${If.End}${If.App.PowerPoint}This presentation is confidential. ${If.End}`
    
    En Word, Excel y Outlook, la etiqueta aplica el texto de pie de página "This content is confidential." En PowerPoint, la etiqueta aplica el texto de pie de página "This presentation is confidential."

- **Establecer el texto específico de marca de agua para Word y PowerPoint y, después, texto de marca de agua texto para Word, Excel y PowerPoint:**
    
    `${If.App.WP}This content is ${If.End}Confidential`
    
    En Word y PowerPoint, la etiqueta aplica el texto de marca de agua "This content is Confidential". En Excel, la etiqueta aplica el texto de marca de agua "Confidential". En Outlook, la etiqueta no aplica texto de marca de agua porque no se admiten distintivos visuales en Outlook.

### <a name="setting-the-font-name"></a>Establecimiento del nombre de fuente

Este valor está actualmente en versión preliminar.

Calibri es la fuente predeterminada para el texto de encabezados, pies de página y marcas de agua. Si especifica un nombre de fuente alternativo, asegúrese de que esté disponible en los dispositivos cliente que vayan a aplicar los marcadores visuales. En caso contrario, la fuente que se use será no determinista. 

Si tiene la versión preliminar del cliente de Azure Information Protection y la fuente especificada no está disponible, el cliente utiliza la fuente Calibri.

### <a name="setting-the-font-color"></a>Establecimiento del color de fuente

Puede elegir en la lista de colores disponibles o especificar un color personalizado al escribir un código hexadecimal triple para los componentes rojo, verde y azul (RGB) del color. Por ejemplo, **#DAA520**. 

Si necesita una referencia para estos códigos, [Colors by Name](https://msdn.microsoft.com/library/aa358802\(v=vs.85\).aspx) (Colores por nombre), en la documentación de MSDN, es un punto de partida útil. También encontrará estos códigos en muchas aplicaciones que permiten editar imágenes. Por ejemplo, Microsoft Paint permite elegir un color personalizado de una paleta y los valores RGB se muestran automáticamente, lo que permite copiarlos.

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
