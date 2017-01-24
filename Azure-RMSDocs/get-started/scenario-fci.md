---
title: 'Escenario: Proteger archivos en un recurso compartido de servidor de archivos | Azure Information Protection'
description: "En este escenario y en la documentación de usuario correspondiente se usa la protección de Azure Rights Management para proteger de forma masiva todos los archivos que quiera proteger en un servidor de archivos con el fin de garantizar que solo los empleados de la organización puedan acceder a ellos, incluso si se copian y se guardan en un almacenamiento que está fuera del control del departamento de TI o se envían por correo electrónico a otros usuarios."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/05/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 283c7db3-5730-439e-a215-40a1088ed506
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: f5a95beb3cd42921351181b412a5b08dd6fa3b9b


---

# <a name="scenario---protect-files-on-a-file-server-share"></a>Escenario: Proteger archivos en un recurso compartido de servidor de archivos

>*Se aplica a: Azure Information Protection, Office 365*

En este escenario y en la documentación de usuario correspondiente se usa la tecnología Azure Rights Management de Azure Information Protection para proteger de forma masiva todos los archivos que quiera proteger en un servidor de archivos con el fin de garantizar que solo los empleados de la organización puedan acceder a ellos, incluso si se copian y se guardan en un almacenamiento que está fuera del control del departamento de TI o se envían por correo electrónico a otros usuarios.

En estas instrucciones se emplea una de las plantillas predeterminadas, que restringe el acceso a todos los empleados con todos los derechos de uso. Pero, en caso necesario, puede restringir aún más los derechos de acceso y de uso si configura una plantilla personalizada en lugar de usar una plantilla predeterminada.

Las instrucciones son adecuadas para el conjunto de circunstancias siguiente:

-   Necesita proteger todos los tipos de archivo, no solo los archivos de Office. Los archivos que no se pueden proteger de forma nativa con Azure RMS se protegerán genéricamente.

-   Todos los archivos incluidos en la ruta de acceso especificada (subcarpetas incluidas) estarán protegidos.

-   La protección se vuelve a aplicar en todos los archivos de forma programada; así, se asegura que los cambios realizados en las plantillas de directiva de permisos surten efecto en esos archivos protegidos.

## <a name="deployment-instructions"></a>Instrucciones de implementación
![Instrucciones para el administrador para la implementación rápida de Azure RMS](../media/AzRMS_AdminBanner.png)

Asegúrese de que se cumplen los siguientes requisitos y, luego, siga las instrucciones de los procedimientos correspondientes antes de pasar a la documentación del usuario.

## <a name="requirements-for-this-scenario"></a>Requisitos para este escenario
Para que las instrucciones de este escenario funcionen, debe cumplir lo siguiente:

