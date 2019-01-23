---
title: Configuración de los parámetros de la directiva de Azure Information Protection (AIP)
description: Configure las directivas de Azure Information Protection que se aplica a todos los usuarios y todos los dispositivos.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/16/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
ms.openlocfilehash: c3d95b0dc8328665c921ab4ff6b37e53ec726f03
ms.sourcegitcommit: 9dc6da0fb7f96b37ed8eadd43bacd1c8a1a55af8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2019
ms.locfileid: "54393478"
---
# <a name="how-to-configure-the-policy-settings-for-azure-information-protection"></a>Configuración directivas para Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Además de la barra de título y la información sobre Information Protection, hay algunas opciones en la directiva de Azure Information Protection que se pueden configurar con independencia de las etiquetas:

![Configuración global de directivas de Azure Information Protection](./media/info-protect-policy-default-settingsv3.png)

Tenga en cuenta que es posible que la configuración de directiva tenga valores predeterminados diferentes, en función de cuándo se compró la suscripción de Azure Information Protection. Es posible que algunas opciones de configuración también se puedan establecer mediante una [configuración de cliente personalizada](./rms-client/client-admin-guide-customizations.md).

Para establecer la configuración:

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e [inicie sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal). Después, vaya a la hoja **Azure Information Protection**.
    
    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. En la opción de menú **Clasificaciones** > **Directivas**: En la hoja **Azure Information Protection: Directivas**, seleccione **Global** si los valores que desea configurar se van a aplicar a todos los usuarios.
    
    Si los valores que quiere configurar se encuentran en una [directiva de ámbito](configure-policy-scope.md) para que se apliquen únicamente a los usuarios seleccionados, seleccione en cambio su directiva de ámbito.

