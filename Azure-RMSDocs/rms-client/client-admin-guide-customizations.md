---
title: Configuraciones personalizadas del cliente de Azure Information Protection
description: Información sobre cómo personalizar el cliente de Azure Information Protection para Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/24/2019
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 71ef2607355cbe84003aaf9fc77dfa5d9a72beff
ms.sourcegitcommit: cf52083dde756ad3620c05fc74f012d8a7abacf3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898858"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-client"></a>Guía del administrador: Configuraciones personalizadas del cliente de Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2*

Use la siguiente información para configuraciones avanzadas que podría necesitar para escenarios específicos o un subconjunto de usuarios cuando administre el cliente de Azure Information Protection.

Algunas de estas opciones requieren la modificación del Registro y otras usan la configuración avanzada que debe configurar en Azure Portal y, después, publicarlas para que los clientes las descarguen.  

### <a name="how-to-configure-advanced-client-configuration-settings-in-the-portal"></a>Cómo establecer opciones de configuración de cliente avanzadas en el portal

1. Si aún no lo ha hecho, en una nueva ventana del explorador, [inicie sesión en Azure Portal](../configure-policy.md#signing-in-to-the-azure-portal) y, después, vaya hasta la hoja **Azure Information Protection**.

2. Desde la opción de menú **Clasificaciones** > **Etiquetas**: seleccione **Directivas**.

3. En la hoja **Azure Information Protection: Directivas**, seleccione el menú contextual (**...**) junto a la directiva para que contenga la configuración avanzada. Después, seleccione **Configuración avanzada**.
    
    Puede establecer la configuración avanzada para la directiva global, así como para las directivas con ámbito.

4. En la hoja **Configuración avanzada**, escriba el nombre y el valor de la configuración avanzada y, después, seleccione **Guardar y cerrar**.

5. Asegúrese de que los usuarios de esta directiva reinician las aplicaciones de Office que hubieran abierto.

6. Si ya no necesita la configuración y quiere revertir al comportamiento predeterminado: en la hoja **Configuración avanzada**, seleccione el menú contextual (**...**) situado junto a la configuración que ya no necesita y después seleccione **Eliminar**. Después, haga clic en **Guardar y cerrar**.

#### <a name="available-advanced-client-settings"></a>Configuración de cliente avanzada disponible

|Setting|Escenario e instrucciones|
|----------------|---------------|
|DisableDNF|[Mostrar u ocultar el botón No reenviar en Outlook](#hide-or-show-the-do-not-forward-button-in-outlook)|
|EnableBarHiding|[Ocultación de manera permanente de la barra de Azure Information Protection](#permanently-hide-the-azure-information-protection-bar)|
|EnableCustomPermissions|[Configuración de las opciones de permisos personalizados para que estén disponibles o no disponibles para los usuarios](#make-the-custom-permissions-options-available-or-unavailable-to-users)|
|EnablePDFv2Protection|[No proteger archivos PDF con el estándar ISO de cifrado de archivos PDF](#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)|
|LabelbyCustomProperty|[Migración de las etiquetas de Secure Islands y otras soluciones de etiquetado](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|LabelToSMIME|[Configuración de una etiqueta para aplicar la protección de S/MIME en Outlook](#configure-a-label-to-apply-smime-protection-in-outlook)|
|LogLevel|[Cambio del nivel de registro local](#change-the-local-logging-level)
|OutlookDefaultLabel|[Establecimiento de otra etiqueta predeterminada para Outlook](#set-a-different-default-label-for-outlook)|
|OutlookRecommendationEnabled|[Habilitación de la clasificación recomendada en Outlook](#enable-recommended-classification-in-outlook)|
|PostponeMandatoryBeforeSave|[Quita "No ahora" en los documentos cuando utilice el etiquetado obligatorio](#remove-not-now-for-documents-when-you-use-mandatory-labeling)|
|ProcessUsingLowIntegrity|[Deshabilitación del nivel de integridad bajo para el analizador](#disable-the-low-integrity-level-for-the-scanner)|
|PullPolicy|[Soporte técnico para equipos desconectados](#support-for-disconnected-computers)
|RemoveExternalContentMarkingInApp|[Quitar encabezados y pies de página de otras soluciones de etiquetado](#remove-headers-and-footers-from-other-labeling-solutions)|
|ReportAnIssueLink|[Agregar "Notificar un problema" para los usuarios](#add-report-an-issue-for-users)|
|RunPolicyInBackground|[Activación de la clasificación que se ejecuta continuamente en segundo plano](#turn-on-classification-to-run-continuously-in-the-background)|
|SyncPropertyName|[Etiquetado de un documento de Office mediante el uso de una propiedad personalizada existente](#label-an-office-document-by-using-an-existing-custom-property)|
|SyncPropertyState|[Etiquetado de un documento de Office mediante el uso de una propiedad personalizada existente](#label-an-office-document-by-using-an-existing-custom-property)|

## <a name="prevent-sign-in-prompts-for-ad-rms-only-computers"></a>Evitar solicitudes de inicio de sesión solo para equipos AD RMS

De forma predeterminada, el cliente de Azure Information Protection intenta conectarse automáticamente al servicio Azure Information Protection. Para equipos que solo establecen comunicación con AD RMS, esta configuración puede producir una solicitud de inicio de sesión para los usuarios que no es necesaria. Se puede evitar esta solicitud de inicio de sesión modificando el Registro.

 - Busque el siguiente nombre de valor y después establezca los datos del valor en **0**:
    
    **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Independientemente de esta configuración, el cliente de Azure Information Protection sigue aún el [proceso de detección del servicio de RMS](client-deployment-notes.md#rms-service-discovery) estándar para buscar su clúster de AD RMS.

## <a name="sign-in-as-a-different-user"></a>Inicio de sesión como un usuario diferente

En un entorno de producción, los usuarios normalmente no necesitarán iniciar sesión como un usuario diferente cuando estén utilizando el cliente de Azure Information Protection. No obstante, como administrador, es posible que tenga que iniciar sesión como un usuario diferente durante la fase de pruebas. 

Puede comprobar con qué cuenta ha iniciado sesión usando el cuadro de diálogo **Microsoft Azure Information Protection**: Abra una aplicación de Office y, en la pestaña **Inicio**, en el grupo **Protección**, haga clic en **Proteger** y luego en **Ayuda y comentarios**. El nombre de cuenta se muestra en la sección **Estado del cliente**.

Asegúrese de comprobar el nombre de dominio de la cuenta de inicio de sesión que se muestra. Puede ser fácil no darse cuenta de que inició sesión con el nombre de cuenta correcto, pero con un dominio incorrecto. Un síntoma de usar una cuenta incorrecta podría ser no poder descargar la directiva de Azure Information Protection o no verse las etiquetas de comportamiento esperadas.

Para iniciar sesión como un usuario diferente:

1. Vaya a **%localappdata%\Microsoft\MSIP** y elimine el archivo **TokenCache**.

2. Reinicie todas las aplicaciones de Office abiertas e inicie sesión con su cuenta de usuario diferente. Si no ve un mensaje en la aplicación de Office para iniciar sesión en el servicio Azure Information Protection, vuelva al cuadro de diálogo **Microsoft Azure Information Protection** y haga clic en **Iniciar sesión** desde la sección **Estado del cliente** actualizada.

Además:

- Si tras completar estos pasos, la sesión del cliente de Azure Information Protection todavía se inicia con la cuenta antigua, elimine todas las cookies de Internet Explorer y, luego, repita los pasos 1 y 2.

- Si usa el inicio de sesión único, debe cerrar la sesión en Windows e iniciarla con la otra cuenta de usuario después de eliminar el archivo de token. El cliente Azure Information Protection se autentica entonces automáticamente mediante la cuenta de usuario que tiene iniciada sesión actualmente.

- Esta solución se admite para iniciar sesión como otro usuario desde el mismo inquilino. No se admite para iniciar sesión como otro usuario desde un inquilino diferente. Para probar Azure Information Protection con varios inquilinos, use equipos diferentes.

- Puede usar la opción **Restablecer configuración** de **Ayuda y comentarios** para cerrar sesión y eliminar la directiva de Azure Information Protection descargada.


## <a name="enforce-protection-only-mode-when-your-organization-has-a-mix-of-licenses"></a>Exigencia del modo de solo protección cuando la organización tiene una combinación de licencias

Si la organización no tiene ninguna licencia de Azure Information Protection, pero tiene licencias de Office 365 que incluyen el servicio de Azure Rights Management para la protección de datos, el cliente de Azure Information Protection para Windows se ejecuta automáticamente en el [modo de solo protección](client-protection-only-mode.md).

Sin embargo, si la organización tiene una suscripción para Azure Information Protection, de forma predeterminada todos los equipos Windows pueden descargar la directiva de Azure Information Protection. El cliente de Azure Information Protection no lleva a cabo la comprobación de licencias ni el cumplimiento. 

Si tiene algunos usuarios que no tiene una licencia de Azure Information Protection, pero sí una licencia de Office 365 que incluye el servicio de Azure Rights Management, edite el Registro en los equipos de estos usuarios para impedir que dichos usuarios ejecuten las características de clasificación y etiquetado sin licencia de Azure Information Protection.

Busque el siguiente nombre de valor y establezca los datos del valor en **0**:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Además, compruebe que estos equipos no tienen un archivo denominado **Policy.msip** en la carpeta **%LocalAppData%\Microsoft\MSIP**. Si el archivo existe, elimínelo. Este archivo contiene la directiva de Azure Information Protection y podría haberse descargado antes de que editara el Registro, o si el cliente de Azure Information Protection se instaló con la opción de demostración.

## <a name="add-report-an-issue-for-users"></a>Agregar "Notificar un problema" para los usuarios

Esta opción utiliza una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se debe definir en Azure Portal. 

Cuando especifique la siguiente configuración de cliente avanzada, los usuarios verán una opción **Notificar un problema** que se puede seleccionar desde el cuadro de diálogo del cliente **Ayuda y comentarios**. Especifique una cadena HTTP para el vínculo. Por ejemplo, una página web personalizada que tiene para que los usuarios notifiquen problemas o una dirección de correo electrónico que vaya a su departamento de soporte técnico. 

Para establecer esta configuración avanzada, especifique las cadenas siguientes:

- Clave: **ReportAnIssueLink**

- Valor: **\<HTTP string>**

Valor de ejemplo para un sitio web: `https://support.contoso.com`

Valor de ejemplo para una dirección de correo electrónico: `mailto:helpdesk@contoso.com`

## <a name="hide-the-classify-and-protect-menu-option-in-windows-file-explorer"></a>Ocultación de la opción de menú Clasificar y Proteger en el Explorador de archivos de Windows

Cree el siguiente nombre de valor DWORD (con cualquier datos de valor):

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

## <a name="support-for-disconnected-computers"></a>Soporte técnico para equipos desconectados

De forma predeterminada, el cliente de Azure Information Protection intenta conectarse automáticamente al servicio Azure Information Protection para descargar la directiva más reciente de Azure Information Protection. Si tiene equipos que sabe que no se podrán conectar a Internet durante un período de tiempo, puede evitar que el cliente intente conectarse al servicio editando el Registro. 

Tenga en cuenta que si no hay conexión a Internet, el cliente no puede aplicar protección (ni quitarla) mediante el uso de la clave basada en la nube de la organización. En su lugar, el cliente está limitado al uso de etiquetas que aplican solo clasificación, o protección que usa [HYOK](../configure-adrms-restrictions.md).

Puede evitar una solicitud de inicio de sesión para el servicio de Azure Information Protection mediante un [ajuste de cliente avanzado](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que debe configurar en Azure Portal. A continuación, descargue la directiva para equipos. O bien, puede evitar esta solicitud de inicio de sesión modificando el Registro.

- Para configurar el ajuste de cliente avanzado:
    
    1. Escriba las siguientes cadenas:
    
        - Clave: **PullPolicy**
        
        - Valor: **False**
    
    2. Descargue la directiva con este ajuste e instálela en equipos mediante las instrucciones siguientes.

- Como alternativa, para editar el Registro:
    
    - Busque el siguiente nombre de valor y después establezca los datos del valor en **0**:
    
        **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 


El cliente debe tener un archivo de directiva válido denominado **Policy.msip** en la carpeta **%LocalAppData%\Microsoft\MSIP**.

Puede exportar la directiva global o una directiva de ámbito desde Azure Portal y copiar el archivo exportado en el equipo cliente. También puede utilizar este método para reemplazar un archivo de directiva no actualizado con la directiva más reciente. Sin embargo, la exportación de la directiva no es compatible con el escenario donde un usuario pertenece a más de una directiva de ámbito. También tenga en cuenta que si los usuarios seleccionan la opción **Restablecer configuración** de [Ayuda y comentarios](client-admin-guide.md#help-and-feedback-section), esta acción elimina el archivo de directiva y hace que el cliente no funcione hasta que se reemplace manualmente el archivo de directiva o el cliente se conecte al servicio para descargar la directiva.

Al exportar la directiva desde Azure Portal, se descarga un archivo comprimido que contiene varias versiones de la directiva. Estas versiones de la directiva se corresponden con las distintas versiones del cliente de Azure Information Protection:

1. Descomprima el archivo y use la tabla siguiente para identificar qué archivo de directiva necesita. 
    
    |Nombre de archivo|Versión de cliente correspondiente|
    |--------------------------|---------------------------------------------|
    |Policy1.1.msip |Versión 1.2|
    |Policy1.2.msip |Versión 1.3 - 1.7|
    |Policy1.3.msip |Versión 1.8 - 1.29|
    |Policy1.4.msip |Versión 1.32 y posteriores|
    
2. Cambie el nombre del archivo identificado a **Policy.msip** y, después, cópielo en la carpeta **%LocalAppData%\Microsoft\MSIP** en equipos que tengan instalado el cliente de Azure Information Protection. 

Si el equipo sin conexión ejecuta la versión preliminar del analizador de Azure Information Protection, hay pasos de configuración adicionales que debe realizar. Para más información, vea [Restricción: el servidor del analizador no tiene conectividad a Internet](../deploy-aip-scanner-preview.md#restriction-the-scanner-server-cannot-have-internet-connectivity) en las instrucciones de implementación del analizador.

## <a name="hide-or-show-the-do-not-forward-button-in-outlook"></a>Mostrar u ocultar el botón No reenviar en Outlook

El método recomendado para configurar esta opción es mediante la [configuración de directiva](../configure-policy-settings.md) **Agregar el botón No reenviar a la cinta de Outlook**. Sin embargo, también puede configurar esta opción mediante una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se establece en Azure Portal.

Al establecer esta configuración, se oculta o se muestra el botón **No reenviar** en la cinta de Outlook. Esta configuración no tiene ningún efecto en la opción No reenviar en los menús de Office.

Para establecer esta configuración avanzada, especifique las cadenas siguientes:

- Clave: **DisableDNF**

- Valor: **True** para ocultar el botón o **False** para mostrarlo

## <a name="make-the-custom-permissions-options-available-or-unavailable-to-users"></a>Configuración de las opciones de permisos personalizados para que estén disponibles o no disponibles para los usuarios

El método recomendado para configurar esta opción es mediante la [configuración de directiva](../configure-policy-settings.md) **Configuración de la opción de permisos personalizados para que esté disponible para los usuarios**. Sin embargo, también puede configurar esta opción mediante una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se establece en Azure Portal. 

Cuando establece esta configuración y publica la directiva para los usuarios, las opciones de permisos personalizados están visibles para que los usuarios seleccionen su propia configuración de protección o están ocultas para que los usuarios no puedan seleccionar su propia configuración de protección a menos que se les solicite.

Para establecer esta configuración avanzada, especifique las cadenas siguientes:

- Clave: **EnableCustomPermissions**

- Valor: **True** para hacer que la opción de permisos personalizados esté visible o **False** para ocultar esta opción


## <a name="permanently-hide-the-azure-information-protection-bar"></a>Ocultación de manera permanente de la barra de Azure Information Protection

Esta opción utiliza una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se debe definir en Azure Portal. Úsela solo cuando la [configuración de directiva](../configure-policy-settings.md) **Mostrar la barra de Information Protection en las aplicaciones de Office** está establecida en **Activado**.

Cuando se establece esta configuración y se publica la directiva para los usuarios, y un usuario decide no mostrar la barra de Azure Information Protection en sus aplicaciones de Office, la barra permanece oculta. Esto ocurre cuando el usuario desactiva la opción **Mostrar barra** en la pestaña **Inicio**, grupo **Protección** , botón **Proteger**. Esta configuración no tiene ningún efecto si el usuario cierra la barra utilizando el icono **Cerrar esta barra**.

Aunque la barra de Azure Information Protection permanece oculta, los usuarios todavía pueden seleccionar una etiqueta de la barra mostrada de manera temporal si se ha configurado la clasificación recomendada, o si el documento o correo electrónico debe tener una etiqueta. 

Para establecer esta configuración avanzada, especifique las cadenas siguientes:

- Clave: **EnableBarHiding**

- Valor: **True**


## <a name="enable-recommended-classification-in-outlook"></a>Habilitación de la clasificación recomendada en Outlook

Esta opción utiliza una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se debe definir en Azure Portal. Esta configuración está en versión preliminar y puede cambiar.

Al configurar una etiqueta para la clasificación recomendada, se pide a los usuarios que acepten o descarten la etiqueta recomendada en Word, Excel y PowerPoint. Esta opción extiende esta recomendación de etiqueta para mostrarse también en Outlook.

Para establecer esta configuración avanzada, especifique las cadenas siguientes:

- Clave: **OutlookRecommendationEnabled**

- Valor: **True**


## <a name="set-a-different-default-label-for-outlook"></a>Establecimiento de otra etiqueta predeterminada para Outlook

Esta opción utiliza una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se debe definir en Azure Portal. 

Al configurar esta opción, Outlook no aplica la etiqueta predeterminada configurada en la directiva de Azure Information Protection para la opción **Seleccione la etiqueta predeterminada**. Por el contrario, Outlook puede aplicar otra etiqueta predeterminada o ninguna.

Para aplicar otra etiqueta, debe especificar el identificador de etiqueta. El valor de identificador de etiqueta se muestra en la hoja **Etiqueta**, al ver o configurar la directiva de Azure Information Protection en Azure Portal. En el caso de los archivos que tienen etiquetas aplicadas, también puede ejecutar el cmdlet de PowerShell [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) para reconocer el identificador de etiqueta (MainLabelId o SubLabelId). Si una etiqueta tiene subetiquetas, especifique únicamente el identificador de una subetiqueta, no el de la etiqueta principal.

Para que Outlook no aplique la etiqueta predeterminada, especifique **Ninguna**.

Para establecer esta configuración avanzada, especifique las cadenas siguientes:

- Clave: **OutlookDefaultLabel**

- Valor: \<**Identificador de etiqueta**> o **Ninguna**

## <a name="configure-a-label-to-apply-smime-protection-in-outlook"></a>Configuración de una etiqueta para aplicar la protección de S/MIME en Outlook

Esta opción utiliza una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se debe definir en Azure Portal. Esta configuración está en versión preliminar y puede cambiar.

Use esta configuración únicamente cuando tenga una [implementación de S/MIME](https://docs.microsoft.com/office365/SecurityCompliance/s-mime-for-message-signing-and-encryption) en funcionamiento y desee que una etiqueta aplique automáticamente este método de protección para los correos electrónicos en lugar de la protección de Rights Management de Azure Information Protection. La protección resultante es la misma que cuando un usuario selecciona manualmente las opciones de S/MIME de Outlook.

Esta configuración requiere que especifique una configuración avanzada de cliente llamada **LabelToSMIME** para cada etiqueta de Azure Information Protection a la que desee aplicar la protección S/MIME. Después, para cada entrada, establezca el valor utilizando la sintaxis siguiente:

`[Azure Information Protection label ID];[S/MIME action]`

El valor de identificador de etiqueta se muestra en la hoja **Etiqueta**, al ver o configurar la directiva de Azure Information Protection en Azure Portal. Para usar S/MIME con una subetiqueta, especifique siempre el identificador de solo la subetiqueta, no de la etiqueta principal. Cuando especifique una subetiqueta, la etiqueta principal debe estar en el mismo ámbito o en la directiva global.

La acción de S/MIME puede ser:

- `Sign;Encrypt`: para aplicar una firma digital y cifrado S/MIME

- `Encrypt`: para aplicar solo cifrado S/MIME

- `Sign`: para aplicar solo una firma digital

Valores de ejemplo para un identificador de etiqueta de **dcf781ba-727f-4860-b3c1-73479e31912b**:

- Para aplicar una firma digital y cifrado S/MIME:
    
    **dcf781ba-727f-4860-b3c1-73479e31912b;Sign;Encrypt**

- Para aplicar solo cifrado S/MIME:
    
    **dcf781ba-727f-4860-b3c1-73479e31912b;Encrypt**
    
- Para aplicar solo una firma digital:
    
    **dcf781ba-727f-4860-b3c1-73479e31912b;Sign**

Como resultado de esta configuración, cuando se aplica la etiqueta para un mensaje de correo electrónico, la protección S/MIME se aplica al correo electrónico además de la clasificación de la etiqueta.

Si la etiqueta especificada está configurada para la protección de Rights Management en Azure Portal, la protección de S/MIME reemplaza la protección de Rights Management solo en Outlook. En el resto de escenarios que admiten el etiquetado, se aplicará la protección de Rights Management.

Si quiere que la etiqueta sea visible solo en Outlook, configure la etiqueta para aplicar la acción única definida por el usuario de **No reenviar**, como se describe en el [Inicio rápido: Configuración de una etiqueta para usuarios para proteger fácilmente los correos electrónicos que contienen información confidencial](../quickstart-label-dnf-protectedemail.md).

## <a name="remove-not-now-for-documents-when-you-use-mandatory-labeling"></a>Quita "No ahora" en los documentos cuando utilice el etiquetado obligatorio.

Esta opción utiliza una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se debe definir en Azure Portal. 

Cuando utilice la [configuración de directiva](../configure-policy-settings.md) de **Todos los documentos y mensajes de correo electrónico deben tener una etiqueta** , se pedirá a los usuarios que seleccionen una etiqueta cuando guarden por primera vez un documento de Office y cuando envíen un mensaje de correo electrónico. Para los documentos, los usuarios pueden seleccionar **No ahora** para descartar temporalmente el aviso para seleccionar una etiqueta y volver al documento. Sin embargo, no pueden cerrar el documento guardado sin etiquetarlo. 

Al configurar esta opción, se quita la opción **Ahora no** para que los usuarios tengan que seleccionar una etiqueta cuando se guarda el documento por primera vez.

Para establecer esta configuración avanzada, especifique las cadenas siguientes:

- Clave: **PostponeMandatoryBeforeSave**

- Valor: **False**

## <a name="turn-on-classification-to-run-continuously-in-the-background"></a>Activación de la clasificación que se ejecuta continuamente en segundo plano

Esta opción utiliza una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se debe definir en Azure Portal. Esta configuración está en versión preliminar y puede cambiar.

Al configurar esta opción, se cambia el [comportamiento predeterminado](../configure-policy-classification.md#how-automatic-or-recommended-labels-are-applied) de cómo el cliente de Azure Information Protection aplica etiquetas automáticas y recomendadas a los documentos: 

- Para Word, Excel y PowerPoint, la clasificación automática se ejecuta continuamente en segundo plano.  

El comportamiento no cambia para Outlook.

Cuando el cliente de Azure Information Protection comprueba periódicamente los documentos en busca de las reglas de condición que se han especificado, este comportamiento permite la clasificación y protección automática y recomendada para los documentos que se almacenan en SharePoint Online. Los archivos de gran tamaño también se guardan más rápidamente porque las reglas de condición ya se han ejecutado. 

Las reglas de condición no se ejecutan en tiempo real mientras el usuario escribe. En su lugar, se ejecutan periódicamente como una tarea en segundo plano si se modifica el documento.

Para establecer esta configuración avanzada, especifique las cadenas siguientes:

- Clave: **RunPolicyInBackground**

- Valor: **True**

## <a name="dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption"></a>No proteger archivos PDF con el estándar ISO de cifrado de archivos PDF

Esta opción utiliza una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se debe definir en Azure Portal. 

Cuando la versión más reciente del cliente de Azure Information Protection protege un archivo PDF, la extensión de nombre de archivo resultante sigue siendo .pdf y cumple con el estándar ISO de cifrado de archivos PDF. Para obtener más información sobre este estándar, vea la sección **Cifrado 7.6** en el [documento que se deriva de ISO-1 32000](https://www.adobe.com/content/dam/acom/en/devnet/pdf/pdfs/PDF32000_2008.pdf) que publica Adobe Systems Incorporated.

Si necesita el cliente para revertir al comportamiento de las versiones anteriores del cliente que protegía archivos PDF mediante el uso de una extensión de nombre de archivo .ppdf, use la siguiente configuración avanzada escribiendo la siguiente cadena:

- Clave: **EnablePDFv2Protection**

- Valor: **False**

Para que el analizador de Azure Information Protection utilice el nuevo valor, haya que reiniciar el servicio del analizador. Además, el analizador no podrá proteger documentos PDF de forma predeterminada. Si quiere que el analizador proteja los documentos PDF cuando EnablePDFv2Protection se establece en False, debe [editar el registro](../deploy-aip-scanner.md#editing-the-registry-for-the-scanner).

Para más información sobre el nuevo cifrado de archivos PDF, consulte la entrada de blog [New support for PDF encryption with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/New-support-for-PDF-encryption-with-Microsoft-Information/ba-p/262757) (Nueva compatibilidad con el cifrado de archivos PDF con Microsoft Information Protection).

### <a name="to-convert-existing-ppdf-files-to-protected-pdf-files"></a>Conversión de archivos .ppdf existentes en archivos .pdf protegidos

Cuando el cliente de Azure Information Protection haya descargado la directiva de cliente con la nueva configuración, puede usar comandos de PowerShell para convertir archivos .ppdf existentes en archivos .pdf protegidos que usan el estándar ISO de cifrado de archivos PDF. 

Para usar las siguientes instrucciones con archivos que no ha protegido usted mismo, debe tener un [derecho de uso de Rights Management](../configure-usage-rights.md) para quitar la protección de los archivos, o ser un superusuario. Para habilitar la característica como superusuario y configurar su cuenta como tal, consulte [Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos](../configure-super-users.md).

Además, cuando use estas instrucciones con archivos que no haya protegido usted mismo, se convertirá en el [emisor de RMS](../configure-usage-rights.md#rights-management-issuer-and-rights-management-owner). En este escenario, el usuario que originalmente protegió el documento ya no puede realizar su seguimiento ni revocarlo. Si los usuarios necesitan realizar un seguimiento de sus documentos PDF protegidos y revocarlos, pídales que quiten manualmente la etiqueta y luego vuelvan a aplicarla mediante el Explorador de archivos, mediante clic con el botón derecho.

Para usar comandos de PowerShell para convertir los archivos .ppdf existentes en archivos .pdf protegidos que usan el estándar ISO de cifrado de archivos PDF, siga estos pasos:

1. Use [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) con el archivo .ppdf. Por ejemplo:
    
        Get-AIPFileStatus -Path \\Finance\Projectx\sales.ppdf

2. En la salida, anote los siguientes valores de parámetro:
    
   - El valor (GUID) de **SubLabelId**, si lo hay. Si este valor está en blanco, no se ha usado una subetiqueta, así que anote en su lugar el valor de **MainLabelId**.
    
     Nota: si no hay ningún valor para **MainLabelId**, el archivo no está etiquetado. En este caso, puede usar los comandos [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) y [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) en lugar de los comandos del paso 3 y 4.
    
   - El valor de **RMSTemplateId**. Si este valor tiene **acceso restringido**, significa que un usuario ha protegido el archivo mediante permisos personalizados en lugar de usar la configuración de protección que está configurada para la etiqueta. Si continúa, la configuración de protección de la etiqueta sobrescribirá esos permisos personalizados. Decida si desea continuar o pida al usuario (valor mostrado para **RMSIssuer**) que quite la etiqueta y vuelva a aplicarla, junto con sus permisos personalizados originales.

3. Quite la etiqueta mediante [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) con el parámetro *RemoveLabel*. Si va a usar la [configuración de directiva](../configure-policy-settings.md) de **Users must provide justification to set a lower classification label, remove a label, or remove protection** (Los usuarios deben proporcionar justificación para establecer una etiqueta de clasificación inferior, quitar una etiqueta o quitar la protección), debe especificar también el parámetro *Justification* con el motivo. Por ejemplo: 
    
        Set-AIPFileLabel \\Finance\Projectx\sales.ppdf -RemoveLabel -JustificationMessage 'Removing .ppdf protection to replace with .pdf ISO standard'

4. Vuelva a aplicar la etiqueta original mediante la especificación del valor de la etiqueta que identificó en el paso 1. Por ejemplo:
    
        Set-AIPFileLabel \\Finance\Projectx\sales.pdf -LabelId d9f23ae3-1234-1234-1234-f515f824c57b

El archivo conserva la extensión de nombre de archivo .pdf, pero se clasifica como antes, y se protege mediante el estándar ISO de cifrado de archivos PDF.

## <a name="support-for-files-protected-by-secure-islands"></a>Compatibilidad con los archivos protegidos por Secure Islands

Esta opción de configuración está actualmente en versión preliminar y sujeta a cambios.

Si utiliza Secure Islands para proteger documentos, es posible que, como resultado de esta protección, haya protegido los archivos de imagen y texto y los archivos protegidos genéricamente. Por ejemplo, los archivos que tienen una extensión de nombre de archivo .ptxt, .pjpeg o .pfile. Cuando el registro se edita tal y como se indica a continuación, Azure Information Protection puede descifrar estos archivos:


Agregue el siguiente valor DWORD de **EnableIQPFormats** a la siguiente ruta de acceso del registro y establezca el valor en **1**:

- Para una versión de 64 bits de Windows: HKEY_LOCAL_MACHINE\\SOFTWARE\\WOW6432Node\\Microsoft\\MSIP

- Para una versión de 32 bits de Windows: HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\MSIP

Como resultado de esta modificación del registro, se admiten los siguientes escenarios:

- El visor de Azure Information Protection puede abrir estos archivos protegidos.

- El analizador de Azure Information Protection puede examinar estos archivos en busca de información confidencial.

- El Explorador de archivos, PowerShell y el analizador de Azure Information Protection pueden etiquetar estos archivos. Como resultado, puede aplicar una etiqueta de Azure Information Protection que aplica una nueva protección de Azure Information Protection, o que quita la protección existente de Secure Islands.

- Puede usar la [personalización de etiquetas del cliente de migración](#migrate-labels-from-secure-islands-and-other-labeling-solutions) para convertir la etiqueta de Secure Islands de estos archivos protegidos en una etiqueta de Azure Information Protection.

## <a name="migrate-labels-from-secure-islands-and-other-labeling-solutions"></a>Migración de las etiquetas de Secure Islands y otras soluciones de etiquetado

Esta opción utiliza una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se debe definir en Azure Portal. Esta configuración está en versión preliminar y puede cambiar.

Esta configuración no es compatible actualmente con el comportamiento predeterminado que protege los archivos PDF mediante el estándar ISO de cifrado de archivos PDF. En este caso, los archivos .ppdf no se pueden abrir con el Explorador de archivos, PowerShell o el analizador. Para resolver este problema, use la opción del cliente avanzado para [no usar el estándar ISO para cifrado de archivos PDF](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption).

Para documentos de Office y documentos PDF etiquetados por Secure Islands, puede volver a etiquetar estos documentos con una etiqueta de Azure Information Protection mediante la asignación que defina. También se utiliza este método para reutilizar etiquetas de otras soluciones cuando sus etiquetas están en documentos de Office. 

> [!NOTE]
> Si tiene otros archivos además de documentos PDF y de Office que están protegidos por Secure Islands, puede volver a etiquetarlos después de modificar el registro tal y como se describe en la [sección anterior](#support-for-files-protected-by-secure-islands). 

Como resultado de esta opción de configuración, el cliente de Azure Information Protection aplica la nueva etiqueta de Azure Information Protection de la siguiente manera:

- Para documentos de Office: cuando el documento se abre en la aplicación de escritorio, la nueva etiqueta de Azure Information Protection se muestra como establecida y se aplica cuando se guarda el documento.

- Para el Explorador de archivos: en el cuadro de diálogo Azure Information Protection, la nueva etiqueta de Azure Information Protection se muestra como establecida y se aplica cuando el usuario selecciona **Aplicar**. Si el usuario selecciona **Cancelar**, no se aplica la nueva etiqueta.

- Para PowerShell: [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) se aplica la nueva etiqueta de Azure Information Protection. [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) no muestra la nueva etiqueta de Azure Information Protection hasta que se establece por otro método.

- Para el analizador de Azure Information Protection: la detección informa cuándo se establecerá la nueva etiqueta de Azure Information Protection y esta etiqueta se puede aplicar con el modo de aplicación.

Esta configuración requiere que especifique una configuración avanzada de cliente llamada **LabelbyCustomProperty** para cada etiqueta de Azure Information Protection que desee asignar a la etiqueta antigua. Después, para cada entrada, establezca el valor utilizando la sintaxis siguiente:

`[Azure Information Protection label ID],[migration rule name],[Secure Islands custom property name],[Secure Islands metadata Regex value]`

El valor de identificador de etiqueta se muestra en la hoja **Etiqueta**, al ver o configurar la directiva de Azure Information Protection en Azure Portal. Para especificar una subetiqueta, la etiqueta principal debe estar en el mismo ámbito o en la directiva global.

Especifique un nombre de regla de migración de su elección. Utilice un nombre descriptivo que le ayude a identificar cómo una o más etiquetas de su solución de etiquetado anterior deben asignarse a una etiqueta de Azure Information Protection. El nombre se muestra en los informes de analizador y en el Visor de eventos. 

Tenga en cuenta que esta configuración no quita los distintivos visuales que haya aplicado la etiqueta anterior. Para quitar los encabezados y los pies de página, vea la sección siguiente, [Quitar encabezados y pies de página de otras soluciones de etiquetado](#remove-headers-and-footers-from-other-labeling-solutions).

### <a name="example-1-one-to-one-mapping-of-the-same-label-name"></a>Ejemplo 1: Asignación uno a uno del mismo nombre de etiqueta

Los documentos etiquetados como "Confidencial" por Secure Islands deben volver a etiquetarse como "Confidencial" en Azure Information Protection.

En este ejemplo:

- La etiqueta de Azure Information Protection de **Confidencial** tiene un identificador de etiqueta de 1ace2cc3 14bc 4142 9125 bf946a70542c. 

- La etiqueta de Secure Islands se almacena en la propiedad personalizada denominada **Classification**.

La configuración de cliente avanzada es la siguiente:

    
|Nombre|Valor|
|---------------------|---------|
|LabelbyCustomProperty|1ace2cc3-14bc-4142-9125-bf946a70542c,"La etiqueta de Secure Islands es Confidential",Classification,Confidential|

### <a name="example-2-one-to-one-mapping-for-a-different-label-name"></a>Ejemplo 2: Asignación uno a uno para un nombre de etiqueta diferente

Los documentos etiquetados como "Confidencial" por Secure Islands se deben volver a etiquetar como "Extremadamente confidencial" en Azure Information Protection.

En este ejemplo:

- La etiqueta de Azure Information Protection **Extremadamente confidencial** tiene un identificador de etiqueta de 3e9df74d 3168 48af 8b11 037e3021813f.

- La etiqueta de Secure Islands se almacena en la propiedad personalizada denominada **Classification**.

La configuración de cliente avanzada es la siguiente:

    
|Nombre|Valor|
|---------------------|---------|
|LabelbyCustomProperty|3e9df74d-3168-48af-8b11-037e3021813f,"La etiqueta de Secure Islands es Sensitive",Classification,Sensitive|


### <a name="example-3-many-to-one-mapping-of-label-names"></a>Ejemplo 3: Asignación de varios a uno de nombres de etiqueta

Tiene dos etiquetas de Secure Islands que incluyen la palabra "Internal" y desea que los documentos que tengan cualquiera de estas etiquetas Secure Islands se vuelvan a etiquetar como "General" por Azure Information Protection.

En este ejemplo:

- La etiqueta de Azure Information Protection **General** tiene un identificador de etiqueta de 2beb8fe7 8293 444 c 9768 7fdc6f75014d.

- La etiqueta de Secure Islands se almacena en la propiedad personalizada denominada **Classification**.

La configuración de cliente avanzada es la siguiente:

    
|Nombre|Valor|
|---------------------|---------|
|LabelbyCustomProperty|2beb8fe7-8293-444c-9768-7fdc6f75014d,"La etiqueta de Secure Islands contiene Internal",Classification,.\*Internal.\*|


## <a name="remove-headers-and-footers-from-other-labeling-solutions"></a>Quitar encabezados y pies de página de otras soluciones de etiquetado

Esta opción usa diversas [opciones de configuración de cliente avanzadas](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se deben definir en Azure Portal. Esta configuración se encuentra en versión preliminar y podría cambiar.

La configuración le permite quitar o reemplazar los encabezados o pies de página basados en texto de los documentos cuando otra solución de etiquetado haya aplicado esos distintivos visuales. Por ejemplo, el pie de página anterior contiene el nombre de una etiqueta antigua que ahora se ha migrado a Azure Information Protection con un nuevo nombre de etiqueta y su propio pie de página.

Cuando el cliente recibe esta configuración en su directiva, los encabezados y pies de página antiguos se quitan o se reemplazan cuando el documento se abre en la aplicación de Office y se aplican al documento las etiquetas de Azure Information Protection existentes.

Esta configuración no es compatible con Outlook, y es necesario tener precaución al usarla con Word, Excel y PowerPoint, ya que puede afectar negativamente al rendimiento de estas aplicaciones para los usuarios. La configuración permite definir las opciones por aplicación, por ejemplo, buscar texto en los encabezados y los pies de página de documentos de Word, pero no en las hojas de cálculo de Excel ni en las presentaciones de PowerPoint.

Dado que la coincidencia de patrones afecta al rendimiento de los usuarios, se recomienda limitar los tipos de aplicaciones de Office (**W**ord, **E**xcel, **P**PowerPoint) únicamente a aquellas en las que se debe buscar:

- Clave: **RemoveExternalContentMarkingInApp**

- Valor: \<**Office application types WXP**> 

Ejemplos:

- Para buscar solo en documentos de Word, especifique **W**.

- Para buscar en documentos de Word y presentaciones de PowerPoint, especifique **WP**.

Necesita al menos otro ajuste de cliente avanzado, **ExternalContentMarkingToRemove**, para especificar el contenido del encabezado o pie de página y cómo quitarlo o reemplazarlo.

### <a name="how-to-configure-externalcontentmarkingtoremove"></a>Cómo configurar ExternalContentMarkingToRemove

Al especificar el valor de cadena para la clave **ExternalContentMarkingToRemove**, existen tres opciones que usan expresiones regulares:

- Una coincidencia parcial para quitar todo el contenido del encabezado o el pie de página.
    
    Ejemplo: los encabezados o los pies de página contienen la cadena **TEXT TO REMOVE**. Quiere quitar por completo estos encabezados o pies de página. Debe especificar el valor `*TEXT*`.

- Una coincidencia completa para quitar solo palabras específicas del encabezado o el pie de página.
    
    Ejemplo: los encabezados o los pies de página contienen la cadena **TEXT TO REMOVE**. Solo quiere quitar la palabra **TEXT**, lo que deja la cadena de encabezado o pie de página como **TO REMOVE**. Debe especificar el valor `TEXT `.

- Una coincidencia completa para quitar todo el contenido del encabezado o el pie de página.
    
    Ejemplo: los encabezados o los pies de página tienen la cadena **TEXT TO REMOVE**. Quiere quitar los encabezados o los pies de página que contienen exactamente esta cadena. Debe especificar el valor `^TEXT TO REMOVE$`.
    

La coincidencia de patrones para la cadena que especifique no distingue mayúsculas de minúsculas. La longitud de cadena máxima es de 255 caracteres.

Dado que algunos documentos podrían incluir caracteres invisibles o diferentes tipos de espacios o tabulaciones, la cadena que especifique para una palabra o frase podría no detectarse. Siempre que sea posible, especifique una sola palabra distintiva para el valor y no olvide probar los resultados antes de su implementación en la producción.

- Clave: **ExternalContentMarkingToRemove**

- Valor: \<**cadena que debe coincidir, definida como expresión regular**> 

#### <a name="multiline-headers-or-footers"></a>Encabezados o pies de página multilínea

Si el texto de un encabezado o un pie de página tiene más de una línea, debe crear una clave y un valor para cada línea. Por ejemplo, imagine que tiene el siguiente pie de página con dos líneas:

**El archivo está clasificado como confidencial**

**Etiqueta aplicada manualmente**

Para quitar este pie de página multilínea, debe crear las dos entradas siguientes:

- Clave 1: **ExternalContentMarkingToRemove**

- Valor de clave 1: **\*Confidencial***

- Clave 2: **ExternalContentMarkingToRemove**

- Valor de clave 2: **\*Etiqueta aplicada*** 

#### <a name="optimization-for-powerpoint"></a>Optimización para PowerPoint

Los pies de página de PowerPoint se implementan como formas. Para evitar la eliminación de las formas con el texto especificado que son encabezados ni pies de página, use un ajuste de cliente avanzado adicional denominado **PowerPointShapeNameToRemove**. También se recomienda usar este ajuste para evitar comprobar el texto de todas las formas, ya que es un proceso que hace un uso intensivo de recursos.

Si no especifica este ajuste de cliente avanzado adicional y PowerPoint está incluido en el valor de clave **RemoveExternalContentMarkingInApp**, se comprobarán todas las formas en busca del texto especificado en el valor  **ExternalContentMarkingToRemove**. 

Para buscar el nombre de la forma que se usa como encabezado o pie de página:

1. En PowerPoint, muestre el panel **Selección**: Pestaña **Formato** > grupo **Organizar** > **Panel de selección**.

2. Seleccione la forma en la diapositiva que contiene el encabezado o el pie de página. El nombre de la forma seleccionada aparece resaltado en el panel de **selección**.

Use el nombre de la forma de especificar un valor de cadena para la clave **PowerPointShapeNameToRemove**. 

Ejemplo: el nombre de la forma es **fc**. Para quitar la forma con este nombre, especifique el valor `fc`.

- Clave: **PowerPointShapeNameToRemove**

- Valor: \<**nombre de la forma de PowerPoint**> 

Cuando haya más de una forma de PowerPoint para quitar, cree tantas claves **PowerPointShapeNameToRemove** como formas quiera quitar. Para cada entrada, especifique el nombre de la forma que quiere quitar.

De forma predeterminada, solo se comprueban las diapositivas patrón en busca de encabezados y pies de página. Para ampliar esta búsqueda a todas las diapositivas, lo que es proceso que hace un uso mucho más intensivo de recursos, use un ajuste de cliente avanzado adicional denominada **RemoveExternalContentMarkingInAllSlides**:

- Clave: **RemoveExternalContentMarkingInAllSlides**

- Valor: **True**

## <a name="label-an-office-document-by-using-an-existing-custom-property"></a>Etiquetado de un documento de Office mediante el uso de una propiedad personalizada existente

> [!NOTE]
> Si usa esta configuración y la configuración para [migrar etiquetas de Secure Islands y otras soluciones de etiquetado](#migrate-labels-from-secure-islands-and-other-labeling-solutions), la configuración de migración de etiquetado tiene prioridad. 

Esta opción utiliza una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se debe definir en Azure Portal. 

Al configurar esta opción, puede clasificar (y, opcionalmente, proteger) un documento de Office cuando tiene una propiedad personalizada existente con un valor que coincide con uno de los nombres de etiqueta. Esta propiedad personalizada se puede establecer desde otra solución de clasificación, o bien se puede establecer como una propiedad mediante SharePoint.

Como resultado de esta configuración, cuando un usuario abre y guarda en una aplicación de Office un documento sin una etiqueta de Azure Information Protection, el documento se etiqueta para que coincida con el valor de propiedad correspondiente. 

Esta configuración requiere la especificación de dos ajustes avanzados que funcionan conjuntamente. El primero se denomina **SyncPropertyName**, y es el nombre de propiedad personalizada que se ha establecido desde la otra solución de clasificación, o una propiedad establecida mediante SharePoint. El segundo se denomina **SyncPropertyState** y debe establecerse en OneWay.

Para establecer esta configuración avanzada, especifique las cadenas siguientes:

- Clave 1: **SyncPropertyName**

- Valor de la clave 1: \<**nombre de propiedad**> 

- Clave 2: **SyncPropertyState**

- Valor de clave 2: **OneWay**

Use estas claves y los valores correspondientes solo para una propiedad personalizada.

Por ejemplo, tiene una columna de SharePoint denominada **Clasificación** con los valores posibles de **Público**, **General** y **Muy confidencial/Todos los empleados**. Los documentos se almacenan en SharePoint y tienen establecidos los valores **Público**, **General** o **Muy confidencial/Todos los empleados** para la propiedad Clasificación.

Para etiquetar un documento de Office con uno de estos valores de clasificación, establezca **SyncPropertyName** en **Clasificación** y **SyncPropertyState** en **OneWay**. 

Ahora, cuando un usuario abra y guarde uno de estos documentos de Office, se le denominará **Público**, **General** o **Muy confidencial/Todos los empleados** si tiene etiquetas con estos nombres en la directiva de Azure Information Protection. Si no tienen etiquetas con estos nombres, el documento permanecerá sin etiquetar.

## <a name="disable-the-low-integrity-level-for-the-scanner"></a>Deshabilitación del nivel de integridad bajo para el analizador

Esta opción utiliza una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se debe definir en Azure Portal.

De forma predeterminada, el analizador de Azure Information Protection se ejecuta con un nivel de integridad bajo. Esta configuración proporciona un mayor aislamiento de seguridad, pero a costa del rendimiento. Un nivel de integridad bajo es adecuado si el analizador se ejecuta con una cuenta que tiene derechos con privilegios (por ejemplo, una cuenta de administrador local) debido a que esta configuración ayuda a proteger el equipo que ejecuta el analizador.

Sin embargo, cuando la cuenta de servicio que ejecuta el analizador tiene únicamente los derechos que se documentan en la sección de [requisitos previos del analizador](../deploy-aip-scanner.md#prerequisites-for-the-azure-information-protection-scanner), el nivel de integridad bajo no es necesario, y no se recomienda porque afecta negativamente al rendimiento. 

Para obtener más información acerca de los niveles de integridad de Windows, vea [What is the Windows Integrity Mechanism?](https://msdn.microsoft.com/library/bb625957.aspx) (¿Qué es el mecanismo de integridad de Windows?).

Para configurar este valor avanzado de modo que el analizador se ejecute con un nivel de integridad asignado automáticamente por Windows (una cuenta de usuario estándar se ejecuta con un nivel de integridad medio), especifique las siguientes cadenas:

- Clave: **ProcessUsingLowIntegrity**

- Valor: **False**


## <a name="change-the-local-logging-level"></a>Cambio del nivel de registro local

Esta opción utiliza una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se debe definir en Azure Portal.

De forma predeterminada, el cliente de Azure Information Protection escribe los archivos de registro del cliente en la carpeta **%localappdata%\Microsoft\MSIP**. Estos archivos están diseñados para solución de problemas por parte del Soporte técnico de Microsoft.
 
Para cambiar el nivel de registro de estos archivos, configure el siguiente parámetro de cliente avanzado:

- Clave: **LogLevel**

- Valor: **\<Nivel de registro>**

Establezca el nivel de registro en uno de los siguientes valores:

- **Desactivada**: Ningún registro local.

- **Error**: Solo errores.

- **Información**: Registro mínimo, que no incluye ningún identificador de evento.

- **Depurar**: Toda la información (el valor predeterminado).

- **Seguimiento**: Registro muy detallado que afecta al rendimiento y debe habilitarse solo si lo solicita el Soporte técnico de Microsoft. Si le piden que establezca este nivel de registro, recuerde establecer un valor diferente cuando se hayan recopilado los registros pertinentes.

Esta configuración de cliente avanzada no cambia la información que se envía a Azure Information Protection para la creación de [informes centrales](../reports-aip.md), ni cambia la información que se escribe en el [registro de eventos](client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client) local.

## <a name="integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution"></a>Integración con la clasificación de mensajes de Exchange para una solución de etiquetado de dispositivo móvil

A pesar de que Outlook en la Web todavía no es compatible de forma nativa con la clasificación y la protección de Azure Information Protection, puede usar la clasificación de mensajes de Exchange para extender las etiquetas de Azure Information Protection a los usuarios móviles cuando usan Outlook en la Web. Outlook Mobile no admite la clasificación de mensajes de Exchange.

Para lograr esta solución: 

1. Use el cmdlet [New-MessageClassification](https://technet.microsoft.com/library/bb124400) de Exchange PowerShell para crear clasificaciones de mensajes con la propiedad Name que se asigna a los nombres de sus etiquetas en la directiva de Azure Information Protection. 

2. Cree una regla de flujo de correo de Exchange para cada etiqueta: aplique la regla cuando las propiedades del mensaje incluyan la clasificación que ha configurado, y modifique las propiedades del mensaje para establecer un encabezado de mensaje. 

     En el caso del encabezado del mensaje, encontrará la información que es necesario especificar al inspeccionar los encabezados de Internet de un correo electrónico que haya enviado y clasificado con una etiqueta de Azure Information Protection. Busque el encabezado **msip_labels** y la cadena inmediatamente posterior, hasta e incluido el punto y coma. Por ejemplo:
    
    **msip_labels: MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;**
    
    Luego, para el encabezado del mensaje en la regla, especifique **msip_labels** para el encabezado y el resto de la cadena para el valor del encabezado. Por ejemplo:
    
    ![Ejemplo de regla de flujo de correo de Exchange Online que establece el encabezado del mensaje para una etiqueta de Azure Information Protection](../media/exchange-rule-for-message-header.png)
    
    Nota: Cuando la etiqueta es una subetiqueta, también debe especificar la etiqueta principal antes de la subetiqueta en el valor de encabezado, con el mismo formato. Por ejemplo, si su subetiqueta tiene un GUID de 27efdf94-80a0-4d02-b88c-b615c12d69a9, su valor podría tener un aspecto similar al siguiente: `MSIP_Label_ab70158b-bdcc-42a3-8493-2a80736e9cbd_Enabled=True;MSIP_Label_27efdf94-80a0-4d02-b88c-b615c12d69a9_Enabled=True;`

Antes de probar esta configuración, recuerde que, al crear o editar reglas de flujo de correo, normalmente se produce un retraso (espere una hora, por ejemplo). Cuando se aplica la regla y los usuarios usan Outlook en la Web o un cliente de dispositivo móvil que admite IRM de Exchange ActiveSync: 

- Los usuarios seleccionan la clasificación de mensajes de Exchange y envían el correo electrónico.

- La regla de Exchange detecta la clasificación de Exchange y, en función de esta, modifica el encabezado del mensaje para agregar la clasificación de Azure Information Protection.

- Cuando los destinatarios internos ven el correo electrónico en Outlook y tienen instalado el cliente de Azure Information Protection, verán asignada la etiqueta de Azure Information Protection. 

Si las etiquetas de Azure Information Protection aplican protección, agregue dicha protección a la configuración de reglas: Seleccione la opción para modificar la seguridad del mensaje, aplique la protección de derechos y después seleccione la plantilla de RMS o la opción No reenviar.

También puede configurar reglas de flujo de correo para realizar la asignación inversa. Cuando se detecta una etiqueta de Azure Information Protection, se establece una clasificación de mensajes de Exchange correspondiente.

- Para cada etiqueta de Azure Information Protection: cree una regla de flujo de correo que se aplique cuando el encabezado **msip_labels** incluya el nombre de la etiqueta (por ejemplo, **General**) y aplique una clasificación de mensajes que se asigne a ella.


## <a name="next-steps"></a>Pasos siguientes
Ahora que personalizó el cliente de Azure Information Protection, consulte en los siguientes recursos información adicional que puede necesitar para la compatibilidad con este cliente:

- [Archivos de cliente y registro de uso](client-admin-guide-files-and-logging.md)

- [Seguimiento de documentos](client-admin-guide-document-tracking.md)

- [Tipos de archivos admitidos](client-admin-guide-file-types.md)

- [Comandos de PowerShell](client-admin-guide-powershell.md)