|Requisito|Si necesita más información|
|---------------|--------------------------------|
|Azure Rights Management no está activado|[Activar Rights Management de Azure](../deploy-use/activate-service.md)|
|Ha sincronizado sus cuentas de usuario de Active Directory locales con Azure Active Directory u Office 365, incluyendo su dirección de correo electrónico. Esto es necesario para todos los usuarios que necesiten tener acceso a los archivos después de que se hayan protegido mediante FCI y Azure Rights Management.|[Preparación de Azure Information Protection](../plan-design/prepare.md)|
|Uno de los siguientes:<br /><br />- Para usar una plantilla predeterminada para todos los usuarios: no se ha archivado la plantilla predeterminada, &lt;nombre de la organización&gt; - Confidencial.<br /><br />- Para usar una plantilla personalizada para usuarios específicos: ha creado y publicado esa plantilla personalizada.|[Configuración de plantillas personalizadas para el servicio Azure Rights Management](../deploy-use/configure-custom-templates.md)|
|La aplicación Rights Management sharing se implementa en los equipos de los usuarios que ejecutan Windows|[Implementación automática de la aplicación Microsoft Rights Management sharing](../rms-client/sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application)|
|Ha descargado la herramienta de protección de RMS y ha configurado los requisitos previos de Azure RMS.|Para obtener instrucciones para descargar la herramienta y los requisitos previos: [RMS Protection Cmdlets](https://msdn.microsoft.com/library/mt433195.aspx) (Cmdlets de protección de RMS).<br /><br />Para configurar más requisitos previos para Azure RMS, como la cuenta de entidad de servicio: [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx).|

### <a name="configuring-a-file-server-to-protect-all-files-by-using-azure-rms-and-file-server-resource-manager-with-file-classification-infrastructure"></a>Configuración de un servidor de archivos para proteger todos los archivos mediante Azure RMS y el Administrador de recursos del servidor de archivos con la infraestructura de clasificación de archivos

1.  Inicie una sesión de WindowsPowerShell. No es necesario hacerlo como administrador.

2.  Autentíquese en Azure RMS:

    ```
    Set-RMSServerAuthentication
    ```
    Cuando se le pida, proporcione los valores de la cuenta de entidad de servicio que creó como requisito previo para los cmdlets de protección de RMS.

3.  Ejecute lo siguiente para detectar el identificador de plantilla que se usará para proteger los archivos:

    ```
    Get-RMSTemplate
    ```
    Para usar la plantilla predeterminada que restringe el acceso a todos los empleados con todos los derechos de uso, busque el nombre de plantilla **&lt;nombre de la organización&gt; - Confidencial**. Por ejemplo, **VanArsdel, Ltd - Confidencial**.

4.  Para ver instrucciones detalladas, vea [RMS Protection with Windows Server File Classification Infrastructure (FCI)](../rms-client/configure-fci.md) (Protección de RMS con la infraestructura de clasificación de archivos de Windows Server [FCI]).

    Estas instrucciones incluyen un script de Windows PowerShell que hay que especificar para ejecutarse como un archivo ejecutable personalizado en el Administrador de recursos del servidor de archivos. También incluyen cómo comprobar que los archivos están protegidos con Azure Rights Management.

## <a name="user-documentation-instructions"></a>Instrucciones de la documentación del usuario
Si los archivos que quiere proteger son solo archivos de Office, puede que no tenga que proporcionar instrucciones a los usuarios sobre los archivos protegidos. Cuando los usuarios autorizados abran estos documentos, se abrirán como de costumbre en Office, con la única diferencia de que puede que se les pida que se autentiquen y que verán una barra de información en la parte superior del documento que les informa de que el documento está protegido.

Si los archivos protegidos tienen una extensión de nombre de archivo **.ppdf** o son archivos de texto o de imagen protegidos (por ejemplo, tienen una extensión de nombre de archivo **.ptxt** o **.pjpg**), estos archivos son ahora de solo lectura y no se pueden editar. Los usuarios pueden verlos con el visor de la aplicación RMS sharing, que se carga automáticamente para estos tipos de archivo. Estos archivos están protegidos de forma nativa con Azure RMS y se aplica toda la configuración de directiva de la plantilla que haya usado, con la excepción de los derechos de uso, porque el archivo es de solo lectura. A menos que sepa que va a proteger estos tipos de archivo, es bastante improbable que vaya a necesitar instrucciones de usuario para este escenario. De todas formas, avise al departamento de soporte técnico de que es posible que deba explicar a los usuarios por qué estos archivos no se pueden editar.

Si los archivos protegidos tienen una extensión de nombre de archivo **.pfile**, los usuarios pueden verlos, pero deben guardarse con su nombre de archivo original (es decir, habrá que quitar la extensión de nombre de archivo .pfile) si quieren editarlos y guardar los cambios. Estos archivos están protegidos genéricamente con Azure RMS y no se pueden aplicar los derechos de uso de la plantilla que haya usado, lo que significa que la protección se perderá si el archivo se guarda con un nuevo nombre. En este escenario será necesario proporcionar instrucciones a los usuarios.

Con la siguiente plantilla, copie y pegue las instrucciones dirigidas a los usuarios finales para que sepan cómo modificar los archivos protegidos de forma genérica. Realice estas modificaciones para reflejar su entorno:

-   Reemplace *&lt;tipo de archivo&gt;* y *&lt;recurso compartido de servidor de archivos&gt;* por el tipo de archivo que se protegerá de forma genérica y el nombre del recurso compartido del servidor de archivos.

-   Reemplace *&lt;nombre de la organización&gt;* por el nombre de su organización, tal y como aparece en las plantillas predeterminadas de Azure Rights Management.

-   Reemplace *&lt;nombre de la organización&gt;* por el nombre de su organización.

-   Reemplace *&lt;Instrucciones para guardar el archivo y quitar la extensión de nombre de archivo .pfile&gt;* por las instrucciones específicas de la aplicación correspondientes a este tipo de archivo.

-   Reemplace los detalles de contacto por instrucciones sobre cómo los usuarios pueden ponerse en contacto con el departamento de soporte técnico como, por ejemplo, un vínculo de sitio web, una dirección de correo electrónico o un número de teléfono.

-   Haga los cambios que quiera en este conjunto de instrucciones y, después, envíelo a estos usuarios.

En la documentación de ejemplo se muestra el aspecto de estas instrucciones para los usuarios tras sus personalizaciones.

![Documentación de usuario de la plantilla para la implementación rápida de Azure RMS](../media/AzRMS_UsersBanner.png)

### <a name="how-to-edit-lttype-of-filegt-from-the-ltfile-server-sharegt"></a>Procedimiento para editar &lt;tipo de archivo&gt; desde el &lt;recurso compartido de servidor de archivos&gt;

1.  Haga doble clic en el archivo para abrirlo. Puede que se le pidan las credenciales.

2.  Verá un cuadro de diálogo de **archivo protegido** de la aplicación Microsoft Rights Management sharing que le indicará que se espera que se respeten los permisos de **&lt;nombre de la organización&gt; - Confidencial**. Dicho de otro modo: no comparta este documento con otras personas si no trabajan para &lt;nombre de la organización&gt;.

3.  Haga clic en **Abrir**.

4.  Para editar el archivo, guárdelo primero y quite la extensión de nombre de archivo .pfile:

    -   &lt;Instrucciones para guardar el archivo y quitar la extensión de nombre de archivo .pfile&gt;

5.  Ahora puede editar y guardar el archivo como de costumbre.

Cada cierto tiempo, el archivo se volverá a proteger, lo que hace que se agregue de nuevo la extensión de nombre de archivo .pfile. Por tanto, tendrá que repetir estos pasos.

**¿Necesita ayuda?**

-   Para obtener información adicional:

    -   [Ver y usar archivos protegidos](../rms-client/sharing-app-view-use-files.md)

-   Póngase en contacto con el departamento de soporte técnico:

    -   *&lt;detalles de contacto&gt;*

### <a name="example-customized-user-documentation"></a>Documentación de usuario personalizada de ejemplo
![Documentación de usuario de ejemplo para la implementación rápida de Azure RMS](../media/AzRMS_ExampleBanner.png)

#### <a name="how-to-edit-cad-drawings-from-the-projectnextgen-share"></a>Procedimiento para editar dibujos de CAD desde el recurso compartido ProjectNextGen

1.  Haga doble clic en el archivo para abrirlo. Puede que se le pidan las credenciales.

2.  Verá un cuadro de diálogo de **archivo protegido** de la aplicación Microsoft Rights Management sharing, lo que significa que se espera que se respeten los permisos de **VanArsdel, Ltd - Confidencial**. Dicho de otro modo: no comparta este documento con otras personas si no trabajan para VanArsdel, Ltd.

3.  Haga clic en **Abrir**.

4.  Para editar el archivo, guárdelo primero y quite la extensión de nombre de archivo .pfile:

    -   **Archivo** &gt; **Guardar como**

    -   Elimine **.pfile** del final del nombre de archivo y haga clic en **Aceptar**.

5.  Ahora puede editar y guardar el archivo como de costumbre.

Cada cierto tiempo, el archivo se volverá a proteger, lo que hace que se agregue de nuevo la extensión de nombre de archivo .pfile. Por tanto, tendrá que repetir estos pasos.

**¿Necesita ayuda?**

-   Para obtener información adicional:

    -   [Ver y usar archivos protegidos](../rms-client/sharing-app-view-use-files.md)

-   Póngase en contacto con el departamento de soporte técnico: helpdesk@vanarsdelltd.com

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



<!--HONumber=Jan17_HO4-->


