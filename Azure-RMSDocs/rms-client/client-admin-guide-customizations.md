---
title: Configuraciones personalizadas del cliente de Azure Information Protection
description: "Información sobre cómo personalizar el cliente de Azure Information Protection para Windows."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 6ab5465db1527e6236d2dca466936c36b260f03d
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2017
---
<a id="custom-configurations-for-the-azure-information-protection-client" class="xliff"></a>

# Configuraciones personalizadas del cliente de Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012*

Use la siguiente información para configuraciones avanzadas que podría necesitar para escenarios específicos o un subconjunto de usuarios cuando administre el cliente de Azure Information Protection. 

<a id="prevent-sign-in-prompts-for-ad-rms-only-computers" class="xliff"></a>

## Evitar solicitudes de inicio de sesión solo para equipos AD RMS

De forma predeterminada, el cliente de Azure Information Protection intenta conectarse automáticamente al servicio Azure Information Protection. Para equipos que solo se comunican con AD RMS, esto puede producir una solicitud de inicio de sesión para los usuarios que no es necesaria. Se puede evitar esta solicitud de inicio de sesión modificando el registro:

Busque el siguiente nombre de valor y después establezca los datos del valor en **0**:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Independientemente de esta configuración, el cliente de Azure Information Protection sigue el [proceso de detección del servicio de RMS](../rms-client/client-deployment-notes.md#rms-service-discovery) estándar para buscar su clúster de AD RMS.

<a id="sign-in-as-a-different-user" class="xliff"></a>

## Inicio de sesión como un usuario diferente

En un entorno de producción, los usuarios normalmente no necesitarán iniciar sesión como un usuario diferente cuando estén utilizando el cliente de Azure Information Protection. Sin embargo, tendrá que hacerlo como administrador si tiene varios inquilinos. Por ejemplo, en caso de que tenga un inquilino de prueba además del inquilino de Office 365 o Azure que usa la organización.

Puede comprobar con qué cuenta ha iniciado sesión en el cuadro de diálogo **Microsoft Azure Information Protection**: abra una aplicación de Office y, en la pestaña **Inicio** del grupo **Protección**, haga clic en **Proteger** y finalmente en **Ayuda y comentarios**. El nombre de cuenta se muestra en la sección **Estado del cliente**.

Especialmente si está usando una cuenta de administrador, asegúrese de comprobar el nombre de dominio de la cuenta con la sesión iniciada que aparece. Por ejemplo, si tiene una cuenta de "administrador" en dos inquilinos diferentes, puede ser fácil pasar por alto que se ha iniciado sesión con el nombre de cuenta correcto pero con el dominio incorrecto. Esto se traduciría en que no se podría descargar la directiva de Azure Information Protection o no se verían las etiquetas de comportamiento esperadas.

Para iniciar sesión como un usuario diferente:

1. Mediante un editor del Registro, vaya a **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP** y elimine el valor **TokenCache** (y sus datos de valores asociados).

2. Reinicie todas las aplicaciones de Office abiertas e inicie sesión con su cuenta de usuario diferente. Si no ve un mensaje en la aplicación de Office para iniciar sesión en el servicio Azure Information Protection, vuelva al cuadro de diálogo **Microsoft Azure Information Protection** y haga clic en **Iniciar sesión** desde la sección **Estado del cliente** actualizada.

Además:

- Si utiliza el inicio de sesión único, debe cerrar la sesión de Windows e iniciar sesión con su cuenta de usuario diferente después de editar el registro. El cliente Azure Information Protection se autenticará automáticamente mediante la cuenta de usuario que tiene iniciada sesión actualmente.

- Si desea reinicializar el entorno para el servicio de Azure Rights Management (también conocido como arranque), puede hacerlo mediante la opción **Restablecer** de la [herramienta RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437).

- Si desea eliminar la directiva actualmente descargada de Azure Information Protection, elimine el archivo **Policy.msip** de la carpeta **%localappdata%\Microsoft\MSIP**.

<a id="hide-the-classify-and-protect-menu-option-in-windows-file-explorer" class="xliff"></a>

## Ocultación de la opción de menú Clasificar y Proteger en el Explorador de archivos de Windows

Puede configurar esta configuración avanzada editando el Registro cuando tenga la versión 1.3.0.0 del cliente de Azure Information Protection o una versión superior. 

Cree el siguiente nombre de valor DWORD (con cualquier datos de valor):

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

<a id="support-for-disconnected-computers" class="xliff"></a>

## Soporte técnico para equipos desconectados

De forma predeterminada, el cliente de Azure Information Protection intenta conectarse automáticamente al servicio Azure Information Protection para descargar la directiva más reciente de Azure Information Protection. Si tiene un equipo que sabe que no se podrá conectar a Internet durante un período de tiempo, puede impedir que el cliente intente conectarse al servicio editando el Registro. Busque el siguiente nombre de valor y establezca los datos del valor en **0**:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Asegúrese de que el cliente tiene un archivo de directiva válido denominado **Policy.msip**, en la carpeta **%localappdata%\Microsoft\MSIP**. Si es necesario, puede exportar la directiva desde Azure Portal y copiar el archivo exportado en el equipo cliente. También puede utilizar este método para reemplazar un archivo de directiva no actualizado con la directiva publicada más reciente.

<a id="integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution" class="xliff"></a>

## Integración con la clasificación de mensajes de Exchange para una solución de etiquetado de dispositivo móvil

A pesar de que Outlook en la Web todavía no es compatible de forma nativa con la clasificación y la protección de Azure Information Protection, puede usar la clasificación de mensajes de Exchange para extender las etiquetas de Azure Information Protection a los usuarios móviles.

Para lograr esta solución: 

1. Use el cmdlet [New-MessageClassification](https://technet.microsoft.com/library/bb124400) de Exchange PowerShell para crear clasificaciones de mensajes con la propiedad Name que se asigna a los nombres de sus etiquetas en la directiva de Azure Information Protection. 

2. Cree una regla de transporte de Exchange para cada etiqueta. Aplique la regla cuando las propiedades del mensaje incluyan la clasificación que ha configurado, y modifique las propiedades del mensaje para establecer un encabezado de mensaje. 

    En el caso del encabezado del mensaje, encontrará la información que es necesario especificar inspeccionando los encabezados de Internet de un correo electrónico que haya enviado y clasificado con una etiqueta de Azure Information Protection. Busque el encabezado **msip_labels** y la cadena inmediatamente posterior, hasta e incluido el punto y coma. En el ejemplo anterior:
    
    **msip_labels: MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;**
    
    Luego, para el encabezado del mensaje en la regla, especifique **msip_labels** para el encabezado y el resto de la cadena para el valor del encabezado. Por ejemplo:
    
    ![Ejemplo de regla de transporte de Exchange Online que establece el encabezado del mensaje para una etiqueta de Azure Information Protection](../media/exchange-rule-for-message-header.png)

Antes de probar esto, recuerde que, al crear o editar reglas de transporte, normalmente se produce un retraso (espere una hora, por ejemplo). Cuando se aplica la regla y los usuarios usan Outlook en la web o un cliente de dispositivo móvil que admite la protección de Rights Management, ocurre lo siguiente: 

- Los usuarios seleccionan la clasificación de mensajes de Exchange y envían el correo electrónico.

- La regla de Exchange detecta la clasificación de Exchange y, en función de esta, modifica el encabezado del mensaje para agregar la clasificación de Azure Information Protection.

- Cuando los destinatarios que ejecutan el cliente de Azure Information Protection ven el correo electrónico en Outlook, verán asignada la etiqueta de Azure Information Protection, así como los correspondientes encabezado, pie de página o marca de agua del correo electrónico. 

Si las etiquetas de Azure Information Protection aplican protección de administración de derechos, agregue dicha protección a la configuración de reglas mediante la selección de la opción para modificar la seguridad de los mensajes, aplique la protección de derechos y luego seleccione la plantilla de RMS o la opción No reenviar.

También puede configurar reglas de transporte para realizar la asignación inversa: al detectar una etiqueta de Information Protection, establezca una clasificación de mensajes de Exchange correspondiente. Para ello:

- Para cada etiqueta de Azure Information Protection, cree una regla de transporte que se aplique cuando el encabezado **msip_labels** incluya el nombre de la etiqueta (por ejemplo, **General**) y aplique una clasificación de mensajes que se asigne a ella.


<a id="next-steps" class="xliff"></a>

## Pasos siguientes
Ahora que personalizó el cliente de Azure Information Protection, consulte la siguiente información adicional que puede necesitar para la compatibilidad con este cliente:

- [Archivos de cliente y registro de uso](client-admin-guide-files-and-logging.md)

- [Seguimiento de documentos](client-admin-guide-document-tracking.md)

- [Tipos de archivos admitidos](client-admin-guide-file-types.md)

- [Comandos de PowerShell](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