3. En la hoja **Directiva**, configure las opciones:
    
   - **Select the default label** (Seleccionar la etiqueta predeterminada): cuando configure esta opción, seleccione la etiqueta que se asignará a documentos y correos electrónicos que no tienen una. No se puede configurar una etiqueta como predeterminada si tiene etiquetas secundarias. 
    
   - **All documents and emails must have a label** (Todos los documentos y correos electrónicos deben tener una etiqueta): cuando establece esta opción en **On** (Activado), todos los documentos guardados y correos electrónicos enviados deben tener aplicada una etiqueta. El etiquetado puede asignarlo manualmente un usuario, se puede asignar automáticamente como resultado de una [condición](configure-policy-classification.md) o asignarse de forma predeterminada (configurando la opción **Select the default label** [Seleccionar la etiqueta predeterminada]).
        
       Si no se asigna ninguna etiqueta cuando los usuarios guardan un documento o envían un correo electrónico, se les pide que seleccionen una. Por ejemplo:
        
       ![Aviso de Azure Information Protection si se aplica el etiquetado](./media/info-protect-enforce-labelv2.png)
        
       Esta opción no se aplica cuando se quita una etiqueta mediante el cmdlet de PowerShell [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) con el parámetro *RemoveLabel*.
        
   - **Users must provide justification to set a lower classification label, remove a label, or remove protection** (Los usuarios deben proporcionar una justificación para establecer una etiqueta de clasificación inferior, quitar una etiqueta o quitar la protección): cuando establece esta opción en **On** (Activado) y un usuario realiza una de estas acciones (por ejemplo, si cambia la etiqueta **Público** por **Personal**), se pide al usuario que indique el motivo de esta acción. Por ejemplo, el usuario podría explicar que el documento ya no contiene información confidencial. La acción y el motivo de justificación se registran en el registro de eventos de Windows local: **Registros de aplicaciones y servicios** > **Azure Information Protection**.  
        
       ![Mensaje de Azure Information Protection si la nueva clasificación es más baja](./media/info-protect-lower-justification.png)
        
       Esta opción no es aplicable para reducir la clasificación de las subetiquetas bajo la misma etiqueta principal ni para la versión preliminar del analizador.
        
   - **For email messages with attachments, apply a label that matches the highest classification of those attachments** (Para los mensajes de correo electrónico con datos adjuntos, aplicar una etiqueta que coincida con la clasificación más alta de los datos adjuntos): al establecer esta opción en **Recommended** (Recomendado), se pide a los usuarios que apliquen una etiqueta a su mensaje de correo electrónico. La etiqueta se elige de manera dinámica, basándose en las etiquetas de clasificación que se han aplicado a los archivos adjuntos, y se selecciona la etiqueta de clasificación más alta. Los datos adjuntos deben ser un archivo físico y no pueden ser un vínculo a un archivo (por ejemplo, un vínculo a un archivo en SharePoint o OneDrive para la Empresa). Los usuarios pueden aceptar la recomendación o descartarla. Cuando esta opción se establece en **Automático**, la etiqueta se aplica automáticamente, pero los usuarios pueden quitarla o seleccionar una etiqueta distinta antes de enviar el correo electrónico.
    
     Cuando los datos adjuntos con la etiqueta de clasificación más alta se configuran para la protección con la configuración de vista previa de los permisos definidos por el usuario, el mensaje de correo electrónico se etiqueta con la misma clasificación, pero no se aplica la protección.
    
   - **Display the Information Protection bar in Office apps** (Mostrar la barra de Information Protection en las aplicaciones de Office): cuando esta opción está desactivada, los usuarios no pueden seleccionar las etiquetas de una barra de Word, Excel, PowerPoint y Outlook. En su lugar, deben seleccionarlas desde el botón **Proteger** de la cinta. Cuando esta opción está activada, los usuarios pueden seleccionar las etiquetas desde la barra o el botón.
        
       Cuando esta opción está activada, se puede usar junto con una configuración de cliente avanzada para que los usuarios puedan [ocultar la barra de Azure Information Protection de forma permanente](./rms-client/client-admin-guide-customizations.md#permanently-hide-the-azure-information-protection-bar) si deciden no mostrarla. Pueden hacerlo si desactiva la opción **Mostrar barra** del botón **Proteger**.
    
   - **Add the Do Not Forward button to the Outlook ribbon** (Agregar el botón No reenviar a la cinta de Outlook): cuando esta opción está activada, los usuarios pueden hacer clic en este botón del grupo **Protección** de la cinta de Outlook además de seleccionar la opción **No reenviar** en los menús de Outlook. Para garantizar que los usuarios puedan clasificar los mensajes de correo, además de protegerlos, es posible que prefiera no agregar este botón, sino [configurar una etiqueta para la protección](configure-policy-protection.md) y un permiso definido por el usuario para Outlook. Esta configuración de protección equivale funcionalmente a hacer clic en el botón **No reenviar**, pero cuando se incluye está funcionalidad con una etiqueta, los mensajes de correo se clasifican y también se protegen.
    
       Esta configuración de directiva también se puede establecer con una configuración de cliente avanzada como una [personalización de cliente](./rms-client/client-admin-guide-customizations.md#hide-or-show-the-do-not-forward-button-in-outlook).
    
   - **Make the custom permissions option available to users** (Configuración de la opción de permisos personalizados para que esté disponible para los usuarios): cuando esta opción está activada, los usuarios pueden ver opciones para establecer su propia configuración de protección que puede invalidar cualquier configuración de protección que es posible que se haya incluido con una configuración de etiqueta. Los usuarios también pueden ver una opción para quitar la protección. Cuando esta opción está desactivada, los usuarios no ven estas opciones.
        
       Tenga en cuenta que esta configuración no tiene ningún efecto en los permisos personalizados que los usuarios pueden configurar en las opciones de menú de Office. Pero también se puede establecer con una configuración de cliente avanzada como una [personalización de cliente](./rms-client/client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users).
        
       Las opciones de permisos personalizados se encuentran en los siguientes lugares:
        
       - En las aplicaciones de Office: desde la cinta, pestaña **Inicio** > grupo **Protección** > **Proteger** > **Permisos personalizados**
        
       - Desde el Explorador de archivos: haga clic con el botón derecho > **Clasificar y proteger** > **Permisos personalizados**
    
   - **Provide a custom URL for the Azure Information Protection client "Tell me more" web page** (Proporcionar una dirección URL personalizada para la página web "Más información" del cliente de Azure Information Protection): los usuarios ven este vínculo en el cuadro de diálogo de **Microsoft Azure Information Protection**, sección **Ayuda y comentarios**, cuando seleccionan **Proteger** > **Ayuda y comentarios** en la pestaña **Inicio** de las aplicaciones de Office. De forma predeterminada, este vínculo dirige al sitio web de [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection). Puede especificar una URL HTTP o HTTPS (recomendado) si quiere que este vínculo dirija a una página web alternativa. No se realiza ninguna comprobación para verificar que la dirección URL personalizada es accesible o se muestra correctamente en todos los dispositivos.
        
       Por ejemplo, para su departamento de soporte técnico, podría indicar la página de la documentación de Microsoft que incluye información sobre cómo instalar y usar el cliente (**https://docs.microsoft.com/information-protection/rms-client/info-protect-client**) o información sobre la versión de lanzamiento (**https://docs.microsoft.com/information-protection/rms-client/client-version-release-history**). También puede publicar su propia página web que incluya información para que los usuarios se pongan en contacto con el soporte técnico o un vídeo en el que se muestre a los usuarios cómo deben usar las etiquetas que haya configurado.

4. Para guardar los cambios y ponerlas a disposición de los usuarios, haga clic en **Guardar**.

Al hacer clic en **Guardar**, los cambios están disponibles para los usuarios y servicios. Ya no hay una opción de publicación separada.

## <a name="next-steps"></a>Pasos siguientes

Para ver cómo algunas de estas configuraciones de directiva pueden trabajar juntas, pruebe el tutorial [Configure Azure Information Protection policy settings that work together](infoprotect-settings-tutorial.md) (Configuración de los parámetros de la directiva de Azure Information Protection que funcionan en conjunto).

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).

