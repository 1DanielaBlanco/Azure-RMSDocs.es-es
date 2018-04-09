---
title: Configuraciones personalizadas del cliente de Azure Information Protection
description: Información sobre cómo personalizar el cliente de Azure Information Protection para Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/02/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 08412c2c1cf1182b6d8bdae6e68d53d0b46f4b41
ms.sourcegitcommit: b17432ed155394111c878eb57b5fa7adf9df9755
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2018
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-client"></a>Guía del administrador: Configuraciones personalizadas del cliente de Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2*

Use la siguiente información para configuraciones avanzadas que podría necesitar para escenarios específicos o un subconjunto de usuarios cuando administre el cliente de Azure Information Protection.

Algunas de estas opciones requieren la modificación del Registro y otras usan la configuración avanzada que debe configurar en Azure Portal y, después, publicarlas para que los clientes las descarguen.  

### <a name="how-to-configure-advanced-client-configuration-settings-in-the-portal"></a>Cómo establecer opciones de configuración de cliente avanzadas en el portal

1. Si aún no lo ha hecho, en una nueva ventana del explorador, [inicie sesión en Azure Portal](../deploy-use/configure-policy.md#signing-in-to-the-azure-portal) y, después, vaya hasta la hoja **Azure Information Protection**.

2. En la hoja inicial de Azure Information Protection, seleccione **Directivas con ámbito**.

3. En la hoja **Azure Information Protection - Directivas con ámbito**, seleccione el menú contextual (**...** ) junto a la directiva para que contenga la configuración avanzada. Después, seleccione **Configuración avanzada**.
    
    Puede establecer la configuración avanzada para la directiva global, así como para las directivas con ámbito.

4. En la hoja **Configuración avanzada**, escriba el nombre y el valor de la configuración avanzada y, después, seleccione **Guardar y cerrar**.

5. Haga clic en **Publicar** y asegúrese de que los usuarios de esta directiva reinician las aplicaciones de Office que hubieran abierto.

6. Si ya no necesita la configuración y desea revertir al comportamiento predeterminado: en la hoja **Configuración avanzada**, seleccione el menú contextual (**...** ) situado junto a la configuración que ya no necesita y, después, seleccione **Eliminar**. Ahora, haga clic en **Guardar y cerrar** y vuelva a publicar la directiva modificada.

## <a name="prevent-sign-in-prompts-for-ad-rms-only-computers"></a>Evitar solicitudes de inicio de sesión solo para equipos AD RMS

De forma predeterminada, el cliente de Azure Information Protection intenta conectarse automáticamente al servicio Azure Information Protection. Para equipos que solo establecen comunicación con AD RMS, esta configuración puede producir una solicitud de inicio de sesión para los usuarios que no es necesaria. Se puede evitar esta solicitud de inicio de sesión modificando el registro:

Busque el siguiente nombre de valor y después establezca los datos del valor en **0**:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Independientemente de esta configuración, el cliente de Azure Information Protection sigue el [proceso de detección del servicio de RMS](../rms-client/client-deployment-notes.md#rms-service-discovery) estándar para buscar su clúster de AD RMS.

## <a name="suppress-the-initial-congratulations-welcome-page"></a>Supresión de la página inicial de "Enhorabuena" página principal

Cuando el cliente de Azure Information Protection se instala por primera vez en un equipo y un usuario abre Word, Excel, PowerPoint o Outlook, aparece una página de **Enhorabuena** con instrucciones breves sobre cómo usar la nueva barra de Information Protection para seleccionar las etiquetas. Puede suprimir esta página editando el registro.

Busque el siguiente nombre de valor y establezca los datos del valor en **0**:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnableWelcomeExperience** 


## <a name="sign-in-as-a-different-user"></a>Inicio de sesión como un usuario diferente

En un entorno de producción, los usuarios normalmente no necesitarán iniciar sesión como un usuario diferente cuando estén utilizando el cliente de Azure Information Protection. No obstante, como administrador, es posible que tenga que iniciar sesión como un usuario diferente durante la fase de pruebas. 

Puede comprobar con qué cuenta ha iniciado sesión en el cuadro de diálogo **Microsoft Azure Information Protection**: abra una aplicación de Office y, en la pestaña **Inicio** del grupo **Protección**, haga clic en **Proteger** y finalmente en **Ayuda y comentarios**. El nombre de cuenta se muestra en la sección **Estado del cliente**.

Asegúrese de comprobar el nombre de dominio de la cuenta de inicio de sesión que se muestra. Puede ser fácil no darse cuenta de que inició sesión con el nombre de cuenta correcto, pero con un dominio incorrecto. Un síntoma de usar una cuenta incorrecta podría ser no poder descargar la directiva de Azure Information Protection o no verse las etiquetas de comportamiento esperadas.

Para iniciar sesión como un usuario diferente:

1. Vaya a **%localappdata%\Microsoft\MSIP** y elimine el archivo **TokenCache**.

2. Reinicie todas las aplicaciones de Office abiertas e inicie sesión con su cuenta de usuario diferente. Si no ve un mensaje en la aplicación de Office para iniciar sesión en el servicio Azure Information Protection, vuelva al cuadro de diálogo **Microsoft Azure Information Protection** y haga clic en **Iniciar sesión** desde la sección **Estado del cliente** actualizada.

Además:

- Esta solución se admite para iniciar sesión como otro usuario desde el mismo inquilino. No se admite para iniciar sesión como otro usuario desde un inquilino diferente. Para probar Azure Information Protection con varios inquilinos, use equipos diferentes.

- Si utiliza el inicio de sesión único, debe cerrar la sesión de Windows e iniciar sesión con su cuenta de usuario diferente después de editar el registro. El cliente Azure Information Protection se autentica entonces automáticamente mediante la cuenta de usuario que tiene iniciada sesión actualmente.

- Puede usar la opción **Restablecer configuración** de **Ayuda y comentarios** para cerrar sesión y eliminar la directiva de Azure Information Protection descargada.


## <a name="enforce-protection-only-mode-when-your-organization-has-a-mix-of-licenses"></a>Exigencia del modo de solo protección cuando la organización tiene una combinación de licencias

Si la organización no tiene ninguna licencia de Azure Information Protection, pero tiene licencias de Office 365 que incluyen el servicio de Azure Rights Management para la protección de datos, el cliente de Azure Information Protection para Windows se ejecuta automáticamente en [el modo de solo protección](../rms-client/client-protection-only-mode.md).

Sin embargo, si la organización tiene una suscripción para Azure Information Protection, de forma predeterminada todos los equipos Windows pueden descargar la directiva de Azure Information Protection. El cliente de Azure Information Protection no lleva a cabo la comprobación de licencias ni el cumplimiento. 

Si tiene algunos usuarios que no tiene una licencia de Azure Information Protection, pero sí una licencia de Office 365 que incluye el servicio de Azure Rights Management, edite el Registro en los equipos de estos usuarios para impedir que dichos usuarios ejecuten las características de clasificación y etiquetado sin licencia de Azure Information Protection.

Busque el siguiente nombre de valor y establezca los datos del valor en **0**:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Además, compruebe que estos equipos no tienen un archivo denominado **Policy.msip** en la carpeta **%LocalAppData%\Microsoft\MSIP**. Si el archivo existe, elimínelo. Este archivo contiene la directiva de Azure Information Protection y podría haberse descargado antes de que editara el Registro, o si el cliente de Azure Information Protection se instaló con la opción de demostración.

## <a name="hide-the-classify-and-protect-menu-option-in-windows-file-explorer"></a>Ocultación de la opción de menú Clasificar y Proteger en el Explorador de archivos de Windows

Cree el siguiente nombre de valor DWORD (con cualquier datos de valor):

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

## <a name="support-for-disconnected-computers"></a>Soporte técnico para equipos desconectados

De forma predeterminada, el cliente de Azure Information Protection intenta conectarse automáticamente al servicio Azure Information Protection para descargar la directiva más reciente de Azure Information Protection. Si tiene un equipo que sabe que no se podrá conectar a Internet durante un período de tiempo, puede impedir que el cliente intente conectarse al servicio editando el Registro. 

Busque el siguiente nombre de valor y establezca los datos del valor en **0**:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Asegúrese de que el cliente tenga un archivo de directiva válido denominado **Policy.msip** en la carpeta **%LocalAppData%\Microsoft\MSIP**. Si es necesario, puede exportar la directiva desde Azure Portal y copiar el archivo exportado en el equipo cliente. También puede utilizar este método para reemplazar un archivo de directiva no actualizado con la directiva publicada más reciente.

Al exportar la directiva, esta acción descarga un archivo comprimido con varias versiones de la directiva que se corresponden a las distintas versiones del cliente de Azure Information Protection:

1. Descomprima el archivo y use la tabla siguiente para identificar qué archivo de directiva necesita. 
    
    |Nombre de archivo|Versión de cliente correspondiente|
    |--------------------------|---------------------------------------------|
    |Policy1.1.msip |Versión 1.2|
    |Policy1.2.msip |Versión 1.3 - 1.7|
    |Policy1.3.msip |Versión 1.8 y posteriores|
    
2. Cambie el nombre del archivo identificado a **Policy.msip** y, después, cópielo en la carpeta **%LocalAppData%\Microsoft\MSIP** en equipos que tengan instalado el cliente de Azure Information Protection. 


## <a name="hide-or-show-the-do-not-forward-button-in-outlook"></a>Mostrar u ocultar el botón No reenviar en Outlook

El método recomendado para configurar esta opción es mediante la [configuración de directiva](../deploy-use/configure-policy-settings.md) **Agregar el botón No reenviar a la cinta de Outlook**. Sin embargo, también puede configurar esta opción mediante una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se establece en Azure Portal.

Al establecer esta configuración, se oculta o se muestra el botón **No reenviar** en la cinta de Outlook. Esta configuración no tiene ningún efecto en la opción No reenviar en los menús de Office.

Para establecer esta configuración avanzada, especifique las cadenas siguientes:

- Clave: **DisableDNF**

- Valor: **True** para ocultar el botón o **False** para mostrarlo.

## <a name="make-the-custom-permissions-options-available-or-unavailable-to-users"></a>Configuración de las opciones de permisos personalizados para que estén disponibles o no disponibles para los usuarios

El método recomendado para configurar esta opción es mediante la [configuración de directiva](../deploy-use/configure-policy-settings.md) **Configuración de la opción de permisos personalizados para que esté disponible para los usuarios**. Sin embargo, también puede configurar esta opción mediante una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se establece en Azure Portal. 

Cuando establece esta configuración y publica la directiva para los usuarios, las opciones de permisos personalizados están disponibles para que los usuarios seleccionen su propia configuración de protección o dejan de estar disponibles para que los usuarios no puedan seleccionar su propia configuración de protección a menos que se les solicite.

Para establecer esta configuración avanzada, especifique las cadenas siguientes:

- Clave: **EnableCustomPermissions**

- Valor: **True** para hacer que la opción de permisos personalizados esté disponible, o bien **False** para que esta opción no esté disponible

> [!IMPORTANT]
> A menos que use la versión preliminar actual del cliente, no establezca esta opción en **False** si tiene etiquetas configuradas para permisos definidos por el usuario para Word, Excel, PowerPoint y el Explorador de archivos. Si lo hace, cuando se aplique la etiqueta, no se les pedirá a los usuarios que configuren los permisos personalizados. Como resultado, el documento se etiquetará, pero no se protegerá como estaba previsto.

## <a name="permanently-hide-the-azure-information-protection-bar"></a>Ocultación de manera permanente de la barra de Azure Information Protection

Esta opción utiliza una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se debe definir en Azure Portal. Úsela solo cuando la [configuración de directiva](../deploy-use/configure-policy-settings.md) **Mostrar la barra de Information Protection en las aplicaciones de Office** está establecida en **Activado**.

Cuando se establece esta configuración y se publica la directiva para los usuarios, y un usuario decide no mostrar la barra de Azure Information Protection en sus aplicaciones de Office, la barra permanece oculta. Esto ocurre cuando el usuario desactiva la opción **Mostrar barra** en la pestaña **Inicio**, grupo **Protección** , botón **Proteger**. Esta configuración no tiene ningún efecto si el usuario cierra la barra utilizando el icono **Cerrar esta barra**.

Aunque la barra de Azure Information Protection permanece oculta, los usuarios todavía pueden seleccionar una etiqueta de la barra mostrada de manera temporal si se ha configurado la clasificación recomendada, o si el documento o correo electrónico debe tener una etiqueta. 

Para establecer esta configuración avanzada, especifique las cadenas siguientes:

- Clave: **EnableBarHiding**

- Valor: **True**


## <a name="enable-recommended-classification-in-outlook"></a>Habilitación de la clasificación recomendada en Outlook

Esta opción de configuración está actualmente en versión preliminar y sujeta a cambios.

Esta opción utiliza una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se debe definir en Azure Portal.

Al configurar una etiqueta para la clasificación recomendada, se pide a los usuarios que acepten o descarten la etiqueta recomendada en Word, Excel y PowerPoint. Esta opción extiende esta recomendación de etiqueta para mostrarse también en Outlook.

Para establecer esta configuración avanzada, especifique las cadenas siguientes:

- Clave: **OutlookRecommendationEnabled**

- Valor: **True**


## <a name="set-a-different-default-label-for-outlook"></a>Establecimiento de otra etiqueta predeterminada para Outlook

Esta opción de configuración está actualmente en versión preliminar y sujeta a cambios. Además, esta opción de configuración necesita la versión preliminar del cliente.

Esta opción utiliza una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se debe definir en Azure Portal. 

Al configurar esta opción, Outlook no aplica la etiqueta predeterminada configurada en la directiva de Azure Information Protection para la opción **Seleccione la etiqueta predeterminada**. Por el contrario, Outlook puede aplicar otra etiqueta predeterminada o ninguna.

Para aplicar otra etiqueta, debe especificar el identificador de etiqueta. El valor de identificador de etiqueta se muestra en la hoja **Etiqueta**, al ver o configurar la directiva de Azure Information Protection en Azure Portal. En el caso de los archivos que tienen etiquetas aplicadas, también puede ejecutar el cmdlet de PowerShell [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) para reconocer el identificador de etiqueta (MainLabelId o SubLabelId). Si una etiqueta tiene subetiquetas, especifique únicamente el identificador de una subetiqueta, no el de la etiqueta principal.

Para que Outlook no aplique la etiqueta predeterminada, especifique **Ninguna**.

Para establecer esta configuración avanzada, especifique las cadenas siguientes:

- Clave: **OutlookDefaultLabel**

- Valor: \<**Identificador de etiqueta**> o **Ninguna**

## <a name="turn-off-classification-running-continuously-in-the-background"></a>Desactivación de la clasificación que se ejecuta continuamente en segundo plano

Esta opción de configuración está actualmente en versión preliminar y sujeta a cambios. Además, esta opción de configuración necesita la versión preliminar del cliente.

Esta opción utiliza una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se debe definir en Azure Portal. 

Cuando define esta configuración, la versión preliminar del cliente de Azure Information Protection no comprueba periódicamente los documentos en busca de las reglas de condición que especifique. En su lugar, se aplican las etiquetas automáticas y recomendadas del [mismo modo que la versión de disponibilidad general del cliente de Azure Information Protection](../deploy-use/configure-policy-classification.md#how-automatic-or-recommended-labels-are-applied). Esta configuración podría ser necesaria por motivos de rendimiento.

Para establecer esta configuración avanzada, especifique las cadenas siguientes:

- Clave: **RunPolicyInBackground**

- Valor: **False**

## <a name="migrate-labels-from-secure-islands-and-other-labeling-solutions"></a>Migración de las etiquetas de Secure Islands y otras soluciones de etiquetado

Esta opción de configuración está actualmente en versión preliminar y sujeta a cambios. Además, esta opción de configuración necesita la versión preliminar del cliente o el analizador de Azure Information Protection.

Esta opción utiliza una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se debe definir en Azure Portal. 

Para documentos de Office y documentos PDF etiquetados por Secure Islands, puede volver a etiquetar estos documentos con una etiqueta de Azure Information Protection mediante la asignación que defina. También se utiliza este método para reutilizar etiquetas de otras soluciones cuando sus etiquetas están en documentos de Office. 

Como resultado de esta opción de configuración, el cliente de Azure Information Protection aplica la nueva etiqueta de Azure Information Protection de la siguiente manera:

- Para documentos Office: cuando el documento se abre en la aplicación de escritorio, la nueva etiqueta de Azure Information Protection se muestra como establecida y se aplica cuando se guarda el documento.

- Para el Explorador de archivos: en el cuadro de diálogo Azure Information Protection, la nueva etiqueta de Azure Information Protection se muestra como establecida y se aplica cuando el usuario selecciona **Aplicar**. Si el usuario selecciona **Cancelar**, no se aplica la nueva etiqueta.

- Para PowerShell: [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) se aplica la nueva etiqueta de Azure Information Protection. [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) no muestra la nueva etiqueta de Azure Information Protection hasta que se establece por otro método.

- Para el analizador de Azure Information Protection: la detección informa cuándo se establecerá la nueva etiqueta de Azure Information Protection y esta etiqueta se puede aplicar con el modo de aplicación.

Esta configuración requiere que especifique una configuración avanzada de cliente llamada **LabelbyCustomProperty** para cada etiqueta de Azure Information Protection que desee asignar a la etiqueta antigua. Después, para cada entrada, establezca el valor utilizando la sintaxis siguiente:

`[Azure Information Protection label ID],[migration rule name],[Secure Islands custom property name],[Secure Islands metadata Regex value]`

El valor de identificador de etiqueta se muestra en la hoja **Etiqueta**, al ver o configurar la directiva de Azure Information Protection en Azure Portal. Para especificar una subetiqueta, la etiqueta principal debe estar en el mismo ámbito o en la directiva global.

Especifique un nombre de regla de migración de su elección. Utilice un nombre descriptivo que le ayude a identificar cómo una o más etiquetas de su solución de etiquetado anterior deben asignarse a una etiqueta de Azure Information Protection. El nombre se muestra en los informes de analizador y en el Visor de eventos. 

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


## <a name="label-an-office-document-by-using-an-existing-custom-property"></a>Etiquetado de un documento de Office mediante el uso de una propiedad personalizada existente

Esta opción de configuración está actualmente en versión preliminar y sujeta a cambios.

> [!NOTE]
> Si utiliza esta configuración y la configuración de la sección anterior para migrar desde otra solución de etiquetado, la configuración de migración de etiquetado tiene prioridad. 

Esta opción utiliza una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se debe definir en Azure Portal. 

Al configurar esta opción, puede clasificar (y, opcionalmente, proteger) un documento de Office cuando tiene una propiedad personalizada existente con un valor que coincide con uno de los nombres de etiqueta. Esta propiedad personalizada se puede establecer desde otra solución de clasificación, o bien se puede establecer como una propiedad mediante SharePoint.

Como resultado de esta configuración, cuando un usuario abre y guarda en una aplicación de Office un documento sin una etiqueta de Azure Information Protection, el documento se etiqueta para que coincida con el valor de propiedad correspondiente. 

Esta configuración requiere la especificación de dos ajustes avanzados que funcionan conjuntamente. El primero se denomina **SyncPropertyName**, y es el nombre de propiedad personalizada que se ha establecido desde la otra solución de clasificación, o una propiedad establecida mediante SharePoint. El segundo se denomina **SyncPropertyState** y debe establecerse en OneWay.

Para establecer esta configuración avanzada, especifique las cadenas siguientes:

- Clave 1: **SyncPropertyName**

- Valor de la clave 1: \<**nombre de propiedad**> 

- Clave 2: **SyncPropertyState**

- Valor de la clave 2: **OneWay**

Use estas claves y los valores correspondientes solo para una propiedad personalizada.

Por ejemplo, tiene una columna de SharePoint denominada **Clasificación** con los valores posibles de **Público**, **General** y **Confidencial**. Los documentos se almacenan en SharePoint y tienen uno de estos valores establecidos para la propiedad de clasificación.

Para etiquetar un documento de Office con uno de estos valores de clasificación, establezca **SyncPropertyName** en **Clasificación** y **SyncPropertyState** en **OneWay**. 

Ahora, cuando un usuario abra y guarde uno de estos documentos de Office, se denomina **Público**, **General** o **Confidencial** si tiene etiquetas con estos nombres en la directiva de Azure Information Protection. Si no tienen etiquetas con estos nombres, el documento permanecerá sin etiquetar.

## <a name="integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution"></a>Integración con la clasificación de mensajes de Exchange para una solución de etiquetado de dispositivo móvil

A pesar de que Outlook en la Web todavía no es compatible de forma nativa con la clasificación y la protección de Azure Information Protection, puede usar la clasificación de mensajes de Exchange para extender las etiquetas de Azure Information Protection a los usuarios móviles cuando usan Outlook en la Web. Outlook Mobile no admite la clasificación de mensajes de Exchange.

Para lograr esta solución: 

1. Use el cmdlet [New-MessageClassification](https://technet.microsoft.com/library/bb124400) de Exchange PowerShell para crear clasificaciones de mensajes con la propiedad Name que se asigna a los nombres de sus etiquetas en la directiva de Azure Information Protection. 

2. Cree una regla de flujo de correo de Exchange para cada etiqueta. Aplique la regla cuando las propiedades del mensaje incluyan la clasificación que ha configurado, y modifique las propiedades del mensaje para establecer un encabezado de mensaje. 

    En el caso del encabezado del mensaje, encontrará la información que es necesario especificar al inspeccionar los encabezados de Internet de un correo electrónico que haya enviado y clasificado con una etiqueta de Azure Information Protection. Busque el encabezado **msip_labels** y la cadena inmediatamente posterior, hasta e incluido el punto y coma. En el ejemplo anterior:
    
    **msip_labels: MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;**
    
    Luego, para el encabezado del mensaje en la regla, especifique **msip_labels** para el encabezado y el resto de la cadena para el valor del encabezado. Por ejemplo:
    
    ![Ejemplo de regla de flujo de correo de Exchange Online que establece el encabezado del mensaje para una etiqueta de Azure Information Protection](../media/exchange-rule-for-message-header.png)

Antes de probar esta configuración, recuerde que, al crear o editar reglas de flujo de correo, normalmente se produce un retraso (espere una hora, por ejemplo). Cuando se aplica la regla y los usuarios usan Outlook en la Web o un cliente de dispositivo móvil que admite IRM de Exchange ActiveSync: 

- Los usuarios seleccionan la clasificación de mensajes de Exchange y envían el correo electrónico.

- La regla de Exchange detecta la clasificación de Exchange y, en función de esta, modifica el encabezado del mensaje para agregar la clasificación de Azure Information Protection.

- Cuando los destinatarios ven el correo electrónico en Outlook y tienen instalado el cliente de Azure Information Protection, verán asignada la etiqueta de Azure Information Protection, así como los correspondientes encabezado, pie de página o marca de agua del correo electrónico. 

Si las etiquetas de Azure Information Protection aplican protección, agregue dicha protección a la configuración de reglas: seleccione la opción para modificar la seguridad de los mensajes, aplique la protección de derechos y luego seleccione la plantilla de RMS o la opción No reenviar.

También puede configurar reglas de flujo de correo para realizar la asignación inversa. Cuando se detecta una etiqueta de Azure Information Protection, se establece una clasificación de mensajes de Exchange correspondiente.

- Para cada etiqueta de Azure Information Protection, cree una regla de flujo de correo que se aplique cuando el encabezado **msip_labels** incluya el nombre de la etiqueta (por ejemplo, **General**) y aplique una clasificación de mensajes que se asigne a ella.


## <a name="next-steps"></a>Pasos siguientes
Ahora que personalizó el cliente de Azure Information Protection, consulte en los siguientes recursos información adicional que puede necesitar para la compatibilidad con este cliente:

- [Archivos de cliente y registro de uso](client-admin-guide-files-and-logging.md)

- [Seguimiento de documentos](client-admin-guide-document-tracking.md)

- [Tipos de archivos admitidos](client-admin-guide-file-types.md)

- [Comandos de PowerShell](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
