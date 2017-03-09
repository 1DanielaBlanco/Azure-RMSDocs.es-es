---
title: "Escenario de AIP: los ejecutivos intercambian información confidencial"
description: "En este escenario y en la documentación de usuario correspondiente se usa la protección de Azure Rights Management para que los ejecutivos puedan intercambiar entre ellos mensajes de correo y datos adjuntos por correo electrónico de forma segura, y para que las directivas restrinjan automáticamente el acceso a los ejecutivos sin que tengan que realizar ninguna acción especial."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e18cf5df-859e-4028-8d19-39b0842df33d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 1407a7bee800fec0ba8498d0439586378003ed54
ms.lasthandoff: 02/24/2017


---

# <a name="scenario---executives-securely-exchange-privileged-information"></a>Escenario: Los ejecutivos intercambian información confidencial de forma segura

>*Se aplica a: Azure Information Protection, Office 365*

En este escenario y en la documentación de usuario correspondiente se usa la tecnología Azure Rights Management de Azure Information Protection para que los ejecutivos puedan intercambiar entre ellos mensajes de correo y datos adjuntos por correo electrónico de forma segura, y para que las directivas restrinjan automáticamente el acceso a los ejecutivos sin que tengan que realizar ninguna acción especial. Los correos electrónicos y los datos adjuntos estarán protegidos automáticamente con Azure Rights Management.

Si lo precisa, puede agregar una excepción a la regla, como la abreviatura NP ("no proteger") en el asunto del mensaje de correo, de forma que los ejecutivos puedan especificarla si necesitan enviar un correo electrónico no protegido a otros ejecutivos (por ejemplo, para revisar el mensaje antes de reenviarlo a otros usuarios).

Las instrucciones son adecuadas para el conjunto de circunstancias siguiente:

-   Los ejecutivos comparten información confidencial entre sí que no se debe compartir con otros usuarios.

-   Los ejecutivos no necesitan hacer nada más que enviar estos correos electrónicos a una dirección de correo electrónico de trabajo en lugar de a una dirección de correo electrónico personal.

-   Los ejecutivos tienen una manera de invalidar la regla por sí mismos en caso de que alguna vez necesiten enviar un mensaje de correo no protegido a otros ejecutivos.

## <a name="deployment-instructions"></a>Instrucciones de implementación
![Instrucciones para el administrador para la implementación rápida de Azure RMS](../media/AzRMS_AdminBanner.png)

Asegúrese de que se cumplen los siguientes requisitos y, luego, siga las instrucciones de los procedimientos correspondientes antes de pasar a la documentación del usuario.

## <a name="requirements-for-this-scenario"></a>Requisitos para este escenario
Para que las instrucciones de este escenario funcionen, debe cumplir lo siguiente:

