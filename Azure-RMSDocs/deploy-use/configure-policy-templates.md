---
title: Configurar y administrar plantillas para Azure Information Protection
description: "Configure y administre plantillas de administración de derechos desde Azure Portal."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/20/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8301aabb-047d-4892-935c-7574f6af8813
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 303b8d55faf3aa25389bf5810df4e65f18459bc6
ms.sourcegitcommit: 67750454f8fa86d12772a0075a1d01a69f167bcb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2018
---
# <a name="configuring-and-managing-templates-for-azure-information-protection"></a>Configuración y administración de plantillas para Azure Information Protection

>*Se aplica a: Azure Information Protection*

>[!NOTE]
>Esta funcionalidad reemplaza la configuración de plantillas personalizadas en el Portal de Azure clásico. El portal clásico ya no está disponible, por lo que debe usar Azure Portal. Para una asignación de procedimientos rápida, vea [Tareas que solía realizar con el Portal de Azure clásico](migrate-portal.md).


Las plantillas de Rights Management ahora están integradas con la directiva de Azure Information Protection. 

**Cuando tiene una suscripción que incluye clasificación, etiquetado y protección (Azure Information Protection P1 o P2):**

- Las plantillas de Rights Management que no están integradas con las etiquetas para el inquilino se muestran en la sección **Plantillas de protección** después de las etiquetas en la hoja **Azure Information Protection - Global policy** (Azure Information Protection: directiva global). Puede convertir estas plantillas en etiquetas o puede crear un vínculo a ellas cuando configure la protección de sus etiquetas. 

**Cuando tiene una suscripción que solo incluye protección (una suscripción a Office 365 que incluye el servicio Azure Rights Management):**

- Las plantillas de Rights Management para el inquilino se muestran en la hoja **Azure Information Protection - Global policy** (Azure Information Protection: directiva global), en la sección **Plantillas de protección**. No se muestran etiquetas. También verá valores de configuración específicos de la clasificación y del etiquetado, pero o no tienen ningún efecto en las plantillas o no se pueden configurar. 

## <a name="default-templates"></a>Plantillas predeterminadas

