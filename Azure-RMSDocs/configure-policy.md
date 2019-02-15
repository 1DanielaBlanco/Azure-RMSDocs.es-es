---
title: 'Configuración de la directiva de Azure Information Protection: AIP'
description: Para configurar la protección, la clasificación y el etiquetado, debe configurar la directiva de Azure Information Protection.
author: cabailey
ms.author: cabailey
ms.date: 02/15/2019
manager: barbkess
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 03b0aa0ef3b5f2a8cb232059fe748b243e067f76
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56258715"
---
# <a name="configuring-the-azure-information-protection-policy"></a>Configuración de la directiva de Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Para configurar la protección, la clasificación y el etiquetado, debe configurar la directiva de Azure Information Protection. Esta directiva se descarga luego en los equipos que tienen instalado el [cliente de Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

La directiva contiene las etiquetas y la configuración siguientes:

- Las etiquetas aplican un valor de clasificación a los documentos y correos electrónicos y, opcionalmente, pueden proteger este contenido. El cliente de Azure Information Protection muestra estas etiquetas para los usuarios en aplicaciones de Office y cuando los usuarios hacen clic con el botón derecho en el Explorador de archivos. Estas etiquetas también se pueden aplicar mediante el uso de PowerShell y el analizador de Azure Information Protection.

- La configuración cambia el comportamiento predeterminado del cliente de Azure Information Protection. Por ejemplo, puede seleccionar una etiqueta predeterminada, si todos los documentos y correos electrónicos deben tener una etiqueta y si la barra de Azure Information Protection se muestra en aplicaciones de Office.

## <a name="subscription-support"></a>Compatibilidad con la suscripción

Azure Information Protection admite distintos niveles de suscripciones:

- Azure Information Protection P2: compatibilidad con todas las características de clasificación, etiquetado y protección.

- Azure Information Protection P1: compatibilidad con la mayoría de las características de clasificación, etiquetado y protección, pero no con la clasificación automática o HYOK.

- Office 365 que incluye el servicio Azure Rights Management: Compatibilidad con protección pero no con clasificación y etiquetado.

Las opciones que requieren una suscripción para Azure Information Protection P2 se identifican en el portal.

Si la organización tiene una combinación de suscripciones, usted es el responsable de asegurarse de que los usuarios no utilicen las características para las que sus cuentas no tienen licencia de uso. El cliente de Azure Information Protection no lleva a cabo la comprobación de licencias ni el cumplimiento. Cuando configure opciones para las que no todos los usuarios tienen una licencia, utilice directivas con ámbito o una configuración del Registro para asegurarse de que la organización cumple con las licencias:

- **Cuando su organización tiene una combinación de licencias de Azure Information Protection P1 y Azure Information Protection P2**: Para los usuarios que tienen una licencia P2, cree y use una o varias [directivas con ámbito](configure-policy-scope.md) al configurar las opciones que requieren una licencia de Azure Information Protection P2. Asegúrese de que la directiva global no contiene opciones que requieren una licencia de Azure Information Protection P2.

