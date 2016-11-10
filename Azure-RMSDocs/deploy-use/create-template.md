---
title: "Creación, configuración y publicación de una plantilla personalizada | Azure Information Protection"
description: "Instrucciones para crear y administrar plantillas personalizadas en el Portal de Azure clásico. Las plantillas facilitan a los usuarios finales y otros administradores la aplicación de las directivas apropiadas que protegen documentos y correos electrónicos."
author: cabailey
manager: mbaldwin
ms.date: 11/03/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d6e9aa0c-1694-4a53-8898-4939f31cc13f
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0046023125fe339ed408edf47c59e36708b01783
ms.openlocfilehash: 00661951513647add0c638e0eeb9e9fe38fa2d8d


---


# <a name="create-configure-and-publish-a-custom-template"></a>Creación, configuración y publicación de una plantilla personalizada

>*Se aplica a: Azure Information Protection, Office 365*


En el Portal de Azure clásico puede crear y administrar plantillas personalizada. Puede hacerlo directamente desde el Portal de Azure clásico o puede iniciar sesión en el Centro de administración de Office 365 y elegir **Características avanzadas** para Rights Management, lo que le redirigirá al Portal de Azure clásico.

Debe ser administrador global para crear y administrar plantillas en el Portal de Azure clásico. Si ha asignado el rol de administrador global del servicio Azure Rights Management a otros usuarios, también podrán crear y administrar plantillas, aunque deberán usar [PowerShell](configure-templates-with-powershell.md). Para obtener más información, vea [¿Debe ser un administrador global para configurar Azure RMS o puedo delegar a otros administradores?](../get-started/faqs-rms.md#do-you-need-to-be-a-global-admin-to-configure-azure-rms-or-can-i-delegate-to-other-administrators) 

Usa los procedimientos siguientes para crear, configurar y publicar plantillas personalizadas para Rights Management.

## <a name="to-create-a-custom-template"></a>Para crear una plantilla personalizada

1.  En función de que inicie sesión en el Centro de administración de Office 365 o en el Portal de Azure clásico, emplee uno de los siguientes procedimientos:

    -   En el [Centro de administración de Office 365](https://portal.office.com/):

        1.  En el panel izquierdo, haga clic en **Configuración del servicio**.

        2.  En la página **Configuración del servicio** , haga clic en **Rights Management**.

        3.  En la sección **Proteja su información** , haga clic en **Administrar**.

        4.  En la sección **Rights Management** , haga clic en **Características avanzadas**.

            > [!NOTE]
            > Si no ha activado todavía el servicio de Rights Management, haga clic primero en **Activar** y confirme la acción. Para más información, consulte [Activación de Azure Rights Management](activate-service.md).
            > 
            > Si no ha hecho clic en **Características avanzadas** antes, después de activar Rights Management, siga las instrucciones que aparecen en pantalla para obtener una suscripción gratuita de Azure, necesaria para poder acceder al Portal de Azure clásico.

            Al hacer clic en **Características avanzadas**, se carga el Portal de Azure clásico, donde puede administrar **RIGHTS MANAGEMENT** para Azure Active Directory de su organización.

    -   Desde el [Portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=275081):

        1.  En el panel izquierdo, haga clic en **ACTIVE DIRECTORY**.

        2.  En la página **Active Directory** , haga clic en **RIGHTS MANAGEMENT**.

        3.  Selecciona el directorio que administrarás para Rights Management.

        4.  Si no ha activado todavía Rights Management, haga clic en **ACTIVAR** y confirme la acción.

            > [!NOTE]
            > Para más información, consulte [Activación de Azure Rights Management](activate-service.md).

2.  Crea una plantilla nueva:

    -   En el Portal de Azure clásico, en la página de inicio rápido **Introducción a Rights Management**, haga clic en **Crear una nueva plantilla de directiva de permisos**.

        Si no ve inmediatamente esta página tras seguir las instrucciones de Office 365, use las instrucciones de navegación del Portal de Azure clásico, enumeradas anteriormente.

3. En la página **Agregar una nueva plantilla de directiva de permisos** , seleccione un idioma en el que tendrá que escribir el nombre de la plantilla y la descripción que verán los usuarios (puede agregar más idiomas más adelante). A continuación, escribe un nombre y una descripción únicos, y haz clic en el botón Completado.

    No incluya una coma ni un punto y coma en el nombre de la plantilla o la descripción. No todos los servicios y aplicaciones que usan plantillas de Rights Management admiten estos caracteres para estas plantillas. En este escenario, es posible que estos servicios y aplicaciones no puedan recuperar o usar estas plantillas de Azure Rights Management.

4. En la página de inicio rápido **Empiece a trabajar con Rights Management** , haga clic en **Administrar sus plantillas de directivas de permisos**. Verá la plantilla recién creada agregada a la lista de plantillas, con el estado **Archivada**. En esta fase, la plantilla se ha creado pero no se ha configurado, y no es visible para los usuarios.

## <a name="to-configure-and-publish-a-custom-template"></a>Para configurar y publicar una plantilla personalizada

1.  Seleccione la plantilla recién creada en la página **PLANTILLAS** del Portal de Azure clásico.

2.  En la página de inicio rápido **Se ha agregado la plantilla** , haga clic en **Introducción** en el paso 1, **Configurar permisos de usuarios y grupos** , elija **EMPEZAR AHORA** o **AGREGAR**y seleccione los usuarios y grupos que tendrán permisos para usar el contenido protegido con la nueva plantilla.

    > [!NOTE]
    > Los usuarios o grupos que selecciones deben disponer de una dirección de correo electrónico. En un entorno productivo, no será un problema, pero en un entorno de pruebas simple, es posible que tengas que agregar direcciones de correo electrónico para cuentas de usuario o grupos.

    Se recomienda usar grupos más que usuarios, lo cual simplifica la administración de las plantillas. Si tiene Active Directory localmente y está sincronizando con Azure AD, puede usar grupos habilitados para correo electrónico que sean grupos de seguridad o grupos de distribución. Sin embargo, si desea conceder derechos a todos los usuarios de la organización, resultará más eficiente copiar una de las plantillas predeterminadas en lugar de especificar varios grupos. Para obtener más información, consulte el [procedimiento para copiar una plantilla](copy-template.md).

    > [!TIP]
    > Puede agregar usuarios de fuera de la organización ("usuarios externos") a la plantilla si selecciona un grupo habilitado para correo que contenga contactos de Office 365 o Exchange Online. Esto le permite asignar derechos a estos usuarios de la misma manera en que los asigna a los usuarios de la organización. Por ejemplo, puede evitar que los clientes editen una lista de precios que les envía. No use esta configuración de plantilla para la protección de mensajes de correo electrónico si los usuarios de fuera de la organización van a leer los mensajes protegidos con Outlook Web App.
    > 
    > Además, posteriormente puede agregar usuarios de fuera de la organización a la plantilla mediante el [Módulo de Windows PowerShell para Azure Rights Management](install-powershell.md) y uno de los métodos siguientes:
    > 
    > -  **Usar un objeto de Rights Definition para actualizar una plantilla**: especifique las direcciones de correo electrónico externas y sus derechos en un objeto de Rights Definition, que después usará para actualizar la plantilla. Especifique el objeto de Rights Definition mediante el cmdlet [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) para crear una variable y, a continuación, suministrar esta variable al parámetro -RightsDefinition con el cmdlet [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) para modificar una plantilla existente. Sin embargo, si agrega estos usuarios a una plantilla existente, también tendrá que definir objetos de Rights Definition para los grupos existentes en las plantillas y no solo los usuarios externos nuevos.
    > -  **Exportar, editar e importar la plantilla actualizada**: use el cmdlet [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) para exportar la plantilla a un archivo que pueda editar para agregar las direcciones de correo electrónico externas de estos usuarios y sus derechos a los grupos y derechos existentes. Luego, use el cmdlet [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) para importar este cambio de nuevo a Azure RMS.

3.  Haz clic en el botón Siguiente y, a continuación, asigna uno de los derechos enumerados a tus usuarios y grupos seleccionados.

    Use la descripción mostrada para obtener más información acerca de cada derecho (y para derechos personalizados). También hay información más detallada disponible en [Configuración de los derechos de uso para Azure Rights Management](configure-usage-rights.md). Sin embargo, las aplicaciones que son compatibles con RMS pueden variar en la forma de aplicar estos derechos. Consulte su documentación y realice sus propias pruebas con las aplicaciones que usan los usuarios para comprobar el comportamiento antes de implementar la plantilla para los usuarios. Para hacer que esta plantilla solo puedan verla los administradores para la realización de las pruebas, defínala como una plantilla de departamento (paso 6).

4.  Si seleccionó **Personalizar**, haga clic en el botón Siguiente y seleccione permisos personalizados.

    Aunque puedas usar cualquier combinación de derechos individuales disponible, en algunas aplicaciones, hay derechos que pueden depender de otros derechos individuales. Cuando es sí, se seleccionan de forma automática los derechos dependientes.

    > [!TIP]
    > Considere la posibilidad de agregar el permiso **Copiar y extraer contenido** y concedérselo a algunos administradores o personal de otros roles que sean responsables de la recuperación de información. Este derecho les permite quitar la protección, si es necesario, de archivos y correos electrónicos que se protegerán con esta plantilla. Esta capacidad de quitar la protección en el nivel de plantilla proporciona un control más minucioso que el uso de la característica de superusuario.

5.  Haz clic en el botón Completar.

6.  En cambio, si desea que la plantilla pueda verla solo un subconjunto de usuarios cuando vean una lista de plantillas en las aplicaciones: Haga clic en **ÁMBITO** para configurar esto como una plantilla de departamento y haga clic en **COMENZAR AHORA**. De lo contrario, vaya al paso 9.

    Obtener más información acerca de las plantillas de departamento: De forma predeterminada, todos los usuarios del directorio de Azure verán todas las plantillas publicadas y, a continuación, pueden seleccionarlas en las aplicaciones cuando deseen proteger el contenido. Si desea que solo usuarios específicos vean algunas de las plantillas publicadas, debe definir el ámbito de las plantillas para estos usuarios. A continuación, solo dichos usuarios podrán seleccionar estas plantillas. Los usuarios no especificados no verán las plantillas y por lo tanto, no pueden seleccionarlas. Esta técnica puede facilitar a los usuarios la elección de la plantilla adecuada, especialmente al crear plantillas que están diseñadas para que las usen grupos o departamentos concretos. Por tanto, los usuarios solo pueden ver las plantillas que se les han designado.

    Por ejemplo, ha creado una plantilla para el departamento de Recursos humanos que aplica el permiso de solo lectura a los miembros del departamento de Finanzas. Para que solo los miembros del departamento de recursos humanos puedan aplicar esta plantilla al usar la aplicación de uso compartido de Administración de derechos, debe definir el ámbito de la plantilla para el grupo habilitado para correo electrónico denominado RecursosHumanos. A continuación, solo los miembros de este grupo pueden ver y aplicar esta plantilla.

7.  En la página **VISIBILIDAD DE PLANTILLA**, seleccione los usuarios y grupos que podrán ver y seleccionar la plantilla desde las aplicaciones habilitadas para RMS. Como antes, como procedimiento recomendado, utilice grupos en lugar de usuarios, y los grupos o usuarios que seleccione deben tener una dirección de correo electrónico.

8.  Haga clic en el botón Siguiente y decida si es necesario configurar la compatibilidad de aplicaciones para la plantilla de departamento. Si lo hace, haga clic en **COMPATIBILIDAD DE APLICACIÓN**, active la casilla y haga clic en **Completa**.

    ¿Por qué debe configurar la compatibilidad de aplicaciones? No todas las aplicaciones pueden admitir plantillas de departamento. Para ello, la aplicación debe autenticarse primero con el servicio RMS antes de descargar las plantillas. Si el proceso de autenticación no se realiza, de forma predeterminada, ninguna de las plantillas de departamento se descargan. Puede invalidar este comportamiento especificando que se deberían descargar todas las plantillas departamentales. Para ello, configure la compatibilidad de aplicaciones y active la casilla **Mostrar esta plantilla a todos los usuarios cuando las aplicaciones no admiten la identidad de usuario** .

    Por ejemplo, si no configura la compatibilidad de aplicaciones para la plantilla de departamento en nuestro ejemplo de recursos humanos, solo los usuarios del departamento de recursos humanos verán la plantilla de departamento cuando utilizan la aplicación de uso compartido de RMS, pero ningún usuario verá la plantilla de departamento al usar Outlook Web Access (OWA) de Exchange Server 2013 porque Exchange OWA y Exchange ActiveSync no son compatibles actualmente con las plantillas de departamento. Si invalida este comportamiento predeterminado mediante la configuración de la compatibilidad de aplicaciones, solo los usuarios del departamento de recursos humanos verán la plantilla de departamento cuando usen la aplicación de uso compartido de RMS, pero todos los usuarios podrán ver la plantilla de departamento al usar Outlook Web Access (OWA). Si los usuarios utilizan OWA o Exchange ActiveSync desde Exchange Online, las plantillas de departamento las verán todos los usuarios o bien ninguno, en función del estado de la plantilla (archivado o publicado) en Exchange Online.

    Office 2016 admite de forma nativa plantillas de departamento, igual que Office 2013 a partir de la versión 15.0.4727.1000, publicada en junio de 2015 como parte de [KB 3054853](https://support.microsoft.com/kb/3054853).

    > [!NOTE]
    > Si tiene aplicaciones que aún no admiten de forma nativa plantillas departamentales, utilice un script personalizado de descarga de plantillas de RMS u otras herramientas para implementar estas plantillas en la carpeta local del cliente de RMS. A continuación, estas aplicaciones mostrarán correctamente las plantillas de departamento solo a los usuarios y grupos que ha seleccionado para el ámbito de la plantilla:
    > 
    > -   En Office 2010, la carpeta de cliente es **%localappdata%\Microsoft\DRM\Templates**.
    > -   Desde un equipo cliente que ha descargado todas las plantillas, puede copiar los archivos de plantilla y pegarlos en otros equipos.
    > 
    > Puede [descargar el script personalizado de plantillas de RMS desde el sitio de Microsoft Connect](http://go.microsoft.com/fwlink/?LinkId=524506). Si ve un error al hacer clic en este vínculo, probablemente no se haya registrado en Microsoft Connect. Para registrarse:
    > 
    > 1.  Vaya al [sitio de Microsoft Connect](http://www.connect.microsoft.com) e inicie sesión con su cuenta de Microsoft.
    > 2.  Haga clic en **Directorio** y seleccione la categoría **Ver los productos Connect que no aceptan comentarios**.
    > 3.  Busque **Rights Management Services** y, para el programa **Microsoft RMS Enterprise Features**, haga clic en **Unirse**.

9. Haz clic en **CONFIGURAR** y agrega los idiomas adicionales que usen los usuarios, junto con el nombre y la descripción de esta plantilla en ese idioma. Si tiene usuarios multilingües, es importante agregar todos los idiomas que usen; además, debe proporcionar un nombre y una descripción en ese idioma. Los usuarios verán entonces el nombre y la descripción de la plantilla en el mismo idioma que su sistema operativo, lo cual garantiza que entenderán la directiva que se aplica a un documento o a un mensaje de correo electrónico. Si no coinciden con el idioma del sistema operativo cliente, el nombre y la descripción que ven se cambiarán al idioma y la descripción que tú hayas definido cuando creaste por primera vez la plantilla.

    Después, comprueba si quieres hacer algún cambio en las configuraciones siguientes:

    |Setting|Más información|
    |-----------|--------------------|
    |**expiración del contenido**|Define una fecha o un número de días para esta plantilla cuando los archivos que están protegidos por dicha plantilla no deben abrirse. Puedes especificar una fecha o un número de días a partir del momento en que se aplica la protección al archivo.<br /><br />Cuando se especifica una fecha, entra en vigor a medianoche en su zona horaria actual.|
    |**acceso sin conexión**|Use esta configuración para equilibrar los requisitos de seguridad que tenga frente al requisito de que los usuarios deben poder abrir archivos protegidos cuando no disponen de conexión a Internet.<br /><br />Si especificas que el contenido no está disponible sin conexión a Internet o que el contenido está disponible solamente durante un número concreto de días, cuando se supere ese umbral, los usuarios deberán volver a autenticarse y se registrará su acceso. Cuando esto sucede, si sus credenciales no se han almacenado en la memoria caché, se pedirá a los usuarios que inicien sesión antes de que puedan abrir el archivo.<br /><br />Además de la reautenticación, también se vuelve a evaluar la directiva y la pertenencia al grupos de usuarios. De modo que los usuarios podrían experimentar diferentes resultados de acceso para el mismo archivo si se producen cambios en la directiva o la pertenencia al grupo desde la última vez que se accedió al archivo.|

10. Cuando esté seguro de que la plantilla está configurada correctamente para los usuarios, haga clic en **PUBLICAR** para que la plantilla esté visible para los usuarios y elija **GUARDAR**.

11. En el Portal clásico, haga clic en el botón Atrás para volver a la página **PLANTILLAS**, donde la plantilla tiene ahora el estado actualizado de **Publicada**.

Para realizar cualquier cambio en tu plantilla, selecciónala y, a continuación, usa los pasos de inicio rápido otra vez. O selecciona una de las opciones siguientes:

-   Para agregar más usuarios y grupos, y definir sus derechos: Haga clic en **PERMISOS**y elija **AGREGAR**.

-   Para quitar los usuarios o grupos que has seleccionado anteriormente: Haga clic en **PERMISOS**, seleccione el usuario o grupo en la lista y elija **ELIMINAR**.

-   Para cambiar qué usuarios pueden ver las plantillas para seleccionarlas desde las aplicaciones: Haga clic en **ÁMBITO**, elija **AGREGAR** , **ELIMINAR**o **COMPATIBILIDAD DE APLICACIÓN**.

-   Para que la plantilla ya no sea visible para todos los usuarios: Haga clic en **CONFIGURAR**, elija **ARCHIVO**y haga clic en **GUARDAR**.

-   Para realizar otros cambios de configuración: Haga clic en **CONFIGURAR**, realice los cambios y elija **GUARDAR**.

> [!WARNING]
> Cuando realices cambios en una plantilla que has guardado antes, los clientes no verán dichos cambios en la plantilla hasta que se actualicen en sus equipos. Para más información, consulte [Actualización de plantillas para usuarios](refresh-templates.md).

## <a name="see-also"></a>Véase también
[Configuración de plantillas personalizadas para Azure Rights Management](configure-custom-templates.md)


<!--HONumber=Nov16_HO1-->


