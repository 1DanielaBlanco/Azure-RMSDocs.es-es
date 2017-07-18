---
title: "Configuración y administración de plantillas en la directiva de Azure Information Protection"
description: "Actualmente en versión preliminar, ahora puede configurar y administrar plantillas de administración de derechos desde la directiva de Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8301aabb-047d-4892-935c-7574f6af8813
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 1f41aad2d132e087e9122b2683be4b45185527de
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2017
---
# <a name="configuring-and-managing-templates-in-the-azure-information-protection-policy"></a>Configuración y administración de plantillas en la directiva de Azure Information Protection

>*Se aplica a: Azure Information Protection*

>[!NOTE]
>Esta funcionalidad actualmente está en versión preliminar y sujeta a frecuentes cambios.
>
>Antes de probar la versión preliminar de esta funcionalidad con plantillas personalizadas que haya creado en el Portal de Azure clásico, tenga en cuenta si tiene una copia de seguridad reciente de las plantillas. Para crear copias de seguridad de las plantillas personalizadas, use el cmdlet [Export-AadrmTemplate](/powershell/module/aadrm/export-aadrmtemplate) de PowerShell y, si es necesario, use [Import-AadrmTemplate](/powershell/module/aadrm/import-aadrmtemplate) para restaurarlas.
>
>Debido a diferencias en la implementación, no se recomienda administrar las mismas plantillas desde el Portal de Azure clásico y Azure Portal.


Las plantillas de administración de derechos ahora están integradas con la directiva de Azure Information Protection. 

**Cuando tiene una suscripción que incluye clasificación, etiquetado y protección (Azure Information Protection P1 o P2):**

- Las plantillas de administración de derechos del inquilino se muestran en la sección **Plantillas** después de las etiquetas. Puede convertir estas plantillas en etiquetas o puede seguir administrándolas como plantillas independientes y crear un vínculo a ellas cuando configure la protección de sus etiquetas. 

**Cuando tiene una suscripción que solo incluye protección (una suscripción a Office 365 que incluye el servicio Azure Rights Management):**

- Las plantillas de administración de derechos del inquilino se muestran como etiquetas y actualmente también están disponibles las opciones de configuración específicas para la clasificación y el etiquetado. 


## <a name="considerations-for-templates-in-the-azure-portal"></a>Consideraciones para las plantillas en Azure Portal

Antes de editar estas plantillas o convertirlas en etiquetas en Azure Portal, tenga en cuenta los cambios siguientes en la implementación de la administración de plantillas en el Portal de Azure clásico. Se espera abordar algunas de las limitaciones durante la versión preliminar:

- Después de editar o convertir una plantilla y guardar la directiva de Azure Information Protection, los [derechos de uso](configure-usage-rights.md) originales se modifican con los siguientes cambios. Si es necesario puede agregar o quitar derechos de uso individuales con los cmdlets [New-AadrmRightsDefinition](/powershell/module/aadrm/set-aadrmtemplateproperty) y [Set-AadrmTemplateProperty](/powershell/module/aadrm/new-aadrmrightsdefinition) de PowerShell.
    
    - Se quita la opción **Guardar como o exportar** (nombre común). En Azure Portal, no puede especificar manualmente este derecho de uso, pero se incluye en el derecho de uso Control total, el que puede agregar si corresponde.
    
    - **Permitir macros** (nombre común) se agrega automáticamente. Se requiere este derecho de uso para la barra Azure Information en aplicaciones de Office.
    
- Actualmente se muestran las plantillas predeterminadas, pero no se pueden editar ni convertir. 

- No es posible copiar ni eliminar una plantilla. Para quitar una plantilla, use el cmdlet [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate) de PowerShell. 

- Actualmente, las plantillas que se configuraron para los idiomas con el Portal de Azure clásico o PowerShell no muestran estos idiomas en el nombre y las descripciones, pero sí se conservan.

