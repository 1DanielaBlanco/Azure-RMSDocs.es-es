---
title: 'Configuración de distintivos visuales para una etiqueta de Azure Information Protection: AIP'
description: Cuando se asigna una etiqueta a un documento o a un mensaje de correo electrónico, puede seleccionar varias opciones para hacer visible la clasificación elegida. Estos marcadores visuales son un encabezado, un pie de página y una marca de agua.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/13/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
ms.openlocfilehash: b0ff274917a78fa031dfe3e6f0665cef104111a9
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56258970"
---
# <a name="how-to-configure-a-label-for-visual-markings-for-azure-information-protection"></a>Configuración de una etiqueta para marcas visuales de Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Cuando se asigna una etiqueta a un documento o a un mensaje de correo electrónico, puede seleccionar varias opciones para hacer visible la clasificación elegida. Estos marcadores visuales son un encabezado, un pie de página y una marca de agua. 

Más información sobre los distintivos visuales:

- Los encabezados y pies de página se aplican a Word, Excel, PowerPoint y Outlook.

- Las marcas de agua se aplican a Word, Excel y PowerPoint:

    - Excel: Las marcas de agua son solo visibles en los modos Diseño de página y Vista previa de impresión y cuando se imprimen.
    
    - PowerPoint: Las marcas de agua se aplican a la diapositiva patrón, como una imagen de fondo. En la pestaña **Vista**, **Patrón de diapositivas**, asegúrese de que la casilla **Ocultar gráficos de fondo** no esté seleccionada.