Al obtener una suscripción a Azure Information Protection o a Office 365 que incluya el servicio Azure Rights Management, se crean automáticamente dos plantillas predeterminadas para el inquilino. Estas plantillas restringen el acceso a los usuarios autorizados de la organización. Al crear estas plantillas, tienen los permisos que aparecen en la documentación [Configuración de los derechos de uso para Azure Rights Management](configure-usage-rights.md#rights-included-in-the-default-templates).

Además, las plantillas están configuradas para permitir el acceso sin conexión durante siete días y no tienen fecha de expiración.

>[!NOTE]
> Puede cambiar esta configuración, así como los nombres y descripciones de las plantillas predeterminadas. Esto no era posible con el Portal de Azure clásico y sigue sin permitirse en PowerShell.

Estas plantillas predeterminadas facilitan a los usuarios el proceso de empezar a proteger de inmediato la información confidencial de la organización. Estas plantillas pueden usarse con etiquetas de Azure Information Protection o de manera independiente con [aplicaciones y servicios](../understand-explore/applications-support.md) que puedan usar plantillas de Rights Management.

También puedes crear tus propias plantillas personalizadas. Aunque probablemente necesite solo unas pocas plantillas, puede tener un máximo de 500 plantillas personalizadas guardadas en Azure.

### <a name="default-template-names"></a>Nombres de plantillas predeterminadas

Si ha adquirido la suscripción hace poco, las plantillas predeterminadas se crearán con los nombres siguientes:

- **Confidencial\Todos los empleados**, que concede permisos de lectura y modificación para el contenido protegido.

- **Extremadamente confidencial\Todos los empleados**, que concede permiso de solo lectura para el contenido protegido.

Si ha adquirido la suscripción hace algún tiempo, las plantillas predeterminadas se crearán con los nombres siguientes:

- **\<nombre de la organización> - Confidencial**, que concede permisos de lectura y modificación para el contenido protegido.

- **\<nombre de la organización> - Solo vista confidencial**, que concede permiso de solo lectura para el contenido protegido. 

Puede cambiar el nombre de estas plantillas predeterminadas (y volver a configurarlas) al usar Azure Portal.

>[!NOTE]
>Si no ve las plantillas predeterminadas en la hoja **Azure Information Protection - Global policy** (Azure Information Protection: directiva global), significa que se han convertido en etiquetas o se han vinculado a una etiqueta. Siguen existiendo como plantillas, pero en el Azure Portal las verá como parte de una configuración de etiqueta que incluye la protección de Azure RMS. Siempre puede confirmar qué plantillas tiene su inquilino. Para ello, ejecute [Get-AadrmTemplate](/powershell/module/aadrm/get-aadrmtemplate) desde el [módulo de AADRM de PowerShell](administer-powershell.md).
>
>Puede convertir manualmente las plantillas, como se explica más adelante en la sección [Para convertir plantillas en etiquetas](#to-convert-templates-to-labels), y después cambiarles el nombre, si le interesa. O bien, se convierten automáticamente si la directiva predeterminada de Azure Information Protection se ha creado recientemente y se ha activado en ese momento el servicio Azure Rights Management para el inquilino.

Las plantillas archivadas se muestran como no disponibles en la hoja **Azure Information Protection - Global policy** (Azure Information Protection: directiva global). Estas plantillas no se puede seleccionar para etiquetas, pero se pueden convertir en etiquetas.

## <a name="considerations-for-templates-in-the-azure-portal"></a>Consideraciones para las plantillas en Azure Portal

Antes de editar estas plantillas o convertirlas en etiquetas, asegúrese de que está al tanto de los siguientes cambios y consideraciones. Debido a cambios en la implementación, la lista siguiente es especialmente importante si ya ha administrado previamente plantillas en el Portal de Azure clásico.

- Después de editar o convertir una plantilla y guardar la directiva de Azure Information Protection, los [derechos de uso](configure-usage-rights.md) originales se modifican con los siguientes cambios. Si procede, puede agregar o quitar derechos de uso individuales con Azure Portal. También puede usar PowerShell con los cmdlets [New-AadrmRightsDefinition](/powershell/module/aadrm/set-aadrmtemplateproperty) y [Set-AadrmTemplateProperty](/powershell/module/aadrm/new-aadrmrightsdefinition).
    
    - **Permitir macros** (nombre común) se agrega automáticamente. Se requiere este derecho de uso para la barra Azure Information en aplicaciones de Office.

- Los valores **Publicada** y **Archivada** se muestran como **Enabled**: **On** (Habilitada: Activada) y **Enabled**: **Off** (Habilitada: Desactivada) respectivamente en la hoja **Etiqueta**. En el caso de que quiera conservar plantillas que no son visibles para los usuarios o los servicios, establézcalas en **Habilitada**: **Desactivada**.

- No es posible copiar ni eliminar una plantilla en Azure Portal. Cuando la plantilla se convierte en una etiqueta, puede configurar la etiqueta para que deje de usar la plantilla. Para ello, seleccione **No configurado** en la opción **Establecer permisos para documentos y correos electrónicos que contengan esta etiqueta**. También puede eliminar la etiqueta. Aun así, en ambos casos, la plantilla no se elimina y permanece en estado archivado.
    
    Para eliminar la plantilla, ahora puede usar el cmdlet [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate) de PowerShell. También puede usar este cmdlet de PowerShell para las plantillas que no se han convertido en etiquetas. Pero si elimina una plantilla que se ha usado para proteger contenido, dicho contenido ya no se podrá abrir. Elimine plantillas solo si está seguro de que no se han usado para proteger documentos o correos electrónicos en producción. Como medida de precaución, conviene que considere la posibilidad de exportar primero la plantilla como una copia de seguridad mediante el cmdlet [Export-AadrmTemplate](/powershell/module/aadrm/export-aadrmtemplate). 

- Las plantillas de departamento (plantillas configuradas para un ámbito) se muestran en la directiva global. Actualmente, si edita y guarda una plantilla de departamento, se quita la configuración del ámbito. El equivalente de una plantilla con ámbito en la directiva de Azure Information Protection es una [directiva con ámbito](configure-policy-scope.md). Si convierte la plantilla en una etiqueta, puede seleccionar un ámbito existente.
    
    Además, actualmente no puede establecer la configuración de compatibilidad de aplicaciones para una plantilla de departamento. Si es necesario, puede establecer la configuración de compatibilidad de aplicaciones con el cmdlet [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty) y el parámetro *EnableInLegacyApps*.

- Al convertir una plantilla en etiqueta o vincular una plantilla a una etiqueta, ya no la pueden usar otras etiquetas. Además, esta plantilla ya no se muestra en la sección **Plantillas de protección**. 

- No puede crear una plantilla desde la sección **Plantillas de protección**. En lugar de eso, cree una etiqueta con el valor **Proteger** y configure los derechos de uso y los valores en la hoja **Protección**. Para instrucciones completas, consulte [Para crear una nueva plantilla](#to-create-a-new-template).

## <a name="to-configure-the-templates-in-the-azure-information-protection-policy"></a>Para configurar las plantillas en la directiva de Azure Information Protection

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e [inicie sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal). Después, vaya a la hoja **Azure Information Protection**.
    
    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. Si la plantilla que quiere configurar es para todos los usuarios, quédese en la hoja **Azure Information Protection - Global policy** (Azure Information Protection: directiva global).
    
    Si la plantilla que quiere configurar se encuentra en una [directiva con ámbito](configure-policy-scope.md) para que se aplique únicamente a los usuarios seleccionados, en la selección del menú **DIRECTIVAS**, seleccione **Directivas con ámbito**. Después, seleccione la directiva con ámbito en la hoja **Azure Information Protection - Scoped policies** (Azure Information Protection: directivas con ámbito).

3. En la hoja **Azure Information Protection - Global policy** (Azure Information Protection: directiva global) o la hoja **Directiva:\<nombre>**, busque la plantilla que quiere configurar:
    
    - Si tiene una suscripción que incluye clasificación, etiquetado y protección: expanda **Plantillas de protección** después de las etiquetas.
    
    - Cuando tiene una suscripción que incluye solo protección: las plantillas se muestran como etiquetas.

4. Seleccione la plantilla y, en la hoja **Etiqueta**, puede cambiar el nombre y la descripción de la plantilla si es necesario. Para ello, edite el **nombre para mostrar de la etiqueta** y la **descripción**. Luego, seleccione la **protección** con un valor de **Azure (clave en la nube)** para abrir la hoja **Protección**.

5. En la hoja **Protección**, puede cambiar los permisos, la expiración del contenido y la configuración de acceso sin conexión. Para más información sobre cómo configurar los valores de protección, consulte [Configuración de una etiqueta para la protección de Rights Management](configure-policy-protection.md)
    
    Haga clic en **Aceptar** para conservar los cambios y, en la hoja **Etiqueta**, haga clic en **Guardar**.

6. Para que los cambios estén disponibles para las aplicaciones y servicios de usuario, en la hoja inicial **Azure Information Protection**, haga clic en **Publicar**.

> [!NOTE]
> También puede editar una plantilla mediante el botón **Editar plantilla** situado en la hoja **Protección** si ha configurado una etiqueta para usar una plantilla predefinida. Siempre y cuando ninguna otra etiqueta use la plantilla seleccionada, este botón convierte la plantilla en una etiqueta y le lleva al paso 5. Para obtener más información sobre lo que ocurre cuando se convierten plantillas en etiquetas, vea la sección siguiente.

## <a name="to-convert-templates-to-labels"></a>Para convertir plantillas en etiquetas

Cuando tiene una suscripción que incluye clasificación, etiquetado y protección, puede convertir una plantilla en una etiqueta. Al convertir una plantilla, se conserva la plantilla original pero en Azure Portal ahora se muestra como incluida en una etiqueta nueva.

Por ejemplo, si convierte una etiqueta llamada **Marketing** que concede derechos de uso al grupo de marketing, en Azure Portal ahora se muestra como una etiqueta llamada **Marketing** con la misma configuración de protección. Si cambia la configuración de protección en esta etiqueta recién creada, la cambia en la plantilla y cualquier usuario o servicio que usa esta plantilla recibirá la nueva configuración de protección en la siguiente actualización de plantilla. 

No es necesario convertir todas las plantillas en etiquetas pero, cuando lo hace, la configuración de protección se integra completamente con la funcionalidad total de las etiquetas para que no sea necesario mantener separadas las configuraciones.

Para convertir una plantilla en etiqueta, haga clic con el botón derecho en la plantilla y seleccione **Convertir en etiqueta**. También puede usar el menú contextual para seleccionar esta opción. 

También puede convertir una plantilla en una etiqueta al configurar una etiqueta para la protección y una plantilla predefinida, mediante el botón **Editar plantilla**. 

Cuando se convierte una plantilla en etiqueta:

- El nombre de la plantilla se convierte en un nombre de etiqueta nuevo y la descripción de la plantilla, en la información sobre herramientas de la etiqueta. 

- Si se publicó el estado de la plantilla, esta configuración se asigna a **Enabled**: **On** (Habilitada: Activada) para la etiqueta, que ahora se muestra como esta etiqueta a los usuarios cuando publique a continuación la directiva de Azure Information Protection. Si se ha archivado el estado de la plantilla, esta configuración se asigna a **Enabled**: **Off** (Habilitada: Desactivada) para la etiqueta y no se muestra como una etiqueta disponible para los usuarios.

- La configuración de protección se conserva y puede editarla si es necesario. Además, puede agregar otros valores de etiqueta como marcadores visuales y condiciones.

- La plantilla original ya no aparece en **Plantillas de protección** y no se puede seleccionar como predefinida al configurar la protección de una etiqueta. Para editar esta plantilla en Azure Portal, ahora debe editar la etiqueta que se ha creado al convertir la plantilla. La plantilla sigue disponible para el servicio Azure Rights Management y todavía se pueden usar los [comandos de PowerShell](administer-powershell.md) para administrarla.  

## <a name="to-create-a-new-template"></a>Para crear una nueva plantilla

Cuando crea una etiqueta nueva con la configuración de protección de **Azure RMS** o **Azure (clave en la nube)**, en segundo plano esta acción crea una plantilla personalizada nueva a la que pueden acceder los servicios y las aplicaciones que se integran con las plantillas de Rights Management.

1. Si la nueva plantilla es para todos los usuarios, quédese en la hoja **Azure Information Protection - Global policy** (Azure Information Protection: directiva global).
    
     Si la nueva plantilla es una plantilla de departamento que se aplicará únicamente a los usuarios seleccionados, en la selección del menú **DIRECTIVAS**, seleccione **Directivas con ámbito**. Después, cree o seleccione la [directiva con ámbito](configure-policy-scope.md) en la hoja **Azure Information Protection - Scoped policies** (Azure Information Protection: directivas con ámbito).

2. En la hoja **Azure Information Protection - Global policy** (Azure Information Protection: directiva global) o la hoja **Directiva:\<nombre>**, haga clic en **Agregar una nueva etiqueta**.

3. En la hoja **Etiqueta**, mantenga el valor predeterminado de **Enabled**: **On** (Habilitada: Activada) para publicar esta plantilla nueva o cambie esta configuración a **Off** (Desactivada) para crear la plantilla como archivada. Luego, escriba un nombre de etiqueta y una descripción para el nombre de la plantilla y la descripción.

4. En **Establecer permisos para documentos y correos electrónicos que contengan esta etiqueta**, seleccione **Proteger** y, luego, **Protección**:
    
     ![Configurar la protección para una etiqueta de Azure Information Protection](../media/info-protect-protection-bar-configured.png)

5. En la hoja **Protección**, puede cambiar los permisos, la expiración del contenido y la configuración de acceso sin conexión. Para más información sobre cómo establecer esta configuración de protección, consulte [Configuración de una etiqueta para la protección de Rights Management](configure-policy-protection.md)
    
    Haga clic en **Aceptar** para conservar los cambios y, en la hoja **Etiqueta**, haga clic en **Guardar**.

6. Para que estas plantillas estén disponibles para las aplicaciones y servicios de usuario, en la hoja inicial **Azure Information Protection**, haga clic en **Publicar**.


## <a name="next-steps"></a>Pasos siguientes

Como ocurre con todos los cambios de la directiva de Azure Information Protection, un equipo que ejecuta el cliente de Azure Information Protection puede tardar hasta 15 minutos en completar la descarga de estas plantillas. Para información sobre cómo los equipos y servicios descargan y actualizan plantillas, consulte [Refreshing templates for users and services](refresh-templates.md) (Actualización de plantillas para usuarios y servicios).

Todo lo que se puede hacer en Azure Portal para crear y administrar plantillas se puede hacer también con PowerShell. Además, PowerShell proporciona más opciones que no están disponibles en el portal. Para obtener más información, vea [Referencia de PowerShell para plantillas de protección](configure-templates-with-powershell.md). 

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
