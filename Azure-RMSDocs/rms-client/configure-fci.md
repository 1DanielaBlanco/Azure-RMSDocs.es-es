---
title: Protección de Azure RMS con FCI de Windows Server - AIP
description: Instrucciones para usar el cliente de Rights Management (RMS) con el cliente de Azure Information Protection para configurar el Administrador de recursos del servidor de archivos y la infraestructura de clasificación de archivos (FCI).
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 12/12/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 9aa693db-9727-4284-9f64-867681e114c9
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: fa836d25fa779d53ada2448a4a9d01144e24e1e6
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56255502"
---
# <a name="rms-protection-with-windows-server-file-classification-infrastructure-fci"></a>Protección de RMS con la infraestructura de clasificación de archivos (FCI) de Windows Server

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2016, Windows Server 2012 y Windows Server 2012 R2*

Use este artículo para obtener instrucciones y un script para utilizar el cliente de Azure Information Protection y PowerShell para configurar el Administrador de recursos del servidor de archivos y la infraestructura de clasificación de archivos (FCI).

Esta solución le permite proteger automáticamente todos los archivos en una carpeta de un servidor de archivos que ejecuta Windows Server o bien proteger automáticamente archivos que cumplen criterios específicos. Por ejemplo, los archivos que se han clasificado como poseedores de información confidencial. Esta solución se conecta directamente al servicio Azure Rights Management desde Azure Information Protection para proteger los archivos, por lo que debe tener este servicio implementado en la organización.

> [!NOTE]
> Aunque Azure Information Protection incluye un [conector](../deploy-rms-connector.md) que admite la infraestructura de clasificación de archivos, dicha solución admite solo la protección nativa (por ejemplo, archivos de Office).
> 
> Para admitir varios tipos de archivo con infraestructura de clasificación de archivos de Windows Server, debe usar el módulo **AzureInformationProtection** de PowerShell, tal como se describe en este artículo. Los cmdlets de Azure Information Protection, como el cliente de Azure Information Protection, admiten la protección genérica, así como la protección nativa, lo que significa que se pueden proteger tipos de archivos que no son documentos de Office. Para más información, vea [Tipos de archivos compatibles con el cliente de Azure Information Protection](client-admin-guide-file-types.md) en la guía para administradores del cliente de Azure Information Protection.

Las instrucciones siguientes sirven para Windows Server 2012 R2 o Windows Server 2012. Si ejecuta otras versiones compatibles de Windows, es posible que tenga que adaptar algunos de los pasos por las diferencias entre la versión de su sistema operativo y la descrita en este artículo.

## <a name="prerequisites-for-azure-rights-management-protection-with-windows-server-fci"></a>Requisitos previos de la protección de Azure Rights Management con FCI de Windows Server
Requisitos previos de estas instrucciones:

