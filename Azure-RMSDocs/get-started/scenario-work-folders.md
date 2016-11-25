---
title: "Escenario: Configurar carpetas de trabajo para la protección persistente | Azure Information Protection"
description: "En este escenario y en la documentación de usuario correspondiente se usa protección de Azure Rights Management para aplicar protección persistente a documentos de Office en Carpetas de trabajo."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1f189345-a69e-4bf5-8a45-eb0fe5bb542b
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: 0d4b1cdc2620a1f8cf9ddced24a898a38d8e9b57


---

# <a name="scenario-configure-work-folders-for-persistent-protection"></a>Escenario: Configurar carpetas de trabajo para la protección persistente

>*Se aplica a: Azure Information Protection, Office 365*

En este escenario y en la documentación de usuario correspondiente se usa la tecnología de Azure Information Protection para aplicar protección persistente a documentos de Office en [Carpetas de trabajo](https://technet.microsoft.com/library/dn265974.aspx). Carpetas de trabajo emplea un servicio de rol para servidores de archivos que ejecutan Windows Server que proporciona a los usuarios una forma coherente de tener acceso a sus archivos de trabajo desde sus equipos y dispositivos. Carpetas de trabajo dispone de un cifrado propio para proteger los archivos, pero esta protección se pierde si los archivos se mueven fuera del entorno de Carpetas de trabajo. Esto ocurre, por ejemplo, cuando un usuario copia los archivos sincronizados y los guarda en un almacenamiento que no está bajo el control del departamento de TI, o cuando los archivos se envían por correo electrónico a otros usuarios.

La protección extra que Azure Rights Management aporta contribuye a evitar la pérdida accidental de datos, ya que impide que personas ajenas a su organización puedan ver los archivos. Para ello, puede usar una de las plantillas de directiva de permisos predeterminadas integradas. Pero, antes de implementar este escenario, tenga en cuenta si los usuarios van a necesitar compartir legítimamente cualquiera de estos archivos con personas ajenas a la organización. Podría ser el caso de un usuario que, tras trabajar en el borrador de una lista de precios, envíe por correo electrónico la versión final a sus clientes de otra organización. Si usa la plantilla de Rights Management predeterminada para Carpetas de trabajo, esos clientes de la otra organización no podrán leer el documento enviado por correo electrónico. Para dar cabida a este requisito, se puede crear una plantilla personalizada que permita a los usuarios aplicar una nueva directiva de permisos al archivo, de forma que se reemplace la restricción original de todos los empleados por las personas que se especifiquen en el correo electrónico.

> [!NOTE]
> Si se usa la plantilla personalizada objeto de este escenario, aunque los usuarios puedan compartir archivos intencionadamente con personas que no estén definidas en la plantilla, la protección extra que se logra con Azure Rights Management reporta numerosas ventajas. Esta protección extra evita la pérdida accidental de datos si el contenido se mueve fuera de los límites de Carpetas de trabajo, ya que el contenido sigue estando protegido de usuarios no autorizados, tanto si se mueve como si no. Ejemplos de esto serían un usuario que pierde un dispositivo en el que usa Carpetas de trabajo, o cuando este dispositivo se sustrae, o bien cuando el contenido sincronizado con este dispositivo se transfiere a través de una infraestructura no segura.
> 
> Si un usuario comparte el contenido con alguien de otra organización, al usar la función de uso compartido protegido de la aplicación Rights Management sharing, ese usuario reemplaza la protección original por su propia directiva de protección. Como resultado, el contenido seguirá estando protegido de accesos no autorizados y solo las personas que ese usuario haya especificado podrán tener acceso al contenido.

Esta protección persistente se puede aplicar a todos los documentos de Office en Carpetas de trabajo o únicamente a los archivos que contengan datos confidenciales o que tengan un gran impacto de negocio.

Las instrucciones son adecuadas para el conjunto de circunstancias siguiente:

-   Los archivos de Carpetas de trabajo que se suelen proteger con protección persistente son archivos de Office. Estos archivos se pueden proteger de forma nativa con Azure Right Management y no cambian su extensión de nombre de archivo ni precisan de un flujo de trabajo diferente para abrirlos.

-   Conviene aplicar la protección persistente a todos los archivos de Office en Carpetas de trabajo, o bien a determinados archivos identificados mediante la infraestructura de clasificación de archivos del Administrador de recursos del servidor de archivos en Windows Server.

-   En cuanto a los archivos que se deben compartir con personas no especificadas en la plantilla de directiva de permisos (por ejemplo, los usuarios de otra organización), habrá que aplicar una nueva directiva de permisos que reemplace la protección de la directiva de permisos original.

## <a name="deployment-instructions"></a>Instrucciones de implementación
![Instrucciones para el administrador para la implementación rápida de Azure RMS](../media/AzRMS_AdminBanner.png)

Asegúrese de que se cumplen los siguientes requisitos y, luego, siga las instrucciones de los procedimientos correspondientes antes de pasar a la documentación del usuario.

## <a name="requirements-for-this-scenario"></a>Requisitos para este escenario
Para que las instrucciones de este escenario funcionen, debe cumplir lo siguiente:

|Requisito|Si necesita más información|
|---------------|--------------------------------|
|Azure Rights Management no está activado|[Activar Rights Management de Azure](../deploy-use/activate-service.md)|
|Ha sincronizado sus cuentas de usuario de Active Directory locales con Azure Active Directory u Office 365, incluyendo su dirección de correo electrónico. Esto es necesario para todos los usuarios que usa Carpetas de trabajo.|[Preparación de Azure Information Protection](../plan-design/prepare.md)|
|Uno de los siguientes:<br /><br />- Para usar una plantilla predeterminada para todos los usuarios que les impida aplicar una nueva directiva de permisos: no se ha archivado la plantilla predeterminada, **&lt;nombre de la organización&gt; - Confidencial**<br /><br />- Para usar una plantilla personalizada que permita a los usuarios aplicar una nueva directiva de permisos: use las siguientes instrucciones para crear una plantilla personalizada|[Configuración de plantillas personalizadas para el servicio Azure Rights Management](../deploy-use/configure-custom-templates.md)|
|El conector de Rights Management está instalado, autorizado para el equipo de Windows Server y configurado para el rol de **servidor FCI**.|[Implementación del conector de Azure Rights Management](../deploy-use/deploy-rms-connector.md)|
|La aplicación Rights Management sharing se implementa en los equipos de los usuarios que ejecutan Windows|[Implementación automática de la aplicación Microsoft Rights Management sharing](../rms-client/sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application)|

### <a name="configuring-the-custom-rights-policy-template-so-that-users-can-share-work-folders-files-outside-the-organization"></a>Configuración de la plantilla de directiva de permisos personalizada para que los usuarios puedan compartir archivos de Carpetas de trabajo fuera de la organización

1.  Inicie sesión en el Portal de Azure clásico y vaya a las plantillas de Azure Rights Management.

2.  Copie la plantilla **&lt;nombre de la organización&gt; - Confidencial** e indique un nombre y una descripción para este escenario de Carpetas de trabajo. Sugerimos lo siguiente:

    -   Nombre: **Contenido protegido por Carpetas de trabajo**

    -   Descripción: **Este contenido está protegido por Carpetas de trabajo y está restringido a únicamente los empleados de la empresa. Para compartir este contenido con personas fuera de la organización, adjunte el documento a un mensaje de correo y use la función de uso compartido protegido.**

3.  En la página **DERECHOS**:

    -   Cambie los derechos existentes de **Personalizado** a **Copropietario**.

4.  En la página **CONFIGURAR**:

    -   Procure que **ESTADO** está establecido en **PUBLICAR**.

    -   En el **nombre y descripción**, elimine las entradas de los idiomas que no use. En cuanto a los idiomas que use, actualice **NOMBRE** y **DESCRIPCIÓN** para que coincidan con el nombre y la descripción que indicó para esta plantilla, usando el idioma especificado.

5.  Guarde la plantilla.

### <a name="configuring-work-folders-to-apply-persistent-protection-to-office-file"></a>Configuración de Carpetas de trabajo para aplicar protección persistente a un archivo de Office

1.  Implemente Carpetas de trabajo para sus usuarios, de forma que los archivos guardados localmente se sincronicen en una carpeta del servidor de archivos, conocida como *recurso compartido de sincronización*. El recurso compartido de sincronización en el servidor de archivos no debe estar en el mismo servidor que ejecuta el conector de Rights Management.

    Esta solución requiere el servicio de rol Carpetas de trabajo del Administrador del servidor para el rol Servicios de archivos y almacenamiento. El servidor de archivos debe ejecutar Windows Server 2012 R2 como mínimo y este servidor puede ser local o estar en una máquina virtual en Azure. Para más información sobre Carpetas de trabajo, vea [Introducción a Carpetas de trabajo](https://technet.microsoft.com/library/dn265974.aspx).

    Si necesita instrucciones de implementación, vea [Implementar Carpetas de trabajo](https://technet.microsoft.com/library/dn528861.aspx). Asegúrese de seleccionar el cifrado integrado (la opción **Cifrar Carpetas de trabajo**), que se aplicará además del cifrado de Azure Rights Management. Además:

    -   Al enlazar el certificado SSL en el servidor de sincronización (paso 4): use el comando netsh (y no la consola de administración de IIS) para enlazar el certificado a la interfaz HTTPS de sitio web predeterminado.

    -   Para evitar que los usuarios reciban el error de configuración de Carpetas de trabajo **Hubo un problema al aplicar directivas de seguridad** y, además, tengan que ser obligatoriamente administradores locales en los equipos unidos al dominio: use el cmdlet [Set-SyncShare](https://technet.microsoft.com/library/dn296649%28v=wps.630%29.aspx) con el parámetro PasswordAutolockExcludeDomain y especifique los nombres de dominio en los que residen estos equipos (por ejemplo, contoso.com).

2.  Para completar la configuración del conector de Rights Management:

    1.  Mediante el Administrador de recursos del servidor de archivos, cree una tarea de administración de archivos que identifique como ámbito a la carpeta del recurso compartido de sincronización.

    2.  Elija como acción **Cifrado RMS** y seleccione una plantilla:

        -   Si no ha creado una plantilla personalizada porque no quiere que los usuarios puedan compartir archivos con otros usuarios fuera de la organización, seleccione el nombre de plantilla **&lt;nombre de la organización&gt; - Confidencial**. Por ejemplo, **VanArsdel, Ltd - Confidencial**.

        -   Si creó una plantilla personalizada siguiendo las instrucciones anteriores, selecciónela. Por ejemplo: **Contenido protegido por Carpetas de trabajo**.

    3.  Especifique una programación que dé tiempo suficiente para que todos los archivos de Office se cifren con Azure Rights Management y especifique la opción **Ejecutar continuamente en archivos nuevos**.

3.  Para probar esta configuración manualmente, asegúrese de que la carpeta contiene algunos archivos de Office; después, use la opción **Ejecutar tarea de administración de archivos ahora** y seleccione **Esperar a que termine la tarea**.

    Espere a que se cierre el cuadro de diálogo **Ejecutando tarea de administración de archivos** para cerrar y, a continuación, ver los resultados en el informe que se muestra automáticamente. Debe ver el número de archivos que se encuentran en su carpeta elegida en el campo **Archivos** . Confirme que los archivos de la carpeta elegida ahora están protegidos por Azure Rights Management. Para ello, abra un archivo y confirme que arriba aparece un banner informativo con el nombre y la descripción de la plantilla de Rights Management.

4.  Si decide proteger solo determinados archivos con la infraestructura de clasificación de archivos, configure la regla y la programación de clasificación y, después, modifique la tarea de administración de archivos de forma que incluya esta propiedad de clasificación como una condición.

## <a name="user-documentation-instructions"></a>Instrucciones de la documentación del usuario
Si los archivos que protege con Azure Rights Management no tienen que compartirse con personas fuera de la organización, no tendrá que proporcionar a los usuarios más instrucciones aparte de las correspondientes al uso de Carpetas de trabajo. Cuando los usuarios abran los archivos protegidos por Azure Rights Management y la plantilla predeterminada, se abrirán como de costumbre en Office, con la única diferencia de que puede que se les pida que se autentiquen y que verán una barra de información en la parte superior del documento que les informa de que el contenido incluye información de propiedad dirigida solo a usuarios internos.

Si ha configurado la plantilla personalizada según lo descrito en este escenario, los usuarios verán la descripción de la plantilla en la barra de información: **Este contenido está protegido por Carpetas de trabajo y está restringido a únicamente los empleados de la empresa. Para compartir este contenido con personas fuera de la organización, adjunte el documento a un mensaje de correo y use la función de uso compartido protegido.** Aunque esta descripción resume cómo compartir el archivo fuera de la organización, probablemente los usuarios necesitarán instrucciones detalladas para llevar esto a cabo, especialmente las primeras veces. Para dar cabida a este escenario de seguimiento, use las instrucciones de administrador y usuario final del [escenario para compartir un archivo de Office con usuarios de otra organización](scenario-share-office-file-externally.md).

> [!TIP]
> Si decide no usar la plantilla personalizada de estas instrucciones (porque no quiera que los usuarios puedan compartir estos archivos fuera de la organización sin supervisión de TI), informe de esto al departamento de soporte técnico para que, cuando el requisito de uso compartido sea legítimo, se pueda cumplir poniendo en marcha el mecanismo más adecuado para su negocio. Por ejemplo, alguien que sea un [superusuario](../deploy-use/configure-super-users.md) podría aplicar una nueva plantilla al contenido que conceda permisos de control total al usuario que lo pida para que, así, este usuario pueda usar la función de uso compartido protegido.
> 
> Transcurrido un período de tiempo, si observa que hay muchas solicitudes de este tipo, podría decidir finalmente definir su propia plantilla personalizada para este escenario que conceda a usuarios específicos (como administradores o el departamento de soporte técnico) el permiso de copropietario, mientras que los usuarios estándar tienen el permiso de coautor o los [permisos](../deploy-use/configure-usage-rights.md) que se consideren adecuados.




<!--HONumber=Nov16_HO2-->


