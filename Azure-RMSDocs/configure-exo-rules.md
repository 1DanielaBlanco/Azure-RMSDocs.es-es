---
title: Configuración de reglas de flujo de correo de Exchange Online para etiquetas de Azure Information Protection
description: Instrucciones y ejemplos para configurar reglas de flujo de correo de Exchange Online para etiquetas de Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ba4e4a4d-5280-4e97-8f5c-303907db1bf5
ms.reviewer: shakella
ms.suite: ems
ms.openlocfilehash: f46e919665d110665ed85b5e2e5c6a979a1958e9
ms.sourcegitcommit: 1fe9720526a2ff814cd5d353249b16497cfcaadc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/20/2019
ms.locfileid: "56425970"
---
# <a name="configuring-exchange-online-mail-flow-rules-for-azure-information-protection-labels"></a>Configuración de reglas de flujo de correo de Exchange Online para etiquetas de Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Consulte la siguiente información como ayuda para configurar las reglas de flujo de correo en Exchange Online para usar etiquetas de Azure Information Protection y para aplicar protección adicional para escenarios específicos. Por ejemplo:

- La etiqueta predeterminada es **General**, que no aplica protección. Para los correos electrónicos con esta etiqueta que se envían externamente, aplique la acción de protección adicional No reenviar.

- Si se envía un archivo adjunto con la etiqueta **Confidencial/Asociados** por correo electrónico a personas fuera de la organización y el correo electrónico no está protegido, aplique la acción de protección Solo cifrar.

Las reglas de flujo de correo que aplican protección como una acción se ignoran si el correo electrónico ya está protegido. Por ejemplo, un mensaje de correo electrónico que se ha protegido con No reenviar no se puede cambiar por una regla de flujo de correo de Exchange para usar la opción Solo cifrar.  

