---
title: Configuraciones personalizadas del cliente de Azure Information Protection
description: "Información sobre cómo personalizar el cliente de Azure Information Protection para Windows."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 9e7e5e67b664d177f60a445aa54df3f6072ff9c7
ms.sourcegitcommit: 13e95906c24687eb281d43b403dcd080912c54ec
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2017
---
# <a name="custom-configurations-for-the-azure-information-protection-client"></a>Configuraciones personalizadas del cliente de Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Use la siguiente información para configuraciones avanzadas que podría necesitar para escenarios específicos o un subconjunto de usuarios cuando administre el cliente de Azure Information Protection.

Algunas de estas opciones requieren la modificación del Registro y otras usan la configuración avanzada que debe configurar en Azure Portal y, después, publicarlas para que los clientes las descarguen. Además, es posible que algunas configuraciones solo estén en una versión preliminar del cliente de Azure Information Protection. Para esta configuración, se documenta una versión mínima de cliente. En el caso de las configuraciones que se admiten en la versión de disponibilidad general del cliente, no se documenta ningún número de versión mínimo de cliente.

### <a name="how-to-configure-advanced-client-configuration-settings-in-the-portal"></a>Cómo establecer opciones de configuración de cliente avanzadas en el portal

Esta configuración está actualmente en versión preliminar.

