---
title: Configurar etiquetas y plantillas para distintos idiomas en Azure Information Protection
description: Para agregar compatibilidad con distintos idiomas a las etiquetas que los usuarios ven en la barra de Information Protection y a todas las plantillas que ven, especifique los idiomas en la directiva de Azure Information Protection e importe las traducciones.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/30/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a0e89fd0-795b-4e7a-aea9-ff6fc9163bde
ms.openlocfilehash: 4131e3afae338d906011a9fe02a941baa61cf892
ms.sourcegitcommit: 87d73477b7ae9134b5956d648c390d2027a82010
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32326810"
---
# <a name="how-to-configure-labels-and-templates-for-different-languages-in-azure-information-protection"></a>Cómo configurar etiquetas y plantillas para distintos idiomas en Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Aunque las etiquetas predeterminadas de Azure Information Protection admiten varios idiomas, debe configurar la compatibilidad con los nombres y descripciones de etiqueta que especifique. Para llevar a cabo esta configuración, debe hacer lo siguiente:

1. Seleccione los idiomas que usan los usuarios. 

2. Exporte los nombres y descripciones de etiqueta actuales a un archivo.

3. Edite el archivo para proporcionar las traducciones.

4. Importe el archivo a la directiva de Azure Information Protection.

También puede configurar plantillas para los distintos idiomas si se cumple alguna de las condiciones siguientes. Esta configuración es adecuada si los usuarios o los administradores necesitan ver el nombre y descripción de la plantilla actual en su idioma localizado.

- La plantilla se ha creado en el Portal de Azure clásico o con PowerShell y no está vinculada a una etiqueta mediante la configuración de protección **Seleccionar una plantilla predefinida**.

- No tiene una suscripción que admite etiquetas, por lo que solo puede crear y administrar plantillas en Azure Portal.

Seleccione los idiomas que coinciden con la configuración de idioma de los usuarios para Office y Windows. Estos nombres y descripciones de etiquetas se muestran entonces en la barra de Azure Information Protection en aplicaciones de Office y en el cuadro de diálogo **Classify and protection - Azure Information Protection** (Clasificación y protección: Azure Information Protection), respectivamente. Para más información sobre el idioma elegido, consulte la sección [Cómo el cliente de Azure Information Protection determina el idioma que se mostrará](#how-the-azure-information-protection-client-determines-the-language-to- display) que aparece en esta página. 

## <a name="to-configure-labels-and-templates-for-different-languages"></a>Para configurar etiquetas y plantillas para distintos idiomas

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e [inicie sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal). Después, vaya a la hoja **Azure Information Protection**.
    
    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. En la opción de menú **ADMINISTRAR** > **Idiomas**: en la hoja **Azure Information Protection: idiomas**, seleccione **Agregar un idioma nuevo para la traducción**. Seleccione los idiomas que quiera agregar y, después, seleccione **Aceptar**. Puede escribir el nombre del idioma en el cuadro de búsqueda o desplazarse por la lista de idiomas disponibles.

3. Los idiomas seleccionados se muestran ahora en la hoja **Azure Information Protection: idiomas**:
    
    - Para agregar otro idioma, seleccione **Agregar un idioma nuevo para la traducción** y repita el paso anterior. 
        
        > [!NOTE]
        > Asegúrese de seleccionar los idiomas que los usuarios tienen para Office y Windows. En algunos casos, esto podría requerir dos selecciones distintas por equipo.
        
    - Si cambia de opinión sobre algún idioma que haya agregado, seleccione esa entrada en la lista y haga clic en **Quitar**.

4. Cuando aparezcan todos los idiomas que desea admitir, active la casilla junto a **LANGUAGE NAME** (Nombre del idioma) para seleccionar todas las entradas (también puede seleccionar entradas individuales) y, luego, haga clic en **Exportar** para guardar una copia local de los nombres y descripciones de las etiquetas existentes en un archivo. 
    
    El archivo descargado se llama **exported localization.zip** y se guarda en la carpeta de descargas local. Para acceder a él, también puede seleccionar este nombre de archivo en la barra de estado de Azure Portal.

5. Extraiga los archivos de **exported localization.zip** para así tener archivos .xml de cada idioma que seleccionó para descarga. 

6. Edite cada archivo .xml. En cada cadena, dentro de las etiquetas `<LocalizedText>`, proporcione las traducciones que desea para cada idioma elegido. 

7. Cuando haya editado cada archivo .xml, cree una nueva carpeta comprimida que contenga estos archivos. La carpeta comprimida puede tener cualquier nombre, pero debe tener la extensión .zip.

8. Vuelva a la hoja **Azure Information Protection: idiomas** y seleccione **Importar**. Observe que si esta opción está deshabilitada, primero debe desactivar la casilla de **LANGUAGE NAME** o las casillas de los idiomas seleccionados de manera individual.
    
    Cuando haya completado la importación, los nombres traducidos y descripciones se descargan a los usuarios.

## <a name="how-the-azure-information-protection-client-determines-the-language-to-display"></a>Cómo el cliente de Azure Information Protection determina el idioma que se mostrará

Cuando los usuarios descarga una directiva de Azure Information Protection que admite distintos idiomas, el idioma que ven los usuarios en los nombres e informaciones sobre herramientas de sus etiquetas lo determina la siguiente lógica:

**En el caso de las etiquetas e informaciones sobre herramientas que ven los usuarios en la barra de Azure Information Protection en las aplicaciones de Office:**

- Cuando existe una coincidencia directa con el idioma de la aplicación de Office, los nombres y las descripciones de etiquetas aparecen en ese idioma.

- Cuando no existe coincidencia con el idioma de la aplicación de Office, los nombres y descripciones de etiquetas aparecen en el idioma que especificó de manera predeterminada para todos los usuarios. Normalmente este idioma es el inglés, el idioma que se usa en la directiva predeterminada.

**En el caso de etiquetas e informaciones sobre herramientas que ven los usuarios cuando hacen clic con el botón derecho para clasificar y proteger archivos o carpetas:**

- Cuando existe una coincidencia directa con el idioma del sistema operativo, los nombres y descripciones de etiquetas aparecen en ese idioma.

- Cuando no existe coincidencia con el idioma del sistema operativo, los nombres y descripciones de etiquetas aparecen en el idioma que especificó de manera predeterminada para todos los usuarios. Normalmente este idioma es el inglés, el idioma que se usa en la directiva predeterminada.

## <a name="when-localized-label-names-are-not-used"></a>Cuándo no se usan los nombres de etiquetas localizados

Los nombres de etiquetas (y subetiquetas) localizados no se usan en los siguientes escenarios. Para mantener la coherencia entre su inquilino, el idioma predeterminado siempre se usa para lo siguiente:

- Registros de uso de cliente

- PowerShell (salida de Get-AIPFileStatus)

- Metadatos de documentos y encabezados de correo electrónico


## <a name="next-steps"></a>Pasos siguientes

Para más información sobre las opciones que puede cambiar para una etiqueta, así como otra configuración de la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