- Para las marcas de agua y los encabezados y pies de página en Word, Excel y PowerPoint, se admiten varias líneas. Si especifica varias líneas para el encabezado o el pie de página de una etiqueta que se aplica en Outlook, se concatenan las líneas. En este escenario, considere el uso de la configuración para [establecer distintivos visuales diferentes para Word, Excel, PowerPoint y Outlook](##setting-different-visual-markings-for-word-excel-powerpoint-and-outlook).

- Longitudes máximas de cadena:
    
    - La longitud máxima de cadena que se puede especificar para los encabezados y pies de página es de 1024 caracteres, aunque Excel tiene un límite total de 255 caracteres para los encabezados y pies de página. Este límite incluye caracteres que no son visibles en Excel, por ejemplo, códigos de formato. Al especificar una cadena larga para encabezados y pies de página en Excel, este texto se puede truncar a 255 caracteres o menos.
    
    - La longitud máxima de cadena para marcas de agua que se puede especificar es de 255 caracteres.

- Puede especificar solo una cadena de texto o usar [variables](#using-variables-in-the-text-string) para crear dinámicamente la cadena de texto cuando se aplica el encabezado, el pie de página o la marca de agua.

- Word, PowerPoint, Outlook y ahora Excel admiten distintivos visuales de colores distintos.

- Los distintivos visuales admiten un solo idioma.

## <a name="when-visual-markings-are-applied"></a>Cuando se aplican distintivos visuales

En los mensajes de correo electrónico, los distintivos visuales se aplican cuando el mensaje de correo electrónico se envía desde Outlook.

Para los documentos, los distintivos visuales se aplican de la siguiente manera:

- En una aplicación de Office, los distintivos visuales de una etiqueta se aplican cuando la etiqueta se aplica. Los distintivos visuales también se aplican cuando se abre un documento etiquetado y el documento se guardó por primera vez.  

- Cuando un documento se etiqueta mediante el Explorador de archivos, PowerShell o el analizador de Azure Information Protection: no se aplican inmediatamente distintivos visuales, sino que el cliente de Azure Information Protection los aplica cuando ese documento se abre en una aplicación de Office y se guarda por primera vez.
    
    La excepción es cuando se usa [Autoguardado](https://support.office.com/article/what-is-autosave-6d6bd723-ebfd-4e40-b5f6-ae6e8088f7a5) con aplicaciones de Office para los archivos que se guardan en SharePoint Online, OneDrive o OneDrive para la Empresa: cuando está activado el Autoguardado, no se aplican distintivos visuales a menos que establezca la [configuración avanzada de cliente](./rms-client/client-admin-guide-customizations.md#turn-on-classification-to-run-continuously-in-the-background) de manera que la clasificación se ejecute continuamente en segundo plano. 

## <a name="to-configure-visual-markings-for-a-label"></a>Para configurar distintivos visuales para una etiqueta

Utilice las siguientes instrucciones para configurar las marcas visuales para una etiqueta.

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e [inicie sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal). Después, vaya a la hoja **Azure Information Protection**. 
    
    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. Desde la opción de menú **Clasificaciones** > **Etiquetas**: en la hoja **Azure Information Protection: etiquetas**, seleccione la etiqueta que contiene los distintivos visuales que quiere agregar o cambiar.

3. En la hoja **Etiqueta** de la sección **Establecer un distintivo visual, como el encabezado o el pie de página**, configure las opciones de los distintivos visuales que quiera y, luego, haga clic en **Guardar**:
    
    - Para configurar un encabezado: en **Documents with this label have a header** (Los documentos con esta etiqueta tienen un encabezado), seleccione **On** (Activado) si quiere un encabezado y **Off** (Desactivado) si no. Si selecciona **Activado**, especifique el texto, el tamaño, la [fuente](#setting-the-font-name), el [color](#setting-the-font-color) y la alineación del encabezado.
    
    - Para configurar un pie de página: en **Documents with this label have a footer** (Los documentos con esta etiqueta tienen un pie de página), seleccione **On** (Activado) si quiere un pie de página y **Off** (Desactivado) si no. Si selecciona **Activado**, especifique el texto, el tamaño, la [fuente](#setting-the-font-name), el [color](#setting-the-font-color) y la alineación del pie de página.
    
    - Para configurar una marca de agua: en **Documents with this label have a watermark** (Los documentos con esta etiqueta tienen una marca de agua), seleccione **On** (Activado) si quiere una marca de agua y **Off** (Desactivado) si no. Si selecciona **Activado**, especifique el texto, el tamaño, la [fuente](#setting-the-font-name), el [color](#setting-the-font-color) y la alineación de la marca de agua.
    
Al hacer clic en **Guardar**, los cambios están disponibles para los usuarios y servicios. Ya no hay una opción de publicación separada.


## <a name="using-variables-in-the-text-string"></a>Uso de variables en la cadena de texto

Puede usar las siguientes variables en la cadena de texto del encabezado, del pie de página o de la marca de agua:

- `${Item.Label}` para la etiqueta seleccionada. Por ejemplo: General

- `${Item.Name}` para el nombre de archivo o el asunto de correo electrónico. Por ejemplo: JulySales.docx

- `${Item.Location}` para la ruta de acceso y el nombre de archivo de documentos, así como el asunto de los correos electrónicos. Por ejemplo: \\\Ventas\2016\T3\InformeJulio.docx

- `${User.Name}` para el propietario del documento o correo electrónico, por el nombre de usuario que haya iniciado sesión en Windows. Por ejemplo: rsimone

- `${User.PrincipalName}` para el propietario del documento o correo electrónico, por la dirección de correo electrónico (UPN) que haya iniciado sesión en el cliente de Azure Information Protection. Por ejemplo: rsimone@vanarsdelltd.com

- `${Event.DateTime}` para la fecha y hora en que se haya configurado la etiqueta seleccionada. Por ejemplo: 8/16/2016 1:30 PM

Ejemplo: Si especifica la cadena `Document: ${item.name}  Classification: ${item.label}` en el pie de página de la etiqueta **General**, el texto de pie de página aplicado a un documento denominado proyecto.docx será **Documento: proyecto.docx Clasificación: general**.

>[!TIP]
> También usa un [código de campo para insertar el nombre de etiqueta](faqs-infoprotect.md#can-i-create-a-document-template-that-automatically-includes-the-classification) en un documento o plantilla.

## <a name="setting-different-visual-markings-for-word-excel-powerpoint-and-outlook"></a>Establecimiento de distintivos visuales diferentes para Word, Excel, PowerPoint y Outlook

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

Calibri es la fuente predeterminada para el texto de encabezados, pies de página y marcas de agua. Si especifica un nombre de fuente alternativo, asegúrese de que esté disponible en los dispositivos cliente que vayan a aplicar los distintivos visuales. 

Si la fuente especificada no está disponible, el cliente vuelve a utilizar la fuente Calibri.

### <a name="setting-the-font-color"></a>Establecimiento del color de fuente

Puede elegir en la lista de colores disponibles o especificar un color personalizado al escribir un código hexadecimal triple para los componentes rojo, verde y azul (RGB) del color. Por ejemplo, **#DAA520**. 

Si necesita una referencia para estos códigos, [Colors by Name](https://msdn.microsoft.com/library/aa358802\(v=vs.85\).aspx) (Colores por nombre), en la documentación de MSDN, es un punto de partida útil. También encontrará estos códigos en muchas aplicaciones que permiten editar imágenes. Por ejemplo, Microsoft Paint permite elegir un color personalizado de una paleta y los valores RGB se muestran automáticamente, lo que permite copiarlos.

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).  

