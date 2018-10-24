---
title: Migración de etiquetas de Azure Information Protection al Centro de seguridad y cumplimiento de Office 365
description: Migración de etiquetas de Azure Information Protection al Centro de seguridad y cumplimiento de Office 365 para clientes que admiten el etiquetado unificado.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/11/2018
ms.topic: article
ms.service: information-protection
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 075330138910da90049cad3c1ccc74a1a360a218
ms.sourcegitcommit: 39403f0e9fe5912d467b119ed45da94bccd1cc80
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/11/2018
ms.locfileid: "49100653"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-the-office-365-security--compliance-center"></a>Cómo migrar etiquetas de Azure Information Protection al Centro de seguridad y cumplimiento de Office 365

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!IMPORTANT]
> Esta característica se encuentra en versión preliminar, y lo que hace es migrar el inquilino a una nueva plataforma que también está en versión preliminar. Esta operación no puede revertirse. La nueva plataforma admite el etiquetado unificada de modo que varios clientes y servicios pueden usar las etiquetas creadas y administradas.

Migre las etiquetas si quiere poder usarlas en el Centro de seguridad y cumplimiento de Office 365, donde [los clientes que admiten el etiquetado unificado](#clients-that-support-unified-labeling) pueden publicarlas y luego descargarlas. El cliente de Azure Information Protection continúa descargando las etiquetas con su directiva de Azure Information Protection desde Azure Portal. 

Después de haber migrado las etiquetas, puede realizar cambios en ellas en Azure Portal o en el Centro de seguridad y cumplimiento de Office 365, y los clientes respectivos descargarán el mismo cambio.

## <a name="considerations-for-unified-labels"></a>Consideraciones sobre las etiquetas unificadas

Antes de migrar las etiquetas, asegúrese de estar al tanto de los siguientes cambios y consideraciones:

- Actualmente, no todos los clientes admiten etiquetas unificadas. Asegúrese de tener [clientes compatibles](#clients-that-support-unified-labeling) y de estar preparado para la administración tanto en Azure Portal (para los clientes que no admiten etiquetas unificadas) y el Centro de seguridad y cumplimiento (para clientes que sí admiten etiquetas unificadas).

- Si se encuentra en el proceso de definir y configurar las etiquetas que quiere usar, se recomienda que lo realice mediante Azure Portal y, luego, migre las etiquetas. Esta estrategia evita la duplicación de etiquetas durante el proceso de migración, que luego deberá modificarse en el Centro de seguridad y cumplimiento.

- Las directivas, incluida la configuración de directivas y quién tiene acceso a ellas (directivas con ámbito), junto con toda la configuración de cliente avanzada, no se migran. Para los cambios que no se migran, se deberán configurar las opciones pertinentes en el Centro de seguridad y cumplimiento después de haber migrado las etiquetas.
    
    Para una experiencia de usuario más coherente, se recomienda publicar las mismas etiquetas en los mismos ámbitos en el Centro de seguridad y cumplimiento.

- No todas las configuraciones de una etiqueta migrada se admiten en el Centro de seguridad y cumplimiento. Use la tabla de la sección [Configuración de etiquetas que no se admite en el Centro de seguridad y cumplimiento](#label-settings-that-are-not-supported-in-the-security--compliance-center) para ayudarle a identificar estos valores y considerar si se deben excluir las etiquetas migradas de la publicación en el Centro de seguridad y cumplimiento.

- Plantillas de protección:
    
    - Las plantillas que usan una clave basada en la nube y que forman parte de una configuración de etiquetas también se migran con la etiqueta. Otras plantillas de protección no se migran. 
    
    - Después de migrar una etiqueta con la configuración de protección basada en la nube, el ámbito resultante de la plantilla de protección es el ámbito que se define en Azure Portal (o por medio del módulo de ADDRM de PowerShell) y el ámbito que se define en el Centro de seguridad y cumplimiento. 

- Cuando migre las etiquetas, verá que los resultados de la migración muestran si una etiqueta se **creó**, **actualizó** o **cambió** debido a la duplicación:

    - Cuando se crea una etiqueta, se debe publicar en el Centro de seguridad y cumplimiento para que esté disponible para aplicaciones y servicios.
    
    - Cuando se cambia el nombre de una etiqueta, se debe editar, lo que puede hacer en el Centro de seguridad y cumplimiento o en Azure Portal. 

- Para cada etiqueta, solo se muestra en Azure Portal el nombre para mostrar de la etiqueta. Este nombre se puede editar. En el Centro de seguridad y cumplimiento se muestra este nombre para mostrar de una etiqueta y el nombre de la etiqueta. El nombre de la etiqueta es el nombre inicial que especificó cuando creó la etiqueta por primera vez y esta propiedad la usa el servicio de back-end con fines de identificación.

- Las cadenas localizadas de las etiquetas no se migran. Deberá definir nuevas cadenas localizadas para las etiquetas migradas en el Centro de seguridad y cumplimiento.

- Después de la migración, al editar una etiqueta migrada en Azure Portal, el mismo cambio se refleja automáticamente en el Centro de seguridad y cumplimiento. Sin embargo, al editar una etiqueta migrada en el Centro de seguridad y cumplimiento, se debe actualizar la etiqueta en Azure Portal para que refleje el cambio. Por ejemplo, edite el cuadro **Add notes for administrator use** (Agregar notas para uso del administrador) en la hoja **Label** (Etiqueta). 

- El etiquetado unificado está aún en proceso de implementación en los inquilinos. Si todavía no se admite en su inquilino, la migración no se realizará correctamente y se desharán los cambios. Hasta que se admita en todos los inquilinos, debe usar un vínculo especial para acceder a la opción para migrar el inquilino y las etiquetas. El vínculo se proporciona en las instrucciones siguientes.

### <a name="label-settings-that-are-not-supported-in-the-security--compliance-center"></a>Configuración de etiquetas que no se admite en el Centro de seguridad y cumplimiento

Use la tabla siguiente para identificar qué valores de configuración de una etiqueta migrada no se admiten en clientes que usan estas etiquetas, y si debe editar y publicar la etiqueta migrada en el Centro de seguridad y cumplimiento. Si publica etiquetas identificadas para excluirse de la publicación, no se muestran etiquetas para los clientes que admiten el etiquetado unificado.

Los clientes de Azure Information Protection pueden usar esta configuración de etiquetas sin problemas, ya que siguen descargando las etiquetas de Azure Portal.

|Configuración de etiquetas|Compatible con el Centro de seguridad y cumplimiento|Excluir de la edición y publicación en el Centro de seguridad y cumplimiento|
|-------------------|---------------------------------------------|-------------------------|
|Estado de habilitado o deshabilitado<br /><br />Notas: No se sincronizan con el Centro de seguridad y cumplimiento |No disponible|No disponible|
|Color de etiqueta: selecciónelo de la lista o especifíquelo mediante código RGB<br /><br />Notas: El Centro de seguridad y cumplimiento no admite etiquetas de colores |No disponible|No disponible|
|Protección basada en la nube o protección basada en HYOK mediante una plantilla predefinida |No|Sí|
|Protección basada en la nube mediante permisos definidos por el usuario en Word, Excel y PowerPoint |No|Sí|
|Protección basada en HYOK mediante permisos definidos por el usuario en Outlook para No reenviar |No|Sí|
|Eliminación de la protección |No|Sí|
|Distintivos visuales (encabezado, pie de página, marca de agua): fuente personalizada y color de fuente personalizada por código RGB|No|Recomendado si se usan variables<br /><br />-En los clientes, las variables se muestran como texto en lugar de mostrar los valores dinámicos|
|Distintivos visuales por aplicación|No|Recomendado si se usan variables<br /><br />-En los clientes, las variables se muestran como texto en lugar de mostrar los valores dinámicos|
|Condiciones y configuración asociada <br /><br />Notas: Incluye etiquetado recomendado y automático, y su información sobre herramientas|No disponible|No|


## <a name="to-migrate-azure-information-protection-labels"></a>Migración de etiquetas de Azure Information Protection

> [!IMPORTANT]
> No migre las etiquetas hasta que haya confirmado que puede editar y publicar etiquetas de confidencialidad en el Centro de seguridad y cumplimiento de Office 365. Las etiquetas de confidencialidad están comenzando a implementarse en los inquilinos de Office 365, pero aún no están disponibles para todos los inquilinos.
> 
> Para comprobarlo: desde el Centro de seguridad y cumplimiento de Office 365, vaya a **Clasificaciones** > **Etiquetas** y vea si tiene la pestaña **Confidencialidad**. Si no ve esta pestaña, significa que el inquilino aún no está listo para etiquetas de confidencialidad y que en este momento no debe migrar las etiquetas de Azure Information Protection.

Cuando haya confirmado que el inquilino admite etiquetas de confidencialidad en el Centro de seguridad y cumplimiento, use las siguientes instrucciones para migrar su inquilino y las etiquetas de Azure Information Protection.

1. Abra una nueva ventana del explorador e inicie sesión en Azure Portal mediante el siguiente vínculo: https://portal.azure.com/?ActivateMigration=true#blade/Microsoft_Azure_InformationProtection/DataClassGroupEditBlade/migrationActivationBlade. 

2. En la hoja **Azure Information Protection - Etiquetado unificado**, seleccione **Activar** y siga las instrucciones en línea.

Los [clientes que admiten el etiquetado unificado](#clients-that-support-unified-labeling) ahora pueden usar las etiquetas migradas correctamente. En cambio, primero debe publicar estas etiquetas en el Centro de seguridad y cumplimiento.


### <a name="clients-that-support-unified-labeling"></a>Clientes que admiten etiquetado unificado

Los clientes que actualmente admiten el etiquetado unificado son:

- Aplicaciones del programa Office Insider. Para más información, consulte la sección [¿Dónde está la característica disponible actualmente?](https://support.office.com/article/2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9?ad=US#bkmk_whereavailable) en la documentación de Office.
    
- Clientes de proveedores y desarrolladores de software que usan el [SDK de MIP](https://docs.microsoft.com/azure/information-protection/develop/mip/mip-sdk-reference).


## <a name="next-steps"></a>Pasos siguientes

Para más información sobre cómo configurar y publicar las etiquetas migradas en el Centro de seguridad y cumplimiento de Office 365, consulte la entrada de blog, [Announcing the availability of unified labeling management in the Security & Compliance Center](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-the-availability-of-unified-labeling-management-in/ba-p/262492) (Anuncio de la disponibilidad de administración de etiquetado unificado en el Centro de seguridad y cumplimiento).