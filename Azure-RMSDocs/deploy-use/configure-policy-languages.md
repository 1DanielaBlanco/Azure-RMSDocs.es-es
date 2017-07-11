---
title: "Configuración de etiquetas para distintos idiomas en Azure Information Protection"
description: Para agregar compatibilidad con distintos idiomas a las etiquetas que los usuarios ven en la barra de Information Protection, especifique los idiomas en la directiva de Azure Information Protection e importe las traducciones.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/05/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a0e89fd0-795b-4e7a-aea9-ff6fc9163bde
ms.openlocfilehash: ec99bf36e8904a7304a9d33c32d17ba92e2e22d2
ms.sourcegitcommit: 8b768e7e249e124f24acdf630d165eaf743f9c21
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/05/2017
---
<a id="how-to-configure-labels-for-different-languages-in-azure-information-protection" class="xliff"></a>

# Configuración de etiquetas para distintos idiomas en Azure Information Protection

>*Se aplica a: Azure Information Protection*

>[!NOTE]
>Esta característica se encuentra actualmente en versión preliminar para usarla en conjunto con la versión **preliminar** del cliente de Azure Information Protection que puede descargar en el [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

De manera predeterminada, los nombres y las descripciones de las etiquetas admiten que se muestre solo un idioma que se muestra a todos los usuarios de la organización. Para agregar compatibilidad con distintos idiomas, seleccione los idiomas que necesita, exporte los nombres y descripciones de etiquetas actuales a un archivo, edite el archivo para proporcionar las traducciones y, luego, importe el archivo de vuelta a la directiva de Azure Information Protection.

Seleccione los idiomas que coinciden con la configuración de idioma de los usuarios para Office y Windows. Estos nombres y descripciones de etiquetas se muestran entonces en la barra de Azure Information Protection en aplicaciones de Office y en el cuadro de diálogo **Classify and protection - Azure Information Protection** (Clasificación y protección: Azure Information Protection), respectivamente. Para más información sobre el idioma elegido, consulte la sección [Cómo el cliente de Azure Information Protection determina el idioma que se mostrará](#how-the-azure-information-protection-client-determines-the-language-to- display) que aparece en esta página. 

<a id="to-configure-labels-to-display-in-different-languages" class="xliff"></a>

## Para configurar etiquetas para mostrarlas en distintos idiomas

1. Si aún no lo ha hecho, abra una nueva ventana del explorador, inicie sesión en [Azure Portal](https://portal.azure.com) como administrador de seguridad o administrador global y, después, navegue hasta la hoja **Azure Information Protection**. 
    
    Por ejemplo, en el menú del centro, haga clic en **Más servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. En la hoja **Azure Information Protection** inicial, ubique **ADMINISTRAR** y, luego, seleccione **Languages (Preview)** (Idiomas [versión preliminar]).

3. En la hoja **Azure Information Protection - Languages (Preview)** (Azure Information Protection - Idiomas [versión preliminar]), para colocar el primer idioma que desea agregar, escriba el nombre en el cuadro de búsqueda o desplácese en la lista de idiomas disponibles. 

4. Seleccione el idioma y, luego, seleccione **Aceptar**.

5. En la hoja siguiente, verá que el idioma seleccionado se agregó a una lista:
    
    - Para agregar otro idioma, seleccione **Add a new language for translation** (Agregar un idioma nuevo para la traducción) y repita los pasos 3 y 4. 
        
        > [!NOTE]
        > Asegúrese de seleccionar los idiomas que los usuarios tienen para Office y Windows. En algunos casos, esto podría requerir dos selecciones distintas por equipo.
        
    - Si cambia de opinión sobre algún idioma que haya agregado, seleccione esa entrada en la lista y haga clic en **Quitar**.

6. Cuando aparezcan todos los idiomas que desea admitir, active la casilla junto a **LANGUAGE NAME** (Nombre del idioma) para seleccionar todas las entradas (también puede seleccionar entradas individuales) y, luego, haga clic en **Exportar** para guardar una copia local de los nombres y descripciones de las etiquetas existentes en un archivo. 
    
    El archivo descargado se llama **exported localization.zip** y se guarda en la carpeta de descargas local. Para acceder a él, también puede seleccionar este nombre de archivo en la barra de estado de Azure Portal.

7. Extraiga los archivos de **exported localization.zip** para así tener archivos .xml de cada idioma que seleccionó para descarga. 

8. Edite cada archivo .xml. En cada cadena, dentro de las etiquetas `<LocalizedText>`, proporcione las traducciones que desea para cada idioma elegido. 

9. Cuando haya editado cada archivo .xml, cree una nueva carpeta comprimida que contenga estos archivos. La carpeta comprimida puede tener cualquier nombre, pero debe tener la extensión .zip.

10. Vuelva a la hoja de Azure Portal y seleccione **Importar**. Observe que si esta opción está deshabilitada, primero debe desactivar la casilla de **LANGUAGE NAME** o las casillas de los idiomas seleccionados de manera individual.
    
    Cuando se completa la importación, los nombres y descripciones de etiquetas localizados se descargarán a los usuarios la próxima vez que publique la directiva de Azure Information Protection. Puede hacer clic en **Publicar** en la hoja **Directiva global** o **Directivas con ámbito**.

<a id="how-the-azure-information-protection-client-determines-the-language-to-display" class="xliff"></a>

## Cómo el cliente de Azure Information Protection determina el idioma que se mostrará

Cuando los usuarios descarga una directiva de Azure Information Protection que admite distintos idiomas, el idioma que ven los usuarios en los nombres e informaciones sobre herramientas de sus etiquetas lo determina la siguiente lógica:

**En el caso de las etiquetas e informaciones sobre herramientas que ven los usuarios en la barra de Azure Information Protection en las aplicaciones de Office:**

- Cuando existe una coincidencia directa con el idioma de la aplicación de Office, los nombres y las descripciones de etiquetas aparecen en ese idioma.

- Cuando no existe coincidencia con el idioma de la aplicación de Office, los nombres y descripciones de etiquetas aparecen en el idioma que especificó de manera predeterminada para todos los usuarios. Normalmente este idioma es el inglés, el idioma que se usa en la directiva predeterminada.

**En el caso de etiquetas e informaciones sobre herramientas que ven los usuarios cuando hacen clic con el botón derecho para clasificar y proteger archivos o carpetas:**

- Cuando existe una coincidencia directa con el idioma del sistema operativo, los nombres y descripciones de etiquetas aparecen en ese idioma.

- Cuando no existe coincidencia con el idioma del sistema operativo, los nombres y descripciones de etiquetas aparecen en el idioma que especificó de manera predeterminada para todos los usuarios. Normalmente este idioma es el inglés, el idioma que se usa en la directiva predeterminada.

<a id="when-localized-label-names-are-not-used" class="xliff"></a>

## Cuándo no se usan los nombres de etiquetas localizados

Los nombres de etiquetas (y subetiquetas) localizados no se usan en los escenarios siguientes. Para mantener la coherencia entre su inquilino, el idioma predeterminado siempre se usa para lo siguiente:

- Registros de uso de cliente

- PowerShell (salida de Get-AIPFileStatus)

- Metadatos de documentos y encabezados de correo electrónico


<a id="next-steps" class="xliff"></a>

## Pasos siguientes

Para más información sobre las opciones que puede cambiar para una etiqueta, así como otra configuración de la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