Puede ampliar estos ejemplos, así como modificarlos. Por ejemplo, agregue más condiciones. Para más información sobre cómo configurar las reglas de flujo de correo electrónico, vea [Reglas de flujo de correo (reglas de transporte) en Exchange Online](https://technet.microsoft.com/library/jj919238(v=exchg.150).aspx) en la documentación de Exchange Online.

Para obtener más información acerca de cómo configurar las reglas de flujo de correo electrónico para cifrar los mensajes de correo electrónico, consulte [Definir las reglas de flujo de correo para cifrar mensajes de correo electrónico en Office 365](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8) en la documentación de Office. 

## <a name="prerequisite-know-your-label-guid"></a>Requisito previo: conocer el GUID de la etiqueta

Dado que una etiqueta de Azure Information Protection se almacena en metadatos, las reglas de flujo de correo de Exchange Online pueden leer esta información para los archivos adjuntos de mensajes y documentos de Office. Las reglas de flujo de correo no admiten la inspección de los metadatos para los documentos PDF.

Antes de configurar las reglas de flujo de correo para identificar los mensajes y documentos etiquetados, asegúrese de que conoce el GUID de la etiqueta de Azure Information Protection que se va a usar. 

Para obtener más información sobre los metadatos almacenados por una etiqueta y cómo identificar los GUID de la etiqueta, consulte [Label information stored in emails and documents](configure-policy.md#label-information-stored-in-emails-and-documents) (Información de la etiqueta almacenada en correos electrónicos y documentos).

## <a name="example-configurations"></a>Configuraciones de ejemplo

En los ejemplos siguientes, cree una nueva regla de flujo de correo mediante el uso de los pasos siguientes:

1. En un explorador web, con una cuenta profesional o educativa a la que se haya concedido permisos de administrador global, inicie sesión en Office 365. 

2. Seleccione el icono de **administración**.

3. En el centro de administración de Office 365, elija **Centros de administración** > **Exchange**.

4. En el centro de administración de Exchange: **flujo de correo** > **reglas** > **+** > **Crear una regla nueva**. 

> [!TIP]
> Si tiene problemas con la interfaz de usuario al configurar las reglas, pruebe un explorador diferente, como Internet Explorer.

Los ejemplos tienen una única condición que aplica la protección cuando se envía un correo electrónico fuera de la organización. Para más información sobre otras condiciones que se pueden seleccionar, vea [Excepciones (predicados) y las condiciones de regla de flujo de correo en Exchange Online](https://technet.microsoft.com/library/jj919235(v=exchg.150).aspx).


### <a name="example-1-rule-that-applies-the-do-not-forward-option-to-emails-that-are-labeled-general-when-they-are-sent-outside-the-organization"></a>Ejemplo 1: Regla que aplica la opción No reenviar para correos electrónicos etiquetados como **General** cuando se envían fuera de la organización

En este ejemplo, la etiqueta **General** tiene un GUID de 0e421e6d-ea17-4fdb-8f01-93a3e71333b8. Sustituya su propio GUID de etiqueta o subetiqueta que desee usar con esta regla. 

En la directiva de Azure Information Protection, esta etiqueta se ha configurado como la etiqueta predeterminada para clasificar los correos electrónicos como **General**, y la etiqueta no aplica protección. 

1. En **Nombre**, escriba un nombre para la regla, como `Apply Do Not Forward for General emails sent externally`.
 
2. Para **Aplicar esta regla si**: seleccione **El destinatario se encuentra**, seleccione **Fuera de la organización** y después **Aceptar**.

3. Seleccione **Más opciones** y, a continuación, seleccione **Agregar condición**.
 
4. Para **y**: seleccione **Un encabezado de mensaje** y después **incluye cualquiera de estas palabras**:
     
    a. Seleccione **Escriba texto** y escriba `msip_labels`.
     
    b. Seleccione **Enter words** (Escriba palabras) y escriba `MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;`.
    
    c. Seleccione **+** y, a continuación, seleccione **Aceptar**.

5. Para **Hacer lo siguiente**: seleccione **Modify the message security** (Modificar la seguridad del mensaje)  > **Apply Office 365 Message Encryption and rights protection** (Aplicar el cifrado de mensajes de Office 365 y protección de derechos) > **No reenviar** y después seleccione **Aceptar**.
    
    Ahora la configuración de la regla debería ser similar a esto:  ![Regla de flujo de correo de Exchange Online configurada para etiquetas de Azure Information Protection: ejemplo1](./media/aip-exo-rule-ex1.png)

7. Seleccione **Guardar**. 

Para obtener más información acerca de la opción No reenviar, consulte [Opción No reenviar para correos electrónicos](configure-usage-rights.md#do-not-forward-option-for-emails).

### <a name="example-2-rule-that-applies-the-encrypt-only-option-to-emails-when-they-have-attachments-that-are-labeled-confidential--partners-and-these-emails-are-sent-outside-the-organization"></a>Ejemplo 2: Regla que aplica la opción Solo cifrar a mensajes de correo electrónico cuando tienen datos adjuntos etiquetados como **Confidencial/Asociados** y estos correos electrónicos se envían fuera de la organización

En este ejemplo, la subetiqueta **Confidencial/Asociados** tiene un GUID de 0e421e6d-ea17-4fdb-8f01-93a3e71333b8. Sustituya su propio GUID de etiqueta o subetiqueta que desee usar con esta regla. 

Esta etiqueta se usa para clasificar y proteger los documentos que usa para la colaboración con socios.   

1. En **Nombre**, escriba un nombre para la regla, como `Apply Encrypt to emails sent externally if protected attachments`.
 
2. Para **Aplicar esta regla si**: seleccione **El destinatario se encuentra**, seleccione **Fuera de la organización** y después **Aceptar**.

3. Seleccione **Más opciones** y, a continuación, seleccione **Agregar condición**.
 
4. Para **y**: seleccione **Any attachment** (Cualquier archivo adjunto) y después seleccione **tiene estas propiedades, incluida cualquiera de estas palabras**:
     
    a. Seleccione **+** > **Especificar una propiedad personalizada de datos adjuntos**.
  
    b. Para **Propiedad**, escriba `MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled`.
    
    c. Para **Valor**, escriba `True`
    
    d. Seleccione **Gyargar** y, luego, **Aceptar**.

5. Para **Hacer lo siguiente**: seleccione **Modify the message security** (Modificar la seguridad del mensaje)  > **Apply Office 365 Message Encryption and rights protection** (Aplicar el cifrado de mensajes de Office 365 y protección de derechos) > **Cifrar** y después seleccione **Aceptar**.
    
    Ahora la configuración de la regla debería ser similar a esto:  ![Regla de flujo de correo de Exchange Online configurada para etiquetas de Azure Information Protection: ejemplo1](./media/aip-exo-rule-ex2.png)

6. Seleccione **Guardar**. 

Para obtener más información acerca de la opción de cifrado, consulte [Opción Solo cifrar para los correos electrónicos](configure-usage-rights.md#encrypt-only-option-for-emails).


## <a name="next-steps"></a>Pasos siguientes

Para obtener información sobre cómo crear y configurar las etiquetas que se usan con reglas de flujo de correo de Exchange Online, vea [Configuración de la directiva de Azure Information Protection](configure-policy.md).

Además, para ayudar a clasificar los mensajes de correo electrónico que contienen datos adjuntos, considere el uso de esta [configuración de directiva](configure-policy-settings.md) de Azure Information Protection: **Para los mensajes de correo electrónico con datos adjuntos, aplicar una etiqueta que coincida con la clasificación más alta de los datos adjuntos**.