1. Si aún no lo ha hecho, abra una nueva ventana del explorador, inicie sesión en [Azure Portal](https://portal.azure.com) como administrador de seguridad o administrador global y, después, navegue hasta la hoja **Azure Information Protection**.

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

## <a name="sign-in-as-a-different-user"></a>Inicio de sesión como un usuario diferente

En un entorno de producción, los usuarios normalmente no necesitarán iniciar sesión como un usuario diferente cuando estén utilizando el cliente de Azure Information Protection. No obstante, como administrador, es posible que tenga que iniciar sesión como un usuario diferente durante la fase de pruebas. 

Puede comprobar con qué cuenta ha iniciado sesión en el cuadro de diálogo **Microsoft Azure Information Protection**: abra una aplicación de Office y, en la pestaña **Inicio** del grupo **Protección**, haga clic en **Proteger** y finalmente en **Ayuda y comentarios**. El nombre de cuenta se muestra en la sección **Estado del cliente**.

Asegúrese de comprobar el nombre de dominio de la cuenta de inicio de sesión que se muestra. Puede ser fácil no darse cuenta de que inició sesión con el nombre de cuenta correcto, pero con un dominio incorrecto. Un síntoma de usar una cuenta incorrecta podría ser no poder descargar la directiva de Azure Information Protection o no verse las etiquetas de comportamiento esperadas.

Para iniciar sesión como un usuario diferente:

1. En función de la versión del cliente de Azure Information Protection: 
    
    - Para la versión de disponibilidad general del cliente de Azure Information Protection: mediante un editor del Registro, vaya a **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP** y elimine el valor **TokenCache** (y sus datos de valores asociados).
    
    - Para la versión preliminar actual del cliente de Azure Information Protection: vaya a **%localappdata%\Microsoft\MSIP** y elimine el archivo **TokenCache**.

2. Reinicie todas las aplicaciones de Office abiertas e inicie sesión con su cuenta de usuario diferente. Si no ve un mensaje en la aplicación de Office para iniciar sesión en el servicio Azure Information Protection, vuelva al cuadro de diálogo **Microsoft Azure Information Protection** y haga clic en **Iniciar sesión** desde la sección **Estado del cliente** actualizada.

Además:

- Esta solución se admite para iniciar sesión como otro usuario desde el mismo inquilino. No se admite para iniciar sesión como otro usuario desde un inquilino diferente. Para probar Azure Information Protection con varios inquilinos, use equipos diferentes.

- Si utiliza el inicio de sesión único, debe cerrar la sesión de Windows e iniciar sesión con su cuenta de usuario diferente después de editar el registro. El cliente Azure Information Protection se autentica entonces automáticamente mediante la cuenta de usuario que tiene iniciada sesión actualmente.

- Si desea restablecer la configuración de usuario para el servicio Azure Rights Management, puede hacerlo mediante el uso de la opción **Ayuda y comentarios**.

- Si desea eliminar la directiva actualmente descargada de Azure Information Protection, elimine el archivo **Policy.msip** de la carpeta **%localappdata%\Microsoft\MSIP**.

- Si tiene la versión preliminar actual del cliente de Azure Information Protection, puede usar la opción **Restablecer configuración** de **Ayuda y comentarios** para cerrar sesión y eliminar la directiva de Azure Information Protection descargada actualmente.

## <a name="hide-the-classify-and-protect-menu-option-in-windows-file-explorer"></a>Ocultación de la opción de menú Clasificar y Proteger en el Explorador de archivos de Windows

Esta opción de configuración está actualmente en versión preliminar.

Puede definir esta configuración avanzada editando el Registro cuando tenga la versión 1.3.0.0 del cliente de Azure Information Protection o una versión superior. 

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


## <a name="hide-the-do-not-forward-button-in-outlook"></a>Ocultación del botón No reenviar en Outlook

Esta opción de configuración está actualmente en versión preliminar.

Esta opción utiliza una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se debe definir en Azure Portal. Esta configuración también requiere una versión preliminar del cliente de Azure Information Protection con una versión mínima de **1.8.41.0**.

Al establecer esta configuración, se oculta el botón **No reenviar** en la cinta de Outlook. No se oculta esta opción en los menús de Office.

Para establecer esta configuración avanzada, especifique las cadenas siguientes:

- Clave: **DisableDNF**

- Valor: **True**

## <a name="make-the-custom-permissions-options-unavailable-to-users"></a>Configuración de opciones de permisos personalizados para que no estén disponibles a los usuarios

Esta opción de configuración está actualmente en versión preliminar.

> [!IMPORTANT]
> No use esta opción si tiene etiquetas que están configuradas para permisos definidos por el usuario para Word, Excel, PowerPoint y el Explorador de archivos. Si lo hace, cuando se aplique la etiqueta, no se les pedirá a los usuarios que configuren los permisos personalizados. Como resultado, el documento se etiquetará, pero no se protegerá como estaba previsto.

Esta opción utiliza una [configuración de cliente avanzada](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que se debe definir en Azure Portal. 

Cuando establece esta configuración y publica la directiva para los usuarios, las opciones de permisos personalizados de las ubicaciones siguientes dejarán de estar disponibles para su selección por los usuarios:

- En las aplicaciones Office: pestaña **Inicio** > grupo **Protección** > **Proteger** > **Permisos personalizados**

- En el Explorador de archivos: haga clic con el botón derecho > **Clasificar y proteger** > **Permisos personalizados**

Esta configuración no tiene ningún efecto en los permisos personalizados que se pueden configurar en las opciones de menú de Office. 

Para establecer esta configuración avanzada, especifique las cadenas siguientes:

- Clave: **EnableCustomPermissions**

- Valor: **False**

## <a name="permanently-hide-the-azure-information-protection-bar"></a>Ocultación de manera permanente de la barra de Azure Information Protection

Esta opción utiliza una configuración avanzada que se debe definir en Azure Portal. Esta configuración también requiere una versión preliminar del cliente de Azure Information Protection con una versión mínima de **1.9.58.0**.

Cuando se establece esta configuración y se publica la directiva para los usuarios, y un usuario decide no mostrar la barra de Azure Information Protection en sus aplicaciones de Office, la barra permanece oculta. Esto ocurre cuando el usuario desactiva la opción **Mostrar barra** en la pestaña **Inicio**, grupo **Protección** , botón **Proteger**. Esta configuración no tiene ningún efecto si el usuario cierra la barra utilizando el icono **Cerrar esta barra**.

Aunque la barra de Azure Information Protection permanece oculta, los usuarios todavía pueden seleccionar una etiqueta de la barra mostrada de manera temporal si se ha configurado la clasificación recomendada, o si el documento o correo electrónico debe tener una etiqueta. La configuración tampoco tiene ningún efecto en las etiquetas que usted u otros usuarios configuren, por ejemplo, la clasificación automática o manual, o la configuración de una etiqueta predeterminada.

Para establecer esta configuración avanzada, especifique las cadenas siguientes:

- Clave: **EnableBarHiding**

- Valor: **True**

## <a name="integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution"></a>Integración con la clasificación de mensajes de Exchange para una solución de etiquetado de dispositivo móvil

A pesar de que Outlook en la Web todavía no es compatible de forma nativa con la clasificación y la protección de Azure Information Protection, puede usar la clasificación de mensajes de Exchange para extender las etiquetas de Azure Information Protection a los usuarios móviles.

Para lograr esta solución: 

1. Use el cmdlet [New-MessageClassification](https://technet.microsoft.com/library/bb124400) de Exchange PowerShell para crear clasificaciones de mensajes con la propiedad Name que se asigna a los nombres de sus etiquetas en la directiva de Azure Information Protection. 

2. Cree una regla de transporte de Exchange para cada etiqueta. Aplique la regla cuando las propiedades del mensaje incluyan la clasificación que ha configurado, y modifique las propiedades del mensaje para establecer un encabezado de mensaje. 

    En el caso del encabezado del mensaje, encontrará la información que es necesario especificar al inspeccionar los encabezados de Internet de un correo electrónico que haya enviado y clasificado con una etiqueta de Azure Information Protection. Busque el encabezado **msip_labels** y la cadena inmediatamente posterior, hasta e incluido el punto y coma. En el ejemplo anterior:
    
    **msip_labels: MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;**
    
    Luego, para el encabezado del mensaje en la regla, especifique **msip_labels** para el encabezado y el resto de la cadena para el valor del encabezado. Por ejemplo:
    
    ![Ejemplo de regla de transporte de Exchange Online que establece el encabezado del mensaje para una etiqueta de Azure Information Protection](../media/exchange-rule-for-message-header.png)

Antes de probar esta configuración, recuerde que, al crear o editar reglas de transporte, normalmente se produce un retraso (espere una hora, por ejemplo). Cuando se aplica la regla y los usuarios usan Outlook en la web o un cliente de dispositivo móvil que admite la protección de Rights Management, tienen lugar los siguientes eventos: 

- Los usuarios seleccionan la clasificación de mensajes de Exchange y envían el correo electrónico.

- La regla de Exchange detecta la clasificación de Exchange y, en función de esta, modifica el encabezado del mensaje para agregar la clasificación de Azure Information Protection.

- Cuando los destinatarios ven el correo electrónico en Outlook y tienen instalado el cliente de Azure Information Protection, verán asignada la etiqueta de Azure Information Protection, así como los correspondientes encabezado, pie de página o marca de agua del correo electrónico. 

Si las etiquetas de Azure Information Protection aplican la protección de administración de derechos, agregue dicha protección a la configuración de reglas: seleccione la opción para modificar la seguridad de los mensajes, aplique la protección de derechos y luego seleccione la plantilla de RMS o la opción No reenviar.

También puede configurar reglas de transporte para realizar la asignación inversa. Cuando se detecta una etiqueta de Azure Information Protection, se establece una clasificación de mensajes de Exchange correspondiente.

- Para cada etiqueta de Azure Information Protection, cree una regla de transporte que se aplique cuando el encabezado **msip_labels** incluya el nombre de la etiqueta (por ejemplo, **General**) y aplique una clasificación de mensajes que se asigne a ella.


## <a name="next-steps"></a>Pasos siguientes
Ahora que personalizó el cliente de Azure Information Protection, consulte en los siguientes recursos información adicional que puede necesitar para la compatibilidad con este cliente:

- [Archivos de cliente y registro de uso](client-admin-guide-files-and-logging.md)

- [Seguimiento de documentos](client-admin-guide-document-tracking.md)

- [Tipos de archivos admitidos](client-admin-guide-file-types.md)

- [Comandos de PowerShell](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