- En cada servidor de archivos donde ejecutará el Administrador de recursos de archivos con la infraestructura de clasificación de archivos:
    
  - Ha instalado el Administrador de recursos del servidor de archivos como uno de los servicios de rol para el rol Servicios de archivo.
    
  - Ha identificado una carpeta local que contiene archivos para proteger con Rights Management. Por ejemplo, C:\FileShare.
    
  - Instaló el módulo AzureInformationProtection de PowerShell y configuró los requisitos previos para que este módulo se conecte con el servicio Azure Rights Management.
    
    El módulo AzureInformationProtection PowerShell se incluye con el cliente de Azure Information Protection. Para obtener instrucciones sobre la instalación, consulte [Instalación del cliente de Azure Information Protection para los usuarios](client-admin-guide-install.md) en la guía del administrador de Azure Information Protection. Si es necesario, puede instalar solo el módulo de PowerShell mediante el parámetro `PowerShellOnly=true`.
    
    Los [requisitos previos para usar este módulo de PowerShell](client-admin-guide-powershell.md#azure-information-protection-and-azure-rights-management-service) incluyen activar el servicio Azure Rights Management, crear una entidad de servicio y editar el registro si el inquilino está fuera de Norteamérica. Antes de comenzar a aplicar las instrucciones de este artículo, asegúrese de tener valores para **BposTenantId**, **AppPrincipalId**y **Symmetric key**, tal como se documenta en estos requisitos previos. 
    
  - Si desea cambiar el nivel predeterminado de protección (nativo o genérico) para las extensiones de nombre de archivo específicas, ha editado el registro como se describe en la sección [Cambio del nivel de protección predeterminado de los archivos](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files) de la guía para administradores.
    
  - Tiene conexión a Internet y ha configurado los ajustes del equipo si es necesario para un servidor proxy. Por ejemplo: `netsh winhttp import proxy source=ie`
    
- Ha sincronizado sus cuentas de usuario de Active Directory locales con Azure Active Directory u Office 365, incluidas sus direcciones de correo electrónico. Esto es necesario para todos los usuarios que necesiten tener acceso a los archivos después de que se hayan protegido mediante FCI y el servicio Azure Rights Management. Si no realiza este paso (por ejemplo, en un entorno de prueba), existe la posibilidad de que se bloquee el acceso de los usuarios a estos archivos. Para más información sobre este requisito, consulte [Preparación de usuarios y grupos para Azure Information Protection](../prepare.md).
    
- Este escenario no admite plantillas de departamento por lo que debe usar una plantilla que no esté configurada para un ámbito, o utilizar el cmdlet [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty) y el parámetro *EnableInLegacyApps*.

## <a name="instructions-to-configure-file-server-resource-manager-fci-for-azure-rights-management-protection"></a>Instrucciones para configurar la infraestructura de clasificación de archivos del Administrador de recursos del servidor de archivos para la protección con Azure Rights Management
Siga estas instrucciones para proteger automáticamente todos los archivos en una carpeta mediante un script de PowerShell como una tarea personalizada. Lleve a cabo estos procedimientos en este orden:

1. Guardar el script de PowerShell

2. Crear una propiedad de clasificación para Rights Management (RMS)

3. Crear una regla de clasificación (clasificar para RMS)

4. Configurar la programación de clasificación

5. Crear una tarea de administración de archivos personalizada (proteger los archivos con RMS)

6. Probar la configuración ejecutando manualmente la regla y la tarea

Al final de estas instrucciones, todos los archivos de su carpeta seleccionada se clasificarán con la propiedad personalizada de RMS y, a continuación, Rights Management protegerá estos archivos. Para una configuración más compleja que protege de forma selectiva algunos archivos y no otros, puede crear o usar una regla y una propiedad de clasificación diferentes con una tarea de administración de archivos que protege solo esos archivos.

Tenga en cuenta que si realiza cambios en la plantilla de Rights Management que usa para FCI, la cuenta de equipo que ejecuta el script para proteger los archivos no obtiene automáticamente la plantilla actualizada. Para ello, en el script, busque el comando `Get-RMSTemplate -Force` convertido en comentario y quite el carácter de comentario `#`. Cuando se descarga la plantilla actualizada (el script se ha ejecutado al menos una vez), puede convertir en comentario este comando para que las plantillas no se descarguen innecesariamente cada vez. Si los cambios que se realizan en la plantilla son lo bastante importantes como para volver a proteger los archivos en el servidor de archivos, puede hacer esto de manera interactiva mediante la ejecución del cmdlet Protect-RMSFile con una cuenta que tenga los derechos de uso de exportación o control completo en los archivos. También debe ejecutar `Get-RMSTemplate -Force` si publica una nueva plantilla que desea usar para FCI.

### <a name="save-the-windows-powershell-script"></a>Guardar el script de Windows PowerShell

1.  Copie el contenido del [script de Windows PowerShell](fci-script.md) para la protección de Azure RMS con FCI del Administrador de recursos del servidor de archivos. Pegue el contenido del script y ponga al archivo el nombre **RMS-Protect-FCI.ps1** en su propio equipo.

2.  Revise el script y realice los cambios siguientes:
    
    - Busque la cadena siguiente y reemplácela por su propio AppPrincipalId, que usa con el cmdlet [Set-RMSServerAuthentication](/powershell/azureinformationprotection/vlatest/set-rmsserverauthentication) para conectarse al servicio Azure Rights Management:

        ```
        <enter your AppPrincipalId here>
        ```
        Por ejemplo, es posible que el script tenga el aspecto siguiente:

        `[Parameter(Mandatory = $false)]`

        `[Parameter(Mandatory = $false)]             [string]$AppPrincipalId = "b5e3f76a-b5c2-4c96-a594-a0807f65bba4",`

    -   Busque la siguiente cadena y reemplácela por su propia clave simétrica, que usa con el cmdlet [Set-RMSServerAuthentication](/powershell/azureinformationprotection/vlatest/set-rmsserverauthentication) para conectarse al servicio Azure Rights Management:

        ```
        <enter your key here>
        ```
        Por ejemplo, es posible que el script tenga el aspecto siguiente:

        `[Parameter(Mandatory = $false)]`

        `[string]$SymmetricKey = "zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA="`

    -   Busque la siguiente cadena y reemplácela por su propio BposTenantId (identificador de inquilino), que usa con el cmdlet [Set-RMSServerAuthentication](/powershell/azureinformationprotection/vlatest/set-rmsserverauthentication) para conectarse al servicio Azure Rights Management:

        ```
        <enter your BposTenantId here>
        ```
        Por ejemplo, es posible que el script tenga el aspecto siguiente:

        `[Parameter(Mandatory = $false)]`

        `[string]$BposTenantId = "23976bc6-dcd4-4173-9d96-dad1f48efd42",`

3.  Firme el script. Si no firma el script (más seguro), debe configurar Windows PowerShell en los servidores que lo ejecutan. Por ejemplo, ejecute una sesión de Windows PowerShell con la opción **Ejecutar como administrador** y escriba: **Set-ExecutionPolicy RemoteSigned**. Sin embargo, esta configuración permite la ejecución de todos los scripts sin firmar cuando se almacenan en este servidor (menos seguro).

    Para obtener más información acerca de la firma de scripts de Windows PowerShell, consulte [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) en la biblioteca de documentación de PowerShell.

4.  Guarde el archivo localmente en cada servidor de archivos que ejecute el Administrador de recursos de archivos con la infraestructura de clasificación de archivos. Por ejemplo, guarde el archivo en **C:\RMS-Protection**. Si utiliza una ruta de acceso diferente o el nombre de la carpeta, elija una ruta de acceso y una carpeta que no incluya espacios. Proteja este archivo mediante permisos NTFS para que los usuarios no autorizados no puedan modificarlo.

Ahora está listo para empezar a configurar el Administrador de recursos del servidor de archivos.

### <a name="create-a-classification-property-for-rights-management-rms"></a>Crear una propiedad de clasificación para Rights Management (RMS)

-   En el Administrador de recursos del servidor de archivos, en Administración de clasificaciones, cree una nueva propiedad local:

    -   **Nombre**: escriba **RMS**

    -   **Descripción**:   escriba **protección de Rights Management**

    -   **Tipo de propiedad**: seleccione **Sí/No**

    -   **Valor**: seleccione **Sí**

Ahora podemos crear una regla de clasificación que usa esta propiedad.

### <a name="create-a-classification-rule-classify-for-rms"></a>Crear una regla de clasificación (clasificar para RMS)

-   Cree una nueva regla de clasificación:

    -   En la pestaña **General** :

        -   **Nombre**: escriba **Clasificar para RMS**

        -   **Habilitada**: Mantenga el valor predeterminado, que es por lo que esta casilla de verificación está seleccionada.

        -   **Descripción**: escriba **Clasificar todos los archivos en la carpeta &lt;nombre de carpeta&gt; para Rights Management**.

            Reemplace *&lt;nombre de carpeta&gt;* por su nombre elegido para la carpeta. Por ejemplo, **clasifique todos los archivos en la carpeta C:\FileShare para Rights Management**.

        -   **Ámbito**: Agregue su carpeta elegida. Por ejemplo, **C:\FileShare**.

            No seleccione las casillas de verificación.

    -   En la pestaña **Clasificación** :

    -   **Método de clasificación**: seleccione **Clasificador de carpetas**

    -   Nombre de la **propiedad**: seleccione **RMS**

    -   **Valor** de propiedad: seleccione **Sí**

Aunque puede ejecutar las reglas de clasificación manualmente, para las operaciones en curso, le interesará que esta regla se ejecute en una programación de modo que los nuevos archivos se clasifiquen con la propiedad RMS.

### <a name="configure-the-classification-schedule"></a>Configurar la programación de clasificación

-   En la pestaña **Clasificación automática** :

    -   **Habilitar programación fija**: Seleccione esta casilla de verificación.

    -   Configure la programación para que se ejecuten todas las reglas de clasificación, lo que incluye nuestra nueva regla para clasificar archivos con la propiedad RMS.

    -   **Permitir clasificación continua de nuevos archivos**: Seleccione esta casilla de verificación de modo que se clasifiquen nuevos archivos.

    -   Opcional: Realice cualquier otro cambios que desee, como configurar opciones para informes y notificaciones.

Ahora que ha completado la configuración de clasificación, está listo para configurar una tarea de administración para aplicar la protección de RMS a los archivos.

### <a name="create-a-custom-file-management-task-protect-files-with-rms"></a>Crear una tarea de administración de archivos personalizada (proteger los archivos con RMS)

-   En **Tareas de administración de archivos**, cree una nueva tarea de administración de archivos:

    -   En la pestaña **General** :

        -   **Nombre de la tarea**: escriba **Proteger archivos con RMS**

        -   Mantener la casilla de verificación **Habilitar** seleccionada.

        -   **Descripción**: escriba **Proteger archivos en &lt;nombre de carpeta&gt; con Rights Management y una plantilla mediante un script de Windows PowerShell.**

            Reemplace *&lt;nombre de carpeta&gt;* por su nombre elegido para la carpeta. Por ejemplo, **Proteger archivos en C:\FileShare con Rights Management y una plantilla mediante un script de Windows PowerShell**.

        -   **Ámbito**: Seleccione su carpeta elegida. Por ejemplo, **C:\FileShare**.

            No seleccione las casillas de verificación.

    -   En la pestaña **Acción** :

        -   **Tipo**: seleccione **Personalizado**

        -   **Ejecutable**: Especifique lo siguiente:

            ```
            C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
            ```
            Si Windows no está en la unidad C:, modifique esta ruta de acceso o vaya a este archivo.

        -   **Argumento**: Especifique lo siguiente, proporcionando sus propios valores para &lt;ruta de acceso&gt; e &lt;identificador de plantilla&gt;:

            ```
            -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID <template GUID> -OwnerMail '[Source File Owner Email]'"
            ```
            Por ejemplo, si ha copiado el script en C:\RMS-Protection y el identificador de plantilla que ha identificado en los requisitos previos es e6ee2481-26b9-45e5-b34a-f744eacd53b0, especifique lo siguiente:

            `-Noprofile -Command "C:\RMS-Protection\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID e6ee2481-26b9-45e5-b34a-f744eacd53b0 -OwnerMail '[Source File Owner Email]'"`

            En este comando, tanto **[Source File Path]** como **[Source File Owner Email]** son variables específicas de FCI, así que escríbalas exactamente como aparecen en el comando anterior. La primera variable la usa FCI para especificar automáticamente el archivo identificado en la carpeta, y la segunda variable es para que FCI recupere automáticamente la dirección de correo electrónico del propietario designado del archivo identificado. Este comando se repite para cada archivo en la carpeta que, en nuestro ejemplo, es cada archivo de la carpeta C:\FileShare que, de forma adicional, tiene RMS como propiedad de clasificación de archivos.

            > [!NOTE]
            > El parámetro y el valor de **-OwnerMail [Source File Owner Email]** aseguran que el propietario original del archivo se designe propietario de Rights Management del archivo una vez que se proteja. Esta configuración garantiza que el propietario del archivo original tenga todos los derechos de Rights Management en sus propios archivos. Cuando un usuario de dominio crea archivos, la dirección de correo electrónico se recupera automáticamente desde Active Directory con el nombre de la cuenta de usuario de la propiedad Owner del archivo. Para ello, el servidor de archivos debe estar en el mismo dominio o dominio de confianza que el usuario.
            > 
            > Siempre que sea posible, asigne los propietarios originales a documentos protegidos para asegurarse de que estos usuarios continúan teniendo control total sobre los archivos que han creado. Pero si usa la variable [Source File Owner Email] como en el comando anterior y un archivo no tiene un usuario de dominio definido como propietario (por ejemplo, se ha usado una cuenta local para crear el archivo, por lo que el propietario aparece como SISTEMA), se producirá un error en el script.
            > 
            > Para los archivos que no tienen un usuario de dominio como propietario, puede copiar y guardar estos archivos usted mismo como usuario de dominio, de modo que se convierta en el propietario de solo estos archivos. O bien, si dispone de permisos, puede cambiar manualmente el propietario.  Como alternativa, puede especificar una dirección de correo electrónico concreta (como la suya propia o una dirección de grupo del departamento de TI) en lugar de la variable [Source File Owner Email], lo que significa que todos los archivos que proteja mediante este script usarán esta dirección de correo electrónico para definir el nuevo propietario.

    -   **Ejecutar el comando como**: seleccione **Sistema local**

    -   En la pestaña **Condición** :

        -   **Propiedad**: seleccione **RMS**

        -   **Operador**: seleccione **Igual**

        -   **Valor**: seleccione **Sí**

    -   En la pestaña **Programación** :

        -   **Ejecutar en**: Configure su programación preferida.

            Conceda al script tiempo de sobra para completarse. Aunque esta solución protege todos los archivos de la carpeta, el script se ejecuta una vez por archivo, cada vez. Aunque este proceso tarda más que proteger todos los archivos al mismo tiempo, un proceso que el cliente Azure Information Protection admite, esta configuración individual de cada archivo para FCI es más eficaz. Por ejemplo, si usa la variable [Source File Owner Email], los archivos protegidos pueden tener distintos propietarios, es decir, conservar el propietario original. Esta acción individual para cada archivo será necesaria si posteriormente cambia la configuración para protegerlos de forma selectiva en lugar de todos los de una carpeta.

        -   **Ejecutarse continuamente en nuevos archivos**: Seleccione esta casilla de verificación.

### <a name="test-the-configuration-by-manually-running-the-rule-and-task"></a>Probar la configuración ejecutando manualmente la regla y la tarea

1.  Ejecute la regla de clasificación:

    1.  Haga clic en **Reglas de clasificación** &gt; **Ejecutar clasificación con todas las reglas ahora**.

    2.  Haga clic en **Esperar a que termine la clasificación**y, a continuación, haga clic en **Aceptar**.

2.  Espere a que se cierre el cuadro de diálogo **Ejecutando clasificación** para cerrar y, a continuación, ver los resultados en el informe que se muestra automáticamente. Debe ver **1** para el campo **Propiedades** y el número de archivos de su carpeta. Confírmelo mediante el Explorador de archivos y comprobando las propiedades de archivos de su carpeta elegida. En la pestaña **Clasificación** ficha, debe ver **RMS** como nombre de la propiedad y **Sí** para su **Valor**.

3.  Ejecute la tarea de administración de archivos:

    1.  Haga clic en **Tareas de administración de archivos** &gt; **Proteger archivos con RMS** &gt; **Ejecutar tarea de administración de archivos ahora**.

    2.  Haga clic en **Esperar a que termine la clasificación**y, a continuación, haga clic en **Aceptar**.

4.  Espere a que se cierre el cuadro de diálogo **Ejecutando tarea de administración de archivos** para cerrar y, a continuación, ver los resultados en el informe que se muestra automáticamente. Debe ver el número de archivos que se encuentran en su carpeta elegida en el campo **Archivos** . Confirme que los archivos de la carpeta elegida ahora están protegidos por Rights Management. Por ejemplo, si su carpeta elegida es C:\FileShare, escriba el comando siguiente en una sesión de Windows PowerShell y confirme que no hay ningún archivo con el estado **Sin proteger**:

    ```
    foreach ($file in (Get-ChildItem -Path C:\FileShare -Force | where {!$_.PSIsContainer})) {Get-RMSFileStatus -f $file.PSPath}
    ```
    > [!TIP]
    > Algunas sugerencias para la solución de problemas:
    > 
    > -   Si ve **0** en el informe, en lugar del número de archivos de su carpeta, esto indica que el script no se ha ejecutado. En primer lugar, compruebe el propio script cargándolo en Windows PowerShell ISE para validar su contenido e intenta ejecutarlo una vez en la misma sesión de PowerShell para ver si se muestra algún error. Si no se especifica ningún argumento, el script intenta conectarse al servicio Azure Rights Management y autenticarse.
    > 
    >     -   Si el script informa de que no ha podido conectarse al servicio Azure Rights Management (Azure RMS), compruebe los valores que muestra para la cuenta de entidad de servicio, especificados anteriormente en el script. Para más información sobre cómo crear esta cuenta de entidad de servicio, vea [Requisito previo 3: proteger o desproteger archivos sin interacción del usuario](client-admin-guide-powershell.md#prerequisite-3-to-protect-or-unprotect-files-without-user-interaction) en la Guía del administrador de cliente de Azure Information Protection.
    >     -   Si el script informa de que se puede conectar a Azure RMS, compruebe que se puede encontrar la plantilla especificada mediante la ejecución de [Get RMSTemplate](/powershell/azureinformationprotection/vlatest/get-rmstemplate) directamente desde Windows PowerShell en el servidor. Debería ver la plantilla especificada que se devuelve en los resultados.
    > -   Si el script por sí solo se ejecuta en ISE de Windows PowerShell sin errores, intente ejecutarlo como se indica a continuación en una sesión de PowerShell, especificando un nombre de archivo para proteger y sin el parámetro - OwnerEmail:
    > 
    >     ```
    >     powershell.exe -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '<full path and name of a file>' -TemplateID <template GUID>"
    >     ```
    >     -   Si el script se ejecuta correctamente en esta sesión de Windows PowerShell, compruebe sus entradas para **Ejecutivo** y **Argumento** en la acción de tarea de administración de archivos.  Si ha especificado **-OwnerEmail [Source File Owner Email]**, pruebe a quitar este parámetro.
    > 
    >         Si la tarea de administración de archivos funciona correctamente sin **-OwnerEmail [Source File Owner Email]**, compruebe que los archivos no protegidos tienen un usuario de dominio que aparece como el propietario del archivo, en lugar de **SISTEMA**.  Para realizar esta comprobación, use la pestaña **Seguridad** de las propiedades del archivo y haga clic en **Avanzadas**. El valor de **propietario** se muestra inmediatamente después del **nombre** del archivo. Compruebe también que el servidor de archivos esté en el mismo dominio o en un dominio de confianza para buscar la dirección de correo electrónico del usuario desde Active Directory Domain Services.
    > -   Si ve el número correcto de archivos en el informe, pero los archivos no están protegidos, intente proteger los archivos manualmente mediante el uso del cmdlet [Protect-RMSFile](/powershell/azureinformationprotection/vlatest/protect-rmsfile) para ver si aparece algún error.

Cuando haya confirmado que estas tareas se ejecutan satisfactoriamente, puede cerrar el Administrador de recursos de archivo. Los nuevos archivos se clasifican y se protegen automáticamente al ejecutar las tareas programadas. 

## <a name="action-required-if-you-make-changes-to-the-rights-management-template"></a>Acción necesaria si realiza cambios en la plantilla de Rights Management

Si realiza cambios en la plantilla de Rights Management a la que hace referencia el script, la cuenta de equipo que ejecuta el script para proteger los archivos no obtiene automáticamente la plantilla actualizada. En el script, busque el comando `Get-RMSTemplate -Force` convertido en comentario en la función Set-RMSConnection y quite el carácter de comentario al principio de la línea. La próxima vez que se ejecuta el script, se descarga la plantilla actualizada. Para optimizar el rendimiento de forma que las plantillas no se descarguen innecesariamente, puede volver a convertir esta línea en comentario. 

Si los cambios que se realizan en la plantilla son lo bastante importantes como para volver a proteger los archivos en el servidor de archivos, puede hacer esto de manera interactiva mediante la ejecución del cmdlet Protect-RMSFile con una cuenta que tenga los derechos de uso de exportación o control completo en los archivos. 

También deberá ejecutar esta línea en el script si publica una nueva plantilla que quiera usar para FCI y cambia el identificador de plantilla en la línea de argumento de la tarea de administración de archivos personalizada.

## <a name="modifying-the-instructions-to-selectively-protect-files"></a>Modificar las instrucciones para proteger archivos de forma selectiva
Cuando tenga las instrucciones anteriores en funcionamiento, será fácil modificarlas para obtener una configuración más sofisticada. Por ejemplo, proteja archivos mediante el uso del mismo script, pero solo para los archivos que contienen información de identificación personal y seleccione quizás una plantilla con permisos más restrictivos.

Para realizar esta modificación, use una de las propiedades de clasificación integradas (por ejemplo, **Información de identificación personal**) o cree su propia propiedad. A continuación, cree una nueva regla que utilice esta propiedad. Por ejemplo, puede seleccionar **Clasificador de contenido**, elija la propiedad **Información de identificación personal** con un valor de **Alto**y configure el modelo de expresiones o cadenas que identifica el archivo que se va a configurar para esta propiedad (como la cadena "**Fecha de nacimiento**").

Ahora todo lo que debe hacer es crear una nueva tarea de administración de archivos que utilice el mismo script, aunque quizás con una plantilla diferente, así como configurar la condición para la propiedad de clasificación que acaba de configurar. Por ejemplo, en lugar de la condición que hemos configurado previamente (propiedad**RMS** , **Igual**, **Sí**), seleccione la propiedad **Información de identificación personal** con el valor **Operador** establecido en **Igual** y el **Valor** de **Alto**.

## <a name="next-steps"></a>Pasos siguientes

Tal vez se pregunte: [¿Cuál es la diferencia entre FCI de Windows Server y el analizador de Azure Information Protection?](../faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner) 

