---
title: Migración de etiquetas de Azure Information Protection al Centro de seguridad y cumplimiento de Office 365 (AIP)
description: Migración de etiquetas de Azure Information Protection al Centro de seguridad y cumplimiento de Office 365 para clientes que admiten el etiquetado unificado.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/26/2019
ms.topic: article
ms.service: information-protection
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 58a563e3d1f43dd312c0d4c9d1ffdf612b1c8d12
ms.sourcegitcommit: 9a9c55c96a7e99bcca742e759a3f08507e3b9801
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/29/2019
ms.locfileid: "55231045"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-the-office-365-security--compliance-center"></a>Cómo migrar etiquetas de Azure Information Protection al Centro de seguridad y cumplimiento de Office 365

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!IMPORTANT]
> Esta característica se encuentra en versión preliminar, y lo que hace es migrar el inquilino a una nueva plataforma. Esta operación no puede revertirse. La nueva plataforma admite el etiquetado unificada de modo que varios clientes y servicios pueden usar las etiquetas creadas y administradas.

Migre las etiquetas si quiere poder usarlas en el Centro de seguridad y cumplimiento de Office 365, donde [los clientes que admiten el etiquetado unificado](#clients-that-support-unified-labeling) pueden publicarlas y luego descargarlas. El cliente de Azure Information Protection continúa descargando las etiquetas con su directiva de Azure Information Protection desde Azure Portal. 

Después de haber migrado las etiquetas, puede realizar cambios en ellas en Azure Portal o en el Centro de seguridad y cumplimiento de Office 365, y los clientes respectivos descargarán el mismo cambio.

### <a name="important-information-about-administrative-roles"></a>Información importante acerca de los roles administrativos

Los [roles de Azure AD ](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) de **administrador de seguridad** y **administrador de Information Protection** no son compatibles con la plataforma de etiquetado unificada. Si estos roles administrativos se utilizan en la organización, antes de migrar las etiquetas, agregue los usuarios que tienen estos roles a los grupos de roles **administrador de cumplimiento** o **administración de la organización** para el Centro de seguridad y cumplimiento de Office 365. Como alternativa, puede crear un nuevo grupo de roles para estos usuarios y agregar los roles de **administración de la retención** o **configuración de la organización** a este grupo. Para obtener instrucciones, consulte [Conceder a los usuarios acceso al Centro de seguridad y cumplimiento de Office 365](https://docs.microsoft.com/office365/securitycompliance/grant-access-to-the-security-and-compliance-center).

Si no da acceso a estos usuarios al Centro de seguridad y cumplimiento mediante una de estas configuraciones, perderán el acceso a las etiquetas y directivas de Azure Portal después de la migración de las etiquetas.

Los administradores globales del inquilino pueden continuar administrando etiquetas y directivas tanto en Azure Portal como en el Centro de seguridad y cumplimiento después de la migración de las etiquetas.


## <a name="considerations-for-unified-labels"></a>Consideraciones sobre las etiquetas unificadas

Antes de migrar las etiquetas, asegúrese de estar al tanto de los siguientes cambios y consideraciones:

- Actualmente, no todos los clientes admiten etiquetas unificadas. Asegúrese de tener [clientes compatibles](#clients-that-support-unified-labeling) y de estar preparado para la administración tanto en Azure Portal (para los clientes que no admiten etiquetas unificadas) y el Centro de seguridad y cumplimiento (para clientes que sí admiten etiquetas unificadas).

- Si se encuentra en el proceso de definir y configurar las etiquetas que quiere usar, se recomienda que lo realice mediante Azure Portal y, luego, migre las etiquetas. Esta estrategia evita la duplicación de etiquetas durante el proceso de migración, que luego deberá modificarse en el Centro de seguridad y cumplimiento.

- Las directivas, incluida la configuración de directivas y quién tiene acceso a ellas (directivas con ámbito), junto con toda la configuración de cliente avanzada, no se migran. Para los cambios que no se migran, se deberán configurar las opciones pertinentes en el Centro de seguridad y cumplimiento después de haber migrado las etiquetas.
    
    Para una experiencia de usuario más coherente, se recomienda publicar las mismas etiquetas en los mismos ámbitos en el Centro de seguridad y cumplimiento.

- No todas las configuraciones de una etiqueta migrada se admiten en el Centro de seguridad y cumplimiento. Use la tabla de la sección [Configuración de etiquetas que no se admiten en el Centro de seguridad y cumplimiento](#label-settings-that-are-not-supported-in-the-security--compliance-center) para ayudarle a identificar los valores no admitidos por el Centro de seguridad y cumplimiento.

- Plantillas de protección:
    
    - Las plantillas que usan una clave basada en la nube y que forman parte de una configuración de etiquetas también se migran con la etiqueta. Otras plantillas de protección no se migran. 
    
    - Después de migrar una etiqueta con la configuración de protección basada en la nube, el ámbito resultante de la plantilla de protección es el ámbito que se define en Azure Portal (o por medio del módulo de AADRM de PowerShell) y el ámbito que se define en el Centro de seguridad y cumplimiento. 

- Cuando migre las etiquetas, verá que los resultados de la migración muestran si una etiqueta se **creó**, **actualizó** o **cambió** debido a la duplicación:

    - Cuando se crea una etiqueta, se debe publicar en el Centro de seguridad y cumplimiento para que esté disponible para aplicaciones y servicios.
    
    - Cuando se cambia el nombre de una etiqueta, se debe editar, lo que puede hacer en el Centro de seguridad y cumplimiento o en Azure Portal. 

- Para cada etiqueta, solo se muestra en Azure Portal el nombre para mostrar de la etiqueta. Este nombre se puede editar. En el Centro de seguridad y cumplimiento se muestra este nombre para mostrar de una etiqueta y el nombre de la etiqueta. El nombre de la etiqueta es el nombre inicial que especificó cuando creó la etiqueta por primera vez y esta propiedad la usa el servicio de back-end con fines de identificación.

- Las cadenas localizadas de las etiquetas no se migran. Deberá definir nuevas cadenas localizadas para las etiquetas migradas en el Centro de seguridad y cumplimiento.

- Después de la migración, al editar una etiqueta migrada en Azure Portal, el mismo cambio se refleja automáticamente en el Centro de seguridad y cumplimiento. Sin embargo, al editar una etiqueta migrada en el Centro de seguridad y cumplimiento, debe volver a Azure Portal, a la hoja **Azure Information Protection - Etiquetado unificado**, y seleccionar **Publicar**. Esta acción adicional es necesaria para que los clientes de Azure Information Protection recojan los cambios de la etiqueta.

### <a name="label-settings-that-are-not-supported-in-the-security--compliance-center"></a>Configuración de etiquetas que no se admite en el Centro de seguridad y cumplimiento

Use la tabla siguiente para identificar qué opciones de configuración de una etiqueta migrada no son compatibles con los clientes de etiquetado unificado, o lo son con limitaciones. Para evitar confusiones, se recomienda que no configure las opciones que no surten ningún efecto en los clientes de etiquetado unificado.

Los clientes de Azure Information Protection pueden usar esta configuración de etiquetas sin problemas, ya que siguen descargando las etiquetas de Azure Portal.

|Configuración de etiquetas|Compatible con los clientes de etiquetado unificado|Excluir de la edición en el Centro de seguridad y cumplimiento|
|-------------------|---------------------------------------------|-------------------------|
|Estado de habilitado o deshabilitado<br /><br />Notas: No se sincronizan con el Centro de seguridad y cumplimiento |No disponible|No disponible|
|Color de etiqueta: selecciónelo de la lista o especifíquelo mediante código RGB<br /><br />Notas: El Centro de seguridad y cumplimiento no admite etiquetas de colores |No disponible|No disponible|
|Protección basada en la nube o protección basada en HYOK mediante una plantilla predefinida |No|Sí|
|Protección basada en la nube mediante permisos definidos por el usuario en Word, Excel y PowerPoint |No|Sí|
|Protección basada en HYOK mediante permisos definidos por el usuario en Outlook para No reenviar |No|Sí|
|Eliminación de la protección |No|Sí|
|Marcas visuales (encabezado, pie de página, marca de agua): Fuente personalizada y color de fuente personalizada mediante código RGB|No|Recomendado si se usan variables<br /><br />-En los clientes, las variables se muestran como texto en lugar de mostrar los valores dinámicos|
|Distintivos visuales por aplicación|No|Recomendado si se usan variables<br /><br />-En los clientes, las variables se muestran como texto en lugar de mostrar los valores dinámicos|
|Condiciones y configuración asociada <br /><br />Notas: Incluye etiquetado recomendado y automático, y su información sobre herramientas|No disponible|No|


## <a name="to-migrate-azure-information-protection-labels"></a>Migración de etiquetas de Azure Information Protection

Siga estas instrucciones para migrar su inquilino y las etiquetas de Azure Information Protection a fin de utilizar el nuevo almacén de etiquetado unificado.

Debe ser administrador global para migrar las etiquetas.

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e [inicie sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal). Después, vaya a la hoja **Azure Information Protection**.
    
    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. En la opción de menú **Administrar**, seleccione **Etiquetado unificado (versión preliminar)**.

3. En la hoja **Azure Information Protection - Etiquetado unificado**, seleccione **Activar** y siga las instrucciones en línea.

Los [clientes que admiten el etiquetado unificado](#clients-that-support-unified-labeling) ahora pueden usar las etiquetas migradas correctamente. En cambio, primero debe publicar estas etiquetas en el Centro de seguridad y cumplimiento.

> [!IMPORTANT]
> Si edita las etiquetas fuera de Azure Portal, para los clientes de Azure Information Protection, vuelva a esta hoja **Azure Information Protection - Etiquetado unificado** y seleccione **Publicar**.

### <a name="clients-that-support-unified-labeling"></a>Clientes que admiten etiquetado unificado

Los clientes que actualmente admiten el etiquetado unificado son:

- [Cliente de etiquetado unificado de Azure Information Protection](./rms-client/unifiedlabelingclient-version-release-history.md) (en versión preliminar)

- Aplicaciones de Office que se encuentran en distintas fases de disponibilidad. Para obtener más información, consulte la sección **¿Donde está la característica disponible actualmente?** de [Aplicar etiquetas de confidencialidad a los documentos y al correo electrónico en Office](https://support.office.com/en-us/article/apply-sensitivity-labels-to-your-documents-and-email-within-office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9) en la documentación de Office.
    
- Clientes de proveedores y desarrolladores de software que usan el [SDK de MIP](https://docs.microsoft.com/azure/information-protection/develop/mip/mip-sdk-reference).


## <a name="next-steps"></a>Pasos siguientes

Para más información sobre las etiquetas migradas que ahora pueden configurarse y publicarse en el Centro de seguridad y cumplimiento de Office 365, consulte [Información general de etiquetas de confidencialidad](/Office365/SecurityCompliance/sensitivity-labels).

Para leer la entrada de blog del anuncio: [Announcing the availability of unified labeling management in the Security & Compliance Center](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-the-availability-of-unified-labeling-management-in/ba-p/262492) (Anuncio de la disponibilidad de la administración de etiquetado unificado en el Centro de seguridad y cumplimiento).