- **Cuando su organización tiene una suscripción de Azure Information Protection pero algunos usuarios solo tienen una licencia para Office 365 que incluye el servicio Azure Rights Management**: Para los usuarios que no tienen una licencia para Azure Information Protection, edite el registro en sus equipos para que no descarguen la directiva de Azure Information Protection. Para obtener instrucciones, vea la siguiente personalización en la guía del administrador: [Exigencia del modo de solo protección cuando la organización tiene una combinación de licencias](./rms-client/client-admin-guide-customizations.md#enforce-protection-only-mode-when-your-organization-has-a-mix-of-licenses).

Para más información sobre las suscripciones, consulte [¿Qué suscripción necesito para Azure Information Protection y qué características se incluyen?](faqs.md#what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included)

## <a name="signing-in-to-the-azure-portal"></a>Inicio de sesión en Azure Portal

Para iniciar sesión en Azure Portal con objeto de configurar y administrar Azure Information Protection:

- Utilice el vínculo siguiente: https://portal.azure.com

- Use una cuenta que tenga uno de los siguientes [roles de administrador](/azure/active-directory/active-directory-assign-admin-roles-azure-portal):
    
  - **Administrador de Information Protection**

  - **Administrador de seguridad**

  - **Administrador global/Administrador de empresa**
    
    > [!NOTE] 
    > Si su inquilino se ha migrado al almacén de etiquetado unificado, la cuenta también debe tener permisos de acceso al Centro de seguridad y cumplimiento de Office 365 para administrar etiquetas desde Azure Portal. [Más información](configure-policy-migrate-labels.md#important-information-about-administrative-roles)
    
    - Use **Lector de seguridad** solo para [análisis de Azure Information Protection](reports-aip.md).

## <a name="to-access-the-azure-information-protection-blade-for-the-first-time"></a>Para acceder a la hoja de Azure Information Protection por primera vez

1. Inicie sesión en Azure Portal.

2. En el menú del concentrador, seleccione **Crear un recurso** y, a continuación, en el cuadro de búsqueda de Marketplace, escriba **Azure Information Protection**. 
    
3. En la lista de resultados, seleccione **Azure Information Protection**. En la hoja **Azure Information Protection**, haga clic en **Crear**.
    
    > [!TIP] 
    > Opcionalmente, seleccione **Anclar al panel** para crear un icono de **Azure Information Protection** en el panel, de modo que pueda omitir el examen del servicio la próxima vez que inicie sesión en el portal.
    
    Haga clic en **Crear** de nuevo.

4. Verá la página **Inicio rápido** que se abre automáticamente la primera vez que se conecta al servicio. Examine los recursos sugeridos o utilice las otras opciones de menú. Utilice el procedimiento siguiente para configurar las etiquetas que los usuarios pueden seleccionar.

La próxima vez que acceda a la hoja de **Azure Information Protection**, se selecciona automáticamente la opción **Etiquetas** para que pueda configurar las etiquetas para todos los usuarios. Puede volver a la página **Inicio rápido** seleccionándola en el menú **General**.

## <a name="how-to-configure-the-azure-information-protection-policy"></a>Para configurar la directiva de Azure Information Protection

1. Asegúrese de que ha iniciado sesión en Azure Portal con uno de estos roles administrativos: Administrador Information Protection, Administrador de seguridad o Administrador global. Vaya a la [sección anterior](#signing-in-to-the-azure-portal) para obtener más información sobre estos roles administrativos.

2. Si es necesario, vaya a la hoja **Azure Information Protection**: Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information Protection** en el cuadro Filtro. De los resultados, seleccione **Azure Information Protection**. 
    
    La hoja **Azure Information Protection: etiquetas** se abre automáticamente para que se puedan ver y editar las etiquetas disponibles. Las etiquetas pueden estar disponibles para todos los usuarios, usuarios seleccionados o ningún usuario mediante la adición o eliminación de una directiva.

3. Para ver y editar las directivas, seleccione **Directivas** entre las opciones de menú. Para ver y editar la directiva que obtienen todos los usuarios, seleccione la directiva **Global**. Para crear una directiva personalizada para usuarios seleccionados, seleccione **Agregar una directiva**.
    

### <a name="making-changes-to-the-policy"></a>Aplicación de cambios en la directiva

Puede crear tantas etiquetas como quiera. Sin embargo, cuando empiezan a ser demasiadas como para que los usuarios puedan verlas fácilmente y seleccionar la etiqueta correcta, puede crear directivas con ámbito para que los usuarios vean solo las etiquetas pertinentes. Hay un límite superior para las etiquetas que aplican protección: 500.

Cuando realice cambios en una hoja de Azure Information Protection, haga clic en **Guardar** para guardar los cambios o en **Descartar** para volver a la última configuración guardada. Cuando se guardan los cambios de una directiva, o cuando se realizan cambios en las etiquetas que se han agregado a las directivas, estos cambios se publican automáticamente. No hay una opción de publicación separada.

El cliente de Azure Information Protection busca cambios cada vez que se inicia una aplicación de Office compatible y descarga los cambios en su directiva de Azure Information Protection más reciente. Desencadenadores adicionales que actualizan la directiva en el cliente:

- Haga clic con el botón derecho para clasificar y proteger un archivo o carpeta.

- Ejecución de los [cmdlets de PowerShell](./rms-client/client-admin-guide-powershell.md) para etiquetado y protección (Get-AIPFileStatus, Set-AIPFileClassification, and Set-AIPFileLabel).

- Cada 24 horas.

- Para el [analizador de Azure Information Protection](deploy-aip-scanner.md): cuando se inicia el servicio (si la directiva es anterior a una hora) y cada hora durante la operación.


>[!NOTE]
>Cuando el cliente descargue la directiva, tenga en cuenta que deberá esperar unos minutos antes de que esté totalmente operativa. El tiempo real varía según factores como el tamaño y la complejidad de la configuración de la directiva y la conectividad de red. Si la acción resultante de las etiquetas no coincide con los cambios más recientes, deje pasar hasta 15 minutos y vuelva a intentarlo.

### <a name="configuring-your-organizations-policy"></a>Configuración de la directiva de la organización

Use la siguiente información como ayuda para configurar la directiva de Azure Information Protection:

- [Directiva predeterminada de Azure Information Protection](configure-policy-default.md)

- [Configuración de directivas](configure-policy-settings.md)

- [Creación de una nueva etiqueta](configure-policy-new-label.md)

- [Cómo agregar o quitar una etiqueta](configure-policy-add-remove-label.md)
 
- [Eliminación o cambio de orden de una etiqueta](configure-policy-delete-reorder.md)

- [Cambio o personalización de una etiqueta existente](configure-policy-change-label.md)

- [Configuración de una etiqueta para la protección](configure-policy-protection.md)

- [Configuración de una etiqueta para marcas visuales](configure-policy-markings.md)

- [Configuración de las condiciones para la clasificación automática y recomendada](configure-policy-classification.md)

- [Configuración de la directiva para usuarios específicos mediante directivas de ámbito](configure-policy-scope.md)

- [Configuración y administración de plantillas](configure-policy-templates.md)

- [Configuración de etiquetas para distintos idiomas](configure-policy-languages.md)

- [Cómo migrar etiquetas de Azure Information Protection al Centro de seguridad y cumplimiento de Office 365](configure-policy-migrate-labels.md)

## <a name="next-steps"></a>Pasos siguientes

Para obtener ejemplos de cómo personalizar la directiva de Azure Information Protection y ver el comportamiento resultante para los usuarios, pruebe los siguientes tutoriales:

- [Edición de la directiva de Azure Information Protection y creación de una nueva etiqueta](infoprotect-quick-start-tutorial.md)

- [Configure Azure Information Protection policy settings that work together](infoprotect-settings-tutorial.md) (Configuración de los parámetros de la directiva de Azure Information Protection que funcionan en conjunto)

Para ver cómo está funcionando la directiva, consulte [Reporting de Azure Information Protection](reports-aip.md) (Informes para Azure Information Protection).