- Los valores **Publicada** y **Archivada** se muestran como **Enabled**: **On** (Habilitada: Activada) y **Enabled**: **Off** (Habilitada: Desactivada) respectivamente en la hoja **Etiqueta**.

- Las plantillas de departamento (plantillas configuradas para un ámbito) se muestran en la directiva Global. Actualmente, si edita y guarda una plantilla de departamento, se quita la configuración del ámbito. El equivalente de una plantilla con ámbito en la directiva de Azure Information Protection es una [directiva con ámbito](configure-policy-scope.md). Si convierte la plantilla en una etiqueta, puede seleccionar un ámbito existente.
    
    Además, actualmente no puede establecer la configuración de compatibilidad de aplicaciones para una plantilla de departamento. Si es necesario, puede usar el cmdlet [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty) de PowerShell para establecer este valor.

- No cree una plantilla nueva desde el contenedor **Plantillas**; en lugar de eso, cree una etiqueta con el valor **Proteger** y configure los derechos de uso y los valores en la hoja **Protección**. Para instrucciones completas, consulte [Para crear una nueva plantilla](#to-create-a-new-template).

## <a name="to-configure-the-templates-in-the-azure-information-protection-policy"></a>Para configurar las plantillas en la directiva de Azure Information Protection

1. En una nueva ventana del explorador, inicie sesión en [Azure Portal](https://portal.azure.com) como administrador de seguridad o administrador global.

2. Vaya a la hoja **Azure Information Protection**: por ejemplo, en el menú del centro, haga clic en **Más servicios** y comience a escribir **Information Protection** en el cuadro Filtro. De los resultados, seleccione **Azure Information Protection**. 

2. Si la plantilla que quiere configurar se va a aplicar a todos los usuarios, seleccione **Global** en la hoja **Azure Information Protection**. Sin embargo, si la plantilla que quiere configurar está en una [directiva con ámbito](configure-policy-scope.md) de modo que se aplica solo a los usuarios seleccionados, seleccione esa directiva de ámbito en su lugar.

3. En la hoja de la directiva, ubique la plantilla que desea configurar:
    
    - Cuando tiene una suscripción que incluye clasificación, etiquetado y protección: expanda **Plantillas** después de las etiquetas.
    
    - Cuando tiene una suscripción que incluye solo protección: las plantillas se muestran como etiquetas.

4. Seleccione la plantilla y, en la hoja **Etiqueta**, puede cambiar el nombre y la descripción de la plantilla si es necesario. Para ello, edite el **nombre de la etiqueta** y la **descripción**. Luego, seleccione la **protección** con un valor de **Azure RMS** para abrir la hoja **Protección**.

5. En la hoja **Protección**, puede cambiar los permisos, la expiración del contenido y la configuración de acceso sin conexión. Para más información sobre cómo configurar los valores de protección, consulte [Configuración de una etiqueta para la protección de Rights Management](configure-policy-protection.md)
    
    Haga clic en **Aceptar** para conservar los cambios y, en la hoja **Etiqueta**, haga clic en **Guardar**.

6. Para que los cambios estén disponibles para las aplicaciones y servicios de usuario, en la hoja **Azure Information Protection**, haga clic en **Publicar**.

## <a name="to-convert-templates-to-labels"></a>Para convertir plantillas en etiquetas

Cuando tiene una suscripción que incluye clasificación, etiquetado y protección, puede convertir una plantilla en una etiqueta. Cuando lo hace, se conserva la plantilla original pero en Azure Portal y ahora se muestra como incluida en una etiqueta nueva.

Por ejemplo, si convierte una etiqueta llamada **Marketing** que concede derechos de uso al grupo de marketing, en Azure Portal ahora se muestra como una etiqueta llamada **Marketing** con la misma configuración de protección. Si cambia la configuración de protección en esta etiqueta recién creada, la cambia en la plantilla y cualquier usuario o servicio que usa esta plantilla recibirá la nueva configuración de protección en la siguiente actualización de plantilla. 

No es necesario convertir todas las plantillas en etiquetas pero, cuando lo hace, la configuración de protección se integra completamente con la funcionalidad total de las etiquetas para que no sea necesario mantener separadas las configuraciones.

Para convertir una plantilla en etiqueta, haga clic con el botón derecho en la plantilla y seleccione **Convertir en etiqueta**. También puede usar el menú contextual para seleccionar esta opción.

Cuando se convierte una plantilla en etiqueta:

- El nombre de la plantilla se convierte en un nombre de etiqueta nuevo y la descripción de la plantilla, en la información sobre herramientas de la etiqueta. 

- Si se publicó el estado de la plantilla, esta configuración se asigna a **Enabled**: **On** (Habilitada: Activada) para la etiqueta, que ahora se muestra como esta etiqueta a los usuarios cuando publique a continuación la directiva de Azure Information Protection. Si se archivó el estado de la plantilla, esta configuración se asigna a **Enabled**: **Off** (Habilitada: Desactivada) para la etiqueta y no se muestra como una etiqueta disponible para los usuarios.

- La configuración de protección se conserva y puede editarla si es necesario. Además, puede agregar otros valores de etiqueta como marcadores visuales y condiciones.

- La plantilla original ya no aparece en **Plantillas** y para editarla en Azure Portal, ahora se edita la etiqueta que se creó. La plantilla sigue disponible para el servicio Azure Rights Management y todavía se pueden usar los [comandos de PowerShell](administer-powershell.md) para administrarla.  

## <a name="to-create-a-new-template"></a>Para crear una nueva plantilla

Cuando crea una etiqueta nueva con la configuración de protección de **Azure RMS**, de forma encubierta, se crea una plantilla personalizada nueva a la que pueden acceder los servicios y las aplicaciones que se integran con las plantillas de Rights Management.

1. Si la nueva etiqueta que quiere crear se aplicará a todos los usuarios, en la hoja **Policy: Global** (Directiva: Global), haga clic en **Add a new label** (Agregar una nueva etiqueta).
    
     Si la nueva plantilla que quiere crear será una plantilla de departamento de modo que se aplique solo a usuarios seleccionados, primero seleccione o cree una directiva con ámbito en la hoja **Azure Information Protection** inicial.

2. En la hoja **Etiqueta**, mantenga el valor predeterminado de **Enabled**: **On** (Habilitada: Activada) para publicar esta plantilla nueva o cambie esta configuración a **Off** (Desactivada) para crear la plantilla como archivada. Luego, escriba un nombre de etiqueta y una descripción para el nombre de la plantilla y la descripción.

3. En **Establecer permisos para documentos y correos electrónicos que contengan esta etiqueta**, seleccione **Proteger** y, luego, **Protección**:
    
     ![Configurar la protección para una etiqueta de Azure Information Protection](../media/info-protect-protection-bar.png)

4. En la hoja **Protección**, puede cambiar los permisos, la expiración del contenido y la configuración de acceso sin conexión. Para más información sobre cómo establecer esta configuración de protección, consulte [Configuración de una etiqueta para la protección de Rights Management](configure-policy-protection.md)
    
    Haga clic en **Aceptar** para conservar los cambios y, en la hoja **Etiqueta**, haga clic en **Guardar**.

5. Para que estas plantillas estén disponibles para las aplicaciones y servicios de usuario, en la hoja **Azure Information Protection**, haga clic en **Publicar**.


## <a name="next-steps"></a>Pasos siguientes

Como ocurre con todos los cambios de la directiva de Azure Information Protection, un equipo que ejecuta el cliente de Azure Information Protection puede tardar hasta 15 minutos en completar la descarga de estas plantillas. Para información sobre cómo los equipos y servicios descargan y actualizan plantillas, consulte [Refreshing templates for users and services](refresh-templates.md) (Actualización de plantillas para usuarios y servicios).

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