|Requisito|Si necesita más información|
|---------------|--------------------------------|
|Preparó las cuentas y los grupos para Office 365 o Azure Active Directory:<br /><br />- Un grupo habilitado para correo denominado **Ejecutivos** del que todos los ejecutivos son miembros<br /><br />- Un grupo habilitado para correo denominado **Administradores de RMS**, del que todos los administradores que configuran Azure RMS son miembros|[Preparación de Azure Information Protection](../plan-design/prepare.md)|
|La clave de inquilino de Azure Information Protection está administrada por Microsoft y no usa BYOK|[Planeamiento e implementación de su clave de inquilino de Azure Information Protection](../plan-design/plan-implement-tenant-key.md)|
|Azure Rights Management no está activado|[Activar Rights Management de Azure](../deploy-use/activate-service.md)|
|Una de estas configuraciones:<br /><br />- Exchange Online está habilitado para Azure Rights Management<br /><br />- El conector RMS está instalado y configurado para Exchange local|Para Exchange Online, vea [Exchange Online: Configuración de IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration).<br /><br />Para Exchange local: [Deploying the Azure Rights Management connector](../deploy-use/deploy-rms-connector.md) (Implementación del conector de Azure Rights Management).|
|Configuró una plantilla personalizada tal y como se describe a continuación|[Configuración de plantillas personalizadas para el servicio Azure Rights Management](../deploy-use/configure-custom-templates.md)|
|Ha configurado una regla de protección de transporte para IRM, tal y como se describe luego en este artículo|Para Exchange Online: [Reglas de transporte o de flujo de correo](https://technet.microsoft.com/library/jj919238(v=exchg.150).aspx)<br /><br />Para Exchange 2013: [Crear una regla de protección de transporte](https://technet.microsoft.com/en-us/library/dd302432(v=exchg.150))<br /><br />Para Exchange 2010: [Crear una regla de protección de transporte](https://technet.microsoft.com/library/dd302432(v=exchg.141))|

### <a name="to-configure-the-custom-template-for-executives"></a>Para configurar la plantilla personalizada para ejecutivos

1.  En el Portal de Azure clásico, cree una plantilla personalizada para Azure Rights Management que contenga estos valores y configuraciones:

    -   Nombre: **Ejecutivos**

    -   Permisos: conceda al grupo habilitado para correo los permisos **Ejecutivos** y **Copropietario**.

    -   Ámbito: seleccione los grupos habilitados para correo **Ejecutivos** y **Administradores de RMS**.

2.  Publique la nueva plantilla.

3.  Solo para Exchange Online: actualice las plantillas con el comando de Windows PowerShell para Exchange Online:

    ```
    Import-RMSTrustedPublishingDomain -Name "RMS Online -1" -RefreshTemplates -RMSOnline
    ```

### <a name="to-configure-the-transport-rule-for-irm"></a>Para configurar la regla de transporte para IRM

-   Consulte la documentación de Exchange a la que remite la tabla para conocer los procedimientos para crear la regla de transporte con la siguiente configuración:

    -   Nombre: **Aplicar las plantillas de Ejecutivos a los correos electrónicos de los ejecutivos**.

    -   Especifique el grupo **Ejecutivos** como el remitente y el destinatario de la regla y la condición adicional.

    -   En la acción, seleccione **Aplicar la protección de derechos al mensaje con** y, después, seleccione la plantilla **Ejecutivos** que ha configurado.

    -   Agregue la excepción **NP** (como abreviatura de "No proteger") o la expresión que prefiera para identificar esta excepción, que se va a incluir en el asunto.

    -   Asegúrese de que la regla está establecida en **Exigir**.

## <a name="user-documentation-instructions"></a>Instrucciones de la documentación del usuario
A menos que quiera proporcionar instrucciones sobre cómo especificar **NP** (o la expresión que prefiera) en el asunto del correo electrónico, no hay ninguna instrucción de procedimiento que pueda proporcionarse a los usuarios en este escenario, ya que la protección del correo que los ejecutivos envían y reciben no requiere ninguna acción especial por su parte. Los mensajes de correo electrónico y los datos adjuntos se protegen automáticamente para que solo los miembros del grupo Ejecutivos puedan acceder a ellos.

Con todo, deberá informar de ello a los ejecutivos y al departamento de soporte técnico y avisarles de cómo esto puede restringir el uso de estos correos electrónicos. Por ejemplo, otras personas no podrán leerlos correctamente si más adelante se reenvían los mensajes de correo electrónico o datos adjuntos a otros usuarios. Si configuró la excepción NP (o equivalente), asegúrese de que el departamento de soporte está al tanto de esta configuración para que los ejecutivos puedan invalidar la regla por sí mismos, sin necesidad de acudir a un administrador de Exchange.

Con la siguiente plantilla, copie y pegue el anuncio en una comunicación dirigida a sus usuarios finales y realice estas modificaciones para reflejar su entorno:

1.  Reemplace las instancias de *&lt;nombre de la organización&gt;* por el nombre de su organización.

2.  Si eligió una expresión distinta a NP como excepción, reemplace ese valor y la explicación según corresponda.

3.  Reemplace *&lt;dominio de correo&gt;* por el nombre de dominio de correo electrónico de su organización.

4.  Reemplace *&lt;detalles de contacto&gt;* por instrucciones sobre cómo los usuarios pueden ponerse en contacto con el departamento de soporte técnico, por ejemplo, un vínculo de sitio web, una dirección de correo electrónico o un número de teléfono.

5.  Haga los cambios que quiera en este anuncio y, después, envíelo a estos usuarios.

En la documentación de ejemplo se muestra cómo ven los usuarios este anuncio tras las personalizaciones.

![Documentación de usuario de la plantilla para la implementación rápida de Azure RMS](../media/AzRMS_UsersBanner.png)

### <a name="it-announcement-ltorganization-namegt-executive-emails-are-now-automatically-protected"></a>Anuncio de TI: Ahora los correos electrónicos de &lt;nombre de la organización&gt; se protegerán automáticamente
De ahora en adelante, siempre que se envíen correos electrónicos a otro ejecutivo de &lt;nombre de la organización&gt;, el contenido de los correos y los datos adjuntos se protegerán automáticamente, de modo que solo otro ejecutivo de la empresa pueda tener acceso a ellos para leer la información, imprimirlos, copiarlos, etc. Esta restricción se aplica incluso si se reenvía el mensaje de correo electrónico a otros usuarios o si se guardan los datos adjuntos. Con esta protección, es más fácil evitar la pérdida de datos confidenciales o importantes.

No olvide que, si quiere que otros usuarios que no sean ejecutivos de &lt;nombre de la organización&gt; puedan leer y editar la información de estos correos, deberá enviarla por separado. O bien, para invalidar la protección automática, escriba **NP** (abreviatura de "No proteger") en cualquier parte del asunto del mensaje de correo.

Al enviar información confidencial de la empresa a otro ejecutivo de &lt;nombre de la organización&gt;, recuerde que debe enviarla a su dirección de correo electrónico de trabajo (*nombre*@&lt;dominio de correo&gt;) y no a una dirección de correo electrónico personal.

**¿Necesita ayuda?**

-   Póngase en contacto con el departamento de soporte técnico: &lt;detalles de contacto&gt;

### <a name="example-user-documentation"></a>Documentación de usuario de ejemplo
![Documentación de usuario de ejemplo para la implementación rápida de Azure RMS](../media/AzRMS_ExampleBanner.png)

#### <a name="it-announcement-vanarsdel-executive-emails-are-now-automatically-protected"></a>Anuncio de TI: Ahora los correos electrónicos de VanArsdel se protegerán automáticamente
De ahora en adelante, siempre que se envíen correos electrónicos a otro ejecutivo de VanArsdel, el contenido de los correos electrónicos y los datos adjuntos se protegerán automáticamente de modo que solo otro ejecutivo de la empresa pueda tener acceso a ellos para leer la información, imprimirlos, copiarlos, etc. Esta restricción se aplica incluso si se reenvía el mensaje de correo electrónico a otros usuarios o si se guardan los datos adjuntos. Con esta protección, es más fácil evitar la pérdida de datos confidenciales o importantes.

No olvide que, si quiere que otros usuarios que no sean ejecutivos de VanArsdel puedan leer y editar la información de estos correos, deberá enviarla por separado. O bien, para invalidar la protección automática, escriba **NP** (abreviatura de "No proteger") en cualquier parte del asunto del mensaje de correo.

Al enviar información confidencial de la empresa a otro ejecutivo de VanArsdel, recuerde que debe enviarla a su dirección de correo electrónico de trabajo (*nombre*@vanarsdelltd.com) y no a una dirección de correo electrónico personal.

**¿Necesita ayuda?**

-   Póngase en contacto con el departamento de soporte técnico: helpdesk@vanarsdelltd.com

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

