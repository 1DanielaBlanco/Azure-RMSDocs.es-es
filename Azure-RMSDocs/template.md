---
# required metadata

title: [TÍTULO DEL ARTÍCULO | NOMBRE DEL SERVICIO]
description:
keywords:
author: [GITHUB USERNAME]
manager: [ALIAS]
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: [GET ONE FROM guidgenerator.com]

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer: [ALIAS]
#ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Metadatos y plantilla Markdown

Esta plantilla docs.ms contiene ejemplos de sintaxis Markdown, así como instrucciones sobre cómo definir los metadatos. Está disponible en el directorio raíz de cada repositorio EM Pilot (por ejemplo, ~/Azure-RMSDocs-pr
/template.md) y está pensado para leerse como un archivo Markdown, aunque puede consultar [la versión publicada](https://stage.docs.microsoft.com/en-us/rights-management/template) para ver cómo se visualizan los ejemplos de Markdown.

Al crear un archivo Markdown, debe copiar la plantilla en un archivo nuevo, rellenar los metadatos como se indica aquí, definir el encabezado H1 encima del título del artículo y eliminar el contenido. 


## Metadatos 

El bloque de metadatos completo está arriba, dividido en campos obligatorios y campos opcionales. Consulte la [hoja de referencia de metadatos OPS](https://ppe.msdn.microsoft.com/en-us/ce-csi-docs/ops/ops-onboarding/managing-content/content-meta-data) para obtener más detalles. Algunas notas fundamentales:

- **Debe** existir un espacio entre los dos puntos (:) y el valor de un elemento de metadatos.
- Si un elemento de metadatos opcional no tiene un valor, comente el elemento con una almohadilla (#). No lo deje vacío ni use "na". Si va a agregar un valor a un elemento que tiene un comentario, procure quitar la almohadilla (#).
- Los dos puntos en un valor (por ejemplo, un título) interrumpen el analizador de metadatos. En su lugar, use la codificación HTML &#58; (por ejemplo, "title: Azure Rights Management&#58; conceptos básicos | Azure RMS").
- **title**: este título aparecerá en los resultados del motor de búsqueda. El título debe finalizar con un carácter de línea vertical (|) seguido del nombre del servicio (vea el ejemplo de arriba). No es necesario (de hecho, probablemente no sea obligatorio) que el título sea idéntico al título del encabezado H1. Debe tener aproximadamente 65 caracteres (incluyendo la parte | NOMBRE DEL SERVICIO).
- **author**, **manager**, **reviewer**: el campo author debe contener el **nombre de usuario de Github** del creador, no el alias.  Los campos "manager" y "reviewer", por su parte, deben contener alias. ms.reviewer especifica el nombre del PM asociado con el artículo o el servicio.
- **ms.assetid**: este es el GUID del artículo desde CAPS. Al crear un archivo Markdown, obtenga un GUID de [https://www.guidgenerator.com](https://www.guidgenerator.com). 
- **ms.prod**, **ms.service**, **ms.technology**, **ms.devlang**, **ms.topic**, **ms.tgt_pltfrm**: [aquí](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default) se pueden encontrar posibles valores para estos elementos.

## Markdown básico y GFM

Se admite todo el Markdown básico y Markdown de estilo Github (GFM). Para más información al respecto, vea:

- [Sintaxis de Markdown de línea base](https://daringfireball.net/projects/markdown/syntax)
- [Documentación de Markdown de estilo Github (GFM)](https://guides.github.com/features/mastering-markdown)

## Encabezados

Arriba encontrará ejemplos de títulos de primer y segundo nivel. 

Solo **debe** haber un encabezado de primer nivel en el tema, que se mostrará como el título de página.  

Los encabezados de segundo nivel generarán la tabla de contenido de la página que aparece en la sección "En este artículo" debajo del título de página.

### Encabezado de tercer nivel
#### Encabezado de cuarto nivel
##### Encabezado de quinto nivel
###### Encabezado de sexto nivel

## Estilo del texto

*Cursiva* 

**Negrita** 

~~Tachado~~



## Links

Para vincular a un archivo Markdown en el mismo repositorio, use [vínculos relativos](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2). 

- Ejemplo: [¿Qué es Azure Rights Management?](./understand-explore/what-is-azure-rms.md)

Para vincular a un encabezado en el mismo archivo Markdown, vea el origen del artículo publicado, busque el identificador del encabezado (por ejemplo, `id="blockquote"`) y vincule usando la estructura # + identificador (por ejemplo, `#blockquote`).

- Ejemplo: [Blockquotes](#blockquote)

Para vincular a un encabezado en un archivo Markdown en el mismo repositorio, use vinculación relativa + vinculación hashtag.

- Ejemplo: [información técnica del proceso de registro](./understand-explore/rms-for-individuals-user-sign-up.md#technical-overview-of-the-sign-up-process)

Para vincular a un archivo externo, use la dirección URL completa como vínculo.

- Ejemplo: [Github](http://www.github.com)

Si aparece una dirección URL en un archivo Markdown, se transformará en un vínculo interactivo.

- Ejemplo: http://www.github.com

## Listas

### Listas ordenadas

1. En esta 
1. Is
1. Un
1. Ordered
1. Lista  


#### Lista ordenada con una lista incrustada

1. Aquí
1. comes
1. an
1. embedded
    1. Miss Scarlett
    1. Professor Plum
1. ordered
1. list


### Listas desordenadas

- En esta
- es
- un
- bulleted
- list


##### Lista desordenada con una lista incrustada

- En esta 
- bulleted 
- list
    - Mrs. Peacock
    - Mr. Green
- contiene  
- otros
    1. Colonel Mustard
    1. Mrs. White
- lists


## Regla horizontal

---

## Tablas

| Tablas        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| col 1 is default | left-aligned     |    $1 |


## Código

### Bloque de código

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }

### Código en línea

Este es un ejemplo de `in-line code`.

## Blockquotes

> The drought had lasted now for ten million years, and the reign of the terrible lizards had long since ended. Here on the Equator, in the continent which would one day be known as Africa, the battle for existence had reached a new climax of ferocity, and the victor was not yet in sight. In this barren and desiccated land, only the small or the swift or the fierce could flourish, or even hope to survive.

## Imágenes

### Imagen estática

![this is the alt text](./media/AzRMS_elements.png)

### Imagen vinculada

[![alt text for linked image](./media/AzRMS_elements.png)](https://azure.microsoft.com) 

### Animated gif

![animated gif](./media/hololens.gif)

## Alertas

### Nota

> [!NOTE]
> This is NOTE

### Advertencia

> [!WARNING]
> This is WARNING

### Sugerencia

> [!TIP]
> This is TIP

### Importante

> [!IMPORTANT]
> This is IMPORTANT

## Vídeos

### Channel 9

<iframe src="http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>


### Youtube

<iframe width="420" height="315" src="https://www.youtube.com/embed/R6_eWWfNB54" frameborder="0" allowfullscreen></iframe>

## docs.ms extentions

### Botón

> [!div class="button"]
[button links](/rights-management)

### Selector

> [!div class="op_single_selector"]
- [foo](/rights-management/template.md)
- [bar](/rights-management/scratch.md)

### Step-By-Step

>[!div class="step-by-step"]
[Pre](https://www.example.com)
[Siguiente](https://www.example.com)

<!--HONumber=Apr16_HO3-->


